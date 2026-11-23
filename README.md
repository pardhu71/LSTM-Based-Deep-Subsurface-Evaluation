# LSTM-Based Deep Subsurface Evaluation

### Statistical Anomaly Identification and Machine Learning-Based Classification

**Project Repository:** LSTM-Based Deep Subsurface Evaluation  
**Institution:** KL University  
**Batch ID:** 23IEESIOT14

---

## Project Team

| Name | Student ID |
|---|---|
| M. Pardhasardhi | 2300049071 |
| N. Abhilash | 2300049207 |
| A. Arsha | 2300040388 |

**Project Guide:** Dr. G. V. Subbarao

---

## 1. Project Overview

This project explores the application of statistical anomaly identification and Long Short-Term Memory (LSTM) neural networks for analysing CFRP subsurface measurement data.

The proposed workflow processes measurement profiles, calculates anomaly scores, generates statistical pseudo-labels, reduces feature dimensions using Principal Component Analysis (PCA), and trains an LSTM-based classification model.

The objective is to identify locations with unusual measurement patterns and classify them as normal or abnormal candidates.

## 2. Dataset Description

**Dataset:** `LFM005CFRP`

The dataset contains subsurface measurements arranged across spatial locations.

| Parameter | Description |
|---|---|
| Dataset dimensions | 160 × 137 × 625 |
| X-Y locations | 21,920 |
| Measurements per location | 625 |
| Total measurement values | 13,700,000 |
| Data type | `uint16` |

Each X-Y location is represented by a profile containing 625 measurement values.

## 3. Proposed Methodology

The project follows these major processing stages:

1. **Data Preprocessing:** Load and organise the CFRP measurement data into individual location profiles.
2. **Median Reference Profile:** Calculate the median reference value at each measurement index across all locations.
3. **Anomaly Score Calculation:** Measure the average absolute deviation of each location profile from the median reference profile.
4. **Robust Statistical Labelling:** Apply the robust Z-score method using the median and Median Absolute Deviation (MAD).
5. **Dimensionality Reduction:** Apply PCA to reduce the original 625 features to 6 principal components.
6. **LSTM Classification:** Train an LSTM-based neural network using the reduced feature representation.
7. **Evaluation and Visualisation:** Analyse model predictions using accuracy, precision, recall, F1-score, confusion matrix, and spatial visualisations.

## 4. Anomaly Detection

The anomaly score is calculated as:

$$
S_i = \frac{1}{625}\sum_{j=1}^{625}|Z_{ij}-M_j|
$$

Where:

- $Z_{ij}$ represents the measurement at location $i$ and index $j$.
- $M_j$ represents the median reference value at index $j$.
- $S_i$ represents the anomaly score for location $i$.

The robust Z-score is calculated as:

$$
R_i = 0.6745 \frac{S_i-\operatorname{median}(S)}{\operatorname{MAD}(S)}
$$

Where:

- $R_i$ represents the robust Z-score for location $i$.
- $\operatorname{median}(S)$ represents the median of all anomaly scores.
- $\operatorname{MAD}(S)$ represents the Median Absolute Deviation of the anomaly scores.

Locations with robust Z-scores greater than 3.5 are labelled as abnormal candidates. Other locations are labelled as normal candidates.

**Important:** These are statistically generated pseudo-labels, not independently verified physical defect labels.

## 5. PCA-Based Feature Reduction

Principal Component Analysis (PCA) is used to reduce the original 625 measurement features to 6 principal components.

- Original features: 625
- Reduced features: 6
- Reported cumulative explained variance: approximately 99.17%

This reduces the input dimensionality while retaining most of the measured variance.

## 6. LSTM Model Architecture

The classification model uses the following architecture:

| Layer | Configuration |
|---|---|
| Input | 6 features, reshaped as 6 steps |
| LSTM | 32 units |
| Dropout | 0.2 |
| Dense | 16 units, ReLU activation |
| Output | 1 unit, Sigmoid activation |

The model produces a probability used to classify each location into one of the two pseudo-label categories.

## 7. Experimental Results

The statistical labelling process produced:

| Category | Number of locations |
|---|---:|
| Normal candidates | 19,779 |
| Abnormal candidates | 2,141 |
| Total | 21,920 |

### LSTM Classification Performance

The reported test-set confusion matrix is:

| | Predicted Normal | Predicted Abnormal |
|---|---:|---:|
| Actual Normal | 3,946 | 10 |
| Actual Abnormal | 3 | 425 |

The classification metrics are:

| Metric | Result |
|---|---:|
| Accuracy | 99.70% |
| Precision | 97.70% |
| Recall | 99.30% |
| F1-score | 98.49% |

**Result interpretation:** These metrics measure agreement with the statistically generated pseudo-labels. They should not be interpreted as independently verified physical defect detection accuracy.

## 8. Project Visualisations

The project includes visual analysis such as:

- CFRP X-Y anomaly score heatmap
- LSTM-based candidate-region spatial map
- LSTM training and validation accuracy curves
- LSTM training and validation loss curves
- Confusion matrix

These visualisations help interpret the spatial distribution of anomaly scores and the classification results.

## 9. Technologies Used

- Python
- NumPy
- Pandas
- Scikit-learn
- TensorFlow / Keras
- Matplotlib
- MATLAB-format dataset processing
- Principal Component Analysis
- Long Short-Term Memory Neural Networks

## 10. Limitations

- The anomaly labels are generated statistically and are not independently verified defect labels.
- The reported classification metrics measure agreement with these pseudo-labels.
- PCA components do not inherently represent chronological time steps; therefore, the LSTM design should be compared with simpler classification models.
- The physical interpretation of the original measurement values requires additional dataset documentation.

## 11. Future Scope

- Validate detected candidate regions against independently confirmed defect information.
- Compare LSTM performance with conventional machine learning classifiers.
- Investigate alternative feature extraction and dimensionality reduction methods.
- Evaluate model generalisation on additional CFRP datasets.
- Improve model interpretability and spatial defect analysis.

## 12. Conclusion

This project presents a statistical and deep learning-based workflow for analysing CFRP subsurface measurement profiles. By combining median-based anomaly scoring, robust statistical pseudo-labelling, PCA-based dimensionality reduction, and LSTM classification, the approach identifies locations with unusual measurement patterns.

The results demonstrate promising agreement with the generated statistical labels and provide a foundation for further investigation using independently validated defect data.

---

**Developed at KL University**  
**Project:** LSTM-Based Deep Subsurface Evaluation  
**Batch:** 23IEESIOT14
