# Literature Review: [Substance / Topic]

**Review type:** literature_review
**Scope modifier:** [comparative | scoping | rapid | none]
**Discipline(s):** [list — from Phase 1 selection]
**Use context:** [dossier / MRL / Art.12 / DP / internal R&D / regulatory position / other]
**Prepared by:** [Author] | Life Scientific
**Date:** [YYYY-MM-DD]
**Version:** 1.0

> **Integrity floor:** anchor 12/12; citation per claim; source-tier via `assets/source_tier_lookup.json`; in-force legislation verified; identity cross-verified (CAS + EC + InChIKey across ≥2 sources); search documented in `SEARCH-LOG.md`; quantitative anchors require value + unit + species/matrix + source; no PRISMA flow required (search documentation required; single-reviewer exclusion rationale logged).

---

## 1. Introduction

### 1.1 Background and Context

[Regulatory and scientific context. Why this review is required. Substance(s) in scope, relevant regulatory procedure, current regulatory status in brief. 1-3 paragraphs. Citations for any regulatory statements.]

### 1.2 Objective

[One sentence. State precisely what this review addresses: which substance(s), which endpoint(s) or regulatory question, which jurisdiction, which instrument/procedure.]

### 1.3 Regulatory Basis

[Applicable EU instruments with CELEX cited. E.g.:]

This review was conducted under [Reg (EC) No 1107/2009 [CIT-1]], specifically in relation to [Article X / Annex Y]. Relevant data requirements are set out in [Reg (EU) No 283/2013 [CIT-2]] and associated guidance documents.

---

## 2. Substance Identity

| Field | Value | Source | CIT |
|---|---|---|---|
| ISO common name | [TODO] | [TODO] | [TODO] |
| CAS RN | [TODO] | [TODO] | [TODO] |
| EC number | [TODO] | [TODO] | [TODO] |
| IUPAC name | [TODO] | [TODO] | [TODO] |
| Molecular formula | [TODO] | [TODO] | [TODO] |
| Molecular weight (g/mol) | [TODO] | [TODO] | [TODO] |
| SMILES | [TODO] | [TODO] | [TODO] |
| InChIKey | [TODO] | [TODO] | [TODO] |
| Chemical class / IRAC group | [TODO] | [TODO] | [TODO] |

![Structure of [substance name]](regulatory_anchor/02_structure.svg)
*Figure 1. 2D structure of [substance name] ([IUPAC name], CAS [RN], InChIKey [KEY]). Source: [chemwise / PubChem CID NNN], accessed [YYYY-MM-DD]. [CIT-N]*

[For analytical/chemistry disciplines: additional structures for metabolites, degradates, analogues required per `references/molecular_structure_rendering.md`.]

---

## 3. Regulatory Anchor

[EU regulatory ground truth established before evidence synthesis. All 12 items resolved via chemwise (preferred) or fallback URLs per `references/anchor_fallback_paths.md`. Waivers require justification in `regulatory_anchor/ANCHOR-MISSES.md`.]

| # | Anchor item | Value / status | Source | Accessed |
|---|---|---|---|---|
| 1 | Identity (CAS + EC + InChIKey cross-verified) | [TODO] | [TODO] | [TODO] |
| 2 | Structure (2D, verified) | Fig. 1 | [TODO] | [TODO] |
| 3 | Registration footprint (MS authorisations) | [TODO] | [TODO] | [TODO] |
| 4 | EU approval status (Reg 1107/2009, Annex in-force) | [TODO] | [TODO] | [TODO] |
| 5 | Renewal / expiry date | [TODO] | [TODO] | [TODO] |
| 6 | Substance review history (EFSA-Q refs, SANTE proc. nos.) | [TODO] | [TODO] | [TODO] |
| 7 | EFSA Conclusion metadata (title, date, journal ref) | [TODO] | [TODO] | [TODO] |
| 8 | EFSA Conclusion endpoint text (sections relevant to scope) | [TODO] | [TODO] | [TODO] |
| 9 | MRL status (Reg 396/2005 Annexes; NA if no food use) | [TODO / NA] | [TODO] | [TODO] |
| 10 | CLP harmonised classification (ECHA CLH; self-class if no CLH) | [TODO] | [TODO] | [TODO] |
| 11 | SVHC status (REACH SVHC candidate list) | [TODO] | [TODO] | [TODO] |
| 12 | BCPC Pesticide Manual entry (current edition) | [TODO] | [TODO] | [TODO] |

---

## 4. Search Methods

[Required for all literature_review type. Reproduced here to enable independent replication. Full query strings documented in `SEARCH-LOG.md` — not repeated here.]

- **Databases searched:** [list; ≥2 required; include EFSA eLibrary + ≥1 peer-reviewed database]
- **Grey literature sources:** [ECHA, RMS registers, EFSA scientific opinions, Commission Implementing Regs]
- **Search period:** [YYYY-MM-DD to YYYY-MM-DD]
- **Substance identifiers used:** CAS [RN], ISO name "[name]", EC [number], InChIKey [KEY]. Trade names not used as primary search terms.
- **Language:** English primary. [Other languages with verified translation where relevant.]
- **Inclusion criteria:** [substance + endpoint/regulatory topic in scope + study type(s) + jurisdiction]
- **Exclusion criteria:** [off-topic; predatory publishers per `assets/credibility_rules.json`; unreliable sources; grey literature without Tier 1-2 corroboration for scientific claims]
- **Source selection note:** Hierarchical — Tier 1 regulatory sources establish ground truth before peer-reviewed synthesis. Tier assignment via `assets/source_tier_lookup.json`.

Full query documentation: `SEARCH-LOG.md`.

---

## [5–N]. Discipline-Specific Content Sections

[Sections 5 onward are generated by the Phase 1.5 contract composer by injecting required section headings, sub-section order, table scaffolds, and figure requirements from `references/discipline_overlays.md` for each selected discipline. Section order follows EU dossier convention where multi-discipline: Identity → Physchem → Analytical → Mammalian tox → Residues → Efate → Ecotox → Efficacy → Exposure → Regulatory implications.]

---

### OUTPUT STYLE BY DISCIPLINE

The following output styles apply within the discipline sections. Model must not deviate.

**Regulatory affairs disciplines:**
- Primary output: structured narrative paragraphs, logically sequenced, legally precise
- Tables: approval/authorisation timeline tables, jurisdictional status matrices, classification matrices
- No cross-study data extraction tables
- Language calibrated: "approved under conditions", "candidate for substitution", "non-renewal proposed" — never "banned"
- Citations: CELEX, document version + date, EFSA-Q reference numbers, SCoPAFF outcomes, Commission Implementing Reg references
- Figures: timeline figure, jurisdictional matrix

**Regulatory science disciplines (mammalian tox / ecotox / efate / residues / efficacy / exposure):**
- Primary output: structured narrative paragraphs per endpoint group + cross-study data tables
- Tables: per-endpoint cross-study table (endpoint × species/matrix × value × units × Klimisch × GLP × OECD TG × source) required in every endpoint section
- WoE statement per endpoint section (calibrated per EFSA WoE guidance, EFSA J. 2017;15(8):4971)
- Quantitative anchors mandatory: value + unit + species/matrix + source for every numerical claim
- Source voice explicit: "EFSA concluded …" / "the applicant reported …" / "[study author] reported …"

**Technical disciplines (analytical / chemistry / phys-chem):**
- Primary output: structured narrative + tables + figures; figure-dense
- Molecular structures: mandatory for every named compound per `references/molecular_structure_rendering.md`
- Method / property tables: mandatory (validation parameters, transition lists, physchem property tables)
- Diagrams: reaction schemes, metabolic pathway diagrams, degradation pathway diagrams, chromatograms, instrument flow diagrams as applicable

---

[DISCIPLINE CONTENT PLACEHOLDER — Phase 1.5 injects required sections below this line for disciplines: {DISCIPLINE_LIST}]

---

## [N+1]. Data Gaps

[Gaps mapped to Reg 283/2013 or Reg 284/2013 data point IDs where applicable. For regulatory affairs discipline: gaps mapped to applicable Reg 1107/2009 provisions or dossier requirements.]

| Data point ID | Description | Gap nature | Regulatory implication |
|---|---|---|---|
| [Reg 283/2013 §X.Y] | [TODO] | [missing / uncertain / outdated / confirmatory required] | [TODO] |

---

## [N+2]. Regulatory Implications

[What do the findings mean for the specific regulatory context identified in §1.3? Calibrated language. Link findings to specific regulatory instruments, thresholds, or decision criteria. For regulatory affairs: legal and procedural implications. For regulatory science: endpoint-level implications for risk assessment. No absolutist language.]

---

## [N+3]. Limitations

- **Review type:** literature_review (narrative synthesis; no formal dual-screening protocol or PRISMA flow)
- **Reviewer:** Single reviewer; exclusion rationale documented in `SEARCH-LOG.md`
- **Search period:** [YYYY-MM-DD to YYYY-MM-DD]
- **Databases:** [list from §4]
- **Language:** English primary; non-English literature may be under-represented
- **[Other scope-specific limitations]**

---

## [N+4]. References

[Generated from `CITATION-LEDGER.md` in citation style selected at Phase 1. Minimum citations per `OUTPUT-CONTRACT.json min_citations`.]

---

## [N+5]. Glossary

| Acronym | Full term |
|---|---|
| ADI | Acceptable daily intake |
| ADME | Absorption, distribution, metabolism, excretion |
| AOEL | Acceptable operator exposure level |
| ARfD | Acute reference dose |
| BCPC | British Crop Production Council |
| CAS | Chemical Abstracts Service |
| CELEX | Communautaire EuropeLex (EU legal database identifier) |
| CLP | Classification, Labelling and Packaging (Reg (EC) No 1272/2008) |
| DAR | Draft Assessment Report |
| DP | Data protection |
| EC | European Commission / Enzyme Commission / European Community (context-dependent) |
| ECHA | European Chemicals Agency |
| ED | Endocrine disruptor |
| EFSA | European Food Safety Authority |
| EFSA-Q | EFSA question number (unique document identifier) |
| GAP | Good Agricultural Practice |
| GLP | Good Laboratory Practice |
| HR | Highest residue |
| IESTI | International estimated short-term intake |
| InChIKey | International Chemical Identifier Key (IUPAC) |
| IUPAC | International Union of Pure and Applied Chemistry |
| MoA | Mode of action |
| MRL | Maximum residue level |
| MS | Member State |
| NOAEL | No observed adverse effect level |
| NOEC | No observed effect concentration |
| OECD | Organisation for Economic Co-operation and Development |
| PEC | Predicted environmental concentration |
| PHI | Pre-harvest interval |
| PPP | Plant protection product |
| RAR | Renewal Assessment Report |
| RMS | Rapporteur Member State |
| SAR | Structure-activity relationship |
| SCoPAFF | Standing Committee on Plants, Animals, Food and Feed |
| SMILES | Simplified Molecular Input Line Entry System |
| STMR | Supervised trials median residue |
| SVHC | Substance of very high concern |
| WoE | Weight of evidence |

[Expand on first use in text. Add discipline-specific acronyms as required.]
