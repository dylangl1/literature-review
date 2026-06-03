---
name: ppp-literature-review
description: Defensible EU PPP regulatory literature reviews on active substances, metabolites, co-formulants, formulations. Covers hazard ID, risk analysis, data gap analysis vs Reg 283/284/2013, MRL review, Art.12, RAR/renewal, ED assessment (Reg 2018/605), substitution (Reg 2015/408), DP checks, WoE, MoA, analytical/chemistry, comparative, scoping, narrative-critical. Sources tiered EFSA/ECHA/RMS > peer-reviewed > grey; bias-class screening (POLITICAL cite-replace, IARC paired); citations verified; EFSA writing. Triggers: lit review, PPP review, evidence synthesis, data gap analysis, WoE, ED assessment, DP check, MRL review, Art.12 review, comparative review, scoping review, analytical method review, /lit-review, /ppp-review, /evidence-synthesis.
allowed-tools: Read, Write, Edit, Grep, Glob, Bash, WebSearch, WebFetch, AskUserQuestion, mcp__chemwise__search_substance, mcp__chemwise__get_registration_summary, mcp__chemwise__get_regulatory_status, mcp__chemwise__get_ppp_approval_status, mcp__chemwise__get_ppp_expiry_alerts, mcp__chemwise__get_mrl_status, mcp__chemwise__get_efsa_conclusion_metadata, mcp__chemwise__get_efsa_conclusion_fulltext, mcp__chemwise__search_efsa_conclusions, mcp__chemwise__get_cl_classification, mcp__chemwise__check_svhc, mcp__chemwise__list_svhc, mcp__chemwise__get_substance_review_history, mcp__chemwise__query_bcpc, mcp__chemwise__get_structure, mcp__chemwise__list_ppp_substances
metadata:
    skill-author: Dylan Grimes Larkin (Regulatory Scientist @ Life Scientific)
    domain: EU PPP Regulatory affairs/science
    version: 2.0
---

# PPP Literature Review

## Supported models (Claude-only)

This skill supports Claude models exclusively.

- **Minimum**: Claude Opus 4.7 Medium reasoning
- **Default**: Claude Opus 4.7 Medium reasoning
- **Preferred (systematic / comparative / multi-discipline)**: Claude Opus 4.7 High reasoning
- **Permitted (rapid archetype only, single discipline)**: Claude Sonnet 4.7
- **Blocked**: Sonnet ≤4.6, Haiku class, all non-Claude models

At Phase 1 entry, detect model via `$ANTHROPIC_MODEL` env / model name. If below floor, halt with:

> Skill ppp-literature-review requires Claude Opus 4.7 (Medium reasoning minimum) or Sonnet 4.7 (rapid archetype only). Current model: {detected}. Halting. Switch model and re-invoke.

## MANDATORY MINIMUMS (read every phase)

These rules are NON-NEGOTIABLE regardless of model, archetype, or "quick" framing.

1. **ANCHOR COVERAGE 12/12.** Every review (including rapid) completes the 12-item regulatory anchor. Chemwise IS preferred but NOT required — use fallback URLs from `references/anchor_fallback_paths.md` when chemwise unavailable. No skipping. No "judging not relevant".
2. **CITATION PER CLAIM.** Every quantitative value, regulatory statement, study reference carries a `[CIT-N]` marker resolving to `CITATION-LEDGER.md`. No orphan claims.
3. **NO CITATION FROM MEMORY.** Every cite must be WebFetched (or chemwise-retrieved) with `fetched_at` timestamp in the ledger. Inventing DOIs/authors/titles is forbidden and gate-detected.
4. **QUANTITATIVE ANCHORS** require value + unit + species/matrix + source. All four. Missing one = orphan = fail.
5. **IDENTITY VERIFIED BEFORE SEARCH.** CAS + EC + InChIKey confirmed across ≥2 sources before any literature search. Trade-name-only searches forbidden.
6. **SOURCE TIER FROM LOOKUP, NOT JUDGEMENT.** `assets/source_tier_lookup.json` is authoritative. Cannot promote EFSA, cannot upgrade preprints.
7. **BIAS-CLASS FROM LOOKUP.** `assets/credibility_rules.json` is authoritative. EFSA + ECHA = authoritative Tier 1 NEUTRAL (define EU regulatory landscape; status unchanged by political pressure). POLITICAL sources (PAN, EWG, Beyond Pesticides, FoE, Greenpeace, etc.) are NEVER standalone evidence — cite-replace rule applies. CAVEAT sources (IARC) require pairing with EU regulatory consensus (EFSA + ECHA) on the contested topic; framework divergence explicitly stated. PREDATORY publishers blocked. UNRELIABLE (Wikipedia, blogs, social) blocked for citation, discovery-only. TRADE-PRESS for market/factual context only, never scientific claim.
8. **CONTESTED ENDPOINTS** require triangulation: ≥1 Tier 1-2 source AND ≥1 independent peer-reviewed Tier 3 corroboration. Single-source on contested endpoint → hedging downgrade + [single-source] tag in ledger.
9. **HAZARD vs RISK** distinction preserved. Hazard classification (CLP CMR, IARC 2A/2B) does NOT equal risk under registered GAP. Claims crossing the boundary require explicit exposure context (PEC, MoE, dietary intake, IESTI) in adjacent text or are reframed/dropped.
10. **CONTRACT-DRIVEN.** Phase 1.5 emits `OUTPUT-CONTRACT.md` + `.json`. All downstream phases must satisfy the contract. Phase 8 gate is mechanical, not judgemental.
11. **QUICK = NARROW SCOPE, NOT FEWER SOURCES.** Rapid archetype reduces scope, not the integrity floor.
12. **NO ABSOLUTIST LANGUAGE.** Forbidden: "proven", "definitive", "conclusive", "obviously", "clearly shows", "undeniably". Use calibrated hedging per `references/quality_appraisal.md`.
13. **NO EM/EN DASHES.** Single hyphens, parentheses, commas, periods only.

## Purpose

Produce literature reviews suitable for EU regulatory submissions, internal scientific decisions, and legal defensibility. Diligence, accuracy, completeness, and traceable citation are non-negotiable. Output must withstand scrutiny from EFSA peer review, RMS evaluators, and competent authority audits — across any model version.

## When to Use

Trigger when the user requests any of:
- Literature review, evidence synthesis, state-of-the-art summary, scoping review, comparative review, narrative position
- Hazard identification, hazard characterisation
- Risk analysis, risk characterisation, weight-of-evidence (WoE)
- Endpoint review (tox, ecotox, fate, residue, efficacy, exposure)
- Analytical method or chemistry / MoA review
- Data gap analysis vs Reg 283/2013 or 284/2013
- MRL review or setting support
- Article 12 MRL review, Article 43 product re-authorisation
- Renewal dossier (RAR/DAR) literature support
- Endocrine disruptor (ED) assessment under Reg 2018/605
- Substitution candidate evaluation under Reg 2015/408
- Data protection / data exclusivity / reference product check
- Comparative assessment, mode-of-action review
- Co-formulant review under REACH
- Regulatory position defence, dispute, or precedent search

Do NOT use for: quick factual lookups (use chemwise directly), single-document summary, drafting non-literature regulatory text.

## Layered Contract Model

Output structure is composed from four layers. Layers tighten downward; no layer can violate a higher layer's floor.

```
Layer 0  EU evaluation spine     (always; integrity floor)
Layer 1  Discipline overlay      (one or more: regulatory / mammalian_tox / ecotox / efate / residues / analytical / chemistry / efficacy / exposure)
Layer 2  Review type + modifier  (type: literature_review / systematic_review / database_study / data_analysis) + (modifier: comparative / scoping / rapid / none)
Layer 3  User overrides          (jurisdiction, citation style, length within L1+L2 floor)
```

L0 reference: see `references/discipline_overlays.md` (multi-discipline composition section at bottom).
L1 reference: `references/discipline_overlays.md` — includes preferred review type, output style, and molecular structure requirements per discipline.
L2 reference: `references/archetype_integrity_contracts.md`.
L3: captured at Phase 1.

## Operating Principles

1. **Regulatory truth precedes peer-reviewed truth.** EFSA Conclusion or RMS RAR overrides journal paper on contested endpoints.
2. **Cite or omit.** Every quantitative claim, regulatory statement, and study reference carries an inline `[CIT-N]` resolving to a verifiable source in `CITATION-LEDGER.md`.
3. **Tier every source** via lookup (`assets/source_tier_lookup.json`). Tier governs weight. Klimisch (or equivalent) recorded per included study.
4. **Document the negative space.** Excluded studies, failed queries, anchor misses, data gaps logged as carefully as included findings.
5. **Calibrated language.** Hedging matches evidence weight. Absolutes only where legislation defines them.
6. **Reproducibility.** Search strings, dates, databases, hit counts captured verbatim in `SEARCH-LOG.md`.
7. **Determinism over judgement.** Model selects among pre-tiered sources, fills pre-scaffolded sections, uses canned search blocks. Contract / scaffold / gate externalised so quality is invariant across models.

## Writing Conventions (enforced at gate)

- Third person. Past tense for findings, present tense for established knowledge and current regulatory status.
- No em-dashes or en-dashes. Single hyphens, parentheses, commas, periods.
- No subjective, informal, ambiguous, vague, passive-leaning language where active is clearer.
- No absolutist language ("proven", "definitive", "conclusive", etc.).
- Quantitative anchors required: NOAEL/LOAEL/NOEC/LC50/LD50/DT50/Koc/LOQ/etc. with units, n, route, species, study duration, CI where reported.
- Acronyms expanded on first use; glossary appended.
- Distinguish source voice explicitly: "EFSA concluded …" vs "the applicant reported …" vs "one peer-reviewed study found …" vs "industry task force documents suggest …".

## Workflow

Execute phases sequentially. Do not skip any phase. Phase 1, 1.5, 2, 7, and 8 are gates.

### Phase 1 — Scope Lock (gate)

Use `AskUserQuestion` to lock scope before any searching. Capture (enum where possible to constrain weak models):

1. **Review type** (enum): `literature_review` | `systematic_review` | `database_study` | `data_analysis`
   - `literature_review`: narrative/descriptive synthesis; no formal search protocol required; primary type for regulatory affairs and standard regulatory science endpoint summaries
   - `systematic_review`: structured protocol; PRISMA flow; dual screening; quality appraisal; required for ED assessment, substitution, litigation defence
   - `database_study`: analysis of existing registry or dataset (MRL DB, resistance monitoring, authorisation footprint)
   - `data_analysis`: modelling or computation (FOCUS PEC, PRIMo, QSAR, trial statistics)
   - If unsure: offer the discipline-appropriate default from `references/discipline_overlays.md §Preferred review type(s)`.

2. **Scope modifier** (optional): `comparative` | `scoping` | `rapid` | none
   - `comparative`: multi-substance symmetric comparison; triggers N×12 anchor; symmetric endpoint matrix required
   - `scoping`: evidence mapping; PCC framework; no quality appraisal; PRISMA-ScR; no synthesis prose
   - `rapid`: narrows question scope (one substance × one endpoint cluster); ≤2000 words narrative; 12/12 anchor still required

3. **Discipline(s)** (multi-select enum): `regulatory` | `mammalian_tox` | `ecotox` | `efate` | `residues` | `analytical` | `chemistry` | `efficacy` | `exposure`

4. **Question type** (enum): hazard ID | hazard characterisation | exposure | risk analysis | risk characterisation | data gap | MRL review | DP/reference product | ED assessment | substitution | renewal | efficacy/resistance | mode of action | regulatory precedent | analytical method | comparative assessment | regulatory position | PEC modelling | dietary intake

5. **PECO-R framework** (for literature_review / systematic_review / data_analysis; PCC for scoping modifier):
   - **P** Population / matrix
   - **E** Exposure (substance + route + duration + concentration range)
   - **C** Comparator (control, reference, baseline GAP, threshold)
   - **O** Outcome (endpoints, parameters)
   - **R** Regulatory context (instrument, Annex point, jurisdiction)

6. **Substance scope**: active substance(s), metabolites, co-formulants, formulation, CAS RN, EC, ISO common name, IUPAC, SMILES/InChIKey. For `comparative` modifier: explicit comparator list + inclusion criteria.

7. **Endpoint scope**: specific Annex II/III data points, or open if exploratory. For `comparative` modifier: locked endpoint set applied to all comparators.

8. **Geography/jurisdiction**: EU-wide | zonal (N/C/S) | specific MS | global comparator

9. **Time window**: default last 10 years; full historical for renewal/ED/substitution

10. **Use context**: dossier (new/renewal/Art.43) | MRL | Art.12 | DP | internal R&D | litigation defence | scientific opinion drafting

11. **Output format**: Markdown only | Markdown + Word (via `anthropic-skills:docx`) | Both

12. **Citation style** (enum): efsa (default) | vancouver | apa | acs

13. **Citation placement** (enum): inline_parenthetical | numbered_superscript | footnote

14. **Model class** (enum, user-confirmed or auto-detected): strong | mid | weak — drives behavioural floor (see §Behavioural Floors per Model Class below)

15. **Anchor waivers** (any of the 12 items NA for this scope): list item IDs + justifications

Write captured scope to `SCOPE.md`. Block downstream phases until user confirms.

### Phase 1.5 — Contract Lock (gate)

Compose `OUTPUT-CONTRACT.md` (human) and `OUTPUT-CONTRACT.json` (machine) from Layer composition:

1. Start with L0 EU spine (always-required sections — `references/discipline_overlays.md` §"Common EU spine" via L1 overlays union).
2. Union all selected L1 disciplines from `references/discipline_overlays.md`. Order per "Multi-discipline composition" rule (Identity → Physchem → Analytical → Mammalian tox → Residues → Efate → Ecotox → Efficacy → Exposure → Regulatory implications).
3. Apply L2 archetype overlay from `references/archetype_integrity_contracts.md` — sets screening protocol, length cap/floor, figure requirements, forbidden behaviours.
4. Apply L3 user overrides — must not violate L0+L1+L2 floor.
5. Validate composed contract against `assets/contract_schema.json`.
6. Write:
   - `OUTPUT-CONTRACT.md` — human-readable with required sections, figures, min counts, citation rules, anchor list, gate criteria
   - `OUTPUT-CONTRACT.json` — machine-readable per schema; consumed at Phase 8 gate via `jq`
   - `QUALITY-CHECKLIST.md` — pre-populated checklist boxes derived from contract
7. Confirm contract to user (display key counts: required sections N, min citations M, min figures F, anchor items 12 or 11-waived).
8. Contract immutable after this gate. Model cannot edit; user-only re-entry via Phase 1.

### Phase 2 — Regulatory Anchor (gate)

Establish regulatory ground truth before any literature search.

1. Generate `regulatory_anchor/CHEMWISE-CHECKLIST.md` from `references/anchor_fallback_paths.md` (12 unchecked items + waivers marked NA).
2. For each item:
   - **Try chemwise primary** (per item's primary tool in `references/anchor_fallback_paths.md`).
   - If chemwise unavailable OR substance not in chemwise DB → **try Fallback 1** (WebFetch).
   - If Fallback 1 fails → **try Fallback 2**.
   - If all fail → log to `regulatory_anchor/ANCHOR-MISSES.md`, leave item unchecked.
3. Cache each item's response to `regulatory_anchor/{NN_item}.md` with YAML frontmatter (source, url, accessed, fallback_tier, chemwise_attempted, chemwise_result).
4. **Identity verification** (item 1): require CAS match across ≥2 sources. Write `cross_verified: true` to `regulatory_anchor/01_identity.md`. If fails, BLOCK Phase 3.
5. For comparative archetype: repeat full anchor for each comparator (N×12).
6. Output `regulatory_anchor/anchor_summary.md` — synthesised identity + regulatory status + key EFSA endpoints + classification + dated source list.
7. For legislation, resolve via `assets/eu_ppp_regulations.json` (CELEX + `eurlex_html` URL) and WebFetch EUR-Lex. Cite as CELEX.

### Phase 3 — Tiered Literature Search

Build search blocks from PECO-R using canned Boolean strings. Pattern: `({SUBSTANCE} OR "{CAS}" OR {SYNONYMS}) AND ({ENDPOINT_TERMS}) AND ({SPECIES/MATRIX_TERMS}) {YEAR_FROM}-{YEAR_TO}`. Substitute `{SUBSTANCE}`, `{CAS}`, `{SYNONYMS}`, `{EC}`, `{INCHIKEY}` tokens. No freeform queries (mid/weak models).

Run tier order so higher-tier sources establish canonical claims first.

**Tier 1 — Regulatory primary** (largely complete via Phase 2): EFSA, ECHA, RMS RAR/DAR, EU Pesticides DB, JMPR/JECFA, OECD monographs.

**Tier 2 — Authoritative secondary**: US EPA, PMRA, APVMA, FAO, IARC, NTP, WHO/IPCS, IUCLID/eChemPortal, BCPC PM, PPDB, BPDB.

**Tier 3 — Peer-reviewed primary**: per discipline source ranking in `references/discipline_overlays.md`. Identifier-first (CAS/EC/ISO). No trade-name queries. Backward + forward citation chase from EFSA Conclusion bibliography (highest yield). For systematic archetype: mandatory.

**Tier 4 — Grey** (cite with tier flag): industry task force (COI flag), conference proceedings, theses (only if Tier 1-3 cited), preprints (label non-peer-reviewed).

**Default reject**: predatory (Beall/Cabells), non-English without verified translation, blog/advocacy claims not triangulated against T1-2, trade press except factual market context.

Document every search in `SEARCH-LOG.md`: database, date, exact query string, filters, hit count, action (include / exclude / pending).

### Phase 4 — Screening and Selection

1. **Deduplicate** by DOI primary, then fuzzy title match.
2. **Title screening** against PECO-R inclusion/exclusion from SCOPE.md. Log every exclusion with reason code (lang | scope | endpoint | quality | duplicate | predatory).
3. **Abstract screening**.
4. **Full-text screening** with study-design quality flags.
5. **Systematic archetype**: simulate dual screening (two passes with different framing — hazard-first vs exposure-first). Disagreement rate logged.
6. Build PRISMA 2020 flow (or PRISMA-ScR for scoping modifier). Write to `PRISMA-FLOW.md`. Required for `systematic_review` type and `scoping` modifier.

### Phase 4.5 — Credibility Triage (gate)

Before quality appraisal. Apply the decision tree in `references/source_ranking.md` §10 to every candidate source surviving Phase 4 screening. For each:

1. Domain → `assets/source_tier_lookup.json` → TIER
2. Domain + author affiliation → `assets/coi_flags.json` + `assets/credibility_rules.json` → BIAS_CLASS
3. Branch:
   - **PREDATORY** (per `credibility_rules.json` predatory_block list + domain_patterns): BLOCK; log to `SEARCH-LOG.md` exclusion section with reason `predatory`.
   - **UNRELIABLE** (Wikipedia, blogs, social): BLOCK for citation; permitted for discovery only.
   - **POLITICAL** (PAN, EWG, Beyond Pesticides, FoE, Greenpeace, etc. per `credibility_rules.json` political_domains list): apply **cite-replace protocol**:
     a. Locate upstream Tier 1-3 primary source.
     b. If primary Tier 1-2: cite primary, drop POLITICAL source.
     c. If primary Tier 3 peer-reviewed: verify primary actually supports claim as POLITICAL represents (selective-quote check, jurisdiction check, hazard-vs-risk check, confidence-interval check). Cite primary if verified; drop both if misrepresented.
     d. If primary Tier 4 or absent: claim not citable; drop.
     e. POLITICAL source NEVER appears in `CITATION-LEDGER.md` as standalone evidence. Exception: review's question is *about* the position itself, or narrative-critical archetype counter-evidence section.
   - **TRADE-PRESS**: permitted for market/factual context only; BLOCK if used for scientific claim.
   - **CAVEAT** (IARC and other caveat_sources per `credibility_rules.json`): ACCEPT at tier, but apply **cite-with-pairing rule** — never cite alone on the contested topic. Pair with relevant regulatory consensus (EFSA + ECHA for EU carcinogenicity claims). State framework divergence explicitly. EU regulatory consensus cited first in paragraph; CAVEAT source follows.
   - **DECLARED-COI** (industry / manufacturer / consultancy): ACCEPT with `coi` flag in ledger row; tier unchanged.
   - **NEUTRAL**: ACCEPT at tier. EFSA and ECHA are explicitly authoritative — Tier 1 NEUTRAL maintained regardless of occasional political pressure.
4. **Grey-listed publishers** (MDPI, Frontiers, Hindawi case-by-case per `credibility_rules.json` grey_listed): default Tier 3 with `peer_review_rigour: questioned` flag; downweight for contested endpoints.
5. **Echo-chamber check**: walk citation chain. If only POLITICAL or TRADE-PRESS sources cite the claim → drop. Require ≥1 independent Tier 1-3 corroborator.
6. **Hazard-vs-risk guard**: scan claim text for forbidden_unguarded phrases (per `credibility_rules.json` hazard_vs_risk_guard). Any claim crossing hazard→risk without exposure context must be reframed or dropped.
7. **Contested endpoint check** (per `credibility_rules.json` contested_endpoints list): triangulation required (≥1 Tier 1-2 + ≥1 independent Tier 3). Single-source = hedging downgrade + `[single-source]` tag.

Output: every surviving source has TIER + BIAS_CLASS + COI + peer_review_rigour fields in `CITATION-LEDGER.md`. Excluded sources logged in `SEARCH-LOG.md` with exclusion reason from enum: `predatory | unreliable | political_no_primary | political_misrepresented | trade_press_scientific | echo_chamber | hazard_risk_conflation`.

### Phase 5 — Quality Appraisal

Apply per `references/quality_appraisal.md` and contract's `quality_tools` field. Record in `EVIDENCE-TABLE.csv` (header pre-populated by skill at Phase 6 scaffold time).

Per study: source tier (from lookup), Klimisch (or equivalent), GLP Y/N, guideline-compliant Y/N, deviations, COI flag (industry-funded | regulator | independent academic | undisclosed) from `assets/source_tier_lookup.json` and `assets/coi_flags.json`.

Scoping archetype: skip Klimisch (descriptive only); source-tier still mandatory.

### Phase 6 — Thematic Synthesis

1. **Scaffold REVIEW.md** by copying the archetype template (`assets/templates/{archetype}.md`) + injecting discipline-specific sections per L1. All required headings + empty tables + `[TODO: …]` placeholders pre-populated by skill (not model).
2. **Fill, do not delete.** Model cannot remove headings or tables. Empty content = gate failure. To declare a section not applicable, write entry to `OMISSIONS.md` with Reg article justification — gate inspects.
3. Synthesise across studies, never study-by-study. Cross-study tables per endpoint section.
4. WoE per endpoint per EFSA WoE guidance (EFSA J. 2017;15(8):4971). Hedging calibrated:
   - "Demonstrated" / "established": ≥2 Klimisch 1 GLP, consistent
   - "Indicated" / "supported by": single Klimisch 1 OR multiple Klimisch 2
   - "Reported": single Klimisch 2-3, or grey triangulated
   - "Suggested but not confirmed": Klimisch 3-4 or unreplicated peer-reviewed
   - Never "proven", "definitive", "conclusive" unless EFSA Conclusion or harmonised classification supports
5. Figures rendered per `OUTPUT-CONTRACT.json` `figure_requirements`. Numbering + caption + source/license + alt-text mandatory. Chemical structures rendered from chemwise InChIKey/SMILES (or PubChem CID fallback).
6. Every quantitative claim: value + unit + species/matrix + source + CIT marker.

### Phase 7 — Citation Verification (gate)

Mandatory before delivery. For each `[CIT-N]` in REVIEW.md:

1. WebFetch the DOI/URL/CELEX; cache response.
2. Compare returned title/authors/year/journal vs claimed in `CITATION-LEDGER.md`. Mismatch → fix or remove.
3. For direct quantitative claims: fuzzy-match `quote_span` field to fetched content (normalised whitespace, case-insensitive grep).
4. For DOIs: validate against CrossRef (`WebFetch https://api.crossref.org/works/{doi}`). Stamp `crossref_match: true|false` in ledger.
5. For EFSA conclusions: verify document version + publication date.
6. For legislation: verify CELEX + current consolidated status (note amendments).
7. Stamp `fetched_at` ISO date per ledger row.

Failed citations: fix or remove. Re-verify until pass rate = 100%.

Output: `CITATION-LEDGER.md` columns per `assets/citation_formats.json` `ledger_required_fields`.

### Phase 8 — Pre-Delivery Mechanical Gate

Run the following inline Bash commands. **Any FAIL routes the model back to the indicated phase. No GATE PASS = no delivery.**

```bash
# Step 1: anchor coverage
TICKED=$(grep -c "^- \[x\]" regulatory_anchor/CHEMWISE-CHECKLIST.md)
REQUIRED=$(jq -r '.anchor_required_count' OUTPUT-CONTRACT.json)
[ "$TICKED" -ge "$REQUIRED" ] && echo "PASS anchor" || echo "FAIL anchor: $TICKED/$REQUIRED -> Phase 2"

# Step 2: identity cross-verified
grep -q "cross_verified: true" regulatory_anchor/01_identity.md && echo "PASS identity" || echo "FAIL identity -> Phase 2"

# Step 3: required sections present
jq -r '.required_sections[]' OUTPUT-CONTRACT.json | while read S; do
  grep -q "^## .*${S}" REVIEW.md && echo "PASS sec: $S" || echo "FAIL sec: $S -> Phase 6"
done

# Step 4: min citations
N_CITES=$(grep -cE '\[CIT-[0-9]+\]' REVIEW.md)
MIN=$(jq -r '.min_citations' OUTPUT-CONTRACT.json)
[ "$N_CITES" -ge "$MIN" ] && echo "PASS cites: $N_CITES" || echo "FAIL cites: $N_CITES/$MIN -> Phase 3"

# Step 5: every CIT-N resolves in ledger
grep -oE '\[CIT-[0-9]+\]' REVIEW.md | sort -u | while read C; do
  ID=$(echo $C | tr -d '[]')
  grep -q "^| ${ID} " CITATION-LEDGER.md && echo "PASS resolve $ID" || echo "FAIL unresolved $ID -> Phase 7"
done

# Step 6: every ledger row has fetched_at
awk -F'|' 'NR>2 && $0 !~ /20[0-9][0-9]-[0-1][0-9]-[0-3][0-9]/ {print "FAIL ledger row missing fetched_at: " $2}' CITATION-LEDGER.md

# Step 7: forbidden language
grep -nE "\b(proven|definitive|conclusive|obviously|clearly shows|undeniably)\b" REVIEW.md && echo "FAIL absolutist" || echo "PASS hedging"
grep -nE "[—–]" REVIEW.md && echo "FAIL em/en dash" || echo "PASS dashes"

# Step 8: unfilled placeholders
grep -nE "\[TODO|\[FILL|\[XX\]|\{\{" REVIEW.md && echo "FAIL placeholder" || echo "PASS scaffold"

# Step 9: min figures
N_FIG=$(grep -cE "^!\[" REVIEW.md)
MIN_FIG=$(jq -r '.min_figures' OUTPUT-CONTRACT.json)
[ "$N_FIG" -ge "$MIN_FIG" ] && echo "PASS figs: $N_FIG" || echo "FAIL figs: $N_FIG/$MIN_FIG -> Phase 6"

# Step 10: evidence rows
N_EV=$(($(wc -l < EVIDENCE-TABLE.csv) - 1))
MIN_EV=$(jq -r '.min_evidence_rows' OUTPUT-CONTRACT.json)
[ "$N_EV" -ge "$MIN_EV" ] && echo "PASS evidence: $N_EV" || echo "FAIL evidence: $N_EV/$MIN_EV -> Phase 5"

# Step 11: no POLITICAL sources as standalone evidence (cite-replace verified)
jq -r '.political_domains.list[]' assets/credibility_rules.json | while read D; do
  grep -q "$D" CITATION-LEDGER.md && echo "FAIL political-source in ledger: $D -> Phase 4.5" || true
done

# Step 12: no PREDATORY publishers in ledger
jq -r '.predatory_block.domain_patterns[]' assets/credibility_rules.json | while read D; do
  grep -q "$D" CITATION-LEDGER.md && echo "FAIL predatory-source in ledger: $D -> Phase 4.5" || true
done

# Step 13: no UNRELIABLE sources in ledger
jq -r '.unreliable_block.domains[]' assets/credibility_rules.json | while read D; do
  grep -q "$D" CITATION-LEDGER.md && echo "FAIL unreliable-source in ledger: $D -> Phase 4.5" || true
done

# Step 13b: CAVEAT sources (e.g. IARC) — must be paired with EU regulatory consensus on the same claim
awk -F'|' 'NR>2 && $0 ~ /CAVEAT/ {print $2}' CITATION-LEDGER.md | while read CLAIM; do
  # Verify ≥1 NEUTRAL Tier-1 EU-regulator row (efsa.europa.eu or echa.europa.eu) supports same claim
  grep -E "(efsa\.europa\.eu|echa\.europa\.eu).*${CLAIM}" CITATION-LEDGER.md >/dev/null || echo "FAIL CAVEAT-unpaired: '$CLAIM' needs EFSA or ECHA pairing -> Phase 4.5"
done

# Step 14: echo-chamber check — every advocacy/trade-press ledger row needs ≥1 tier ≤2 corroborator
awk -F'|' 'NR>2 && ($0 ~ /advocacy/ || $0 ~ /trade_press/) {print "FLAG echo-chamber risk row: " $2 " -- verify Tier 1-2 corroborator"}' CITATION-LEDGER.md

# Step 15: hazard-vs-risk guard — forbidden unguarded phrases
jq -r '.hazard_vs_risk_guard.forbidden_unguarded[]' assets/credibility_rules.json | while read P; do
  grep -inE "\b${P}\b" REVIEW.md && echo "REVIEW: hazard-risk conflation risk: '$P' -- verify exposure context cited adjacent" || true
done

# Step 16: contested-endpoint triangulation — for each contested endpoint mentioned, verify ≥2 independent sources
jq -r '.contested_endpoints.list[]' assets/credibility_rules.json | while read E; do
  if grep -qi "$E" REVIEW.md; then
    # Count distinct ledger rows supporting this endpoint
    N=$(grep -ciE "$E" CITATION-LEDGER.md)
    [ "$N" -ge 2 ] || echo "FAIL contested-endpoint single-source: '$E' has $N corroborators (need ≥2 independent) -> Phase 4.5"
  fi
done

# Step 17: quality checklist all ticked
DONE=$(grep -c "^- \[x\]" QUALITY-CHECKLIST.md)
TOTAL=$(grep -c "^- \[" QUALITY-CHECKLIST.md)
[ "$DONE" -eq "$TOTAL" ] && echo "GATE PASS" || echo "FAIL checklist: $DONE/$TOTAL"
```

Model interprets output: any `FAIL` line triggers loopback to indicated phase. Re-run gate after fixes until `GATE PASS`.

### Phase 9 — Output Delivery

Only after `GATE PASS`. Generate artefact set in working directory:

- `REVIEW.md` — main narrative (archetype-shaped)
- `SCOPE.md` — locked scope (Phase 1)
- `OUTPUT-CONTRACT.md` + `OUTPUT-CONTRACT.json` — Phase 1.5
- `SEARCH-LOG.md` — queries and database hits
- `PRISMA-FLOW.md` (or `PRISMA-SCR-FLOW.md` for scoping) — screening counts
- `EVIDENCE-TABLE.csv` — per-study structured data
- `CITATION-LEDGER.md` — verified citation registry
- `BIBLIOGRAPHY.bib` — BibTeX with `tier`, `klimisch`, `glp`, `guideline`, `coi` custom fields
- `GAPS.md` — data gaps mapped to Reg 283/284 IDs
- `LIMITATIONS.md` — methodological caveats
- `QUALITY-CHECKLIST.md` — all boxes ticked
- `OMISSIONS.md` — justified omissions (if any)
- `regulatory_anchor/` — Phase 2 cached outputs

If user selected Word output: invoke `anthropic-skills:docx` on `REVIEW.md` to produce `.docx` with EFSA-style formatting (Times New Roman 11pt or Arial 11pt, justified body, numbered headings, footnote citations if applicable).

## Behavioural Floors per Model Class

| Class | Behaviour |
|---|---|
| Strong (Opus 4.7 High) | Default flow; cross-discipline narrative integration; can extend canned Boolean blocks (log in SEARCH-LOG.md) |
| Default (Opus 4.7 Medium) | Default flow; canned Boolean blocks preferred; extension with logging permitted |
| Permitted (Sonnet 4.7) | Rapid modifier only; canned Boolean blocks mandatory; no freeform queries; scaffold fill only; `STATE.md` confirmation per phase; one chemwise call per turn max |
| Blocked (Sonnet ≤4.6, Haiku class, non-Claude) | Skill halts at Phase 1 with model-class error |

Gate is identical across classes. Quality floor invariant.

## Source Hierarchy Quick Reference

See `references/source_ranking.md` and `references/discipline_overlays.md` per-discipline rankings. Tier assignment by lookup (`assets/source_tier_lookup.json`), not model judgement.

When sources conflict, higher tier wins unless lower-tier post-dates higher-tier AND presents new data. Document conflict resolution explicitly.

## Common Pitfalls

1. **Skipping Phase 2 regulatory anchor** — gate Step 1 + 2 catch.
2. **Trade-name searches** — Phase 3 search blocks require CAS/ISO substitution.
3. **Single-database peer-reviewed search** — contract enforces `databases_min` per archetype.
4. **Treating preprints as peer-reviewed** — source-tier lookup pins preprints at Tier 4 with flag.
5. **Ignoring metabolite literature** — search blocks require metabolite tokens.
6. **Citing repealed legislation** — Phase 7 verifies CELEX consolidated status.
7. **Confusing approval status with authorisation status** — anchor distinguishes item 4 (approval) from item 3 (registration footprint).
8. **Failing to distinguish original vs amended text** — citation ledger captures document version.
9. **Quantitative claim without units/species/route/duration** — gate Step 4 + manual quant check.
10. **Synthesising study-by-study instead of thematically** — Phase 6 scaffold enforces thematic spine.
11. **"Quick review" → drop everything** — MANDATORY MINIMUMS + rapid template integrity floor.
12. **Comparative asymmetry** — gate enforces N×12 anchor + symmetric endpoint matrix.

## Bundled Resources

**Templates** (`assets/templates/`):
- `literature_review.md` — narrative/descriptive synthesis; discipline output style injection; regulatory affairs + regulatory science + technical variants
- `systematic_review.md` — PRISMA-grade; dual screening; quality appraisal; WoE per endpoint
- `database_study.md` — registry/dataset analysis; gap analysis; MRL coverage; authorisation footprint
- `data_analysis.md` — modelling/computation; FOCUS PEC; PRIMo; QSAR; trial statistics

**References** (`references/`):
- `source_ranking.md` — source ranking + bias-class + cite-replace + triangulation + echo-chamber + hazard-vs-risk decision document
- `discipline_overlays.md` — Layer 1 per-discipline sections, figures, source rankings, quality tools, anchors, output styles, preferred review types, molecular structure requirements (9 disciplines)
- `archetype_integrity_contracts.md` — Layer 2 review type integrity contracts + scope modifier contracts
- `molecular_structure_rendering.md` — structure figure rendering protocol; source priority; caption format; gate requirements
- `anchor_fallback_paths.md` — chemwise + 2 fallback URLs per anchor item
- `quality_appraisal.md` — Klimisch, OHAT, AMSTAR-2, CRED, OECD criteria

**Machine-readable assets** (`assets/`):
- `contract_schema.json` — OUTPUT-CONTRACT JSON schema
- `source_tier_lookup.json` — domain → tier
- `coi_flags.json` — domain → COI category
- `credibility_rules.json` — bias-class lookup; political_domains; predatory_block; contested_endpoints; hazard_vs_risk_guard
- `citation_formats.json` — citation style templates
- `eu_ppp_regulations.json` — CELEX index with EUR-Lex URLs (legislation lookup via WebFetch)
- `oecd_test_guidelines.json` — OECD TG URL resolver

## Integration

- **chemwise MCP** — preferred (not required) regulatory data source for Phase 2 anchor
- **anthropic-skills:data-protection** — RR sourcing for DP scope
- **anthropic-skills:docx** — Word deliverable
- **anthropic-skills:m365-email-search** — retrieve prior internal correspondence on substance if relevant
- **WebSearch / WebFetch** — Tier 2-4 sources + anchor fallbacks

## Quality Checklist (pre-delivery, machine-checked)

Generated to `QUALITY-CHECKLIST.md` at Phase 1.5; ticked through Phases 2-7; gate Step 11 confirms 100% ticked.

- [ ] Scope locked in `SCOPE.md` and confirmed by user
- [ ] Contract locked in `OUTPUT-CONTRACT.md` + `.json` (Phase 1.5)
- [ ] Anchor 12/12 (or N/12 with waivers) — `regulatory_anchor/CHEMWISE-CHECKLIST.md`
- [ ] Identity cross-verified across ≥2 sources
- [ ] Every endpoint claim tier-tagged via lookup
- [ ] Every ledger row carries bias_class (NEUTRAL / DECLARED-COI / POLITICAL excluded / TRADE-PRESS market-only / etc.)
- [ ] No POLITICAL sources as standalone evidence (cite-replace applied)
- [ ] No PREDATORY publishers in ledger
- [ ] No UNRELIABLE sources (Wikipedia, blogs, social) in ledger
- [ ] CAVEAT sources (IARC etc.) cited with EFSA/ECHA pairing + divergence noted (not alone on contested claims)
- [ ] Echo-chamber check passed (every advocacy/trade-press row has Tier 1-2 corroborator)
- [ ] Contested endpoints triangulated (≥1 Tier 1-2 + ≥1 independent Tier 3)
- [ ] Hazard-vs-risk distinction preserved (no unguarded conflation)
- [ ] PRISMA flow (or PRISMA-ScR) complete
- [ ] All citations verified (100% pass, every ledger row has `fetched_at`)
- [ ] Evidence table populated with Klimisch/equivalent per study (where archetype requires)
- [ ] Data gaps mapped to Reg 283/284 data point IDs (where applicable)
- [ ] No em-dashes / en-dashes
- [ ] No absolute language unmatched to evidence weight
- [ ] Source voice attributed explicitly (EFSA vs applicant vs author)
- [ ] Repealed/amended legislation flagged correctly
- [ ] COI flags on industry-funded sources via `assets/coi_flags.json`
- [ ] Limitations section drafted
- [ ] Figures meet contract `figure_requirements`
- [ ] No unfilled `[TODO`/`[FILL` placeholders
- [ ] Gate Step 1-11 all `PASS`

Review fails if any box unchecked. Do not deliver.
