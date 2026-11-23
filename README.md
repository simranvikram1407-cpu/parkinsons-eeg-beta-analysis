# Parkinson's Disease: EEG Beta-Band Power Analysis

An exploratory computational neuroscience project investigating beta-band (13–30 Hz) activity in resting-state EEG recordings from individuals with Parkinson's disease and healthy controls.

## 1. Research Objective

This project investigates two questions:

1. Do individuals with Parkinson's disease show differences in relative beta-band power compared with healthy controls?
2. Does dopaminergic medication influence relative beta-band power in Parkinson's disease?

Beta-band activity is particularly relevant to Parkinson's disease research because of its association with basal ganglia–cortical motor networks.

## 2. Dataset

**Source:** [OpenNeuro – ds002778](https://openneuro.org/datasets/ds002778)

The dataset contains resting-state EEG recordings collected using a BioSemi ActiveTwo system.

The analysis includes 46 recordings:

| Group | Recordings |
|---|---:|
| Healthy controls | 16 |
| Parkinson's disease – OFF medication | 15 |
| Parkinson's disease – ON medication | 15 |
| **Total** | **46** |

The 15 Parkinson's disease participants have paired ON and OFF medication recordings.

- Sampling frequency: 512 Hz
- Scalp channels analysed: 32
- Beta frequency band: 13–30 Hz

## 3. Methodology

### EEG preprocessing

The analysis pipeline includes:

- Selection of 32 scalp EEG channels.
- Removal of channel-wise DC offsets.
- Common-average referencing.
- Band-pass filtering between 0.5 and 45 Hz.
- Automated signal-quality screening.
- Rejection of selected extreme-amplitude and nearly flat signal windows.

### Power spectral analysis

Power spectral density (PSD) was estimated using Welch's method.

Analysis parameters:

- Window duration: 4 seconds.
- Overlap: 50%.
- Beta band: 13–30 Hz.
- Total reference band: 1–45 Hz.

Relative beta power was calculated as:

Relative Beta Power (%) = (Beta-band power / Total power from 1–45 Hz) × 100

Two measures were investigated:

1. **Whole-scalp relative beta power:** Average of the relative beta-power estimates across 32 scalp channels.
2. **Sensorimotor relative beta power:** Average of the relative beta-power estimates from C3 and C4.

### Statistical analysis

The following statistical tests were used:

- Mann–Whitney U test: Healthy controls versus Parkinson's OFF medication.
- Wilcoxon signed-rank test: Parkinson's ON versus OFF medication.
- Holm correction for multiple comparisons across four primary tests.

Significance threshold: p < 0.05.

## 4. Results

### Descriptive statistics

Relative beta power is reported as mean ± standard deviation.

| Measure | Control | PD OFF | PD ON |
|---|---:|---:|---:|
| Whole scalp (%) | 19.535 ± 9.329 | 18.294 ± 6.976 | 18.227 ± 6.483 |
| C3/C4 (%) | 26.277 ± 13.005 | 24.172 ± 8.509 | 24.740 ± 8.212 |

### Statistical comparisons

| Comparison | Measure | p-value | Holm-adjusted p |
|---|---|---:|---:|
| Control vs PD OFF | Whole scalp | 0.7369 | 1.0000 |
| PD ON vs PD OFF | Whole scalp | 0.9341 | 1.0000 |
| Control vs PD OFF | C3/C4 | 0.7669 | 1.0000 |
| PD ON vs PD OFF | C3/C4 | 0.5245 | 1.0000 |

No statistically significant differences were detected in any of the four comparisons after multiple-comparison correction.

These findings do not establish equivalence between groups or demonstrate the absence of a medication effect.

## 5. Visualisations

### Whole-scalp relative beta power

![Whole-scalp relative beta power](figures/whole_scalp_relative_beta_percent_plot.png)

### C3/C4 relative beta power

![C3/C4 relative beta power](figures/C3_C4_relative_beta_percent_plot.png)

## 6. Quality Control

Signal-quality screening was conducted across all 46 recordings.

The analysis included:

- A 150 µV peak-to-peak screening threshold for identifying potentially contaminated windows.
- A conservative 500 µV peak-to-peak rejection threshold for four-second PSD windows.
- A flat-signal screening criterion of standard deviation below 0.1 µV.
- A previously identified global recording disturbance in one PD ON recording, which did not overlap any complete four-second PSD window.

The 150 µV screening flags were retained for quality-control reporting and were not automatically treated as confirmed artifacts.

## 7. Limitations

- The sample size is relatively small, limiting statistical power.
- Dedicated EOG channels were not available in the dataset.
- The EEG reference configuration was not documented in the metadata.
- Automated artifact screening cannot replace comprehensive expert visual inspection.
- Relative beta power does not directly measure absolute beta-band power.
- The analysis focuses on scalp EEG and cannot directly establish activity in deep basal ganglia structures.
- The results should be interpreted as exploratory rather than definitive evidence.

## 8. Repository Structure

```text
parkinsons-eeg-beta-analysis/
│
├── README.md
├── parkinsons_beta_analysis.ipynb
│
├── final_beta_power_results.csv
├── descriptive_statistics.csv
├── statistical_tests.csv
├── recording_quality_control.csv
├── channel_quality_control.csv
│
├── whole_scalp_relative_beta_percent_plot.png
└── C3_C4_relative_beta_percent_plot.png
```

## 9. Tools and Technologies

- Python
- MNE-Python
- NumPy
- Pandas
- SciPy
- Matplotlib
- Google Colab
- Statistical hypothesis testing

## 10. References

1. Jackson et al. (2019). *Characteristics of Waveform Shape in Parkinson's Disease Detected with Scalp Electroencephalography.* eNeuro. https://doi.org/10.1523/ENEURO.0151-19.2019

2. OpenNeuro dataset: ds002778. https://openneuro.org/datasets/ds002778

---

**Project Type:** Undergraduate Computational Neuroscience Research Project

**Focus Areas:** EEG Signal Processing | Parkinson's Disease | Computational Neuroscience | Statistical Analysis

**Disclaimer:** This project is intended for research and educational purposes. It is not a clinical diagnostic tool.
