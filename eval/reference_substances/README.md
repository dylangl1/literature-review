# Reference substances — golden corpus for model-drift detection

Periodic skill run end-to-end on these substances; diff vs golden output. Drift > 5% on any metric blocks deployment for that model class.

## Recommended seed corpus (3-5)

Pick to span chemistry classes + regulatory states:

1. **Glyphosate** (CAS 1071-83-6) — herbicide; renewal 2023; high public scrutiny; rich EFSA + ECHA + IARC literature
2. **Chlorpyrifos** (CAS 2921-88-2) — non-approved insecticide; substitution / ED relevance
3. **Boscalid** (CAS 188425-85-6) — approved fungicide; SDHI; broad MRL coverage
4. **Sulfoxaflor** (CAS 946578-00-3) — new-chemistry insecticide; bee restrictions
5. **Cypermethrin** (CAS 52315-07-8) — pyrethroid; isomer chemistry; analytical complexity

## Per-substance golden artefacts

For each substance:

- `{substance}/golden_anchor.md` — known correct 12-item anchor values with source + date
- `{substance}/golden_endpoints.md` — known correct pivotal endpoint values (NOAEL, ADI, ARfD, LC50 daphnia, DT50 soil, log Kow, MRL key crop) with EFSA Conclusion citation
- `{substance}/golden_citations.md` — minimum-set citations every review must include (EFSA Conclusion DOI, key RAR vol, harmonised CLP entry)
- `{substance}/golden_search_log.md` — expected query/hit-count baseline

## Metrics tracked per model version

| Metric | Definition | Threshold |
|---|---|---|
| Anchor accuracy | 12 items × N substances, exact-match % vs golden | ≥95% |
| Citation precision | % cited claims verified against source-of-truth (Phase 7) | 100% (gate) |
| Citation recall | % golden citations that appear in output | ≥90% |
| Quant completeness | % quant claims with all 4 fields (value+unit+species+source) | 100% (gate) |
| Section completeness | % required sections non-empty per contract | 100% (gate) |
| Hallucination rate | % cites failing CrossRef / WebFetch verification | 0% (gate) |
| Hedging compliance | % claims with calibrated hedging vs absolutist | ≥98% |

## Run procedure

1. Spin a fresh worktree.
2. Run skill against substance with archetype=structured, all disciplines selected, depth=structured.
3. Compare REVIEW.md + CITATION-LEDGER.md + regulatory_anchor/ outputs vs `golden_*`.
4. Score metrics manually (or via diff tooling).
5. Record per `eval/runs/{date}_{model}.md`:
   - model name + version
   - per-substance scores
   - regression vs prior version
6. If any metric drops >5% vs prior: open issue in skill repo; do not deploy that model class until skill update tightens floor or restores parity.

## Update cadence

Re-run on golden corpus:
- On every model version change (Claude major release, GPT major release)
- On every skill version bump
- Quarterly for stability
