# Canned Search Blocks

Structure: `assets/search_blocks/{archetype}/{discipline}/{endpoint}.txt`

Each file contains one Boolean string with token placeholders. Phase 3 substitutes:

- `{SUBSTANCE}` — ISO common name
- `{CAS}` — CAS RN
- `{SYNONYMS}` — pipe-separated synonyms from Phase 2 anchor item 1
- `{EC}` — EC number
- `{INCHIKEY}` — InChIKey first block (14 chars)
- `{YEAR_FROM}` — start year per SCOPE.md time window
- `{YEAR_TO}` — end year (or "*" for current)

**No freeform queries (mid / weak model classes).** Strong-class models may extend blocks but must log the additions in SEARCH-LOG.md.

## Examples

### `rapid/mammalian_tox/noael.txt`
```
({SUBSTANCE} OR "{CAS}" OR {SYNONYMS}) AND (NOAEL OR "no observed adverse effect" OR "no-observed-adverse-effect-level") AND (rat OR rodent OR dog OR mouse) AND (oral OR gavage OR "dietary administration") {YEAR_FROM}-{YEAR_TO}
```

### `structured/ecotox/aquatic_acute.txt`
```
({SUBSTANCE} OR "{CAS}") AND (LC50 OR EC50 OR "acute toxicity") AND (fish OR Daphnia OR algae OR "rainbow trout" OR Lemna OR "Oncorhynchus mykiss" OR "Pseudokirchneriella subcapitata") {YEAR_FROM}-{YEAR_TO}
```

### `structured/efate/soil_degradation.txt`
```
({SUBSTANCE} OR "{CAS}") AND (DT50 OR "half-life" OR "degradation" OR "dissipation") AND (soil OR aerobic OR anaerobic) AND (OECD 307 OR OECD307 OR "OECD Test Guideline 307" OR FOCUS) {YEAR_FROM}-{YEAR_TO}
```

### `structured/residues/field_trials.txt`
```
({SUBSTANCE} OR "{CAS}") AND ("field trial" OR "supervised trial" OR "residue trial" OR "OECD 509" OR "OECD509") AND (crop OR commodity OR PHI OR "pre-harvest interval") {YEAR_FROM}-{YEAR_TO}
```

### `technical/analytical/method.txt`
```
({SUBSTANCE} OR "{CAS}") AND (LC-MS/MS OR GC-MS/MS OR HRMS OR QuEChERS OR "SANTE/11312" OR "SANCO/12571") AND (validation OR LOQ OR recovery OR "method development") AND (food OR feed OR water OR soil OR matrix) {YEAR_FROM}-{YEAR_TO}
```

### `comparative/{discipline}/{endpoint}.txt`
Same string format; runs once per comparator with `{SUBSTANCE}` substituted per row.

### `scoping/{discipline}/{endpoint}.txt`
Broader blocks (drop method restrictions, broaden endpoint synonyms); aim for high recall, low precision; PRISMA-ScR charts everything that passes title/abstract.

## Adding new blocks

When a new endpoint appears in scope (Phase 1), if no canned block exists for `{archetype}/{discipline}/{endpoint}`:

1. Strong-class model: author a block following the patterns above; commit to `assets/search_blocks/` as part of the deliverable. Log addition in SEARCH-LOG.md.
2. Mid / weak model: prompt user for the block; do not author freeform.
