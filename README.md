# Insurance Data Analysis

This project analyzes a health insurance dataset to uncover key factors influencing insurance charges. The analysis includes data cleaning, feature engineering, exploratory data analysis, correlation and statistical testing, and data preprocessing for modeling.

## Files Included

- **Insurance-1.ipynb**: Jupyter notebook containing all code and analysis steps.
- **insurance.csv**: The dataset used for analysis (1338 rows × 7 columns).

---

## Dataset Overview

The dataset (`insurance.csv`) contains the following columns:

| Column    | Description                             |
|-----------|-----------------------------------------|
| age       | Age of the primary beneficiary          |
| sex       | Gender (male, female)                   |
| bmi       | Body mass index                         |
| children  | Number of children/dependents covered   |
| smoker    | Smoker status (yes, no)                 |
| region    | Residential area in the US              |
| charges   | Individual medical costs billed by insurer|

---

## Analysis Steps

### 1. **Importing Libraries**

```
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import warnings
warnings.filterwarnings('ignore')
from sklearn.preprocessing import StandardScaler
from scipy.stats import pearsonr, chi2_contingency
```

### 2. **Loading the Data**

```
df = pd.read_csv('insurance.csv')
```

### 3. **Initial Exploration**

- **View first few rows and summary statistics:**

```
df.head()
df.describe()
```

- **Sample Output:**

| age | sex    | bmi    | children | smoker | region     | charges     |
|-----|--------|--------|----------|--------|------------|-------------|
| 19  | female | 27.900 | 0        | yes    | southwest  | 16884.92400 |
| 18  | male   | 33.770 | 1        | no     | southeast  | 1725.55230  |
| ... | ...    | ...    | ...      | ...    | ...        | ...         |

---

### 4. **Feature Engineering**

- **Convert categorical variables to numeric:**
    - `sex` → `is_female` (1 if female, 0 if male)
    - `smoker` → `is_smoker` (1 if yes, 0 if no)

```
df['is_female'] = (df['sex'] == 'female').astype(int)
df['is_smoker'] = (df['smoker'] == 'yes').astype(int)
```

- **One-hot encode region:**

```
df = pd.get_dummies(df, columns=['region'], drop_first=True)
```

- **Create BMI categories:**

```
def bmi_category(bmi):
    if bmi  df['charges'].median()))
# Repeat for other categorical features
```

- **Significant predictors (p < 0.05):**
    - is_smoker
    - region_southeast
    - is_female
    - bmi_category_Obese

---

### 7. **Data Preprocessing**

- **Standardize numerical features:**

```
scaler = StandardScaler()
df[['age', 'bmi', 'children']] = scaler.fit_transform(df[['age', 'bmi', 'children']])
```

- **Final processed DataFrame (sample):**

| age      | is_female | bmi      | children | is_smoker | charges | region_southeast | region_southwest | bmi_category_Normal | bmi_category_Overweight | bmi_category_Obese |
|----------|-----------|----------|----------|-----------|---------|------------------|------------------|--------------------|------------------------|--------------------|
| -1.44... | 1         | -0.51... | -0.90... | 1         | 16884   | 0                | 1                | 0                  | 1                      | 0                  |
| ...      | ...       | ...      | ...      | ...       | ...     | ...              | ...              | ...                | ...                    | ...                |

---

## Key Insights

- **Smoking status** is by far the most important factor affecting insurance charges.
- **Age** and **obesity** also have a significant positive impact.
- **Sex** and **region** (especially southeast) are relevant but less influential.
- All significant features are encoded and standardized for modeling.

---

## How to Use

1. **Open `Insurance-1.ipynb` in Jupyter Notebook.**
2. **Run all cells sequentially.**
3. **Review the outputs and visualizations for insights.**
4. **Use the final processed DataFrame for further modeling or analysis.**

---

## Requirements

- Python 3.x
- pandas, numpy, seaborn, matplotlib, scikit-learn, scipy

---
