# Mexico Real Estate: Data Wrangling & Exploratory Analysis

An end-to-end data cleaning and exploratory data analysis (EDA) project on Mexican property listings. The notebook takes three messy datasets with different formats, cleans and standardizes them, combines them into one dataset, and explores what drives property prices.

## Project Overview

The property data comes as three separate CSV files, each structured differently (prices in different currencies and formats, location stored in different ways). The goal is to:

1. Clean each dataset individually
2. Standardize them into a single common structure
3. Explore the combined data visually to understand price patterns

## Datasets

| File | Key differences |
|------|-----------------|
| `mexico-real-estate-1.csv` | Prices stored as text with `$` and `,` symbols |
| `mexico-real-estate-2.csv` | Prices given in Mexican pesos (`price_mxn`) |
| `mexico-real-estate-3.csv` | Coordinates stored as a single `lat-lon` string; state buried inside `place_with_parent_names` |

After cleaning, all three share the same columns, including `price_usd`, `area_m2`, `property_type`, `lat`, `lon` and `state`.

## What I Did

### 1. Data Cleaning
- Inspected each dataset with `.head()`, `.shape`, `.info()`, `.dtypes` and `.isnull().sum()`
- Dropped rows with missing values using reusable helper functions
- Removed `$` and `,` characters from `price_usd` and converted it to a float
- Converted `price_mxn` to `price_usd` (assuming an exchange rate of 19 MXN per 1 USD) and dropped the peso column
- Split the `lat-lon` string into separate numeric `lat` and `lon` columns
- Extracted the `state` from `place_with_parent_names`
- Used method chaining (`.assign()`, `.drop()`) for a cleaner workflow

### 2. Combining the Data
- Verified that all three DataFrames had identical column sets
- Merged them into one DataFrame with `pd.concat()`
- Generated summary statistics for `price_usd` and `area_m2`

### 3. Visualization & Analysis
- **Histograms** of property prices and property sizes to see how the data is distributed
- **Box plots** comparing prices across property types
- **Box plots** comparing prices across the three states with the most listings
- **Scatter plots** of area vs. price, before and after outlier removal
- **Regression plot** (`seaborn.regplot`) showing the trend between area and price

### 4. Outlier Handling
Extreme values squeezed most of the data into one corner of the scatter plot. I used quantile-based filtering (removing the lowest 5% and highest 10% of prices, plus unusually large areas) instead of an arbitrary fixed cutoff. This made the underlying relationship much clearer.

## Key Finding

There is a **positive relationship between property area and price**: as property size increases, price tends to increase.

## Tools & Libraries

- Python
- pandas
- matplotlib
- seaborn
- Jupyter Notebook



## Repository Structure

```
├── Wqu_First_project.ipynb        # Main analysis notebook
├── mexico-real-estate-1.csv       # Dataset 1
├── mexico-real-estate-2.csv       # Dataset 2
├── mexico-real-estate-3.csv       # Dataset 3
└── README.md
`

## Author

**Abdulsabur**
[]
