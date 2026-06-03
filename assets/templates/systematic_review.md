# Systematic Review: [Substance] — [Endpoint / Research Question]

**Review type:** systematic_review
**Scope modifier:** [comparative | scoping | rapid | none]
**Discipline(s):** [list — from Phase 1 selection]
**PECO-R:**
  - P (Population): [organism, species, matrix, life stage]
  - E (Exposure): [substance ISO name, CAS RN, route, duration, concentration range]
  - C (Comparator): [untreated control / reference substance / regulatory threshold]
  - O (Outcome): [specific endpoints — e.g., NOAEL, LC50, DT50, LOQ, binding affinity]
  - R (Regulatory context): [instrument, Annex point, jurisdiction — e.g., Reg 283/2013 §X.Y, EFSA Guidance Doc YYYY]
**Use context:** [ED assessment / substitution evaluation / litigation defence / scientific opinion / dossier support / other]
**Prepared by:** [Author] | Life Scientific
**Date:** [YYYY-MM-DD]
**Protocol pre-specified:** [Yes — SCOPE.md dated YYYY-MM-DD | No — rationale: [state reason]]

> **Integrity floor:** PRISMA 2020 flow mandatory; dual-screening simulation documented (two passes, disagreement rate logged); quality appraisal per study via discipline-appropriate tool (Klimisch / ToxRTool / CRED / OHAT RoB / AMSTAR-2); WoE per endpoint per EFSA guidance (EFSA J. 2017;15(8):4971); anchor 12/12; citation per claim; quantitative anchors require value + unit + species/matrix + source; in-force legislation verified; ≥3 databases + grey literature.

---

## 1. Introduction

### 1.1 Background

[Regulatory and scientific context. Substance in scope. Why a systematic review is required (ED assessment, dispute resolution, substitution evaluation, etc.). Current regulatory status in brief. Citations for regulatory statements.]

### 1.2 Research Question

[PECO-R stated as prose.]

### 1.3 Regulatory Basis

[Applicable instruments and guidance with CELEX. Specific Annex/Article driving the question.]

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

[Additional structures for metabolites, degradates per `references/molecular_structure_rendering.md` where discipline requires.]

---

## 3. Regulatory Anchor

| # | Anchor item | Value / status | Source | Accessed |
|---|---|---|---|---|
| 1 | Identity (CAS + EC + InChIKey cross-verified) | [TODO] | [TODO] | [TODO] |
| 2 | Structure (2D, verified) | Fig. 1 | [TODO] | [TODO] |
| 3 | Registration footprint | [TODO] | [TODO] | [TODO] |
| 4 | EU approval status | [TODO] | [TODO] | [TODO] |
| 5 | Renewal / expiry date | [TODO] | [TODO] | [TODO] |
| 6 | Substance review history | [TODO] | [TODO] | [TODO] |
| 7 | EFSA Conclusion metadata | [TODO] | [TODO] | [TODO] |
| 8 | EFSA Conclusion endpoint text | [TODO] | [TODO] | [TODO] |
| 9 | MRL status (NA if no food use) | [TODO / NA] | [TODO] | [TODO] |
| 10 | CLP harmonised classification | [TODO] | [TODO] | [TODO] |
| 11 | SVHC status | [TODO] | [TODO] | [TODO] |
| 12 | BCPC Pesticide Manual entry | [TODO] | [TODO] | [TODO] |

---

## 4. Methods

### 4.1 Protocol

[Protocol documented in `SCOPE.md` before any searching commenced (date: [YYYY-MM-DD]). Deviations from protocol, if any, noted here with rationale.]

### 4.2 Eligibility Criteria

**Inclusion:**

| Criterion | Specification |
|---|---|
| Population / organism | [species, strain, life stage, sex — or open if scoped broadly] |
| Exposure | [CAS [RN], ISO name, synonyms; route; duration; concentration range] |
| Outcome | [specific endpoints from PECO-R] |
| Study design | [GLP guideline-compliant; non-GLP with Klimisch ≤ 2; peer-reviewed; other] |
| Jurisdiction | [EU-wide / global; specific regulatory contexts included] |
| Language | [English; [other languages] with verified translation] |
| Date range | [YYYY-MM-DD to YYYY-MM-DD; rationale for window] |

**Exclusion:**

| Code | Criterion |
|---|---|
| `scope` | Off-endpoint / off-substance |
| `quality` | Klimisch 4 without supporting higher-tier data |
| `lang` | Non-English without verified translation |
| `predatory` | Predatory publisher per `assets/credibility_rules.json` |
| `duplicate` | Superseded by newer pivotal study (superseding study cited) |
| `unreliable` | Wikipedia, blog, social — discovery only, not citation |
| `echo_chamber` | Only POLITICAL/TRADE-PRESS sources support claim; no Tier 1-3 corroboration |

### 4.3 Information Sources

| Database / register | Coverage type | Date searched | Query ref (SEARCH-LOG.md) |
|---|---|---|---|
| EFSA eLibrary | Regulatory conclusions, opinions, supporting publications | [YYYY-MM-DD] | #S01 |
| ECHA registered dossiers / CLH | REACH/CLP endpoints | [YYYY-MM-DD] | #S02 |
| PubMed / MEDLINE | Peer-reviewed biomedical | [YYYY-MM-DD] | #S03 |
| [≥1 additional peer-reviewed DB] | | [YYYY-MM-DD] | #S04 |
| EU Pesticides Database | MRL, approval status | [YYYY-MM-DD] | #S05 |
| [Grey: RMS RAR/DAR register] | Regulatory grey | [YYYY-MM-DD] | #S06 |

### 4.4 Search Strategy

[Canned Boolean blocks from `assets/search_blocks/{discipline}/{endpoint}.txt` used. Substance identifiers: CAS [RN], ISO name "[name]", EC [number], InChIKey [KEY]. No trade-name-only queries. Full strings: `SEARCH-LOG.md`.]

### 4.5 Study Selection and Screening

**Pass 1 — Title and abstract screening:** [criteria applied; decision rule]

**Pass 2 — Full-text screening:** [criteria applied; minimum Klimisch threshold; study design check]

**Dual-screening simulation:** Two independent screening passes conducted with different framings — Pass A (hazard-endpoint primary framing) and Pass B (exposure/dose primary framing). Disagreement rate: [N discordant / N total screened = X%]. Discordant records resolved by [rule: e.g., conservative inclusion / anchor against EFSA Conclusion].

### 4.6 Data Extraction

Fields extracted per study:

| Field | Definition |
|---|---|
| Reference [CIT-N] | Author, year, journal/source, DOI |
| Study type | GLP guideline / non-GLP peer-reviewed / grey |
| Species / organism | Latin binomial where available |
| Route / matrix | Oral / dermal / inhalation / aquatic / soil / etc. |
| Duration | Days/weeks/generations |
| Endpoint(s) | As reported |
| Key value | NOAEL / NOEC / LC50 / EC50 / DT50 / LOQ / etc. |
| Units | mg/kg bw/d / mg/L / mg/kg / etc. |
| n (per group) | Number of replicates or animals |
| Klimisch | 1 / 2 / 3 / 4 |
| GLP | Y / N |
| OECD TG | Number where applicable |
| Deviations | Y / N — detail if Y |
| COI | Independent / industry-funded / regulator / undisclosed |
| Source tier | 1 / 2 / 3 / 4 via `assets/source_tier_lookup.json` |

Full extraction: `EVIDENCE-TABLE.csv`.

### 4.7 Quality Appraisal

[Quality tool(s) per `references/quality_appraisal.md` and discipline overlay. Applied per study. Recorded in `EVIDENCE-TABLE.csv`.]

| Discipline | Primary tool | Secondary tool |
|---|---|---|
| Mammalian tox | Klimisch + ToxRTool | OHAT RoB (epidemiology), AMSTAR-2 (included SRs) |
| Ecotox | Klimisch + CRED (Moermond 2016) | SETAC RoB where applicable |
| Efate | OECD TG conformity + FOCUS Kinetics 2014 compliance | Klimisch |
| Residues | OECD TG conformity + GAP alignment | SANCO/7525 sufficiency check |
| Analytical | SANTE/11312/2021 pass/fail | — |
| Chemistry | Structural verification + mechanism plausibility | — |

### 4.8 Synthesis Approach

Thematic synthesis by endpoint group, not study-by-study narrative. Cross-study tables per endpoint. WoE per endpoint per EFSA WoE guidance (EFSA J. 2017;15(8):4971 [CIT-N]). Hedging calibrated:

- "Demonstrated" / "established": ≥2 Klimisch 1 GLP, consistent findings across species/routes
- "Indicated" / "supported by": single Klimisch 1 OR multiple Klimisch 2, broadly consistent
- "Reported": single Klimisch 2-3, or grey triangulated against Tier 1-2
- "Suggested but not confirmed": Klimisch 3-4 or unreplicated peer-reviewed finding

Quantitative meta-analysis where ≥3 comparable studies permit; narrative synthesis otherwise.

---

## 5. Study Selection Results (PRISMA 2020)

[Full PRISMA flow in `PRISMA-FLOW.md`. Summary reproduced here.]

| Stage | Records (n) | Notes |
|---|---|---|
| Identified via databases + registers | [TODO] | |
| Duplicates removed | [TODO] | |
| Records screened (title / abstract) | [TODO] | |
| Records excluded at title / abstract | [TODO] | [primary reason codes] |
| Full-text reports assessed | [TODO] | |
| Full-text reports excluded | [TODO] | [reason codes: `scope` / `quality` / `lang` / `predatory` / `duplicate`] |
| Studies included in synthesis | [TODO] | |

---

## 6. Characteristics of Included Studies

[Overview of included study set. One row per unique study.]

| Ref [CIT] | Study type | Species / organism | Route / matrix | Duration | Key endpoints | Klimisch | GLP | COI flag |
|---|---|---|---|---|---|---|---|---|
| [TODO] | | | | | | | | |

---

## [7–N]. Discipline-Specific Results and Synthesis

[Sections injected from L1 discipline overlay(s). Phase 1.5 contract composer injects required endpoint sections per `references/discipline_overlays.md` for each selected discipline. Section order follows EU dossier convention where multi-discipline.]

---

### REQUIRED STRUCTURE PER ENDPOINT SECTION

Each endpoint section must contain all three elements:

**[N.1] Narrative synthesis**
[Thematic. Cross-study, not study-by-study. Source voice explicit: "EFSA concluded …", "the applicant reported …", "[Author et al. year] found …". Calibrated hedging.]

**[N.2] Cross-study data table**

| Study [CIT] | Species / organism | Route / matrix | Duration | [Endpoint] value | Units | n | Klimisch | GLP | OECD TG | Deviations | COI |
|---|---|---|---|---|---|---|---|---|---|---|---|
| [TODO] | | | | | | | | | | | |

**[N.3] WoE statement**
"Based on [N] studies ([Klimisch 1: N1; Klimisch 2: N2; Klimisch 3: N3]), with [consistent / inconsistent / conflicting] findings, [substance name] [hedging verb per §4.8] [endpoint conclusion with quantitative anchor: value + units + species/route]. [Single-source tag if applicable.]"

---

[DISCIPLINE CONTENT PLACEHOLDER — Phase 1.5 injects endpoint sections below]

---

## [N+1]. Weight of Evidence Summary

| Endpoint | Studies (n) | Klimisch range | Consistency | WoE conclusion | Confidence | Key value |
|---|---|---|---|---|---|---|
| [TODO] | | | [consistent / variable / conflicting] | | [high / medium / low / insufficient] | |

---

## [N+2]. Data Gaps

| Reg 283/2013 data point | Description | Gap nature | Priority |
|---|---|---|---|
| [§X.Y] | [TODO] | [missing / uncertain / confirmatory] | [critical / moderate / low] |

---

## [N+3]. Regulatory Implications

[Endpoint-level implications for risk assessment. Link WoE conclusions to regulatory decision criteria: NOAEL vs ADI/ARfD derivation, ED screening criteria per Reg 2018/605, substitution thresholds per Reg 2015/408, etc. Calibrated language. No absolutist statements.]

---

## [N+4]. Limitations

- **Review type:** systematic_review (dual-screen simulation — not independent dual reviewer)
- **Reviewer:** Single institution
- **Search period:** [YYYY-MM-DD to YYYY-MM-DD]
- **Databases:** [list from §4.3]
- **Language bias:** English primary; non-English literature may be under-represented
- **Study availability:** GLP proprietary studies accessible only via EFSA Conclusion or RMS RAR; raw data not independently verifiable
- **[Other scope-specific limitations]**

---

## [N+5]. References

[Generated from `CITATION-LEDGER.md`. Minimum citations per `OUTPUT-CONTRACT.json min_citations`.]

---

## [N+6]. Glossary

[Same standard glossary as `literature_review.md §Glossary`. Add discipline-specific acronyms.]
