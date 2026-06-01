# data-analysis-tool

A powerful Python toolkit for **data preprocessing, cleaning, feature engineering, and interactive visualization** designed specifically for **Google Colab workflows**.
The package streamlines common data science operations including missing value treatment, outlier detection, normalization, categorical encoding, and statistical association analysis.

---

## Features

### Intelligent Data Loading

* Supports **Google Colab local file uploads**.
* Automatically loads CSV datasets using pandas.
* Detects and converts common invalid entries:

  * `'?'`
  * `'N/A'`
  * `'NULL'`
  * blank strings
* Performs automatic numeric type inference when conversion is valid.

### Comprehensive Dataset Inspection

Quickly analyze dataset structure with:

* Row count
* Column count
* First 20 records preview
* Numerical column detection
* Categorical column detection

### Automated Data Cleaning

#### Missing Value Handling

Supports multiple imputation strategies:

* Mean
* Median
* Mode
* Constant replacement

#### Duplicate Removal

* Detect and remove exact duplicate rows.
* Reports number of removed duplicates.

#### Outlier Management

Uses **Interquartile Range (IQR) detection**:

* Q1
* Q3
* IQR calculation
* Lower and Upper bounds

Supports:

* Outlier flagging
* Optional outlier removal

#### Dataset Pruning

Interactive deletion support for:

* Specific rows
* Specific columns

---

### Feature Engineering & Normalization

#### Numeric Data Scaling

Supports:

* MinMax Scaling
* Standard Scaling (Z-score)
* Robust Scaling

#### Categorical Encoding

Supports:

* One-Hot Encoding
* Ordinal Encoding
* Uniform 0–1 Encoding

Generate normalized numeric and categorical datasets ready for Machine Learning pipelines.

---

### Interactive Plotly Visualizations

#### Numerical Distribution Visualization

Automatic **3-panel exploratory plots** containing:

1. Horizontal Violin / Box Plot
2. Scatter Plot (Index vs Value)
3. Histogram

#### Smart Relationship Plotting

Automatically selects visualization type:

| Variable Types            | Plot                    |
| ------------------------- | ----------------------- |
| Numeric – Numeric         | Scatter + OLS Trendline |
| Categorical – Numeric     | Box Plot                |
| Categorical – Categorical | Grouped Bar Chart       |

#### Frequency Visualization

Categorical plots include:

* Raw frequency counts
* Percentage labels

---

### Advanced Statistical Association Analysis

Unified association mapping across all variable types.

#### Numeric – Numeric

* Pearson Correlation

#### Categorical – Categorical

* Cramér’s V Association

#### Numeric – Categorical

* Point-Biserial Correlation
* Eta Correlation (ANOVA-based)

Results are visualized using **interactive Plotly heatmaps**.

---

## Installation

### Standard Installation

```bash
pip install "git+https://github.com/yourusername/data-analysis-tool.git"
```

### Install with Plotting Support

```bash
pip install data-analysis-tool[plotting]
```

---

## Quick Start (Google Colab)

### 1. Data Upload & Cleaning

```python
from data_analysis import DataInspector

inspector = DataInspector()

# Upload CSV file
inspector.upload_data()

# Handle missing values
inspector.handle_missing_values(strategy='mean')

# Remove duplicates
inspector.remove_duplicates()
```

---

### 2. Dataset Inspection

```python
inspector.data_summary()
```

---

### 3. Outlier Detection

```python
# Detect outliers
inspector.handle_outliers('Salary')

# Remove outliers
inspector.handle_outliers('Salary', remove=True)
```

---

### 4. Data Normalization & Encoding

```python
# Normalize numeric data
numeric_df = inspector.extract_normalized_numeric_data(
    method='standard'
)

# Encode categorical data
categorical_df = inspector.extract_normalized_categorical_data(
    method='onehot'
)

# Merge processed datasets
final_df = inspector.merge_data(
    numeric_df,
    categorical_df
)
```

---

### 5. Interactive Visualization

#### Numerical Exploration

```python
inspector.plot_numerical(['Age', 'Income'])
```

#### Relationship Analysis

```python
inspector.plot_relationship(
    x='Department',
    y='Salary'
)
```

#### Association Heatmap

```python
inspector.plot_all_associations_heatmap()
```

---

### 6. PlottingMethods Utilities

Direct plotting helpers return Plotly HTML output.

```python
from data_analysis import PlottingMethods

plotter = PlottingMethods()
```

#### Bar Plot

```python
result = plotter.bar_plot(
    x='Department',
    y='Salary'
)
```

#### Pie Plot

```python
result = plotter.pie_plot(
    names='Category',
    values='Revenue'
)
```

#### Histogram Plot

```python
result = plotter.histogram_plot(
    x='Age'
)
```

---

## Project Structure

```plaintext
data-analysis-tool/
├── data_analysis/
│   ├── __init__.py
│   └── core.py
├── pyproject.toml
└── README.md
```

---

## Package Design

### DataInspector

Responsible for:

* Data ingestion
* Cleaning
* Missing value handling
* Outlier detection
* Scaling
* Encoding
* Dataset merging
* Statistical visualization

### PlottingMethods

Provides reusable modular plotting utilities:

* Bar plots
* Pie charts
* Histograms

All figures are generated using **Plotly interactive visualization**.

---

## Authors

Your Name — [your.email@example.com](mailto:your.email@example.com)

---

## License

This project is licensed under the **MIT License**.

