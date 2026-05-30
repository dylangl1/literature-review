# Archetype Integrity Contracts (Layer 2)

Failure modes + integrity guarantees per archetype. Each archetype sets depth, screening rigour, length cap, figure floor — but cannot relax the **universal integrity floor** (anchor coverage, citation per claim, source-tier per cite, in-force legislation check, identity verification).

---

## Universal integrity floor (applies to EVERY archetype)

Non-negotiable regardless of "quick", "narrow", or model class:

1. **Anchor coverage 12/12** — every anchor item in `anchor_fallback_paths.md` must resolve (chemwise OR fallback URL). Coverage gate non-negotiable.
2. **Citation per claim** — no orphan claims. Every quantitative value, regulatory statement, study reference carries an inline `[CIT-N]` resolving to `CITATION-LEDGER.md`.
3. **Quantitative anchors require**: value + unit + species/matrix + source. Missing any one = orphan.
4. **Source-tier flag per cite** — Tier 1-4 visible in `BIBLIOGRAPHY.bib` and ledger.
5. **In-force legislation check** — repealed/amended cites flagged or replaced.
6. **Identity verification** — CAS / EC / InChIKey resolved before any search. Trade-name-only searches forbidden.
7. **Date stamps** — search date per query in `SEARCH-LOG.md`; accessed date per cited URL/DOI.
8. **Caveats section** — Limitations subsection mandatory (single-reviewer, time-box, single-screen flagged).

---

## Rapid / quick review

**Use**: time-boxed scoping for a narrow question. NOT for shallow data coverage.

### Failure modes (observed)

- Model skips anchor entirely ("just answers from training data")
- Single web search → narrative summary, no source tier, no citations
- Structure dropped, narrative-only output
- Trade-name search misses substance
- "Quick" interpreted as "fewer sources allowed"
- Length cap met by truncating data section, not narrative

### Integrity guarantees

- **Scope narrowed, not data narrowed.** Rapid = narrow question (one substance × one endpoint cluster). Anchor still 12/12.
- **Mandatory 5-block structure** (pre-scaffolded):
  1. Identity and scope (CAS, EC, ISO common name, structure image, PECO-R one-line)
  2. Regulatory anchor (12-row table; source + date per row)
  3. Key findings — top 3-5 endpoints; quantitative anchors with units, species, source per claim
  4. Gaps (mapped to Reg 283/284 data point IDs where applicable)
  5. References (≥5 sources, ≥1 Tier-1 regulatory)
- **Min source count**: 5 cited sources, ≥1 EFSA/RMS/ECHA, ≥1 peer-reviewed Tier 3.
- **Min quantitative anchors**: 3 (each with value + unit + species/matrix + source).
- **Length cap**: ≤2000 words narrative (tables don't count).
- **Forbidden in rapid**: narrative-only claims; "generally", "typically", "is known to" without citation; collapsed anchor table.
- **Screening**: single-pass, top-20 hits per endpoint, deterministic canned Boolean blocks only.
- **Figures**: ≥1 structure (parent substance) + ≥1 endpoint summary table.

---

## Structured (default)

**Use**: dossier support, RAR contribution, internal scientific decision, MRL setting, ED assessment first pass.

### Failure modes

- Section depth uneven across endpoints
- WoE skipped or merged into narrative
- Cross-jurisdictional section reduced to one-liner
- Data gaps not mapped to specific Reg data points
- Citation density drops in late sections (fatigue effect)

### Integrity guarantees

- Full IMRaD-extended structure (15 sections per `templates/structured.md`)
- PRISMA 2020 flow diagram mandatory
- Cross-study tables every endpoint section (≥1 row per included study)
- WoE per endpoint per EFSA WoE guidance (EFSA J. 2017;15(8):4971)
- Cross-jurisdictional section with explicit EU vs US vs other table
- Data gaps mapped to Reg 283/2013 or 284/2013 data point IDs
- Single-reviewer with documented exclusion rationale
- 3 academic databases + grey lit handsearch
- Length: 8000–15000 words narrative

---

## Systematic (PRISMA-grade)

**Use**: regulatory dispute, litigation defence, scientific opinion drafting, ED categorisation for substitution.

### Failure modes

- "Systematic" claimed without dual screening
- RoB applied inconsistently across study types
- Protocol not registered or not pre-specified
- AMSTAR-2 skipped for included SRs
- GRADE / WoE table missing

### Integrity guarantees

- Pre-registered protocol section (or rationale for not registering)
- Dual-screening simulation: two independent passes with different framing (hazard-first vs exposure-first); disagreement rate logged
- RoB applied per study type per `references/quality_appraisal.md`
- AMSTAR-2 for every included systematic review
- GRADE / WoE table per endpoint
- PRISMA 2020 + PRISMA-S (search extension) + PRISMA-RR (rapid extension — only for rapid)
- All databases + grey lit + backward + forward citation chasing
- Length: 15000–40000 words narrative

---

## Comparative

**Use**: substitution candidate evaluation, alternatives analysis, cross-jurisdictional decision divergence, MoA family review.

### Failure modes

- Asymmetric data — comparator A deep, B shallow; false equivalence drawn
- Cherry-picked comparators
- Inconsistent endpoint set across comparators
- Different jurisdictional time windows compared as equivalent
- Aggregated dissimilar endpoints
- Ranking presented without evidence-weighted scoring

### Integrity guarantees

- **Comparator selection criteria** written to `SCOPE.md` before any data work. Inclusion basis explicit (same MoA / same chemical class / same target / same regulatory status). User confirms.
- **Symmetric data matrix mandatory.** For each comparator: full 12-item anchor + same endpoint set. Missing cell = explicit `data not available [source checked: X, Y on date]` not blank.
- **Per-comparator anchor**: full Phase 2 run for each substance. N substances × 12 = N×12 calls minimum.
- **Endpoint normalisation**: endpoint set locked in SCOPE, applied to all comparators identically.
- **Time-window lock**: same window per comparator, or different windows declared in caption.
- **Source-tier parity check**: gate fails if comparator A cites only Tier-1 and B only Tier-3 without explicit justification.
- **Divergence section mandatory**: explicit convergence + divergence + hypothesised drivers (different MoA / different data vintage / jurisdictional difference / formulation difference).
- **Structure (matrix-first)**:
  1. Scope + comparator selection criteria
  2. Comparator framework (axes locked)
  3. Per-axis tables (rows = comparators)
  4. Convergence
  5. Divergence + hypothesised drivers
  6. Implications
- **Forbidden**: ranking without evidence-weighted scoring; aggregating non-homologous endpoints; "X is safer than Y" without endpoint-specific MoE/RQ comparison.
- **Figures**: structure grid for all comparators; jurisdictional matrix.

---

## Scoping

**Use**: map evidence landscape, identify gaps, scope a future systematic review, characterise emerging substance literature.

### Failure modes

- Treated as narrative review → loses charting discipline
- No protocol → unreplicable
- No gap map → no deliverable value
- Single database → biased map
- Synthesis prose written ("evidence suggests…") — wrong for scoping

### Integrity guarantees (Arksey/O'Malley + JBI 2020)

- **Protocol mandatory** in SCOPE.md before searching: research question (PCC), eligibility, sources, charting fields, planned categories.
- **PCC framework** (Population, Concept, Context) — not PECO-R.
- **Source coverage**: ≥3 databases + ≥2 grey sources + handsearch of EFSA/ECHA/RMS registers.
- **Charting form mandatory**: structured extraction to `SCOPING-CHART.csv` — author, year, jurisdiction, substance, endpoint, study type, method, key finding, source tier.
- **No quality appraisal required** (scoping doesn't appraise) — but source-tier still mandatory per item.
- **Evidence map mandatory**: matrix or bubble plot (endpoints × study type × volume).
- **Gap map mandatory**: empty-cell visualisation.
- **No synthesis prose.** Descriptive only. Forbidden: "evidence suggests", "WoE indicates", "results support".
- **PRISMA-ScR flow** mandatory (scoping extension).
- Anchor still 12/12.
- **Structure**:
  1. Background + objective
  2. Methods (PCC, eligibility, sources, charting)
  3. Results (PRISMA-ScR flow, characteristics table, evidence map, gap map)
  4. Discussion (gaps, implications for further research)
  5. Conclusion (no recommendation prose; only "further evidence required on X")

---

## Narrative-critical

**Use**: expert position paper, regulatory commentary, MoA narrative for internal R&D, historical perspective.

### Failure modes

- Confirmation bias / unbalanced citation
- No search documentation
- No quality scoring
- Expert opinion masquerading as evidence

### Integrity guarantees

- **SANRA score mandatory** (Baethge et al. 2019; 6 items, 0-12). Score <4 = reject draft, redraft.
- **Search documentation required** (relaxed: top-50 per axis, single database OK if justified in Limitations).
- **Author COI statement mandatory.**
- **Counter-evidence section mandatory** — must engage opposing findings, not omit.
- **Hedging strictest** — single-reviewer subjective lens flagged in Limitations.
- Anchor 12/12.
- **Length**: 3000–10000 words.

---

## Technical (chemistry / analytical / MoA)

**Use**: analytical method review, chemistry-focused MoA review, residue chemistry deep-dive, photochemistry / hydrolysis pathway review.

### Failure modes

- Endpoint structure imposed on method-centric topic → bad fit
- Figures missing (chromatograms, structures, transitions)
- Manufacturer app notes cited as primary
- No validation parameter table
- SAR not tabulated

### Integrity guarantees

- **Structure follows discipline taxonomy** (technique / chemical class / pathway), not regulatory endpoint spine.
- **Figure floor**: ≥1 structure per named substance; ≥1 method or pathway diagram; ≥1 validation or property table.
- **Source ranking strict**: SANTE/SANCO guidance + EURL methods + IUPAC top. Manufacturer notes COI-flagged.
- **Validation parameters mandatory per method cited**: LOQ, recovery, RSDr, n, matrix.
- Anchor 12/12 (identity + reg status frames the chemistry).
- **Length**: 5000–20000 words.
- **Templates**: `templates/technical.md` for analytical; `templates/chemistry.md` for MoA/pathway (same skeleton, different figure mix).

---

## Cross-archetype rules

1. **No archetype permits skipping the 12-item anchor.**
2. **No archetype permits orphan claims.**
3. **No archetype permits citation-from-memory** — every cite must have been WebFetched (Phase 7 timestamp).
4. **Length caps are guides, not gates** — but caps below the discipline floor (e.g. <1500w for residues) auto-trigger user confirmation prompt.
5. **User-overrides** can extend depth, never reduce below archetype integrity floor.
