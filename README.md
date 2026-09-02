# ClinVerify

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21255695.svg)](https://doi.org/10.5281/zenodo.21255695)

**ClinVerify** is an open-source, single-file (HTML/CSS/JS) clinical laboratory
verification tool. It runs entirely in the browser — no server, no install,
no internet connection required after loading the page — and is designed for
routine use by clinical laboratories performing method and instrument
verification in line with CLSI guidelines.

🔗 **Live tool:** https://mfkilinckaya-svg.github.io/ClinVerify/

## Modules

| Module | Standard | Purpose |
|---|---|---|
| M1 — Within-run precision | CLSI EP15-A3 | Repeatability verification |
| M2 — Between-day precision | CLSI EP15-A3 | Within-laboratory precision (ANOVA) |
| Method Comparison | CLSI EP09c | Passing-Bablok regression, Bland-Altman |
| Reference Interval Verification | CLSI EP28-A3c | Verification of manufacturer/transferred RIs |
| Biological Variation | EFLM Biological Variation Database | APS-based acceptance criteria |
| Mentor Recalibration | Kallner (2013) | Two-point recalibration uncertainty (U_rel) |
| Inter-Instrument Comparison | Fraser (CG, 1999) | Cross-instrument bias verification |
| Bias (IQC/EQA) | — | Z-score based bias monitoring |

## Instruments in scope

Roche cobas c703 / e801, Sysmex XR-Series, Sysmex InteRRliner (ESR),
Siemens CS-5100 (coagulation), Siemens Atellica NEPH (nephelometry only),
Tosoh G11 (HbA1c).

## Design philosophy

- **Single file** — the entire application is one `.html` file; no build step,
  no server dependency, works offline once downloaded.
- **Standards-first** — each module follows its CLSI/EFLM/Kallner reference
  method exactly, without added complexity beyond what the standard specifies.
- **Validated** — outputs cross-checked against the
  [CLSIEP15 R package](https://github.com/clauciorank/CLSIEP15), Analyse-it,
  and Kallner's official Mentor v1.35 Excel workbook.

## Usage

Open `index.html` in any modern browser (Chrome, Firefox, Edge, Safari), or
use the hosted version linked above. Each module accepts manual data entry or
CSV/XLSX import (drag-and-drop supported).

## Citation

If you use ClinVerify in academic work, please cite it using the metadata in CITATION.cff, or as:

Kilinckaya, M. F. (2026). ClinVerify: An Open-Source Single-File Tool for Clinical Laboratory Method Verification (v1.2.1) [Software]. Zenodo. https://doi.org/10.5281/zenodo.21255694

The DOI above is the concept DOI and always resolves to the latest version. To cite the exact release you used, take the version DOI from the Zenodo record (v1.2.1: https://doi.org/10.5281/zenodo.XXXXXXXX).

## License

Released under the [MIT License](LICENSE).

## Author

Muhammed F. Kilinckaya, Helse Møre og Romsdal (HMR), Norway
