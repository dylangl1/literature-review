# Anchor Fallback Paths (Phase 2)

Chemwise is the **preferred** path for Phase 2 regulatory anchor — fastest, structured, version-controlled. Chemwise is NOT a gate. When chemwise is unavailable (MCP not connected, substance not in DB, model variant without MCP access), use fallback paths. Coverage of all 12 anchor items is mandatory; the **source** is flexible.

`CHEMWISE-CHECKLIST.md` in `regulatory_anchor/` tracks each item's resolution:

```
- [ ] 1. Identity (CAS/EC/ISO)            source: __  date: __
- [ ] 2. Structure (SMILES/InChIKey)      source: __  date: __
- [ ] 3. Registration footprint           source: __  date: __
- [ ] 4. PPP approval status              source: __  date: __
- [ ] 5. Renewal/expiry timeline          source: __  date: __
- [ ] 6. Substance review history         source: __  date: __
- [ ] 7. EFSA conclusion metadata         source: __  date: __
- [ ] 8. EFSA conclusion fulltext         source: __  date: __  (only if endpoint extraction needed)
- [ ] 9. MRL status                       source: __  date: __  (residue scope only)
- [ ] 10. CLP harmonised classification   source: __  date: __
- [ ] 11. REACH SVHC cross-check          source: __  date: __
- [ ] 12. BCPC entry                      source: __  date: __
```

Tick `[x]` only when output cached to `regulatory_anchor/<item>/`. Coverage check: count of `[x]` must equal 12 (or 11 if residue scope absent, then item 9 NA).

---

## 12-item resolver

| # | Item | Primary (chemwise) | Fallback 1 | Fallback 2 | Cache file |
|---|---|---|---|---|---|
| 1 | Identity (CAS/EC/ISO) | `mcp__chemwise__search_substance` | EU Pesticides Database (`https://ec.europa.eu/food/plant/pesticides/eu-pesticides-database/start/screen/active-substances`) | ECHA dissemination (`https://echa.europa.eu/information-on-chemicals`) | `01_identity.md` |
| 2 | Structure (SMILES/InChIKey) | `mcp__chemwise__get_structure` | PubChem (`https://pubchem.ncbi.nlm.nih.gov/`) | ChemSpider (`https://www.chemspider.com/`) | `02_structure.md` (+ SVG if rendered) |
| 3 | Registration footprint | `mcp__chemwise__get_registration_summary` | EU Pesticides DB authorisations | MS competent authority registers (BVL, ANSES, CTGB, HSE) | `03_registration.md` |
| 4 | PPP approval status | `mcp__chemwise__get_ppp_approval_status` | EU Pesticides DB → active substance detail page | Commission Implementing Reg via EUR-Lex CELEX | `04_approval.md` |
| 5 | Renewal/expiry timeline | `mcp__chemwise__get_ppp_expiry_alerts` | Commission renewal programme reg (e.g. Reg 2022/378, 2024/2545) | EU Pesticides DB approval period field | `05_renewal.md` |
| 6 | Substance review history | `mcp__chemwise__get_substance_review_history` | EUR-Lex CELEX search by substance | EFSA register of questions (`https://www.efsa.europa.eu/en/registerofquestions`) | `06_review_history.md` |
| 7 | EFSA conclusion metadata | `mcp__chemwise__get_efsa_conclusion_metadata` | EFSA Journal search (`https://efsa.onlinelibrary.wiley.com/`) | OpenAlex search w/ filter `journal_id=efsa_journal` | `07_efsa_meta.md` |
| 8 | EFSA conclusion fulltext | `mcp__chemwise__get_efsa_conclusion_fulltext` | Direct `WebFetch` of EFSA Journal article DOI | Wayback Machine snapshot if document moved | `08_efsa_fulltext.md` |
| 9 | MRL status | `mcp__chemwise__get_mrl_status` | EU Pesticides DB MRL search (`https://ec.europa.eu/food/plant/pesticides/eu-pesticides-database/start/screen/mrls`) | Codex Alimentarius (`https://www.fao.org/fao-who-codexalimentarius/codex-texts/dbs/pestres/`) | `09_mrl.md` |
| 10 | CLP harmonised classification | `mcp__chemwise__get_cl_classification` | ECHA C&L Inventory (`https://echa.europa.eu/information-on-chemicals/cl-inventory-database`) | CLP Annex VI via Reg 1272/2008 consolidated (EUR-Lex CELEX 02008R1272) | `10_clp.md` |
| 11 | REACH SVHC | `mcp__chemwise__check_svhc` | ECHA Candidate List (`https://echa.europa.eu/candidate-list-table`) | ECHA Authorisation List Annex XIV | `11_svhc.md` |
| 12 | BCPC entry | `mcp__chemwise__query_bcpc` | BCPC Pesticide Manual online (subscription) | Pesticide Manual print ref (cite edition + page) | `12_bcpc.md` |

---

## Fallback execution protocol

When chemwise unavailable for an item:

1. **Try Fallback 1**: `WebFetch` the URL. Cache full response to the listed file in `regulatory_anchor/`.
2. **If Fallback 1 fails or substance not found**: try Fallback 2.
3. **If both fail**: log to `regulatory_anchor/ANCHOR-MISSES.md` with: item, sources tried, dates, response snippet. **Do not tick the checkbox.** Gate will fail unless user explicitly waives in SCOPE.md.
4. **Waiver protocol**: user can mark an item NA in SCOPE.md `anchor_waivers:` list with justification (e.g. item 9 MRL NA for non-pesticide substance). Waived items count as resolved for gate.

---

## Identity verification (item 1) is the highest priority

If item 1 fails (substance identity cannot be confirmed CAS/EC/ISO/InChIKey across at least 2 sources), **block all downstream phases**. Searching against an unverified identity is the largest hallucination risk.

Minimum identity confirmation: CAS RN matches across 2 of {chemwise, PubChem, ECHA, EU Pesticides DB}. Synonym list collected for search-block substitution.

---

## EUR-Lex / EFSA Journal access notes

- EUR-Lex: prefer local markdown copies via `assets/eu_ppp_regulations.json` lookup before WebFetch.
- EFSA Journal: open-access; direct DOI fetch via `https://doi.org/10.2903/j.efsa.YYYY.NNNN`.
- ECHA: dissemination dossiers may be partially redacted (confidential business information); cite as available.
- Codex: PestRes DB requires query by substance + commodity; cite specific MRL with adoption year.

---

## Caching format

Each cache file is markdown with frontmatter:

```yaml
---
item: 4
source: EU Pesticides Database
url: https://ec.europa.eu/food/plant/pesticides/eu-pesticides-database/start/screen/active-substances/details/12345
accessed: 2026-05-30
fallback_tier: 1
chemwise_attempted: true
chemwise_result: unavailable
---

[Captured content here, structured.]
```

This frontmatter feeds the CITATION-LEDGER.md and BIBLIOGRAPHY.bib generation.
