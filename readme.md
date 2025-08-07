# ECG Signal Classification Using Autoencoder Features

## Problem Statement:
The goal of this project is to automatically classify normal and abnormal heartbeats from ECG signals using a combination of autoencoder-based feature extraction and traditional machine learning classifiers. We utilize the MIT-BIH Arrhythmia Database, which includes 48 ECG recordings from different patients, each consisting of .dat (signal), .hea (metadata), and .atr (annotations) files. Due to the high dimensionality, noise, and variability in raw ECG signals, we first train a 1D convolutional autoencoder to learn compressed representations (bottleneck features) of individual heartbeats. These features are then used to train classifiers such as Random Forest or XGBoost to identify arrhythmic beats. This approach improves classification efficiency and accuracy by focusing on essential signal characteristics, enabling faster and more reliable ECG interpretation.


![ECG signal summary in dataframe format](Images/Signal_summary.png)


