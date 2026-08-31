# Changelog

All notable changes to ClinVerify are recorded here. Versions follow semantic
versioning. Each release is archived on Zenodo and carries its own version DOI.

## [1.2.0] — 2026-08-31

The release the manuscript is pinned to. It corrects three defects that affected
reported numbers, removes two transcribed guideline tables from the computation
path, and adds a set of checks that run against the published tables every time
the application is opened.

### Fixed

- **Chi-square quantile.** `regularizedGammaInc()` used only the series
  expansion, which converges too slowly once *x* > *a* + 1 — the region every
  quantile at *p* = 0.95 or 0.975 falls in. The inverse built on it drifted with
  the degrees of freedom: 0.07 % low at df = 8 and 7.9 % low at df = 50. That
  value sets the 95 % confidence interval of every CV% the program prints.
  Replaced with the series-plus-continued-fraction form and a bracketed Newton
  iteration; agreement with the exact quantile is now better than 1 × 10⁻⁹
  relative.
- **Upper verification limit factor.** `calcUVLfactor()` did not use the
  quantile function at all: it carried its own Wilson–Hilferty approximation,
  which missed 12 of the 180 entries of EP15-A3 Table 7 at the printed two
  decimals and gave 1.3915 where the guideline and the CLSIEP15 R package give
  1.392269 for the worked example. It now uses the exact quantile and reproduces
  all 180 published entries.
- **Confidence interval of the reported statistic.** For a multi-replicate
  between-day design the program reported the within-laboratory CV% but computed
  its interval from the pooled SD on *N* − 1 degrees of freedom, while labelling
  it with df_WL. The interval is now built from s_WL on df_WL.
- **Printable verification record.** The report recomputed a plain pooled CV%
  from the raw values instead of carrying the statistic the analysis produced; a
  between-day record printed 0.68 % where the screen showed 0.72 %, and the
  verdict rows were judged against the wrong number. The analysis now publishes
  its result and the report reads it.
- **EP15-A3 Table 6, seven-run column.** The row (ρ = 1.14, df_WL = 26) was
  missing, so every entry below it was one degree of freedom low and the
  verification limit 0.30–0.39 % too permissive for 7 × 5 designs with
  ρ ≤ 1.13. The table was transcribed twice and the copy feeding the
  verification limit still carried the error. Both copies have been removed from
  the computation path (see below).
- **Goal inputs were silently discarded.** `refreshGoalInputs()` rebuilt the
  goal fields whenever a level was added, removed or re-dimensioned, wiping the
  manufacturer override, the long-term CV% and the manually entered goal. Only
  the EFLM goal survived, because it is recomputed from the CVI field. Entered
  values are now preserved across the rebuild.
- **Approval followed a fixed priority** — manufacturer, then EFLM, then
  laboratory, then manual — so a laboratory that selected a goal source still
  had its verdict decided by the EFLM specification whenever a CVI had been
  filled in automatically. Approval now follows the selected source, and says so
  on the page and in the report.
- Selecting a between-day goal source cleared the active state of the per-level
  tabs in the within-run module.
- The interpolation trace printed a template placeholder instead of the lower
  package-insert concentration.
- The Mentor demonstration data set loaded three replicates per level instead of
  the ten used for the published example.

### Changed

- **Degrees of freedom for the within-laboratory SD are computed from CLSI
  EP15-A3 Appendix B rather than read from a transcribed Table 6.** Appendix B4
  gives the Satterthwaite expression; the note "The Calculations Underlying
  Table 6" gives the back-calculation from the claims ratio. Together they
  reproduce all 72 published entries exactly, so the table is no longer embedded,
  the risk of a transcription error is gone, and the guideline's restriction to
  designs of five, six or seven runs with five replicates no longer applies.
- The report now carries s_R, s_B, s_WL, df_WL and the 95 % confidence interval
  of the CV%, and lists every goal that was entered — manufacturer, EFLM,
  laboratory long-term and manual — each with the limit applied and a marker
  showing which one the approval state was taken from.
- Comparison sections are numbered in the order they are produced, and the
  overall verdict states how many of the active criteria were met rather than
  assuming two.
- All remaining Turkish interface strings translated to English.

### Added

- **Built-in checks against the guidelines**, shown in About & Guide and run at
  every page load: all 72 entries of EP15-A3 Table 6, all 180 entries of
  Table 7, the Satterthwaite worked example of Appendix B4 (df_WL = 11.46), and
  the multiplicity-adjusted Z of EP06-Ed2 Table 21 (2.311 and 2.378). The
  published tables are kept as test fixtures only; nothing computes from them.
- **A fourth goal source, "Manual / Published"**, for a specification that comes
  neither from the package insert nor from the EFLM database — a professional
  body or programme criterion, for example the ADA/NGSP imprecision goal for
  HbA1c. The source is entered as free text and is carried into the report, with
  an optional switch to apply the EP15-A3 verification limit to it. The
  within-run module's "Other" target gained the same source field.
- Linearity (CLSI EP06-Ed2): a combined allowable deviation from linearity
  expressed as a percentage, a fixed value, or the larger of the two; a two-step
  derivation of the ADL from the allowable total error with both fractions
  declared and editable; the replicate-adequacy check of Appendix D, eq. (D1);
  the constant-SD precondition of subchapter 4.1.2; a warning on non-monotonic
  fitted sigma; and the verified interval, narrowed where an end level fails.
- The creatinine demonstration data set can be downloaded as an import-ready CSV
  that reproduces the demonstration exactly on re-import.

## [1.1.0] — 2026-07

Archived on Zenodo. Nine verification modules; reference databases for
manufacturer precision claims, biological variation and reference intervals;
four selectable sources of total allowable error.
