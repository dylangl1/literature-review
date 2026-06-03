# Molecular Structure Rendering Protocol

Applies to all reviews in this skill. Rendering requirements vary by discipline — see §When Required.

---

## When Required

| Discipline | Parent compound | Metabolites / degradates | Analogues (SAR) | ISTD |
|---|---|---|---|---|
| Analytical chemistry | **MANDATORY** | **MANDATORY** | Where discussed | **MANDATORY** |
| Chemistry / MoA | **MANDATORY** | **MANDATORY** | **MANDATORY** (SAR section) | — |
| Phys-chem / identity | **MANDATORY** | Where discussed | — | — |
| Environmental fate | **MANDATORY** | **MANDATORY** (all with >5 %AR or regulatory trigger) | — | — |
| Residues | **MANDATORY** | **MANDATORY** (enforcement + risk assessment residue definition) | — | — |
| Mammalian tox | **MANDATORY** | Key metabolites in ADME section | — | — |
| Ecotox | **MANDATORY** | Key metabolites tested | — | — |
| Efficacy | **MANDATORY** | — | — | — |
| Exposure | **MANDATORY** | — | — | — |
| Regulatory affairs | **MANDATORY** (parent) | Where identity relevant | — | — |

Parent compound structure is mandatory in ALL reviews at §2 Substance Identity.

---

## Source Priority

1. **chemwise `get_structure`** — returns InChIKey, SMILES, and optionally SVG. Preferred.
2. **PubChem** — WebFetch `https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/inchikey/{INCHIKEY}/property/IsomericSMILES/JSON` for SMILES; `https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/inchikey/{INCHIKEY}/PNG` for image.
3. **ChemSpider** — fallback if PubChem unavailable. Note CAS + InChIKey in ledger for cross-verification.

Log the source used per structure in `CITATION-LEDGER.md` with `fetched_at` timestamp.

---

## Rendering Format

### Markdown output

Use SVG where available (scales cleanly, print-safe):

```markdown
![Structure of [compound name]](figures/[compound_slug].svg)
*Figure N. 2D structure of [compound name] ([IUPAC name], CAS [RN], InChIKey [KEY]). Source: [chemwise / PubChem CID NNN], accessed [YYYY-MM-DD]. [CIT-N]*
```

If only PNG available:

```markdown
![Structure of [compound name]](figures/[compound_slug].png)
*Figure N. 2D structure of [compound name] ([IUPAC name], CAS [RN], InChIKey [KEY]). Source: PubChem CID [NNN], accessed [YYYY-MM-DD]. [CIT-N]*
```

If image retrieval fails entirely — embed SMILES in the identity table and flag:

```markdown
> **Note:** Structure image could not be retrieved for [compound name]. SMILES: `[SMILES string]`. InChIKey: `[KEY]`. Render using a structure editor before submission.
```

Never omit the structure entry — always provide at minimum SMILES + flag.

### Word output (via `anthropic-skills:docx`)

Embed PNG retrieved from PubChem. Minimum 200×200 px at 150 dpi. Caption as above.

---

## Identity Table (adjacent to every structure figure)

Every structure figure must have an adjacent identity table containing:

| Field | Value | Source | CIT |
|---|---|---|---|
| ISO common name | | | |
| CAS RN | | | |
| EC number | | | |
| IUPAC name | | | |
| Molecular formula | | | |
| Molecular weight (g/mol) | | | |
| SMILES | | | |
| InChIKey | | | |

---

## Multi-structure figures

For SAR sections, metabolic pathways, or degradation pathway diagrams with multiple compounds: arrange in a single composite figure with individual labels (a), (b), (c) etc. Each compound labelled with: name + CAS + InChIKey below its structure.

```markdown
![Metabolic pathway — [substance]](figures/metabolic_pathway.svg)
*Figure N. Metabolic pathway of [substance] in [rat liver / plant / soil]. Structures: (a) parent [CAS], (b) [metabolite M1, CAS], (c) [metabolite M2, CAS]. Percentage of total radioactive residue (%TRR) at [timepoint] shown where reported. Source: [CIT-N, CIT-M].*
```

---

## Naming convention for figure files

```
figures/{compound_role}_{compound_slug}.{ext}
```

Examples:
- `figures/parent_chlorpyrifos.svg`
- `figures/metabolite_tcp.svg`
- `figures/metabolic_pathway_chlorpyrifos_rat.svg`
- `figures/chromatogram_lod_spike.svg`

---

## Gate check

Phase 8 gate Step 9 verifies figure count against `OUTPUT-CONTRACT.json min_figures`. For chemistry/analytical disciplines, gate also checks that every compound named in text has a corresponding structure figure or SMILES + flag entry. Missing structure without flag = FAIL.
