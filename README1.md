# Atlantic Equatorial Mode (Atlantic Niño) – Observational Study

## TL;DR
This repository presents an observational analysis of the Atlantic Niño and its comparison with ENSO over the period 1960–2020.
The focus is on seasonal variability, spatial structure, and ocean–atmosphere coupling.
The Atlantic Niño is shown to be a regional, seasonal mode whose identification is highly sensitive to the methodological definition.
Conclusions are still under development; this README documents the analysis workflow and scientific reasoning.

---

## 1. Scientific motivation and scope

The Atlantic Equatorial Mode, also known as the Atlantic Niño, is a pattern of climate variability
characterized by positive sea surface temperature (SST) anomalies in the eastern equatorial Atlantic.
Although it shares some physical mechanisms with the Pacific El Niño–Southern Oscillation (ENSO),
the Atlantic Niño exhibits a weaker amplitude, shorter duration, and a markedly seasonal and regional character.

The objective of this study is to characterize the Atlantic Niño observationally and compare it
systematically with the Pacific Niño, focusing on temporal variability, spatial structure, and
atmospheric impacts over the period 1960–2020.

A central aspect of the work is the definition of robust event-identification criteria, paying
special attention to the seasonal nature of the Atlantic Niño and its independence from ENSO.
Because global warming introduces a background trend in SST records, the analysis is based on
seasonal anomalies to avoid biases toward recent decades.

---

## 2. Data sources

### Sea Surface Temperature (SST)
- HadISST (1° × 1°)
- ERSST (2° × 2°)

### Precipitation
- NOAA PCP (2.5° × 2.5°)
- NCEP–NCAR Reanalysis (1.875° × 1.875°)

The study period spans 1960–2020, selected for data quality and homogeneity.

---

## 3. Methodological overview (high-level)

> **Reading guide**  
> This section summarizes the methodology at a conceptual level.
> Detailed technical justifications, sensitivity tests, and refinements are introduced later
> when required by the results.

Main steps:
- Linear detrending of SST to remove long-term warming signals
- Computation of seasonal SST and precipitation anomalies
- Definition of SST-based indices in ATL3 and Niño 3.4 regions
- Monthly and seasonal variability analysis
- SST–precipitation coupling via correlation and regression
- Event intensity quantified using standardized indices (Z-score)

---

## 4. Mean SST and preliminary methodological considerations

Mean annual SST time series are shown for the ATL3 and Niño 3.4 regions.
Both regions exhibit a clear positive temperature trend over the study period,
consistent with global warming, motivating the application of a detrend prior to
the computation of anomalies.

HadISST and ERSST show coherent behavior, with ERSST presenting slightly higher values.
These differences are attributed to resolution, reconstruction methodology, and
observational coverage.

Values above 35 °C are discarded to avoid land contamination, and values below −1.79 °C
are removed to avoid ice-related artifacts, particularly relevant for ERSST.

---

### Methodological note (optional reading): spatial averaging approximations

Spatial averages were initially computed using direct grid-cell means.
A physically rigorous approach would require weighting by the cosine of latitude,
as grid-cell area decreases with latitude.

Given that the analyzed regions are confined within ±5°, the cosine factor remains
close to unity (≈0.996), leading to relative errors below 0.5%.
Similarly, direct index-based selection was used instead of exact boundary interpolation.

These approximations introduce negligible errors and are validated quantitatively below.

---

## 5. Validation of approximations and robustness checks

The calculation is repeated using exact spatial interpolation and cosine-latitude
area weighting.
Differences in trends and peak values are found to be negligible (<0.1 °C),
confirming that the simplified approach is adequate for the regions considered.

---

## 6. Quality control and outlier filtering

Global maps of SST anomalies reveal the presence of physically inconsistent outliers
in HadISST, particularly in polar regions, with anomalies exceeding 1000 °C.
Such values are non-physical and indicate data artifacts.

A conservative filtering threshold of ±10 °C is applied globally.
This removes spurious values without affecting the physical climate signal, as the
maximum observed anomaly is below 9.3 °C.

---

## 7. Seasonal variability of SST and precipitation

### 7.1 SST monthly variability

Monthly SST anomaly variability over 61 years shows:
- Atlantic Niño (ATL3): peak variability in boreal summer (June–July)
- Pacific Niño (Niño 3.4): peak variability in boreal winter (December–January)

Differences between HadISST and ERSST are small in absolute terms (~0.05 °C),
though relatively more important for the weaker Atlantic Niño signal.

---

### 7.2 Precipitation monthly variability

Precipitation variability shows stronger dependence on the dataset used.
NOAA and NCEP exhibit coherent seasonal cycles but differ in amplitude and phase,
particularly in the equatorial Pacific, reflecting the non-linear nature of
precipitation and reanalysis uncertainties.

---

## 8. Spatial patterns and ocean–atmosphere coupling

### 8.1 SST anomalies vs index

The Atlantic Niño exhibits a localized warming pattern centered in the eastern
equatorial Atlantic, with limited spatial extent and weak teleconnections.

ENSO shows a much stronger and more spatially extensive pattern, with a canonical
equatorial tongue and robust global teleconnections.

---

### 8.2 Precipitation anomalies vs index

Atlantic Niño–related precipitation anomalies are mainly confined to the equatorial
Atlantic and adjacent regions, with weaker and less coherent remote responses.

ENSO produces a highly organized global precipitation response associated with
Walker and Hadley circulation adjustments.

---

## 9. Identification of years with maximum thermal intensity

The five years with the highest SST peaks are identified in both ATL3 and Niño 3.4.
These years are treated as candidate events but do not, by themselves, constitute
proof of an Atlantic or Pacific Niño occurrence.

---

## 10. Event intensity characterization

Event intensity is quantified using a standardized Z-score, defined as the ratio
between the mean anomaly during peak months and the interannual standard deviation.

Classification:
- Z < 0.5: not considered
- 0.5 ≤ Z < 1.0: weak
- 1.0 ≤ Z < 1.5: moderate
- Z ≥ 1.5: strong

Normality of anomaly distributions is verified and found to be reasonable for the
months considered.

---

## 11. Pacific Niño (ENSO) detection methodology

ENSO events are identified following the NOAA ONI definition:
- Threshold: SST anomaly ≥ 0.5 °C in Niño 3.4
- Duration: at least 5 consecutive overlapping 3-month means

Event intensity is evaluated using November–December anomalies and the Z-score.
Canonical and non-canonical events are distinguished based on temporal structure.

---

## 12. Refinement of Atlantic Niño detection criteria

Initial selection based on annual mean SST was found to be inadequate due to the
strong seasonal nature and weaker amplitude of the Atlantic Niño.

The refined approach:
- Uses seasonal SST anomalies instead of absolute SST
- Focuses on boreal summer months (JJA)
- Requires at least three consecutive months above 0.4 °C
- Enforces independence from concurrent ENSO activity

This refinement yields a more physically consistent identification of Atlantic Niño events.

---

## 13. Case studies: Atlantic Niño candidates

Individual years are analyzed in detail to assess temporal structure, intensity,
and ENSO independence.
Several warm years fail to meet the refined criteria, illustrating the sensitivity
of Atlantic Niño detection to methodology.

---

## 14. Updated seasonal-based selection of Atlantic Niño events

The revised anomaly-based, seasonal selection substantially modifies the set of
Atlantic Niño candidates while leaving ENSO selection largely unchanged.

This contrast highlights the fundamental dynamical differences between the two
phenomena and reinforces the need for a tailored, seasonally constrained definition
of the Atlantic Niño.

---

## 15. Work in progress

Conclusions and synthesis of results are currently under development.
This README focuses on documenting the analysis workflow, methodological decisions,
and intermediate physical interpretation.
