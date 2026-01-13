# Data Analysis and Predictive Modeling of Laptop Prices and Types

## Project Overview

This project performs an in-depth analysis of the laptop market to develop high-performance predictive models for price estimation and product categorization. The primary goal is to move beyond basic hardware specifications and uncover the underlying drivers of market value, such as brand equity, display technology, and design language.

By applying advanced **Natural Language Processing (NLP)** to unstructured text data, rigorous **Feature Engineering**, and **Ensemble Learning**, the project features a regression model that explains over **90% of price variance**.

## Key Objectives & Experimental Findings

### 1. Exploratory Data Analysis (EDA)

A dataset of 1,275 laptops was examined to understand the impact of various technical segments. Key observations included:

- **Skewed Price Distribution**: `Price_euros` was found to be heavily right-skewed. To address this, a **Log-Transformation** was applied, which significantly stabilized variance and reduced error in high-end price brackets.
- **Physical vs. Value Correlations**:
  - **RAM** showed the strongest correlation with price (**0.74**).
  - **Weight** exhibited a non-linear relationship: both ultra-light business devices and heavy gaming machines command premium prices.
- **Data Integrity**: Missing values for `TypeName` and `Inches` were handled using median/mode imputation to ensure a clean baseline for modeling.

### 2. Strategic Feature Engineering with NLP

Raw data columns like `Product` and `ScreenResolution` were leveraged to engineer new features that capture hidden market dimensions:

- **Product Categorization (NLP)**: NLP techniques were used to scan model names for high-value keywords. By identifying brands like "Alienware," "ThinkPad," or "Zenbook," a `Product_Category` feature was created to segment the market into **Gaming**, **Business**, and **Premium** tiers.
- **Display Sharpness (PPI)**: Instead of relying solely on resolution, **Pixels Per Inch (PPI)** was calculated by combining `ScreenW`, `ScreenH`, and `Inches` into a single, highly predictive metric of visual quality.
- **Component Decomposition**: The `CPU_model` was parsed to extract specific brands (Intel/AMD) and frequencies, and storage configurations were separated into dedicated `SSD` and `HDD` binary indicators.

### 3. Predictive Modeling Strategy

To achieve maximum accuracy, the project implements **Voting Ensembles** to combine the diverse strengths of several algorithms:

- **Price Regression**: A **Voting Regressor** consisting of **Random Forest**, **Gradient Boosting**, and **XGBoost** was trained.
  - _Optimization_: By training on `log1p(Price)` and evaluating with `expm1`, an **R² score of 0.9024** was reached.
- **Type Classification**: A similar **Voting Classifier** predicts the laptop category (e.g., Ultrabook vs. Notebook), achieving an accuracy of **82%**.

## Final Performance Summary

| Task                          | Model Architecture                          | Metric             | Score            |
| :---------------------------- | :------------------------------------------ | :----------------- | :--------------- |
| **Price Prediction**    | **Voting Regressor** (RF + GB + XGB)  | **R²**      | **0.9024** |
| **Type Classification** | **Voting Classifier** (RF + GB + XGB) | **Accuracy** | **0.82**   |

> [!NOTE]
> The analysis shows that the engineered **Product_Category** (from NLP) and **Weight** are among the most critical features in determining both price and intended laptop use.

### Understanding Classification Accuracy (82%)

While the price prediction model is highly precise, the classification accuracy of **82%** reflects the inherent ambiguity in the laptop market's product segmentation. Key reasons for this include:

- **Feature Overlap**: Modern "Notebooks" and "Ultrabooks" often share nearly identical hardware specifications (RAM, CPU, Storage). Their primary difference is often chassis thickness or weight, which can vary by only a few millimeters or grams, making distinct categorization challenging for data-driven models.
- **Class Imbalance**: The dataset is numerically dominated by the "Notebook" category. This natural market distribution makes it more difficult for the model to achieve 100% precision on rarer categories like "Workstations" or "2 in 1 Convertibles," which may share specs with higher-volume models.

## Technologies Utilized

- **Core Engine**: Python 3.x
- **Analysis**: `pandas`, `numpy`
- **Visualization**: `matplotlib`, `seaborn`
- **Machine Learning**: `scikit-learn`, `xgboost`

## How to Explore This Work

1. **Install Requirements**:
   ```bash
   pip install -r requirements.txt
   ```
2. **Launch the Core Analysis**:
   Explore the logic and visualizations inside the Jupyter Notebook:
   ```bash
   jupyter notebook "Data Analysis and Predictive Modeling of Laptop Prices and Types Using Machine Learning.ipynb"
   ```

## Author

**Md. Tausif Jafar**
