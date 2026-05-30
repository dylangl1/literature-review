# Model Floor Protocol

Quality must be invariant across model versions. Strong models (Opus, GPT-5-high) and weak models (Haiku 3.5, small local) must produce reviews that pass the same mechanical gate. This document defines the model-floor mechanics.

## Core principle

**Move quality out of model judgement into deterministic artefacts and mechanical checks.** The model becomes a filler of pre-built scaffolds, not an author of contracts.

---

## Five-layer defence

### Layer 1 — Externalised contract

The contract lives on disk, not in the prompt. Model re-reads it at each phase start.

- `OUTPUT-CONTRACT.md` — human-readable; required sections, figures, citation rules, anchor list, min counts.
- `OUTPUT-CONTRACT.json` — machine-readable mirror (schema in `assets/contract_schema.json`). Inline Bash + `jq` reads it at gate time.
- Contract is immutable post-Phase-1.5. Edits require explicit Phase 1 re-entry by user.

### Layer 2 — Pre-scaffolded artefacts

Empty stubs = visible failures.

- `REVIEW.md` skeleton pre-written by skill (using the discipline × archetype composed template) at Phase 6 start. All required `##`/`###` headings + empty tables + `[TODO: …]` placeholders pre-populated.
- `EVIDENCE-TABLE.csv` header row pre-written with required columns.
- `CITATION-LEDGER.md` header pre-written.
- `regulatory_anchor/CHEMWISE-CHECKLIST.md` pre-populated with 12 unchecked items.
- Gate inspects: any `[TODO`, `[FILL`, `[XX]` placeholder remaining = fail.

### Layer 3 — Deterministic inputs

Remove model query authoring (high-variance step).

- `assets/search_blocks/{archetype}/{discipline}/{endpoint}.txt` — canned Boolean strings. Model substitutes `{SUBSTANCE}`, `{CAS}`, `{SYNONYMS}` tokens only.
- `assets/anchor_fallback_paths.md` (and per-item URLs) — model cannot invent paths.
- `assets/citation_formats.json` — citation style templates with named slots; model fills slots only.
- `assets/source_tier_lookup.json` — domain → tier mapping. Model cannot promote/demote sources.

### Layer 4 — Mechanical pre-delivery gate (inline Bash, no scripts)

The gate is a sequence of Bash commands the model runs at end of Phase 8. Each step asserts a condition; failure routes the model back to the indicated phase.

```bash
# Step 1: anchor coverage 12/12
TICKED=$(grep -c "^- \[x\]" regulatory_anchor/CHEMWISE-CHECKLIST.md)
REQUIRED=$(jq -r '.anchor_required_count' OUTPUT-CONTRACT.json)
[ "$TICKED" -ge "$REQUIRED" ] && echo "PASS anchor" || echo "FAIL anchor: $TICKED/$REQUIRED → return to Phase 2"

# Step 2: required sections present
jq -r '.required_sections[]' OUTPUT-CONTRACT.json | while read S; do
  grep -q "^## .*${S}" REVIEW.md && echo "PASS section: $S" || echo "FAIL section: $S → return to Phase 6"
done

# Step 3: min citations
N_CITES=$(grep -cE '\[CIT-[0-9]+\]' REVIEW.md)
MIN=$(jq -r '.min_citations' OUTPUT-CONTRACT.json)
[ "$N_CITES" -ge "$MIN" ] && echo "PASS cites: $N_CITES" || echo "FAIL cites: $N_CITES < $MIN → return to Phase 3"

# Step 4: every CIT-N resolves in ledger
grep -oE '\[CIT-[0-9]+\]' REVIEW.md | sort -u | while read C; do
  ID=$(echo $C | tr -d '[]')
  grep -q "^| ${ID} " CITATION-LEDGER.md && echo "PASS resolve $ID" || echo "FAIL unresolved $ID → return to Phase 7"
done

# Step 5: every ledger row has a fetched_at date
awk -F'|' 'NR>2 && $7 !~ /20[0-9][0-9]-[0-1][0-9]-[0-3][0-9]/ {print "FAIL ledger row missing fetched_at: " $2}' CITATION-LEDGER.md

# Step 6: forbidden language
grep -nE "\b(proven|definitive|conclusive|obviously|clearly shows|undeniably)\b" REVIEW.md && echo "FAIL absolutist language" || echo "PASS hedging"
grep -nE "[—–]" REVIEW.md && echo "FAIL em/en dash" || echo "PASS dashes"

# Step 7: orphan placeholders
grep -nE "\[TODO|\[FILL|\[XX\]|\{\{" REVIEW.md && echo "FAIL unfilled placeholder" || echo "PASS placeholders"

# Step 8: figure count
N_FIG=$(grep -cE "^!\[" REVIEW.md)
MIN_FIG=$(jq -r '.min_figures' OUTPUT-CONTRACT.json)
[ "$N_FIG" -ge "$MIN_FIG" ] && echo "PASS figs: $N_FIG" || echo "FAIL figs: $N_FIG < $MIN_FIG → return to Phase 6"

# Step 9: evidence rows
N_EV=$(($(wc -l < EVIDENCE-TABLE.csv) - 1))
MIN_EV=$(jq -r '.min_evidence_rows' OUTPUT-CONTRACT.json)
[ "$N_EV" -ge "$MIN_EV" ] && echo "PASS evidence: $N_EV" || echo "FAIL evidence: $N_EV < $MIN_EV → return to Phase 5"

# Step 10: identity verification min 2 sources
grep -q "cross_verified: true" regulatory_anchor/01_identity.md && echo "PASS identity" || echo "FAIL identity → return to Phase 2"

# Step 11: orphan quant claims (regex heuristic — flags numeric+unit without nearby CIT-N)
grep -nE "[0-9]+(\.[0-9]+)? (mg/kg|µg/L|ug/L|ng/L|mg/L|g/ha|kg/ha|%|d|days|h)" REVIEW.md | grep -v "CIT-" && echo "REVIEW: quant claim without nearby cite — manual check" || echo "PASS quant"

# Step 12: contract checklist count
DONE=$(grep -c "^- \[x\]" QUALITY-CHECKLIST.md)
TOTAL=$(grep -c "^- \[" QUALITY-CHECKLIST.md)
[ "$DONE" -eq "$TOTAL" ] && echo "GATE PASS" || echo "FAIL checklist: $DONE/$TOTAL"
```

The model runs each step via the `Bash` tool. Output is interpreted by the model: any `FAIL` triggers return to the indicated phase. No `.sh` file is bundled — the commands live in `SKILL.md` Phase 8 instructions and the model copy-runs them.

### Layer 5 — Hallucination defence (citation integrity)

Weak models invent DOIs, authors, titles. Hard counter:

- **Every citation requires source-of-truth fetch.** Phase 7 `WebFetch` each DOI/URL/CELEX, writes fetched title/authors/year to `CITATION-LEDGER.md` with `fetched_at` ISO date.
- **Quote-grounding for direct claims.** Phase 6 quantitative claims require `quote_span` field in evidence table — actual text from source. Phase 7 fuzzy-matches the quote against fetched content via inline Bash grep with normalised whitespace.
- **No citation-from-memory rule.** Model cannot add a citation without a corresponding ledger row with `fetched_at`. Gate step 5 enforces.
- **CrossRef DOI validation.** For DOIs, `WebFetch https://api.crossref.org/works/{doi}` and compare returned author/year/title vs claimed cite. Mismatch flagged in `CITATION-LEDGER.md` field `crossref_match: true|false`.

---

## Supported models (Claude-only)

This skill supports Claude models only. Non-Claude models are not supported because the deterministic-contract + mechanical-gate architecture was calibrated against Claude behaviour. Running on other models is out of scope and undefined.

| Tier | Models | Reasoning effort | Use cases |
|---|---|---|---|
| **PREFERRED** | Opus 4.7 | High | Systematic, comparative (N>3 comparators), multi-discipline (3+ disciplines), regulatory dispute, ED categorisation, full renewal dossier support |
| **DEFAULT** | Opus 4.7 | Medium | Structured single-substance review (1-2 disciplines), Art.12 MRL review, DP check, scoping review, narrative-critical, technical / analytical review |
| **PERMITTED** | Sonnet 4.7 | High or Medium | Rapid archetype only; single discipline; single substance. Behavioural floor applies (canned Boolean blocks, no freeform query authoring). Use when speed matters more than depth and the question is genuinely narrow. |
| **BLOCKED** | Sonnet ≤4.6, Haiku class, any non-Claude | — | Skill halts at Phase 1 with model-class error. The gate convergence cost on weaker models exceeds the benefit. |

### Minimum floor

**Minimum supported model = Opus 4.7 Medium.** Below this floor, the skill refuses to start. The model class check runs at Phase 1 entry; if the active model is below floor, output a clear message:

> Skill ppp-literature-review requires Claude Opus 4.7 (Medium reasoning minimum) or Sonnet 4.7 (rapid archetype only). Current model: {detected}. Halting. Switch model and re-invoke.

### Model detection

Read `$ANTHROPIC_MODEL` env / model name string at skill start. Match against:

```
opus-4-7        → PREFERRED/DEFAULT (use reasoning effort flag)
opus-4.7        → PREFERRED/DEFAULT
sonnet-4-7      → PERMITTED (rapid only)
sonnet-4.7      → PERMITTED (rapid only)
*               → BLOCKED
```

If detection ambiguous, ask user to confirm model + reasoning effort via `AskUserQuestion`.

### Behavioural floors per model tier

The protocol adjusts model behaviour, never the gate.

| Tier | Behaviour | Gate |
|---|---|---|
| **PREFERRED (Opus 4.7 High)** | Default flow; can author cross-discipline narrative integration; can extend canned Boolean blocks (logged in SEARCH-LOG.md additions). All standard latitudes. | All gates |
| **DEFAULT (Opus 4.7 Medium)** | Default flow; cross-discipline integration permitted; canned Boolean blocks preferred but extension permitted with logging. | All gates |
| **PERMITTED (Sonnet 4.7)** | **Rapid archetype only**. Force canned Boolean blocks (no freeform query authoring). Stricter scaffold adherence — model fills only, no section restructuring. Contract recap mandatory at start of every phase. Per-discipline sections only (no cross-discipline narrative integration). One chemwise call per turn max. `STATE.md` confirmation per phase transition. | All gates |
| **BLOCKED** | Skill halts. | N/A |

Gate output is identical across all permitted tiers. Quality floor is invariant.

### Why Claude-only

- Contract schema, gate Bash commands, and credibility decision tree were calibrated against Claude's instruction-following profile.
- Tool-use patterns (chemwise MCP, WebFetch sequencing, AskUserQuestion enum prompts) assume Claude's tool-use semantics.
- Hallucination defence (Phase 7 quote-grounding) assumes Claude's WebFetch fidelity profile.
- Other models may work but quality is not warranted by the eval harness.

---

## Calibration to ground truth (model drift detection)

- **Reference dossier set** `eval/reference_substances/` — small golden corpus (3–5 substances) with known correct anchor data + known endpoint values + known EFSA conclusion citations.
- Periodic skill run end-to-end on golden corpus; manual diff vs golden output.
- **Metrics tracked per model version**:
  - Anchor accuracy: 12 items × N substances, exact-match % vs golden
  - Citation precision: % of cited claims that are verified against source-of-truth
  - Citation recall: % of golden citations that appear in output
  - Quant anchor completeness: % quant claims with all 4 fields (value + unit + species + source)
  - Section completeness: % required sections non-empty
  - Hallucination rate: % cites that fail CrossRef / WebFetch verification
- **Regression rule**: any metric drop >5% vs prior model version blocks deployment for that model class until skill updated or model behaviour-mode tightened.

---

## Source-quality enforcement (model-independent)

Source-tier assignment by lookup, not judgement:

- `assets/source_tier_lookup.json` — domain / journal / publisher → tier (1–4).
- Examples: `efsa.europa.eu` → 1; `echa.europa.eu` → 1; `eur-lex.europa.eu` → 1; `pubs.acs.org/jafc` → 3 (Tier-3 specialist peer-reviewed); `medrxiv.org` → 4 (preprint); `biorxiv.org` → 4.
- Unknown domain → flagged `tier: unknown` in ledger; user confirms; default Tier-4 if no confirmation.
- COI flags from `assets/coi_flags.json`: industry consortium domains, manufacturer domains, advocacy NGOs all carry visible `coi: industry|manufacturer|advocacy|regulator|academic` field.

Model cannot downgrade EFSA or upgrade a preprint — tier comes from lookup.

---

## Anti-pattern guardrails (forbidden behaviours, enforced at gate)

| Behaviour | Forbidden because | Gate detection |
|---|---|---|
| Skip Phase 2 anchor | Loses regulatory ground truth | Step 1 (anchor 12/12) |
| Cite from memory | Hallucination vector | Step 5 (no fetched_at) |
| Narrative-only paragraph | Orphan claims | Step 11 + paragraph-citation density check |
| Trade-name-only search | Misses substance under CAS | Search-log inspection in Step 3 |
| Single-source claim on contested endpoint | Lack of triangulation | Manual review flag |
| Decide section "not relevant" | Coverage erosion | Requires `OMISSIONS.md` entry with Reg article justification |
| Em/en dashes | Style violation, mid-model fingerprint | Step 6 |
| Absolutist language ("proven", "definitive") | Calibration violation | Step 6 |
| Aggregating dissimilar endpoints | False equivalence | Comparative-archetype manual check |
| Length cap below discipline floor | Coverage compromise | Auto-prompt user to confirm |

---

## Summary

Quality invariance = deterministic everything that can be deterministic. The model writes prose and chooses among pre-tiered sources. Contract, scaffold, gate, source-tier, citation-style, search-blocks, anchor-paths — all externalised. The gate is inline Bash + `jq` + `grep`, no bundled scripts. The eval harness is a manual periodic procedure against the golden corpus, not an automated CI.
