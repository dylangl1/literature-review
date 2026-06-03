# Database Study: [Substance(s) / Registry / Dataset] — [Objective]

**Review type:** database_study
**Scope modifier:** [comparative | rapid | none]
**Discipline(s):** [list — from Phase 1 selection]
**Dataset(s):** [name, version/date, URL/access point]
**Use context:** [MRL coverage analysis / resistance monitoring / registration footprint / residue trial meta-analysis / MRL review Art.12 / other]
**Prepared by:** [Author] | Life Scientific
**Date:** [YYYY-MM-DD]

> **Integrity floor:** dataset provenance documented (source, version, access date); extraction logic reproducible; gap analysis explicit; anchor 12/12; citation per claim; source-tier via lookup; in-force legislation verified; quantitative summaries include n, unit, and source.

---

## 1. Introduction

### 1.1 Background and Objective

[Why this dataset analysis is required. Regulatory context. Which registry or dataset is analysed. 1-2 paragraphs.]

### 1.2 Regulatory Basis

[Applicable instruments with CELEX. E.g., Reg (EC) No 396/2005 [CIT-1] for MRL analysis; Reg (EC) No 1107/2009 [CIT-2] for authorisation footprint.]

---

## 2. Substance Identity

| Field | Value | Source | CIT |
|---|---|---|---|
| ISO common name | [TODO] | [TODO] | [TODO] |
| CAS RN | [TODO] | [TODO] | [TODO] |
| EC number | [TODO] | [TODO] | [TODO] |
| IUPAC name | [TODO] | [TODO] | [TODO] |
| SMILES | [TODO] | [TODO] | [TODO] |
| InChIKey | [TODO] | [TODO] | [TODO] |

![Structure of [substance name]](regulatory_anchor/02_structure.svg)
*Figure 1. 2D structure of [substance name] (CAS [RN], InChIKey [KEY]). Source: [chemwise / PubChem CID NNN], accessed [YYYY-MM-DD]. [CIT-N]*

[For multi-substance comparative scope: repeat identity block per substance or use composite table.]

---

## 3. Regulatory Anchor

| # | Anchor item | Value / status | Source | Accessed |
|---|---|---|---|---|
| 1 | Identity | [TODO] | [TODO] | [TODO] |
| 2 | Structure | Fig. 1 | [TODO] | [TODO] |
| 3 | Registration footprint | [TODO] | [TODO] | [TODO] |
| 4 | EU approval status | [TODO] | [TODO] | [TODO] |
| 5 | Renewal / expiry | [TODO] | [TODO] | [TODO] |
| 6 | Review history | [TODO] | [TODO] | [TODO] |
| 7 | EFSA Conclusion metadata | [TODO] | [TODO] | [TODO] |
| 8 | EFSA Conclusion endpoint text | [TODO] | [TODO] | [TODO] |
| 9 | MRL status | [TODO / NA] | [TODO] | [TODO] |
| 10 | CLP classification | [TODO] | [TODO] | [TODO] |
| 11 | SVHC status | [TODO] | [TODO] | [TODO] |
| 12 | BCPC entry | [TODO] | [TODO] | [TODO] |

---

## 4. Dataset Description

### 4.1 Dataset(s) Used

| Dataset | Custodian | Version / snapshot date | URL / access point | CIT |
|---|---|---|---|---|
| [e.g., EU Pesticides Database MRL Annexes] | [e.g., European Commission, DG SANTE] | [YYYY-MM-DD accessed] | [URL] | [CIT-N] |
| [e.g., EFSA PRIMo rev. 3.1] | EFSA | [version + access date] | [URL] | |
| [Additional datasets] | | | | |

### 4.2 Dataset Coverage and Known Limitations

[What the dataset covers (jurisdictions, substances, time period, commodity scope). Known gaps, update frequency, caveats. Source voice: "The EU Pesticides Database [CIT-N] records MRLs currently in Annexes I-IV of Reg (EC) No 396/2005 …"]

### 4.3 Dataset Reliability

[Tier per `assets/source_tier_lookup.json`. Official EU/regulatory databases = Tier 1. Note version-dependency: MRLs, authorisation status, and classification data change with legislative amendments. Snapshot date determines validity window.]

---

## 5. Methods

### 5.1 Data Extraction Logic

[Describe extraction: which fields extracted, filters applied, any transformations. Reproducible — another person following this description should obtain the same dataset extract.]

- **Fields extracted:** [list]
- **Filters applied:** [e.g., substance = CAS [RN]; commodity group = []; jurisdiction = EU]
- **Date of extraction:** [YYYY-MM-DD]
- **Format:** [database query / manual download / WebFetch / chemwise tool]
- **Query log:** `SEARCH-LOG.md` entry #S[N]

### 5.2 Analytical Approach

[How the extracted data are analysed: counting, grouping, gap identification, comparison against reference set. State any calculation methods.]

---

## 6. Results

### 6.1 Overview Summary

| Parameter | Value | Source | CIT |
|---|---|---|---|
| Total records extracted | [N] | [dataset] | |
| Jurisdictions / MS covered | [N] | | |
| Commodities / matrices | [N categories] | | |
| Date range of records | [YYYY to YYYY] | | |

### 6.2 [Primary Results Table(s)]

[Discipline-specific. Examples:]

**For MRL database study:**

| Commodity | EU MRL (mg/kg) | Basis | Codex MRL | US tolerance | CIT |
|---|---|---|---|---|---|
| [TODO] | | [EFSA opinion / default / import tolerance] | | | |

**For registration footprint / authorisation database study:**

| MS | Authorisation status | Use type | Formulation types | Expiry | CIT |
|---|---|---|---|---|---|
| [TODO] | [authorised / expired / pending / not registered] | | | | |

**For resistance monitoring dataset:**

| Species | Resistance mechanism | Frequency | Region / year | Source | CIT |
|---|---|---|---|---|---|
| [TODO] | | | | | |

### 6.3 Gap Analysis

[Explicit identification of gaps, blanks, missing data, coverage limitations. Mapped to regulatory context where applicable.]

| Gap type | Description | Jurisdictions / commodities affected | Regulatory significance |
|---|---|---|---|
| Missing MRL | No MRL set; default of 0.01 mg/kg applies [CIT-N] | [list] | [TODO] |
| Expired authorisation | [substance] not authorised in [MS] since [date] | [list] | [TODO] |
| [Other gap type] | | | |

### 6.4 Figures

[As required by discipline and scope. Examples: MRL comparison bar chart; jurisdictional authorisation heatmap; MRL exceedance risk vs consumption data.]

---

## 7. Discussion

[Interpret results in regulatory context. What do the gaps and distributions mean? Comparison against prior dataset version or different substance where comparative modifier applied. Calibrated language. No absolutist statements.]

---

## 8. Regulatory Implications

[Link findings to specific regulatory instruments, thresholds, or procedural triggers. E.g., an MRL gap for a commodity group triggers Art.6 application requirements under Reg 396/2005.]

---

## 9. Limitations

- **Dataset snapshot:** Results valid as of [YYYY-MM-DD]; dataset updates may alter findings
- **Coverage:** [known jurisdictional / commodity gaps in dataset itself]
- **Access:** [any fields not publicly accessible]
- **[Other]**

---

## 10. References

[Generated from `CITATION-LEDGER.md`. Minimum citations per `OUTPUT-CONTRACT.json min_citations`.]

---

## 11. Glossary

[Standard glossary from `literature_review.md §Glossary`. Add dataset-specific abbreviations.]
