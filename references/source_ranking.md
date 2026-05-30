# Source Ranking — Authoritative Decision Document

Single source of truth for how the skill ranks, accepts, downgrades, or rejects sources. Supersedes `source_hierarchy.md` (deprecated). All other ranking references defer to this document.

This document covers:
1. The tier system (1-4) and what each tier means
2. The bias-class system (separate axis from tier)
3. The decision algorithm (how a model goes from "found this" to "cite this")
4. The cite-replace rule (handling POLITICAL sources)
5. The triangulation rule (handling contested endpoints)
6. Echo-chamber detection
7. Predatory journal handling
8. Hazard-vs-risk conflation guard
9. Per-discipline ranking quick reference

---

## 1. Tier system (defensibility axis)

Tier comes from `assets/source_tier_lookup.json` by domain match. Model never assigns tier by judgement.

| Tier | Definition | EU-context weight |
|---|---|---|
| **1** | Regulatory primary (EU and EU-recognised authoritative): EFSA, ECHA, EUR-Lex, RMS RAR/DAR, Commission Implementing Regs, EPPO standards, OECD Test Guidelines, OECD monographs, EU Reference Laboratories | Highest |
| **2** | Authoritative secondary: non-EU national regulators (US EPA, PMRA, APVMA), international bodies (FAO/Codex, WHO/IPCS, IARC, NTP, OECD SIDS), established curated databases (PPDB, BPDB, eChemPortal, PubChem, ECHA C&L) | High (but EU-context tiebreak goes to Tier 1) |
| **3** | Peer-reviewed primary literature (Tier-3-specialist journals listed below): J. Agric. Food Chem., Pest Manag. Sci., Environ. Toxicol. Chem., Chemosphere, Sci. Total Environ., Regul. Toxicol. Pharmacol., Food Chem. Toxicol., Arch. Toxicol., EFSA Journal, Environ. Sci. Technol., Ecotoxicol. Environ. Saf., J. Chromatogr. A, Anal. Chim. Acta, Crop Protection, Pest Manag. Sci., Weed Res., Plant Dis., Phytopathology, Ann. Work Expo. Health, Crit. Rev. Toxicol. | Per Klimisch / CRED / OHAT |
| **4** | Grey literature: industry task force reports (COI), conference proceedings, theses (only if cited by Tier 1-3), preprints (non-peer-reviewed flag), trade press, advocacy NGO publications | Lowest; cite-replace applies |

**Tiebreak rules within tier**:
- Recency: newer wins only if same tier AND new data (not new opinion).
- EU-relevance: Tier-1 EU body > Tier-1 non-EU body on EU-applicability claims.
- Document version: cite most recent consolidated / amended version.

---

## 2. Bias-class system (credibility axis, orthogonal to tier)

Tier measures *defensibility of evidentiary weight*. Bias class measures *credibility of framing and intent*. A Tier 4 grey source can be NEUTRAL (e.g. an academic thesis). A Tier 3 peer-reviewed paper can be DECLARED-COI (industry-funded but published). Both axes apply.

Bias class comes from `assets/coi_flags.json` + `assets/credibility_rules.json` by domain match + author affiliation match.

| Class | Meaning | Cite policy |
|---|---|---|
| **NEUTRAL** | Regulator, academic, public research institute, non-affiliated researcher | Cite normally per tier |
| **DECLARED-COI** | Industry-funded, manufacturer-employed authors, registrant data | Cite with `coi: industry|manufacturer` flag visible in ledger; does not auto-downrank tier |
| **POLITICAL** | Advocacy NGO with declared anti or pro-PPP agenda (PAN, PAN-Europe, PAN-NA, EWG, Beyond Pesticides, Friends of the Earth, Greenpeace, advocacy think tanks) | **Cite-replace rule** (§4) — never appears as standalone evidence |
| **PREDATORY** | Beall/Cabells listed publisher; pay-to-publish without peer review | **Block** — do not cite |
| **TRADE-PRESS** | Industry trade outlets (Agrow, AgriBusiness Global, Phillips McDougall) | Cite only for market or factual industry context; **never for scientific claims** |
| **UNRELIABLE** | Wikipedia, Reddit, blogs, social media, anonymous web sources | **Block** for citation; permitted for discovery / synonym lookup only |

---

## 3. Decision algorithm

For every potential source the model encounters:

```
1. Resolve source domain → assets/source_tier_lookup.json → get TIER
2. Resolve source domain → assets/coi_flags.json + credibility_rules.json → get BIAS_CLASS
3. Branch on BIAS_CLASS:
   PREDATORY     → BLOCK; do not cite; log to SEARCH-LOG.md as rejected (reason: predatory)
   UNRELIABLE    → BLOCK; permitted for discovery only; never enters ledger
   POLITICAL     → CITE-REPLACE protocol (§4); source never enters ledger as standalone evidence
   TRADE-PRESS   → Permitted only for market/factual context; if used for scientific claim, BLOCK
   DECLARED-COI  → ACCEPT with `coi` flag in ledger row; tier unchanged
   NEUTRAL       → ACCEPT at tier
4. Branch on TIER (after bias clear):
   Tier 1        → Primary citation; high weight
   Tier 2        → Secondary citation; EU-context tiebreak applies
   Tier 3        → Per-study quality (Klimisch / CRED / OHAT) applied
   Tier 4        → Tier-flagged in ledger; weight = lowest; never for contested claims alone
5. For contested-endpoint claims (§5):
   Require Tier 1-2 + ≥1 independent Tier 3 corroboration
   Single-source flagged with hedging downgrade
6. Cross-check echo chamber (§6):
   If only POLITICAL or TRADE-PRESS sources cite the claim → drop
7. Hazard-vs-risk guard (§8):
   If claim conflates hazard with risk → either fix framing or drop
```

---

## 4. Cite-replace rule (POLITICAL sources)

When the model surfaces a claim from a POLITICAL source (PAN, EWG, Beyond Pesticides, etc.):

### Step-by-step

1. **Locate upstream primary.** Every advocacy claim references something — EFSA reasoned opinion, peer-reviewed paper, court ruling, EU document, IARC monograph. Find it.
2. **If primary exists and is Tier 1-2**: cite primary. **Drop POLITICAL source.** The framing the advocacy applied is irrelevant; the primary is what supports the claim.
3. **If primary is Tier 3 peer-reviewed**: open the primary. Verify it actually supports the claim as the POLITICAL source represents it. Common failures:
   - Selective quotation (advocacy quoted a subordinate clause; full passage carries caveats)
   - Wrong jurisdiction (US EPA finding cited as if EU)
   - Hazard-as-risk conflation (CLP CMR cited as proof of consumer harm)
   - Confidence-interval dropped (point estimate cited as definitive)
   - Outdated cite (older publication superseded by EFSA Conclusion)
4. **If primary verified**: cite primary at Tier 3 with Klimisch/CRED applied. Drop POLITICAL.
5. **If primary misrepresented**: drop both. Optionally note misrepresentation in `LIMITATIONS.md` if relevant to the review's purpose (e.g. regulatory-dispute archetype).
6. **If primary is Tier 4 grey OR absent**: the claim is not citable for a regulatory review. Drop entirely.

### POLITICAL sources NEVER appear in CITATION-LEDGER.md as standalone evidence

Allowed exceptions (narrow):
- The review's question is *about* the advocacy position (e.g. "characterise PAN Europe's pesticide criticism scope"). Then PAN is the subject, not the evidence. Cite as primary source of the position itself, never of the underlying scientific claim.
- Regulatory dispute / litigation defence archetype where engaging the opposing argument is required. Counter-evidence section (§5 in `templates/narrative_critical.md`) cites the position then rebuts with Tier 1-2 evidence.

### Why this rule

PAN, EWG, Beyond Pesticides etc. are designed to influence regulatory and public policy. Their selection of which papers to cite, which findings to amplify, which to omit is value-laden. Even when they correctly report a Tier 1-2 finding, citing them adds the framing — and the framing is what makes the review unscientific. Citing the primary directly costs nothing and removes the framing.

---

## 5. Triangulation rule (contested endpoints)

For endpoints with high political loading or active regulatory dispute:

- Glyphosate / glyphosate-class carcinogenicity (IARC 2A vs EFSA / ECHA non-classification)
- Neonicotinoid bee toxicity (Reg 485/2013 restrictions vs new applications)
- Endocrine disruption categorisation under Reg 2018/605
- PFAS in PPPs (current revision activity)
- Co-formulant safety (POE-tallowamine etc.)
- Any substance in active SCoPAFF dispute

### Rule

Any claim on a contested endpoint requires:
1. ≥1 Tier 1-2 source AND
2. ≥1 independent peer-reviewed Tier 3 corroboration

"Independent" = different first-author, different funder, different institution.

Single-source claims on contested endpoints receive **hedging downgrade**:
- "Demonstrated" → "Reported but not independently confirmed"
- "Indicated" → "Suggested by single-source data"
- Add `[single-source]` tag in ledger row

### Why

Contested endpoints attract motivated citation. A single industry-funded study or a single advocacy-promoted study should never settle a contested question — both directions get the same triangulation requirement.

---

## 6. Echo-chamber detection

Heuristic check at Phase 4 (screening) and Phase 7 (verification):

### Detection

Walk the citation chain of each candidate source. If the chain is:
- `NGO-A → NGO-B → NGO-A` (circular advocacy)
- `NGO-A → trade-press → NGO-B` (advocacy-trade loop)
- `NGO → blog → NGO` (advocacy-blog loop)

with no Tier 1-2 or independent Tier 3 source upstream → **claim not citable, drop.**

### Gate check (inline Bash at Phase 8)

```bash
# Per ledger row, if coi=advocacy or coi=trade_press,
# require ≥1 other ledger row at tier ≤2 with matching claim_summary
awk -F'|' '
  NR>2 && ($0 ~ /advocacy/ || $0 ~ /trade_press/) {
    claim=$2; tier=$11
    if (!(claim in supported)) {
      print "FLAG echo-chamber risk: " claim " — verify Tier 1-2 corroborator exists"
    }
  }' CITATION-LEDGER.md
```

If flagged, model loops back to Phase 7 to add corroborator or drop claim.

---

## 7. Predatory journal handling

### Hard block

Domains / publishers in `assets/credibility_rules.json` `predatory_block:` list. Includes:
- OMICS International
- Bentham Open (legacy; current Bentham Science separate)
- Allied Academies
- SciRes Literature
- David Publishing
- Scientific Research Publishing (SCIRP)
- IISTE
- Academic Journals Inc.
- World Academic Publishing
- Various "International Journal of …" with no editorial board

Gate: any ledger row matching block list → FAIL.

### Grey-listed (case-by-case)

- **MDPI**: large legitimate corpus + predatory-adjacent edge cases. Per-journal evaluation. *Environments*, *Toxics*, *Molecules* generally OK for chemistry/tox; some journals raise flags. **Default Tier 3 with `peer-review-rigour: questioned` flag.**
- **Frontiers**: similar pattern. *Frontiers in Toxicology* / *Frontiers in Environmental Science* legitimate but rapid peer review weakens RoB. **Default Tier 3 with flag.**
- **Hindawi** (post-Wiley acquisition cleanup): legacy issues; case-by-case.

### Discovery exception

Predatory-published paper may legitimately discover a finding later replicated in Tier 1-3 source. Use the Tier 1-3 replication; do not cite the predatory original.

---

## 8. Hazard-vs-risk conflation guard

Advocacy sources (and occasionally even mid-quality peer-reviewed sources) routinely conflate. Skill must flag whenever a candidate citation makes one of these moves:

| Hazard claim | Risk claim (DIFFERENT) |
|---|---|
| "Substance is CLP-classified Carc 1B" | "Substance causes human cancer at use rates" |
| "Substance is IARC 2A (probable)" | "Substance is a known human carcinogen" |
| "Residue detected at X μg/kg in food" | "Residue exceeds safe limit" |
| "In vitro genotoxicity at 1 mM" | "Substance is genotoxic at human exposure" |
| "High dose causes effect Y in rats" | "Substance causes effect Y in humans at GAP exposure" |
| "Substance is ED-modality positive in OECD 441" | "Substance disrupts human endocrine function" |
| "Detection in groundwater above 0.1 μg/L" | "Drinking water exceeds health-based limit" |

### Rule

Any claim that crosses hazard → risk without explicit exposure context (PEC, MoE, dietary intake, IESTI) gets:
- Reframed to maintain the distinction: "EFSA classified Substance as Carc 1B based on rat mechanistic data [CIT]; human risk under registered GAP characterised by MoE = X [CIT]"
- OR dropped if exposure context not retrievable

This is critical in PPP context because the entire EU regulatory framework (Reg 1107/2009 Art 4 hazard cut-offs, Reg 396/2005 MRL exposure refinement, Reg 2018/605 ED criteria) is built on this distinction. Conflation undermines the review's regulatory utility.

### Gate

Gate Step 7 (forbidden language) extended to flag phrases that indicate conflation without exposure context: "causes cancer", "is carcinogenic to humans", "is toxic to consumers", "exceeds safe limits" without nearby exposure citation.

---

## 9. Per-discipline ranking (quick reference)

Authoritative per-discipline rankings live in `references/discipline_overlays.md`. This is a quick-reference summary; the discipline overlays file is canonical.

| Discipline | Top 3 sources |
|---|---|
| Regulatory | EU legislation (CELEX consolidated) → EFSA Conclusion → ECHA RAC opinion |
| Mammalian tox | EFSA Conclusion §B.6 → RMS RAR Vol 3 B.6 → JMPR monograph |
| Ecotox | EFSA Conclusion §B.9 → EFSA discipline-specific Guidance (Bee 2013/2023, Aquatic 2013, Birds & Mammals 2009) → RMS RAR Vol 3 B.9 |
| Efate | EFSA Conclusion §B.8 → FOCUS Working Group reports → RMS RAR Vol 3 B.8 |
| Residues | EFSA MRL Reasoned Opinion / Art.12 → EFSA Conclusion §B.7 → JMPR monograph |
| Analytical | SANTE/11312/2021 (current) → SANCO/3029/99 rev.4 → EFSA Conclusion §B.5 |
| Chemistry / MoA | EFSA Conclusion §B.2 → IUPAC technical reports → BCPC Pesticide Manual |
| Efficacy | EPPO Standards PP1 series → zonal efficacy assessments (zRMS) → MS authorisation decisions |
| Exposure | EFSA Guidance on Operator/Worker/Bystander/Resident (2022) → AOEM Calculator → RMS RAR Vol 3 B.6.12 |

---

## 10. Source-acceptance decision tree (compact)

```
candidate source surfaced
├── domain in predatory_block?
│   ├── yes → BLOCK; log; do not cite
│   └── no → continue
├── domain in unreliable_block (Wikipedia, blogs, etc.)?
│   ├── yes → BLOCK for citation; OK for discovery only
│   └── no → continue
├── bias_class lookup
│   ├── POLITICAL → cite-replace protocol (§4)
│   ├── TRADE-PRESS → market/factual context only; BLOCK for scientific claim
│   ├── DECLARED-COI → accept with coi flag; tier unchanged
│   └── NEUTRAL → continue
├── tier lookup
│   ├── Tier 1 → primary cite
│   ├── Tier 2 → secondary; EU-context tiebreak
│   ├── Tier 3 → Klimisch / CRED / OHAT applied
│   └── Tier 4 → tier-flagged; never alone for contested
├── grey-listed publisher (MDPI / Frontiers)?
│   ├── yes → flag peer-review-rigour; default Tier 3 with downweight
│   └── no → continue
├── contested endpoint?
│   ├── yes → require ≥1 Tier 1-2 + ≥1 independent Tier 3
│   └── no → continue
├── echo-chamber check
│   ├── only advocacy/trade-press cite trail → drop
│   └── independent corroboration → continue
└── hazard-vs-risk guard
    ├── conflates without exposure context → reframe or drop
    └── distinction preserved → ACCEPT into CITATION-LEDGER.md
```

This decision tree runs for every candidate source. Model executes deterministically. Gate verifies output.
