# Modeling time series extracted from brain activity

Detrended Fluctuation Analysis (DFA) of EEG recordings from patients with epilepsy, split into the general, pre-ictal (before the seizure), ictal (during) and post-ictal (after) phases of the first seizure. This repository holds the data and analysis behind the paper below.

**Paper:** Orlando Mota Pires, Adrian Widmer and Florêncio Mendes Oliveira Filho. *Modeling Ictal Sentences Characterized by the Occurrence of Seizures in a Setting of Neurological Disorder.* XXVIII Encontro Nacional de Modelagem Computacional (ENMC), 2025. [PDF](https://orlandomotapires.github.io/assets/pdf/MISCOSSND.pdf)

![DFA fluctuation function F(n) of patient PN06 for channels Fp1, O1, Cz, Fp2 and O2, one panel per phase](<Patients Data 00 - 17/INDIVIDUO_EDF_PN06/Graph06.PNG>)

*Patient PN06: the DFA fluctuation function F(n) of five channels in each phase. A change of slope (a crossover) marks a change in how the signal is correlated.*

## Result

The paper looks closely at three patients (PN00, PN06 and PN07) and five channels spread over the frontal (Fp1, Fp2), central (Cz) and occipital (O1, O2) regions. The DFA exponent was fitted per channel and per phase. Every phase of every patient showed at least two crossovers, and the fitted exponents ranged from anti-persistent through 1/f noise to non-stationary behaviour. The behaviour depends on the patient, the time of the discharge and the phase, which makes DFA useful for separating the phases. The same method can be applied to all 14 patients in the database.

## Data

The recordings come from the [Siena Scalp EEG Database](https://physionet.org/content/siena-scalp-eeg/1.0.0/) on PhysioNet, recorded at the Neurology and Neurophysiology Unit of the University of Siena (512 Hz, 10-20 electrode system). It is published under the [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/) license. If you use the data, cite:

- Detti, P., Vatti, G. and Zabalo Manrique de Lara, G. (2020). EEG synchronization analysis for seizure prediction: a study on data of noninvasive recordings. *Processes*, 8(7), 846.
- Goldberger, A. L. et al. (2000). PhysioBank, PhysioToolkit, and PhysioNet: components of a new research resource for complex physiologic signals. *Circulation*, 101(23), e215–e220.

The [MIT license](LICENSE) in this repository covers the code, not the EEG data.

## What is in the repository

| Path | Contents |
| --- | --- |
| `Patients Data 00 - 17/INDIVIDUO_EDF_PNxx/` | One folder per patient: the signals and annotations exported from EDF, the `GENERAL`, `PRE_ICTAL`, `ICTAL` and `POST_ICTAL` windows for each channel, the DFA output, the Origin projects (`.OPJ`) with the plots and fits, and the plots as images |
| `Patients 00 - 17.pdf` | The DFA plots of every patient, one page each |
| `General_pre_post_ictal RESUME.xlsx` | The fitted DFA exponents per patient, channel and phase, with the scale ranges between crossovers |
| `calculate_shannon_entropy.ipynb` | Normalised Shannon entropy of each window |
| `Patients Entropy Tables/` | The entropy results per patient |

## How it was done

For each patient:

1. Convert the EDF recording to text with `edf2ascii.exe`.
2. Cut the general, pre-ictal, ictal and post-ictal windows of each channel with `cutting_sections.ipynb`, using the seizure start and end times listed in the database.
3. Compute the DFA fluctuation function of each window with `dfa12.exe`.
4. Fit the DFA exponent and find the crossovers in Origin (the `.OPJ` projects).

The `.exe` tools run on Windows. The notebooks need Python 3 with `numpy` and `pandas`.

## Authors

Orlando Mota Pires, Adrian Widmer and Florêncio Mendes Oliveira Filho, Senai Cimatec.
