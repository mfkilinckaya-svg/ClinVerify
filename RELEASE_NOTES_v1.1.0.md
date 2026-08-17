# ClinVerify v1.1.0

Release date: 2026-08-11

## Added

- **Linearity / analytical measuring interval module (CLSI EP06-Ed2, 2020).**
  Implements the current edition of the guideline: a weighted least-squares
  straight-line fit, deviation from linearity assessed against a clinically
  derived allowable deviation from linearity (ADL), and multiplicity-adjusted
  confidence intervals for verification studies (EP06-Ed2 equations 55–60,
  Tables 21 and 24). Supports both the verification design of Chapter 4 and the
  validation design of Chapter 3, with weighting from a precision profile, from
  replicate variances, or unweighted.
  The module reproduces both worked examples given in the guideline: the
  verification example of Tables 18–23 (intercept 35.30, slope 3149.739,
  Z = 2.38 for n = 6) and the design A1 example of Table 14 (A = 0.9600).

- **Selectable total allowable error schemes.** Acceptance criteria can now be
  taken from Nordic EQA programmes (Labquality / NOKLUS / RfB / DEKS),
  CLIA 2024 (42 CFR 493), RCPAQAP 2022 or Rili-BAEK 2023, and a
  laboratory-specific table can be imported from CSV.

- **Data-entry documentation** in About & Guide: the four import routes, the
  simple and full templates, and the columns each module requires.

- **Version indicator** in the sidebar and a statement that all calculations run
  locally and no data leaves the device.

## Fixed

- **Decimal commas were lost when importing .xlsx files.** The CSV reader
  normalised values such as `90,3` to `90.3`; the .xlsx reader did not, so
  text-formatted cells were either dropped or silently truncated (`90,3` was
  read as `90`). Affected within-run precision, between-day precision and any
  other module fed from a text-formatted workbook. All import routes
  (CSV and .xlsx, simple and full templates) are now covered by a regression
  test.

- **An intermediate value was rounded before use.** The absolute imprecision
  derived from a manufacturer %CV claim was rounded to four decimal places and
  the rounded value was then used in the calculation. Rounding is now applied
  only for display.

- **Loading demonstration or pasted data into the linearity module could be
  overwritten** by the previously rendered input grid.

## Changed

- **Reporting resolution.** Displayed precision is now derived from the
  resolution of the entered data rather than fixed: values in measurement units
  follow the data, percentages are given to two decimal places, regression and
  uncertainty coefficients to four significant figures. Computation remains at
  full precision; rounding is applied only for display.

- `ROCHE_DB` renamed to `MANUFACTURER_DB`, since it holds package-insert claims
  for Roche, Sysmex, Siemens and Tosoh analysers.

- Embedded database descriptions in About & Guide corrected
  (biological variation 142 analytes, reference intervals 100 entries,
  total allowable error 107 analytes).

- CLSI EP06-Ed2 and Kallner et al. (2005) added to the reference list.
