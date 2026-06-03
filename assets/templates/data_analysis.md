# Data Analysis: [Substance] — [Model / Calculation / Scenario]

**Review type:** data_analysis
**Scope modifier:** [comparative | rapid | none]
**Discipline(s):** [list — from Phase 1 selection]
**Model / tool:** [FOCUS SW v1.4 / FOCUS GW v3.3 / PRIMo rev. 3.1 / QSAR / statistical / other]
**Analysis type:** [exposure modelling / dietary intake / QSAR / trial data statistics / PEC derivation / other]
**Prepared by:** [Author] | Life Scientific
**Date:** [YYYY-MM-DD]

> **Integrity floor:** model/tool version and regulatory basis documented; input parameters fully tabled with sources and citations; outputs traceable to inputs; regulatory threshold comparison explicit; limitations of modelling approach documented; anchor 12/12; citation per claim; quantitative outputs include value + unit + scenario + source.

---

## 1. Introduction

### 1.1 Background and Objective

[Why this analysis is needed. Regulatory context. Which model or analytical approach is applied and why. 1-2 paragraphs.]

### 1.2 Regulatory Basis

[Instruments, guidance documents, and EFSA opinions governing the modelling approach. CELEX citations. E.g., FOCUS WORK GROUP guidance documents [CIT-1], EFSA PRIMo guidance [CIT-2].]

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

[Additional structures for metabolites and degradates where included in analysis, per `references/molecular_structure_rendering.md`.]

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

## 4. Model / Approach Description

### 4.1 Model Name and Version

| Field | Value | CIT |
|---|---|---|
| Model / tool name | [TODO] | |
| Version | [TODO] | |
| Regulatory guidance basis | [e.g., FOCUS Work Group on Landscape and Mitigation Measures (2007)] | |
| Endorsed by | [EFSA / SANTE / OECD — with document reference] | |
| Scenarios included | [list] | |

### 4.2 Model Assumptions

[State assumptions inherent to the model that affect interpretation of results. E.g., FOCUS Step 1 worst-case assumptions; PRIMo chronic diet assumption; QSAR applicability domain.]

### 4.3 Applicability to this Substance

[Confirm model is applicable: substance class within applicability domain, relevant use scenario covered, no known structural alerts that invalidate the approach.]

---

## 5. Input Parameters

### 5.1 Substance Properties

| Parameter | Value | Unit | Source | CIT | Notes |
|---|---|---|---|---|---|
| [e.g., DT50 soil (lab, 20°C, pF 2)] | [TODO] | d | [TODO] | | [geomean of N studies] |
| [e.g., Koc] | [TODO] | mL/g | [TODO] | | |
| [e.g., Vapour pressure] | [TODO] | Pa | [TODO] | | |
| [e.g., Solubility in water] | [TODO] | mg/L | [TODO] | | |
| [e.g., log Kow] | [TODO] | — | [TODO] | | |
| [e.g., pKa] | [TODO] | — | [TODO] | | |
| [etc. — all parameters required by model] | | | | | |

### 5.2 Use Pattern / GAP

| Parameter | Value | Unit | Source | CIT |
|---|---|---|---|---|
| Application rate | [TODO] | g a.s./ha | [GAP / label / dossier] | |
| Number of applications | [TODO] | — | | |
| Application interval | [TODO] | d | | |
| BBCH stage (application) | [TODO] | — | | |
| Crop / use | [TODO] | — | | |
| Formulation type | [TODO] | — | | |

### 5.3 Metabolite / Degradate Parameters (where included)

[Repeat §5.1 table for each relevant metabolite or degradate, with compound identity (name + CAS) cross-referenced to structure figure.]

### 5.4 Reference Values (for risk characterisation, where applicable)

| Value | Amount | Unit | Basis | Source | CIT |
|---|---|---|---|---|---|
| ADI | [TODO] | mg/kg bw/d | [TODO] | EFSA | |
| ARfD | [TODO] | mg/kg bw | [TODO] | EFSA | |
| AOEL | [TODO] | mg/kg bw/d | [TODO] | EFSA | |
| RAC (soil) | [TODO] | mg/kg | [TODO] | EFSA | |
| RAC (surface water) | [TODO] | μg/L | [TODO] | EFSA | |
| [Other threshold] | | | | | |

---

## 6. Results

### 6.1 [Model Output Tables]

[Discipline-specific. See examples below. All values: value + unit + scenario + source.]

**Environmental fate / PEC modelling example:**

| Scenario | Step | PEC (surface water) | Unit | Window | Model run date | Comparison vs RAC | CIT |
|---|---|---|---|---|---|---|---|
| [e.g., R1 Châteaudun] | Step 1 | [TODO] | μg/L | 1st window | [YYYY-MM-DD] | [PEC/RAC = X] | |
| [e.g., D6 Thiva] | Step 1 | [TODO] | μg/L | 1st window | | | |
| [etc.] | | | | | | | |

**Dietary exposure / PRIMo example:**

| Commodity | STMR / HR | MRL applied | PHE chronic (% ADI) | PHE acute (% ARfD) | Population group | CIT |
|---|---|---|---|---|---|---|
| [TODO] | | | | | | |

**QSAR / in silico example:**

| Model | Endpoint predicted | Value | Unit | Applicability domain | Reliability | CIT |
|---|---|---|---|---|---|---|
| [TODO] | | | | [within / border / outside] | [Klimisch equivalent] | |

**Statistical trial data analysis example:**

| Trial | Dose (g a.s./ha) | % control (mean ± SD) | n | Reference product % control | CIT |
|---|---|---|---|---|---|
| [TODO] | | | | | |

### 6.2 Figures

[As applicable. Required for PEC modelling: PEC distribution chart vs RAC. Required for dietary exposure: intake bar chart vs ADI/ARfD. Required for QSAR: applicability domain plot, predicted vs observed. Required for trial statistics: dose-response curve, box plots.]

---

## 7. Regulatory Threshold Comparison

[Explicit comparison of outputs against applicable regulatory thresholds. No narrative ambiguity — tabulated pass/fail or RQ/MoE.]

| Output | Value | Unit | Threshold | Basis | RQ / % threshold | Pass / Fail / Refer |
|---|---|---|---|---|---|---|
| [TODO] | | | | | | |

---

## 8. Sensitivity Analysis

[Where applicable. Identify which input parameters drive the output most. If DT50 uncertainty ranges applied: show output range. If STMR vs HR comparison: show both.]

| Parameter varied | Range tested | Output range | Impact on regulatory conclusion |
|---|---|---|---|
| [TODO] | | | |

---

## 9. Limitations

- **Model step:** [Step 1 / Step 2 / higher-tier — inherent conservatism noted]
- **Input parameter uncertainty:** [DT50 from N studies; range and geomean noted in §5.1]
- **Applicability domain:** [where QSAR or model has boundary conditions]
- **GAP assumptions:** [label vs. field use]
- **[Other]**

---

## 10. References

[Generated from `CITATION-LEDGER.md`. Minimum citations per `OUTPUT-CONTRACT.json min_citations`.]

---

## 11. Glossary

| Acronym | Full term |
|---|---|
| ADI | Acceptable daily intake |
| AOEL | Acceptable operator exposure level |
| ARfD | Acute reference dose |
| BCF | Bioconcentration factor |
| DT50 | Time for 50% dissipation |
| DT90 | Time for 90% dissipation |
| FOCUS | Forum for the Co-ordination of pesticide fate models and their Use |
| GAP | Good Agricultural Practice |
| GLP | Good Laboratory Practice |
| HR | Highest residue |
| IESTI | International estimated short-term intake |
| Koc | Soil organic carbon-water partition coefficient |
| log Kow | n-octanol/water partition coefficient (logarithm) |
| MoE | Margin of exposure |
| MRL | Maximum residue level |
| PEC | Predicted environmental concentration |
| PHI | Pre-harvest interval |
| PRIMo | Pesticide Residue Intake Model |
| QSAR | Quantitative structure-activity relationship |
| RAC | Regulatory acceptable concentration |
| RQ | Risk quotient |
| STMR | Supervised trials median residue |
| [Add discipline-specific terms as required] | |
