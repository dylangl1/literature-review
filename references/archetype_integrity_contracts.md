# Review Type Integrity Contracts (Layer 2)

Integrity guarantees per review type and scope modifier. Each type sets screening rigour, length floor/cap, figure requirements, and forbidden behaviours — but cannot relax the **universal integrity floor** below.

---

## Universal Integrity Floor (ALL types, ALL modifiers)

Non-negotiable regardless of review type, scope modifier, or model class:

1. **Anchor 12/12** — all items in `references/anchor_fallback_paths.md` resolved (chemwise OR fallback URL). Waivers require justification in `regulatory_anchor/ANCHOR-MISSES.md`.
2. **Citation per claim** — no orphan claims. Every quantitative value, regulatory statement, study reference carries an inline `[CIT-N]` resolving to `CITATION-LEDGER.md`.
3. **Quantitative anchors** — value + unit + species/matrix + source. Missing any one = orphan = gate FAIL.
4. **Source-tier flag per cite** — Tier 1-4 visible in `BIBLIOGRAPHY.bib` and ledger. Assigned via `assets/source_tier_lookup.json`, not model judgement.
5. **In-force legislation check** — repealed/amended cites flagged or replaced. CELEX consolidated status verified (Phase 7).
6. **Identity verification** — CAS + EC + InChIKey resolved across ≥2 independent sources before any search. Trade-name-only searches forbidden.
7. **Date stamps** — search date per query in `SEARCH-LOG.md`; accessed date per cited URL/DOI.
8. **Limitations section** — mandatory. Flag single-reviewer, time-box, search scope.
9. **No absolutist language** — "proven", "definitive", "conclusive", "obviously", "clearly shows", "undeniably" are forbidden.
10. **No em-dashes or en-dashes** — single hyphens, parentheses, commas, periods only.
11. **Source voice attributed** — "EFSA concluded …" / "the applicant reported …" / "[Author] found …" — not collapsed to passive.
12. **Structure figure** — parent compound structure mandatory in §2 Substance Identity, all types. Per `references/molecular_structure_rendering.md`.

---

## Review Type 1: literature_review

**Use cases:** Narrative/descriptive evidence synthesis without predefined search criteria. Standard for regulatory affairs (Art.12 review, Art.43, approval history, regulatory position, DP check). Also standard for routine endpoint summaries in regulatory science disciplines where systematic protocol is not required or proportionate.

**Template:** `assets/templates/literature_review.md`

### Failure modes

- Search undocumented ("based on available literature" with no database list, no dates)
- No source hierarchy applied — peer-reviewed and grey cited at equal weight
- Tables absent for regulatory science disciplines
- Figures absent for technical/chemistry disciplines
- Regulatory language imprecise ("banned" used instead of "non-renewal proposed")
- Source voice collapsed to passive, losing the distinctions between EFSA / applicant / author
- Anchor skipped on grounds that "regulatory review scope does not need it"

### Integrity guarantees

- **Search documented** in `SEARCH-LOG.md`: databases, dates, strings, hit counts. ≥2 sources searched.
- **No PRISMA flow required** — but search rationale and inclusion/exclusion logic documented in §4 of template.
- **Output style enforced per discipline:**
  - Regulatory affairs: narrative paragraphs + regulatory tables (timeline, approval matrix, classification matrix). No cross-study data extraction tables.
  - Regulatory science: narrative paragraphs + cross-study endpoint tables per section + WoE statement per endpoint.
  - Technical (analytical/chemistry/phys-chem): figure-primary; structures rendered per `references/molecular_structure_rendering.md`; property/validation tables per method/compound.
- **Minimum source counts by discipline:**
  - Regulatory affairs: ≥5 sources; ≥3 Tier 1 (EU instruments + EFSA Conclusions)
  - Regulatory science: ≥10 sources; ≥2 Tier 1; ≥3 peer-reviewed Tier 3
  - Technical: ≥8 sources; ≥2 Tier 1 guidance documents; ≥3 peer-reviewed Tier 3
- **Minimum quantitative anchors:** 3 (regulatory affairs) / 5 (regulatory science) / 5 (technical), each with value + unit + species/matrix + source.
- **Forbidden:** "based on limited data, no conclusion can be drawn" without citing what data were found and what they showed. Data gaps must be mapped, not asserted.

---

## Review Type 2: systematic_review

**Use cases:** Structured, protocol-driven evidence synthesis. Required for: ED assessment (Reg 2018/605), substitution candidate evaluation (Reg 2015/408), litigation defence, scientific opinion drafting, contested endpoint review.

**Template:** `assets/templates/systematic_review.md`

### Failure modes

- "Systematic" label claimed without formal protocol, I/E criteria, or PRISMA flow
- Dual screening absent or simulated in a way that does not vary framing between passes
- RoB or quality appraisal applied inconsistently across study types
- AMSTAR-2 skipped for included systematic reviews
- WoE table absent at end of synthesis
- Study-by-study narration instead of thematic synthesis
- Protocol written after data collection (post-hoc; must be declared)

### Integrity guarantees

- **Protocol pre-specified** in `SCOPE.md` before searching. Post-hoc protocol permitted only with explicit declaration and rationale.
- **PRISMA 2020 flow mandatory** (or PRISMA-ScR if scoping modifier applied). Full flow in `PRISMA-FLOW.md`.
- **Dual-screening simulation:** two independent passes — Pass A (hazard-endpoint primary framing), Pass B (exposure/dose primary framing). Disagreement rate logged. Discordance rule stated.
- **Quality appraisal per study:** Klimisch (tox/ecotox/efate/residues); CRED (ecotox non-GLP); OHAT RoB (epidemiology); AMSTAR-2 (included SRs). Tool recorded per study in `EVIDENCE-TABLE.csv`.
- **WoE per endpoint** per EFSA guidance (EFSA J. 2017;15(8):4971 [CIT-N]). Summary WoE table mandatory.
- **Minimum databases:** ≥3 peer-reviewed + grey lit handsearch + EFSA/ECHA/RMS registers.
- **Minimum source counts:** ≥15 citations; ≥2 Tier 1; ≥5 peer-reviewed Tier 3 with Klimisch recorded.
- **Minimum quantitative anchors:** 8, each with value + unit + species/matrix + source.
- **Thematic synthesis required:** cross-study tables per endpoint section. No study-by-study narrative paragraphs.
- **Length:** 10,000-40,000 words depending on endpoint scope and discipline.
- **Forbidden:** GRADE alone without WoE table; "systematic review" label with single database; endpoint conclusions from single study without [single-source] tag.

---

## Review Type 3: database_study

**Use cases:** Analysis of existing datasets or registries. Examples: MRL coverage analysis (EU Pesticides Database), resistance monitoring database query (IRAC/HRAC/FRAC registries), residue trial meta-dataset analysis, MRL-setting support via Art.12 database query.

**Template:** `assets/templates/database_study.md`

### Failure modes

- Dataset provenance not documented (version, access date, custodian)
- Extraction logic not reproducible
- Gap analysis omitted or narrative-only ("some MRLs are missing")
- Dataset version mismatch — citing old snapshot as current
- Confusing dataset coverage gaps with substance-specific data gaps

### Integrity guarantees

- **Dataset provenance documented:** name, custodian, version/snapshot date, URL, access date, CIT-N in ledger.
- **Extraction logic documented** in §5.1: fields, filters, query logic. Reproducible by a second person.
- **Gap analysis explicit:** missing cells, missing jurisdictions, default MRLs applied vs. set MRLs, data LOD vs. MRL explicitly distinguished.
- **Summary tables mandatory:** at minimum one overview summary table + one gap analysis table.
- **No synthesis prose for dataset rows** — tabulate; interpret in Discussion. Do not say "MRL coverage appears adequate" without a table supporting it.
- **Version-dependency flagged:** note that results are valid as of snapshot date; regulatory status changes with legislative amendments.
- **Minimum citations:** ≥5; ≥2 Tier 1 (EU legislation underpinning the database).
- **Minimum quantitative anchors:** 3 (summary statistics with n, unit, source).

---

## Review Type 4: data_analysis

**Use cases:** Modelling or computational analysis producing new outputs. Examples: FOCUS Step 1 PEC modelling, PRIMo dietary exposure calculation, QSAR prediction run, FOCUS STEP 3/4 surface water modelling, statistical analysis of efficacy trial data, BMD modelling.

**Template:** `assets/templates/data_analysis.md`

### Failure modes

- Input parameters undocumented (value dropped in without source or CIT)
- Model version unstated
- Regulatory endorsement of model not cited
- Regulatory threshold comparison missing or narrative-only
- Sensitivity analysis absent when input parameters carry material uncertainty
- QSAR applicability domain not checked
- Step 1 worst-case outputs presented without acknowledging conservatism

### Integrity guarantees

- **Model/tool version documented** with regulatory endorsement citation.
- **All input parameters tabled:** value + unit + source + CIT-N. No input without a source.
- **Outputs tabled:** value + unit + scenario + comparison vs. regulatory threshold.
- **Regulatory threshold comparison mandatory** — explicit RQ/MoE table or pass/fail matrix.
- **Sensitivity analysis required** where any input parameter carries uncertainty range of >×2.
- **Model step/tier declared** with inherent conservatism noted (Step 1 worst-case, Step 3 realistic worst-case, etc.).
- **Figures required:** ≥1 output figure (PEC distribution vs RAC, or intake bar vs ADI, or predicted vs observed, or dose-response) + structure figure.
- **QSAR applicability domain** documented for any in silico outputs.
- **Minimum citations:** ≥5; ≥2 Tier 1 (model guidance document + regulatory basis document).
- **Minimum quantitative anchors:** 5 (each input + output parameter pair with value + unit + source).

---

## Scope Modifier A: rapid

**Applies to:** any review type. Narrows question scope; does NOT reduce data integrity requirements.

### What rapid changes

- **Scope:** one substance × one endpoint cluster × one regulatory question.
- **Length cap:** ≤2,000 words narrative (tables and figures excluded from count).
- **Screening:** single pass, top-20 hits per endpoint via canned Boolean blocks only.
- **Minimum sources:** 5 (vs. type-specific minimum); ≥1 Tier 1 regulatory; ≥1 peer-reviewed Tier 3.
- **Minimum quantitative anchors:** 3.
- **Minimum figures:** ≥1 structure (parent) + ≥1 endpoint summary table.
- **Anchor:** still 12/12 — non-negotiable even for rapid.

### What rapid does NOT change

- Citation per claim.
- Source-tier assignment via lookup.
- Identity verification.
- Bias-class screening.
- Hazard-vs-risk distinction.
- No absolutist language.
- No em/en dashes.

### Forbidden in rapid

- Narrative-only output with no tables.
- "Generally", "typically", "is known to" without citation.
- Collapsing anchor table to fewer than 12 rows.
- Reducing scope of anchor coverage below 12/12.

---

## Scope Modifier B: comparative

**Applies to:** any review type. Compares ≥2 substances symmetrically.

### Integrity guarantees

- **Comparator selection criteria** written to `SCOPE.md` before data work. Inclusion basis explicit (same MoA / same chemical class / same target / same regulatory status). User confirms.
- **Symmetric data matrix mandatory.** For each comparator: full 12-item anchor + same endpoint set. Missing cell = explicit "data not available [source checked: X, Y on YYYY-MM-DD]" — not blank.
- **Per-comparator anchor:** full Phase 2 run for each substance. N substances × 12 = minimum calls.
- **Endpoint set locked** in SCOPE.md, applied identically across all comparators.
- **Source-tier parity check:** gate fails if Comparator A cites only Tier 1 and Comparator B only Tier 3 without explicit justification.
- **Divergence section mandatory:** explicit convergence + divergence + hypothesised drivers.
- **Forbidden:** ranking without evidence-weighted scoring; "X is safer than Y" without endpoint-specific MoE/RQ comparison; aggregating non-homologous endpoints.
- **Structure grid mandatory:** all comparator parent structures in a single composite figure.

---

## Scope Modifier C: scoping

**Applies to:** literature_review and systematic_review types. Maps evidence landscape; does not synthesise or appraise quality.

### Integrity guarantees (per Arksey/O'Malley + JBI 2020)

- **Protocol mandatory** in `SCOPE.md` before searching: research question in PCC format (Population, Concept, Context — NOT PECO-R), eligibility criteria, sources, charting fields, planned categories.
- **PCC framework** replaces PECO-R for question framing.
- **Source coverage:** ≥3 databases + ≥2 grey sources + handsearch of EFSA/ECHA/RMS registers.
- **Charting form mandatory:** structured extraction to `SCOPING-CHART.csv` — author, year, jurisdiction, substance, endpoint, study type, method, key finding, source tier.
- **No quality appraisal** — source tier still mandatory per item, but Klimisch not applied.
- **Evidence map mandatory:** matrix or bubble plot (endpoints × study type × evidence volume).
- **Gap map mandatory:** empty-cell visualisation.
- **No synthesis prose.** Descriptive only. Forbidden: "evidence suggests", "WoE indicates", "results support", "data confirm".
- **PRISMA-ScR flow mandatory** (scoping extension).
- **Anchor still 12/12.**
- **No recommendations prose** — conclusions state only "further evidence required on X" or "evidence gap identified for Y".

---

## Cross-type rules

1. No type or modifier permits skipping the 12-item anchor.
2. No type or modifier permits orphan claims.
3. No type or modifier permits citation from memory — every cite must have been WebFetched or chemwise-retrieved with `fetched_at` timestamp.
4. Length caps are output quality guides, not gates — but output below the minimum word count for a type auto-triggers user confirmation before delivery.
5. User overrides can extend depth; cannot reduce below the type integrity floor.
6. Bias-class screening (Phase 4.5 / `assets/credibility_rules.json`) applies to all types.
7. Phase 8 mechanical gate runs identically across all types and modifiers.
