# Discipline Overlays (Layer 1)

Each overlay defines: required sections, required figures/tables, source ranking (top→bottom, EU-context), quality tool per study type, quantitative anchors, EU instrument focus. Loaded by Phase 1.5 contract composer based on user-selected discipline(s). Multi-discipline reviews union the overlays.

---

## 1. Regulatory-centric

**Use cases**: approval status, data protection (DP) check, Art.12 MRL review, Art.43 re-authorisation, substitution assessment (Reg 2015/408), ED categorisation (Reg 2018/605), regulatory precedent, dossier procedural history.

**Preferred review type(s):** `literature_review` (primary). `database_study` for Art.12 MRL coverage or registration footprint analysis. `systematic_review` only for ED/substitution where structured evidence collation is required.

**Output style:** Structured narrative paragraphs with logical legal/regulatory sequencing. Tables for approval timelines, jurisdictional status matrices, classification matrices — but NOT study data extraction tables. Precise regulatory language throughout: "approved under conditions", "candidate for substitution", "non-renewal proposed", "revocation of approval" — never "banned". CELEX citations, EFSA-Q reference numbers, document version + date per cited instrument. No cross-study quantitative data tables; regulatory decisions cited as authoritative (Tier 1). Source voice maintained: "The Commission, by Commission Implementing Regulation (EU) [no.] [CIT-N], [did X]".

**Molecular structure requirements:** Parent compound mandatory in §2 Substance Identity. Additional structures only if substance identity itself is disputed or if co-formulant/metabolite identity is the regulatory question.

**Required sections** (in order):
1. Legal basis (Reg 1107/2009 + relevant Implementing Regs, CELEX cited)
2. Approval / authorisation history (timeline)
3. Endpoint-by-endpoint EFSA position
4. RMS / MS divergence
5. Procedural history (peer review dates, SCoPAFF, Commission Decision)
6. Precedent (analogous substances / decisions)
7. Regulatory implications

**Required figures/tables**:
- Timeline figure (approval → renewal → expiry)
- Jurisdictional matrix (substance × MS × authorisation status)
- Classification matrix (CLP hazard classes × evidence basis)

**Source ranking** (top wins):
1. EU legislation (CELEX, in-force consolidated text)
2. EFSA Conclusion (peer-reviewed by MS)
3. ECHA RAC opinion (CLH dossiers)
4. RMS RAR / DAR
5. SCoPAFF outcomes, Commission Implementing Regs
6. EFSA Scientific Opinion / Reasoned Opinion
7. MS competent authority decisions
8. Legal/regulatory commentary (peer-reviewed regulatory journals: Reg. Toxicol. Pharmacol., Eur. Food Feed Law Rev.)
9. Industry position papers (ECPA / CropLife Europe; COI flag mandatory)

**Quality tool**: source-tier only (no Klimisch — not study-level). Version + date per cited document.

**Anchors required**: dates, CELEX, Article/Annex refs, document version numbers, peer review report numbers (EFSA-Q-YYYY-NNNNN).

**Hedging**: legal language calibrated. "Approved" vs "approved under conditions" vs "candidate for substitution" vs "non-renewal proposed". Never "banned" — use "non-approval" or "withdrawal of approval".

---

## 2. Mammalian toxicology

**Preferred review type(s):** `literature_review` (standard endpoint summary). `systematic_review` for ED endpoint review, genotoxicity mode-of-action dispute, carcinogenicity weight-of-evidence, or litigation context.

**Output style:** Structured narrative paragraphs per endpoint group, each followed by a mandatory cross-study endpoint table. WoE statement per endpoint section. Quantitative anchors mandatory for all NOAEL/LOAEL/NOEC/LC50/BMD values: value + unit + species + strain + sex + n + route + duration + GLP + OECD TG + source. Source voice explicit: "EFSA concluded a NOAEL of X mg/kg bw/d based on [study type, species] [CIT-N]" vs "the applicant reported a NOAEL of X mg/kg bw/d [CIT-N]". Calibrated hedging per WoE strength. Regulatory reference values (ADI, ARfD, AOEL, AAOEL) with derivation basis cited.

**Molecular structure requirements:** Parent compound mandatory. Key metabolites in ADME section where metabolic scheme figures are required.

**Required sections**:
1. ADME (absorption, distribution, metabolism, excretion)
2. Acute toxicity (oral, dermal, inhalation; skin/eye irritation; sensitisation)
3. Short-term toxicity (28-d, 90-d; oral + dermal + inhalation where relevant)
4. Genotoxicity (in vitro battery + in vivo)
5. Long-term toxicity and carcinogenicity (chronic + carc, 2 species)
6. Reproductive and developmental toxicity (multi-gen / EOGRTS, dev tox 2 species)
7. Neurotoxicity (acute, sub-chronic, developmental where indicated)
8. Endocrine disruption (Reg 2018/605 §A T-modality + §B EATS)
9. Immunotoxicity (where indicated)
10. Reference values (ADI, ARfD, AOEL, AAOEL derivation)

**Required figures/tables**:
- Dose-response per pivotal study (≥1 per endpoint)
- BMD plots where BMD modelling applied
- AOP diagram (for ED endpoint)
- Metabolic scheme (rat + non-rodent species, if available)
- Cross-study table per subsection: endpoint × species × NOAEL/LOAEL × route × duration × Klimisch × GLP × source

**Source ranking**:
1. EFSA Conclusion §B.6 tox sections
2. RMS RAR Vol 3 B.6
3. JMPR monograph
4. ECHA RAC CLH opinion (for CMR / STOT-RE / STOT-SE)
5. IARC monograph, NTP Technical Report
6. US EPA OPP HHRA, PMRA HHRA
7. WHO/IPCS EHC, OECD SIDS
8. Peer-reviewed Klimisch 1 GLP OECD-compliant
9. Peer-reviewed Klimisch 2
10. NAM / in vitro Klimisch 2+ w/ OECD GD 286 alignment
11. Klimisch 3
12. Grey, preprint (flag)

**Quality tool**: Klimisch (primary), ToxRTool (secondary), OHAT RoB (epidemiology), AMSTAR-2 (included SRs).

**Anchors required**: NOAEL / LOAEL (mg/kg bw/d), species, strain, sex, n per group, route, duration, GLP Y/N, OECD TG number, deviations noted.

**Hedging**: EFSA WoE guidance (EFSA J. 2017;15(8):4971). "Demonstrated" needs ≥2 Klimisch 1 GLP consistent.

---

## 3. Ecotoxicology

**Preferred review type(s):** `literature_review` (standard taxon-by-taxon endpoint summary). `systematic_review` for SSD derivation, bee risk assessment dispute, ED mode-of-action review.

**Output style:** Structured narrative paragraphs per taxon group, each followed by a cross-study table. WoE per taxon. Quantitative anchors mandatory: LC50/EC50/NOEC with units, exposure duration, test species (Latin binomial), test medium, n, statistical method, OECD TG, GLP, source. Regulatory trigger values stated per taxon (e.g., TER vs trigger of 10 for birds; RQ vs 1 for aquatic organisms; TER vs trigger of 1000 for bees). RQ/TER computed and tabulated with PEC source explicitly cited. Source voice: "EFSA [year] concluded …" / "CRED-appraised peer-reviewed studies indicated …".

**Molecular structure requirements:** Parent compound mandatory. Metabolites/degradates included in analysis (where ecotox data on metabolites assessed) require structures per `references/molecular_structure_rendering.md`.

**Required sections**:
1. Aquatic vertebrates (fish — acute + chronic + ELS + FSDT for ED)
2. Aquatic invertebrates (daphnia + sediment dweller)
3. Algae and aquatic plants (green algae + Lemna)
4. Sediment organisms (Chironomus, Lumbriculus)
5. Birds (acute LD50, dietary LC50, repro)
6. Wild mammals
7. Bees (acute oral, acute contact, chronic adult, chronic larval, HPG / BroodTest)
8. Non-target arthropods (NTA — Aphidius, Typhlodromus tier I; ext lab tier II)
9. Earthworms and soil macro-organisms (acute + reproduction)
10. Soil microorganisms (N + C transformation)
11. Non-target terrestrial plants (NTTP — vegetative vigour + seedling emergence)

**Required figures/tables**:
- SSD (species sensitivity distribution) curves where ≥5 species per taxon
- RQ / TER bar charts per taxon vs trigger
- Exposure-effect overlay with PEC (FOCUSsw, soil)
- Cross-study table per subsection: taxon × endpoint × value × test duration × test type (static/semi-static/flow) × Klimisch × OECD TG × source

**Source ranking**:
1. EFSA Conclusion §B.9 ecotox sections
2. EFSA Bee Guidance (2013, 2023 revision), Aquatic Guidance (2013), Birds and Mammals Guidance (2009), Soil Organisms Guidance (2017)
3. RMS RAR Vol 3 B.9
4. ECHA REACH dossier endpoints (eChemPortal)
5. US EPA EFED ecological risk assessment, PMRA ERA
6. PPDB (University of Hertfordshire), EnviroTox DB, ECOTOX (EPA)
7. Peer-reviewed Klimisch 1 GLP OECD-compliant
8. CRED-appraised (Moermond) peer-reviewed non-GLP
9. Klimisch 2-3
10. Grey, preprint (flag)

**Quality tool**: Klimisch + CRED (Moermond 2016) for non-GLP peer-reviewed. SETAC RoB framework where applicable.

**Anchors required**: LC50/EC50/NOEC (with units, exposure duration, test species Latin binomial, test medium, n, statistical method), OECD TG number, GLP Y/N.

---

## 4. Environmental fate (efate)

**Preferred review type(s):** `literature_review` (standard fate parameter summary). `data_analysis` for FOCUS PEC modelling runs. `systematic_review` for contested persistence classification or leaching potential dispute.

**Output style:** Structured narrative paragraphs per fate endpoint, each followed by a cross-study parameter table. Quantitative anchors mandatory: DT50/DT90 with kinetic model (SFO/FOMC/DFOP/HS), chi-squared, geomean across n studies, normalisation to reference conditions (20°C, pF 2), species, soils, OECD TG, GLP. Koc with method, soil type, pH range. FOCUS scenario PEC values with model version, scenario name (e.g. R1 Châteaudun), window stated. Metabolite table included where relevant metabolites reach threshold. Source voice: "EFSA [year] used a geomean DT50 of X d [CIT-N]" vs "the RMS proposed a DT50 of X d [CIT-N]".

**Molecular structure requirements:** Parent compound mandatory. All metabolites appearing in fate pathway diagram require structures per `references/molecular_structure_rendering.md`. Metabolic pathway/degradation scheme diagram mandatory in most reviews.

**Required sections**:
1. Route of degradation in soil (aerobic, anaerobic, sterile)
2. Rate of degradation in soil (DT50 / DT90, kinetic model SFO/FOMC/DFOP/HS)
3. Adsorption / desorption (Koc, Kfoc, Freundlich 1/n, pH-dependence)
4. Mobility and leaching (column, lysimeter, FOCUS PEARL/PELMO)
5. Fate in water (hydrolysis vs pH, photolysis, ready/inherent biodeg, water/sediment DT50)
6. Fate in air (vapour pressure, Henry, atmospheric photolysis)
7. Bioconcentration (BCF, depuration)
8. PEC modelling (FOCUSsw, FOCUSgw, FOCUSair, soil PECini/PECacc)

**Required figures/tables**:
- Degradation kinetics curves per scenario (model fit + χ² visible)
- FOCUS scenario PEC distributions (PECsw 1st/2nd/3rd window)
- Metabolite formation/decline pathway diagrams
- Koc vs pH plot where pH-dependent
- Cross-study table: study × scenario × kinetic model × χ² × DT50 (geomean) × source
- Metabolite table: name × structure × max %AR × matrix × DT50 × trigger threshold

**Source ranking**:
1. EFSA Conclusion §B.8 fate sections
2. FOCUS Working Group reports (Kinetics 2014, Surface Water v1.4, Groundwater v3.3, Air, Landscape)
3. RMS RAR Vol 3 B.8
4. EFSA PERSAM tool outputs, MACRO, PEARL, PELMO standardised runs
5. US EPA EFED fate, PMRA EAD
6. PPDB, BPDB (Biocides Properties DB)
7. Peer-reviewed Klimisch 1 GLP OECD TG 307/308/309/106/308/313 etc.
8. Peer-reviewed Klimisch 2
9. Grey, preprint (flag)

**Quality tool**: OECD TG conformity flag, FOCUS Kinetics 2014 guidance compliance (χ² ≤ threshold per FOCUS Table 4), GLP, normalisation to reference conditions (20°C, pF 2 moisture).

**Anchors required**: DT50 (geomean across studies, with n), Koc (mL/g, with study soils), kinetic model chosen + justification, scenario name (e.g. R1 Châteaudun, D6 Thiva), endpoint trigger (e.g. 90th percentile PECsw vs RAC).

---

## 5. Residues / dietary exposure

**Preferred review type(s):** `literature_review` (standard residue data package summary). `database_study` for MRL coverage analysis, Art.12 MRL database review. `data_analysis` for PRIMo dietary exposure runs (IEDI/IESTI calculations).

**Output style:** Structured narrative paragraphs per residue topic, each supported by detailed data tables. Quantitative anchors mandatory: STMR, HR, MRL (mg/kg), PHI (days), GAP (rate g a.s./ha × applications × interval × BBCH stage), crop/commodity, sample type (raw/processed), n trials, jurisdiction. Metabolic pathway diagrams mandatory for plant and animal metabolism sections. MRL comparison tables across jurisdictions. Dietary exposure results (IEDI, IESTI) tabulated as % ADI and % ARfD per population group. Source voice: "EFSA MRL Reasoned Opinion [CIT-N] proposed a STMR of X mg/kg for [commodity]".

**Molecular structure requirements:** Parent compound mandatory. Enforcement and risk assessment residue definition components require structures — all named metabolites in the residue definition section per `references/molecular_structure_rendering.md`. Metabolic pathway diagrams show structures of parent + all named metabolites with %TRR.

**Required sections**:
1. Plant metabolism (primary crops representing groups 1-4)
2. Livestock metabolism (lactating ruminant, laying hen; if relevant pig, fish)
3. Residue definition (enforcement vs risk assessment, parent ± metabolites)
4. Field trials (NEU + SEU + import tolerances; per crop per use)
5. Processing studies (transfer factors, hydrolysis simulation)
6. MRL coverage (existing vs proposed, EU vs Codex vs third-country)
7. Dietary exposure (chronic IEDI via PRIMo rev.3.1, acute IESTI)
8. Livestock dietary burden (where animal commodities have MRLs)

**Required figures/tables**:
- Metabolic pathway diagrams (plant + animal, parent → metabolites with %TRR)
- Residue decline curves per PHI
- MRL comparison chart (EU / Codex / US / target third countries)
- IESTI / TMDI bar chart vs ARfD / ADI
- Trial table: crop × GAP × residue (n, median, HR, STMR, STMR-P)
- MRL table: matrix × jurisdiction × MRL × basis × in-force date

**Source ranking**:
1. EFSA MRL Reasoned Opinion / Art.12 review
2. EFSA Conclusion §B.7 residues
3. JMPR monograph (Codex MRL basis)
4. RMS RAR Vol 3 B.7
5. EU Pesticides Database MRLs (Reg 396/2005 Annexes)
6. EFSA PRIMo model outputs (current version)
7. US EPA OPP residue chemistry, PMRA residue
8. Peer-reviewed Klimisch 1 GLP OECD TG 501/502/503/506/507/508/509
9. Peer-reviewed Klimisch 2

**Quality tool**: OECD residue TG conformity, GAP alignment, NEU/SEU residue trial number sufficiency per SANCO/7525/VI/95 rev.10.3, OECD MRL Calculator alignment.

**Anchors required**: STMR, HR, MRL (mg/kg), PHI (days), GAP (rate g a.s./ha × applications × interval × growth stage), crop / commodity, sample (raw / processed), n trials.

---

## 6. Analytical chemistry / methods review

**Preferred review type(s):** `systematic_review` (primary — method landscape is structured and requires protocol-driven search). `data_analysis` where the primary output is a method validation run or comparison of detection limits.

**Output style:** Figure-primary, table-dense. Narrative paragraphs provide context and synthesis, but figures and tables carry the primary scientific content. Molecular structures mandatory for every named compound (analyte, metabolites, degradates, ISTD) per `references/molecular_structure_rendering.md`. Method comparison tables with LOQ, recovery, RSD, matrix, instrument, column, mobile phase. Validation tables per SANTE/11312/2021 pass/fail criteria. MS/MS transition tables. Representative chromatogram figures (blank, LOQ-spike, sample) mandatory. Flow diagrams for sample preparation workflows recommended. All values in tables include units, n replicates, source, CIT.

**Molecular structure requirements:** MANDATORY for all named compounds — analyte(s), metabolites, degradates, internal standard(s). Composite structure figures for multi-analyte methods. Structures included at first mention and in the Chemical Identity section. Per `references/molecular_structure_rendering.md`.

**Required sections**:
1. Analyte scope (parent + metabolites + isomers + degradates)
2. Matrix scope (high-water, high-acid, high-oil, high-protein, dry, water, soil, air, body fluids)
3. Extraction (solvent, QuEChERS, SPE, etc.)
4. Clean-up (dSPE, GPC, freezing-out)
5. Determination (LC-MS/MS, GC-MS/MS, HRMS, immunoassay)
6. Validation (LOQ, linearity, recovery, RSDr, RSDR, matrix effect)
7. Confirmation (ion ratio, retention time, transitions)
8. ILV / CCV (independent laboratory validation / confirmatory)
9. Multi-residue applicability

**Required figures/tables** (figures-heavy):
- Structures: analyte + ISTD + degradates (first mention each)
- Representative chromatograms (blank, LOQ-spike, sample)
- MS/MS transition diagrams (Q1 > Q3, CE)
- Calibration curves (matrix-matched)
- Flow diagrams (sample prep workflow)
- Method × matrix × LOQ × recovery (range, mean, RSD) × n × ref
- Transition table: analyte × Q1 × Q3 × CE × dwell × quantifier/qualifier
- Validation table: parameter × criterion (SANTE) × result × pass/fail

**Source ranking**:
1. SANTE/11312/2021 (current method validation guidance for residues in food/feed)
2. SANCO/3029/99 rev.4 (water/environmental methods)
3. SANTE/2020/12830 (post-approval method requirements)
4. EFSA Conclusion §B.5 analytical methods
5. CEN standards (EN 15662 QuEChERS, EN 12393 multi-residue)
6. EU Reference Laboratory methods (EURL-FV, EURL-CF, EURL-AO, EURL-SRM)
7. AOAC Official Methods
8. Peer-reviewed Tier-1 analytical journals (J. Chromatogr. A, Anal. Chim. Acta, J. AOAC Int., Anal. Bioanal. Chem., Food Chem., J. Agric. Food Chem.)
9. Manufacturer application notes (COI flag)
10. ISO standards (general analytical)
11. Theses (only if cited Tier 1-3)

**Quality tool**: SANCO/SANTE validation criteria pass/fail (recovery 70-120%, RSDr ≤20%, LOQ ≤ MRL/10 or ≤0.01 mg/kg whichever lower), ion-ratio tolerance ±30%, guideline-compliant flag.

**Anchors required**: LOQ (mg/kg or μg/L), recovery (%, range and mean), RSDr (%), n replicates, matrix, ISTD, instrument, column, mobile phase, gradient.

---

## 7. Chemistry / mechanism / MoA review

**Preferred review type(s):** `systematic_review` (primary — structured search of chemistry literature required). `data_analysis` for QSAR landscape, in silico endpoint prediction. `literature_review` for regulatory MoA narrative (e.g., EFSA MoA guidance-based narrative for ED or resistance mode-of-action).

**Output style:** Figure-primary, table-supported. Molecular structures are the central scientific objects — every named compound rendered. Reaction schemes and degradation pathways mandatory where synthesis routes, biotransformation, or photolysis are in scope. Physchem property tables with method, value, unit, source per property. SAR matrices tabulated. Binding site figures or docking representations where literature provides them. Narrative provides mechanistic synthesis and regulatory interpretation. Source voice: "EFSA [year] noted a primary MoA of [X] [CIT-N]"; "IRAC classifies [substance] in Group [Y] based on [Z] [CIT-N]".

**Molecular structure requirements:** MANDATORY for parent compound, all named analogues (SAR section), all key metabolites and degradates discussed in MoA context. Markush structures for SAR analysis. Reaction scheme figures for synthesis routes, photolysis, hydrolysis, biotransformation. Per `references/molecular_structure_rendering.md`.

**Required sections**:
1. Chemical class and taxonomy (IRAC/HRAC/FRAC group; sub-class)
2. Synthesis routes (where in scope; literature + patent)
3. Physicochemistry (mp, bp, vp, water solubility, log Kow, pKa, density, λmax)
4. Stability and degradation chemistry (hydrolysis pathway, photolysis pathway, thermal)
5. Target site biochemistry (receptor / enzyme / pathway)
6. Selectivity basis (target vs non-target taxa)
7. SAR / QSAR landscape
8. Resistance mechanisms (target-site, metabolic, penetration)

**Required figures/tables** (figures-heavy):
- Structures: parent, key analogues, metabolites, degradates (Markush where SAR)
- Reaction schemes (synthesis, degradation, biotransformation)
- Binding site / docking figures (where literature provides)
- SAR matrices (R-group × bioactivity × ref)
- Resistance mechanism schematic
- Physchem table: property × method × value × ref
- SAR table: structure feature × activity (target × value × ref)

**Source ranking**:
1. EFSA Conclusion §B.2 identity / physchem + MoA where present
2. IUPAC technical reports
3. BCPC Pesticide Manual (current edition)
4. IRAC / HRAC / FRAC classification + technical bulletins
5. Peer-reviewed Tier-1 chem journals (J. Agric. Food Chem., Pest Manag. Sci., J. Med. Chem., Chem. Rev., Chem. Soc. Rev., Tetrahedron)
6. ACS monographs, RSC reviews
7. Patent literature (with scope and COI flag)
8. Conference proceedings (IUPAC Crop Protection Congress, BCPC Congress, ACS AGRO Division)
9. PubChem / ChemSpider curated entries (source-traceable only)

**Quality tool**: structural verification (InChIKey exact match), reproducibility of synthesis/measurement, mechanism plausibility (cross-source triangulation).

**Anchors required**: structure (rendered, with InChIKey), Ki / IC50 (with assay), log P (method: shake-flask / HPLC / calc), pKa, melting/boiling point (with method), λmax (with solvent).

---

## 8. Efficacy / resistance

**Preferred review type(s):** `literature_review` (standard efficacy summary). `database_study` for resistance monitoring registry analysis (IRAC/HRAC/FRAC databases). `data_analysis` for dose-response statistical modelling or trial data meta-analysis.

**Output style:** Structured narrative paragraphs per target pest/disease, supported by trial data tables and dose-response figures. Quantitative anchors mandatory: % control / yield response, dose (g a.s./ha), timing (BBCH stage), trial n, sites, region, year, target pest/disease (scientific name), reference product. EPPO standard compliance stated per trial. GEP (Good Experimental Practice) flag per trial. Resistance classification (IRAC/HRAC/FRAC group) cited with resistance mechanism where known. Source voice: "Zonal efficacy assessment for [zone] [CIT-N] concluded …"; "IRAC classifies [substance] in MoA Group [Y] [CIT-N]".

**Molecular structure requirements:** Parent compound mandatory in §2. No additional structure requirements for standard efficacy reviews unless MoA or resistance mechanism discussion requires structural comparison of analogues.

**Required sections**:
1. GAP (rate, applications, interval, timing, formulation)
2. Trial design (EPPO PP1 series alignment)
3. Dose-response
4. Spectrum (target species)
5. Resistance status (IRAC / HRAC / FRAC group; documented resistance)
6. Mixture / programme positioning

**Required figures/tables**:
- Dose-response curves (% control vs rate)
- % control bar charts by trial site / region
- Resistance frequency maps (if available from monitoring)
- Trial table: trial × pest/disease × dose × % efficacy × reference product × ref × EPPO standard

**Source ranking**:
1. EPPO Standards PP1 series (specific pest standards)
2. Zonal efficacy assessments (zRMS reports)
3. MS authorisation decisions with efficacy basis
4. EFSA peer review (limited efficacy coverage; only where Annex II §6 addressed)
5. IRAC / HRAC / FRAC resistance databases
6. Peer-reviewed: Crop Protection, Pest Manag. Sci., Weed Res., Plant Dis., Phytopathology, Eur. J. Plant Pathol.
7. Industry trial reports (COI flag)
8. Extension service bulletins (national agronomy services)

**Quality tool**: EPPO standard adherence flag, GEP (Good Experimental Practice) flag, reference product used.

**Anchors required**: % control / yield response, dose (g a.s./ha), timing (BBCH stage), trial n, sites, region, year, target pest/disease (scientific name), reference product.

---

## 9. Exposure (operator / worker / bystander / resident)

**Preferred review type(s):** `data_analysis` (primary — AOEM or model-based exposure calculations). `literature_review` for narrative summary of exposure scenario basis. `systematic_review` for contested AOEL/AAOEL derivation.

**Output style:** Scenario-driven. Structured narrative paragraphs per scenario type, each followed by a scenario summary table. Quantitative anchors mandatory: exposure (mg a.s./kg bw/d), AOEL/AAOEL (mg/kg bw/d), MoE, PPE level (none / gloves / gloves+coverall / +RPE), application equipment, body weight assumption. MoE distributions presented for each scenario and PPE tier. Contribution-to-exposure breakdown (hand/body/inhalation) where model outputs permit. Source voice: "Under the AOEM default assumptions [CIT-N], estimated operator exposure was X mg/kg bw/d, yielding a MoE of Y against the AOEL of Z mg/kg bw/d [CIT-N]".

**Molecular structure requirements:** Parent compound mandatory. No additional structure requirements unless metabolite exposure is an element of the assessment.

**Required sections**:
1. AOEL / AAOEL derivation (link to tox §10)
2. Operator exposure scenarios (AOEM 2014)
3. Worker re-entry
4. Bystander / resident (EFSA 2022 guidance)
5. PPE assumptions and stepwise refinement
6. Aggregate exposure (multi-route, multi-source where relevant)

**Required figures/tables**:
- Exposure scenario diagrams (spray operator, mixer/loader, re-entry worker, bystander, resident)
- MoE distributions per scenario
- Contribution-to-exposure waterfalls (hand vs body vs inhalation)
- Scenario table: scenario × model × estimated exposure × AOEL × MoE × PPE level

**Source ranking**:
1. EFSA Guidance on the Assessment of Exposure of Operators, Workers, Residents and Bystanders (2022)
2. AOEM Calculator (current version)
3. RMS RAR Vol 3 B.6.12
4. MS-specific models (BBA / UK POEM / Italian model / Dutch model) where used
5. Peer-reviewed exposure literature (Ann. Work Expo. Health, Sci. Total Environ.)
6. AHETF / ARTF / EUROPOEM database entries

**Anchors required**: exposure (mg a.s./kg bw/d), AOEL/AAOEL (mg/kg bw/d), MoE, PPE level (none / gloves / gloves+coverall / +RPE), application equipment, body weight assumption (70 kg or 60 kg per scenario).

---

## Multi-discipline composition

Real reviews often span disciplines (renewal = identity + physchem + analytical + tox + residue + efate + ecotox + efficacy). Composition rule:

1. Union the L1 sections, ordered per EU dossier convention:
   - Identity → Physchem → Analytical methods → Mammalian tox → Residues → Efate → Ecotox → Efficacy → Exposure → Regulatory implications
2. Apply each discipline's source ranking within its section only.
3. Cross-discipline claims (e.g. "metabolite M1 drives both groundwater PEC and dietary exposure") use the highest-ranking applicable source per discipline, cited per discipline.
4. WoE per endpoint per discipline; integrated WoE in §11 Cross-cutting.
