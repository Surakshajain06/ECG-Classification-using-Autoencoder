# ECG Signal Classification Using Autoencoder Features

## Problem Statement:
The goal of this project is to automatically classify normal and abnormal heartbeats from ECG signals using a combination of autoencoder-based feature extraction and traditional machine learning classifiers. We utilize the MIT-BIH Arrhythmia Database, which includes 48 ECG recordings from different patients, each consisting of .dat (signal), .hea (metadata), and .atr (annotations) files. Due to the high dimensionality, noise, and variability in raw ECG signals, we first train a 1D convolutional autoencoder to learn compressed representations (bottleneck features) of individual heartbeats. These features are then used to train classifiers such as Random Forest or XGBoost to identify arrhythmic beats. This approach improves classification efficiency and accuracy by focusing on essential signal characteristics, enabling faster and more reliable ECG interpretation.

## Exploratory data analysis
Each row in the summary table represents one ECG record from the MIT-BIH Arrhythmia Database. The ID is the unique record number. Sampling Rate shows how many data points were recorded per second (360 Hz for all records). Total Samples indicates the length of the signal in data points. Channels and Channel Names tell how many ECG leads were used and their names. Beats Detected shows the number of heartbeats identified based on R-peak annotations, where each beat typically includes a full PQRS complex.
<div align="center">
  <figure>
    <img src="Images/Signal_summary.png" alt="ECG signal summary" width="100%"/>
    <figcaption>
      <p style="font-size:13px; margin-top: 8px;">
        <b>Figure 1:</b> ECG signal summary
      </p>
    </figcaption>
  </figure>
</div>

## ECG Beat Types 

<div align="center">
  <figure>
    <img src="Images\ECG_types.png" alt="ECG signal summary" width="100%"/>
    <figcaption>
      <p style="font-size:13px; margin-top: 8px;">
        <b>Figure 1:</b> ECG signal summary
      </p>
    </figcaption>
  </figure>
</div>

## 1. Normal Beat (N)
**Looks like:**
- Clear **P wave**, sharp **QRS complex**, smooth **T wave**.
- Evenly spaced (**regular rhythm**).
- Consistent amplitude and shape in the same lead.

## 2. Atrial Premature Beat (APB / A)
**Looks like:**
- Comes **earlier than expected** (interrupts normal rhythm).
- **P wave** may look different or be hidden in QRS.
- QRS is usually narrow (unless abnormal conduction).
- Shorter **R–R interval** before it, then a pause afterward.
- Early spike with **no P wave** and **improper QRS shape** → possible noise.

## 3. Ventricular Beat (V)  
- **Wide QRS** (≥120 ms), abnormal shape.
- No visible **P wave** before it.
- **T wave** usually in opposite direction of main QRS spike.
- May come early or in regular ventricular rhythm.
- Very narrow but tall spike is **not ventricular** (likely noise).

## 4. Paced Beat (+)
**Looks like:**
- Very small, sharp **pacemaker spike** before QRS.
- QRS often wide or unusual after spike.
- Often very regular if patient is paced.
- Spike without a QRS in all leads → noise.
- True pacing spikes are narrow and followed by consistent ventricular complex.

---

## Artifact Clues for Any Beat Type
- Appears only in **one lead**.
- Shape doesn’t match surrounding beats.
- Happens **too soon** after last QRS (<200 ms).
- Extremely sharp vertical edges, no real QRS morphology.
- Baseline jumps before/after spike.


