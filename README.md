# In-Vehicle Respiration Analysis for Driver Monitoring System (DMS) Using AI

## Executive Overview
This repository holds the Master's dissertation research report for an end-to-end signal processing and deep learning pipeline developed to analyze driver respiratory rates for in-cabin Driver Monitoring Systems (DMS). 

* **Author:** Adithya Satheesh Kumar Pillai
* **Institution:** School of Physics, Engineering and Computer Science, University of Hertfordshire
* **Degree:** MSc Automotive Engineering (Commendation)

📄 **[Download / View Full MSc Thesis Report PDF](./Final_Report.docx)** *(Or update file name if PDF)*

---

## 🛠️ Technical Methodology & Pipeline

1. **Dataset Selection & Extraction:**
   * Utilized the **BIDMC PPG and Respiration Dataset** (53 subjects, ECG/PPG/Respiration signals sampled at 125 Hz).
   * Segmented ECG data into intervals and categorized them based on Respiratory Rate (RR) into 3 physiological classes: **Low (Bradypnea), Normal, and High (Tachypnea)**.

2. **Feature Engineering (Time-Series to Scalograms):**
   * Transformed 1D time-domain ECG/respiratory signals into 2D time-frequency representations using **Continuous Wavelet Transform (CWT)** in MATLAB.
   * Outputted 2,448 resized RGB scalogram images (Normal: 1,896 | High: 465 | Low: 87).

3. **Deep Learning Architecture & Model Training:**
   * Selected pre-trained **GoogLeNet** (22-layer deep CNN architecture with multi-scale Inception modules).
   * Replaced the classification layer with a Fully Connected layer of `OutputSize = 3`.
   * **Initial Baseline Performance (No Augmentation):** Trained with SGDM optimizer, `InitialLearnRate = 0.0001`, `MiniBatchSize = 16`, `MaxEpochs = 50`. Achieved an initial validation accuracy of **90.59%**.

4. **Signal Data Augmentation & Hyperparameter Tuning:**
   * Performed time-series signal transformations including **White Noise injection, Blurring, and Sharpness adjustment** to expand the dataset to **9,792 scalogram images**.
   * Executed exhaustive sweep hyperparameter tuning using MATLAB **Experiment Manager**.
   * **Final Model Performance:** Achieved **99.23% Validation Accuracy** (`Trial 3: LearnRate = 0.001`, `BatchSize = 16`).

---

## 📊 Experimental Results Summary

| Model Setup | Total Scalograms | Initial Validation Acc | Final Validation Acc | Normal Class Error |
| :--- | :---: | :---: | :---: | :---: |
| **Without Augmentation** | 2,448 | 90.59% | 91.41% | 4.0% |
| **With Signal Augmentation** | 9,792 | 97.55% | **99.23%** | **0.3%** |

---

> **Note on Datasets and Code:** 
> Data preprocessing, CWT image transformations, and CNN network training were conducted using university-licensed MATLAB, Deep Network Designer, and Experiment Manager toolboxes. All architectural parameters, confusion matrices, and validation curves are documented in detail within the thesis report document.
