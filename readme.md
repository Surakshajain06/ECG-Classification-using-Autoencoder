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



