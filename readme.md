# ECG Signal Classification Using Autoencoder Features

## Problem Statement:
The aim is to classify normal and abnormal heartbeats from MIT-BIH ECG data by first using a 1D convolutional autoencoder to extract compressed heartbeat features, then training classifiers like Random Forest or XGBoost on these features. This reduces noise and dimensionality, improving efficiency and accuracy in arrhythmia detection.

## Exploratory data analysis
Each row summarizes one MIT-BIH ECG record, including its ID, sampling rate, total samples, and lead information. It also lists the number of detected heartbeats based on R-peak annotations.
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
    <img src="Images\ECG_types.png" alt="Beat_types" width="100%"/>
    <figcaption>
      <p style="font-size:13px; margin-top: 8px;">
        <b>Figure 2:</b> ECG signal summary
      </p>
    </figcaption>
  </figure>
</div>

### 1. Normal Beat (N)
**Looks like:**
- Clear **P wave**, sharp **QRS complex**, smooth **T wave**.
- Evenly spaced (**regular rhythm**).
- Consistent amplitude and shape in the same lead.

### 2. Atrial Premature Beat (APB / A)
**Looks like:**
- Comes **earlier than expected** (interrupts normal rhythm).
- **P wave** may look different or be hidden in QRS.
- QRS is usually narrow (unless abnormal conduction).
- Shorter **R–R interval** before it, then a pause afterward.
- Early spike with **no P wave** and **improper QRS shape** → possible noise.

### 3. Ventricular Beat (V)  
- **Wide QRS** (≥120 ms), abnormal shape.
- No visible **P wave** before it.
- **T wave** usually in opposite direction of main QRS spike.
- May come early or in regular ventricular rhythm.
- Very narrow but tall spike is **not ventricular** (likely noise).

### 4. Paced Beat (+)
**Looks like:**
- Very small, sharp **pacemaker spike** before QRS.
- QRS often wide or unusual after spike.
- Often very regular if patient is paced.
- Spike without a QRS in all leads → noise.
- True pacing spikes are narrow and followed by consistent ventricular complex.

---

### Artifact Clues for Any Beat Type
- Appears only in **one lead**.
- Shape doesn’t match surrounding beats.
- Happens **too soon** after last QRS (<200 ms).
- Extremely sharp vertical edges, no real QRS morphology.
- Baseline jumps before/after spike.


