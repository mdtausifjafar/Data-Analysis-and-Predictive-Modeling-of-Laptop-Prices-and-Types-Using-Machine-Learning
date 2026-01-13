# Dataset Information

## Overview

This directory contains the dataset used for laptop price prediction and type classification analysis.

## Files

### `laptop_prices.csv`

The main dataset containing laptop specifications and pricing information.

**Dataset Statistics:**

- **Total Records**: 1,275 laptops
- **Features**: 23 columns
- **Target Variables**:
  - Price_euros (for regression)
  - TypeName (for classification)

## Data Dictionary

| Column               | Data Type | Description                      | Example Values                                  |
| -------------------- | --------- | -------------------------------- | ----------------------------------------------- |
| Company              | Object    | Laptop manufacturer              | Apple, Dell, HP, Lenovo, Asus                   |
| Product              | Object    | Product name/model               | MacBook Pro, ThinkPad, Pavilion                 |
| TypeName             | Object    | Laptop category                  | Ultrabook, Notebook, Gaming, 2 in 1 Convertible |
| Inches               | Float     | Screen size in inches            | 13.3, 15.6, 17.3                                |
| Ram                  | Integer   | RAM capacity in GB               | 4, 8, 16, 32                                    |
| OS                   | Object    | Operating system                 | Windows 10, macOS, Linux                        |
| Weight               | Float     | Laptop weight in kg              | 1.2, 2.1, 2.8                                   |
| Price_euros          | Float     | Price in Euros                   | 400.0, 1500.0, 3000.0                           |
| Screen               | Object    | Screen type                      | Standard, Full HD, 4K                           |
| ScreenW              | Integer   | Screen width in pixels           | 1366, 1920, 3840                                |
| ScreenH              | Integer   | Screen height in pixels          | 768, 1080, 2160                                 |
| Touchscreen          | Object    | Touchscreen capability           | Yes, No                                         |
| IPSpanel             | Object    | IPS panel availability           | Yes, No                                         |
| RetinaDisplay        | Object    | Retina display feature           | Yes, No                                         |
| CPU_company          | Object    | CPU manufacturer                 | Intel, AMD                                      |
| CPU_freq             | Float     | CPU frequency in GHz             | 1.8, 2.5, 3.2                                   |
| CPU_model            | Object    | CPU model name                   | Core i5, Core i7, Ryzen 5                       |
| PrimaryStorage       | Integer   | Primary storage capacity in GB   | 128, 256, 512, 1000                             |
| SecondaryStorage     | Integer   | Secondary storage capacity in GB | 0, 500, 1000                                    |
| PrimaryStorageType   | Object    | Primary storage type             | SSD, HDD, Flash Storage                         |
| SecondaryStorageType | Object    | Secondary storage type           | SSD, HDD, No                                    |
| GPU_company          | Object    | GPU manufacturer                 | Intel, Nvidia, AMD                              |
| GPU_model            | Object    | GPU model name                   | GeForce GTX, Radeon, Iris                       |

## Derived Features (Post-Engineering)

The following features are extracted and engineered during the analysis:

- **PPI (Pixels Per Inch)**: Calculated from Screen Resolution and Size.
- **Touchscreen**: Binary flag (1/0) extracted from Screen description.
- **IPS**: Binary flag (1/0) for IPS panel presence.
- **CPU_Name**: Simplified CPU model grouping (e.g., "Intel Core i7").
- **CPU_Brand**: Brand extraction (Intel, AMD).
- **SSD/HDD**: Binary flags indicating storage type presence.

## Data Quality

### Missing Values (Before Preprocessing)

- **TypeName**: 12 missing values
- **Inches**: 12 missing values
- **Touchscreen**: 589 missing values
- **CPU_model**: 5 missing values

### Data Preprocessing Applied

1. **Missing Value Handling**:

   - Numeric columns: Filled with median values
   - Categorical columns: Filled with mode values

2. **Advanced Feature Engineering**:

   - Extraction of screen technologies (IPS, Touchscreen)
   - Resolution parsing to calculate PPI
   - Storage type decomposition (SSD/HDD)
   - CPU/GPU brand simplification
   - NLP keyword extraction for Product Category (Gaming, Business, Premium)

3. **Data Cleaning**:
   - Removed extra spaces from column names
   - Handled inconsistent data formats

## Usage Notes

1. **Price Prediction**: Use engineered features like PPI, RAM, CPU/GPU brands for higher accuracy (>0.88 R²).
2. **Type Classification**: Hardware specs combined with form factor indicators (Touchscreen, Weight) predict type with >82% accuracy.

## Data Source

This dataset contains laptop specifications and pricing information collected for machine learning analysis. The data represents a comprehensive sample of laptops available in the market with various configurations and price points.

## Recommended Preprocessing Steps

1. **For Regression (Price Prediction)**:

   ```python
   features = ['Company', 'TypeName', 'Inches', 'Ram', 'Weight',
               'Touchscreen', 'IPS', 'PPI', 'CPU_Name', 'CPU_freq', 'CPU_Brand',
               'PrimaryStorage', 'SecondaryStorage', 'SSD', 'HDD',
               'GPU_company', 'OS']
   target = 'Price_euros'
   ```

2. **For Classification (Type Prediction)**:

   ```python
   features = ['Ram', 'Weight', 'Inches', 'Touchscreen', 'IPS', 'PPI',
               'CPU_Name', 'CPU_Brand', 'PrimaryStorage', 'GPU_company']
   target = 'TypeName'
   ```

3. **Standard Preprocessing Pipeline**:
   - Impute missing values (Median/Mode)
   - One-Hot Encode categorical variables
   - Scale numeric features
   - Use Ensemble Models (VotingRegressor/VotingClassifier) for best results

## Data Insights

- **Price Range**: €217 - €6,099 (wide variation across brands and specifications)
- **Popular Brands**: Dell, Lenovo, and HP dominate the market
- **Common Configurations**: 8GB RAM, 15.6" screen, Intel processors
- **Storage Trends**: SSD becoming more common for primary storage
- **GPU Distribution**: Mix of integrated and dedicated graphics cards
