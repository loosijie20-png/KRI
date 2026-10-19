# **Machine Learning-Based Prediction of Tsunami Occurrence Using Global Seismic Data**

## Project Background

**Context**

Submitted in fulfilment of the course SIT3020 Python for Data Science, Universiti Malaya, Academic Session 2025/2026, Semester II. A group project involving 6 members.

**Problem statement**

Major earthquakes pose a severe threat to coastal areas because they can trigger catastrophic tsunamis. The project asks whether tsunami occurrence can be predicted from earthquake characteristics such as magnitude, depth and station distance.

## Objectives

1. Explore the distribution of key earthquake features: magnitude, depth, significance score, distance-related variables, intensity measures and geographic location.
2. Examine the relationships between seismic features and tsunami occurrence using descriptive statistics, visualisations and correlation analysis.
3. Apply and compare machine learning models for binary classification of tsunami occurrence, and identify the model with the best predictive performance.

## Data Sources

| Dataset | Source / Link | Size (rows × cols) | Time period |
| --- | --- | --- | --- |
| earthquake.csv | [URL](https://www.kaggle.com/datasets/warcoder/earthquake-dataset/data) | 1,000 × 19 | 1995–2023 |

## Key Findings

- **Random Forest was the best overall model**, with a Test macro F1 of 0.6218 and a Test Accuracy of 0.7143, out of seven algorithms compared (Logistic Regression, KNN, Decision Tree, Random Forest, Gradient Boosting, Naive Bayes, SVM).
- **Magnitude alone does not explain tsunami occurrence.** Its point-biserial correlation with tsunami was r = −0.0012 (not significant); the horizontal distance from the epicenter to the nearest station had the strongest positive association (r = 0.4432), and the total number of seismic stations used to determine earthquake location had the strongest negative association (r = −0.4260).

| Model | Training F1 (Macro) | Test F1 (Macro) |
| --- | --- | --- |
| **Random Forest** | 0.7493 | **0.6218** |
| Logistic Regression | 0.6701 | 0.6041 |
| SVM | 0.6761 | 0.5698 |
| Naive Bayes | 0.6431 | 0.5585 |
| KNN | 1.0000 | 0.5578 |
| Gradient Boosting | 0.9210 | 0.5514 |
| Decision Tree | 0.8610 | 0.5204 |

## Project Structure

```
[Python] Tsunami Prediction/
├── analysis.ipynb        # Code: cleaning, EDA, preprocessing, model comparison
├── earthquake.csv        # Main dataset: 1,000 major earthquakes, 19 columns
├── best_model.pkl        # Best model saved by the model selector (Random Forest)
├── requirements.txt      # Required Python packages
├── report.pdf            # Written report
└── README.md
```

## Skills I Learned

**Technical skills**

- Data cleaning: missing-value audit, datetime conversion, filtering to the reliable 2013+ records
- Exploratory data analysis: descriptive statistics, skewness, boxplots, point-biserial correlation and correlation heatmaps
- Preprocessing pipelines: scikit-learn Pipeline and ColumnTransformer with RobustScaler, after a stratified 80/20 train-test split to prevent data leakage
- Model evaluation: confusion matrices and learning curves

**Tools & libraries**

- Data: pandas, NumPy, SciPy
- Visualisation: Matplotlib, seaborn
- Machine learning: scikit-learn, imbalanced-learn

## My Contribution

- Data cleaning and EDA
- Key involvement includes identifying, through time-series analysis, that none of the 547 records before 2013 were labelled as tsunami events, which was not explicitly mentioned in the dataset description. This finding led to restricting modelling to 2013 onwards.

## Challenges & Lessons Learned

| Challenge | How it was addressed |
| --- | --- |
| No tsunami labels in the 547 records before 2013, likely a change in data collection or labelling | Filtered to the 453 records from 2013 onwards before modelling |
| High missingness in categorical columns | Excluded categorical columns from the pipeline instead of imputing |
| Class imbalance in training data | Benchmarked four imbalance configurations; kept the baseline and optimised for macro F1 |
| Heavily right-skewed features and outliers | Compared StandardScaler, MinMaxScaler and RobustScaler; chose RobustScaler |
