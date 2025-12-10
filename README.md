# Impact of COVID-19 on the Economy: Home Prices and Household Earnings  

## Contributors
- **Alevtyna Rypninska** – Data Analysis & Visualization Lead  
- **Seongwook Min** – Data Integration & Cleaning Lead  

---

## Project Summary

This project examines how the COVID-19 pandemic reshaped housing affordability by analyzing two key indicators: inflation-adjusted residential home prices in Connecticut and real median household income in the United States. Housing markets experienced dramatic volatility during the pandemic, and policymakers, researchers, and households continue to debate whether these shifts reflect genuine economic resilience or growing structural inequality. Our project aims to provide empirical insight into this question by integrating multiple datasets, performing systematic data cleaning, and generating reproducible year-level indicators for the period 2015–2023.

The motivation for this work centers on a broader economic concern: while home prices surged nationwide during the pandemic, income growth did not appear to keep pace. Connecticut provides a strong case study because its real estate market reflects both regional economic pressures and national housing dynamics. By comparing pre-pandemic (2015–2019) and pandemic-era (2020–2023) trends, we aim to quantify the magnitude of these changes and assess whether rising home values aligned with or diverged from changes in household economic well-being.

Our analysis is guided by four research questions:

1. **How did Connecticut home prices change during the COVID-19 period (2019–2023) compared to the pre-pandemic years (2015–2019)?**  
   This question allows us to determine whether the widely reported housing boom is reflected in inflation-adjusted, transaction-level data.

2. **How did real median household income in the United States evolve across the same period?**  
   Because household income strongly shapes housing demand and affordability, understanding its trajectory is essential for interpreting price dynamics.

3. **What relationship exists between changes in income and changes in home prices during and after the pandemic?**  
   By computing correlations and estimating a simple regression model, we explore whether income movements help explain the surge in real estate prices or whether other forces dominated the market.

4. **What broader conclusions can we draw about post-pandemic affordability and economic resilience?**  
   This question synthesizes the quantitative patterns to evaluate whether the housing market reflected a healthy economic recovery or signaled an erosion of affordability.

To address these questions, we curated two datasets: the Connecticut Real Estate Sales dataset from Data.gov and the FRED series for median household income (MEHOINUSA672N). After extensive data profiling, we applied filtering rules to retain only residential property transactions, removed rows with missing classification fields, standardized column names and data types, harmonized dates, and corrected for inflation using annual CPI-U values. We then integrated the datasets at the year level and constructed a final analytical table containing mean inflation-adjusted home prices, mean nominal sale prices, and median household income for each year from 2015 through 2023.

Our findings indicate that while income increased modestly over the period, real home prices rose sharply during the pandemic, suggesting a widening gap between housing costs and household purchasing power. A moderate positive correlation exists between income and home prices, but income changes explain only a limited portion of the pandemic price surge. These high-level results set the stage for deeper discussion in the Findings section of the report.

Overall, this project demonstrates that systematic, transparent data curation enables meaningful economic analysis. By transforming raw, inconsistent datasets into a reproducible workflow and integrating them into a unified analytical framework, we provide evidence-based insight into one of the most pressing questions of the post-pandemic economy: whether households have become more financially resilient—or whether housing affordability has deteriorated despite economic recovery efforts.

## Data Profile

This project integrates two primary datasets: (1) the Connecticut Real Estate Sales dataset from Data.gov, and (2) the U.S. Median Household Income series (MEHOINUSA672N) from the Federal Reserve Bank of St. Louis (FRED). Together, these datasets enable longitudinal analysis of housing affordability by combining transaction-level real estate records with national income indicators. This section describes each dataset in detail, including structure, variables, collection methods, limitations, legal and ethical constraints, and the transformations required to prepare them for analysis.

### 1. Connecticut Real Estate Sales (2001–2023)

**Source:** Connecticut Office of Policy and Management, publicly available through Data.gov  
**URL:** https://catalog.data.gov/dataset/real-estate-sales-2001-2018  
**Format used:** CSV extracted for the extended 2001–2023 dataset  
**Size:** ∼580,000 rows originally; ∼462,000 rows after filtering to 2015–2023; ∼442,000 after cleaning missing classification fields.

This dataset provides detailed information on property sales across Connecticut. Each row corresponds to a single transaction and includes a mix of numeric, categorical, and geographic variables. The key variables relevant to our project include:

- **Serial Number**: Unique transaction identifier  
- **List Year (renamed to Year)**: Year the property was listed  
- **Date Recorded**: Official date the transaction was captured  
- **Town**: Municipality where the property is located  
- **Address**: Street-level property location  
- **Assessed Value**: Value assigned for tax purposes  
- **Sale Amount**: Actual sale price  
- **Sales Ratio**: Ratio of assessed value to sale price  
- **Property Type**: Classification such as Residential, Commercial, Condo, etc.  
- **Residential Type**: Further granularity (Single Family, Two Family, Condo, etc.)  
- Additional text fields (Assessor Remarks, OPM Remarks) and geographic data (POINT location) were not used in the final analysis.

The dataset required substantial cleaning to ensure suitability for trend analysis. Several columns contain mixed types, including strings where numeric values were expected. Missing values were most prevalent in the **Property Type** and **Residential Type** columns. Because the project focuses exclusively on residential home prices, we applied a rule to drop rows where both fields were missing. This step removed ∼20,500 transactions, representing non-residential or incomplete records.

Dates were standardized using `pd.to_datetime` to correct inconsistent formatting and convert the dataset into a sortable temporal structure. Records were then filtered to include only the years 2015–2023, aligning with the pre-pandemic versus COVID-era comparison central to our research questions. Finally, we merged the dataset with an externally constructed CPI table to adjust sale prices into 2023 U.S. dollars, enabling valid comparisons across years.

### 2. U.S. Median Household Income (MEHOINUSA672N)

**Source:** Federal Reserve Bank of St. Louis (FRED)  
**Series ID:** MEHOINUSA672N  
**URL:** https://fred.stlouisfed.org/series/MEHOINUSA672N  
**Format used:** Excel file (Annual frequency)

This dataset provides yearly estimates of median household income in the United States adjusted for inflation. The dataset spans multiple decades, but we extracted only the years 2015–2023 to match the temporal scope of the Connecticut housing data.

The fields included were:

- **observation_date**: Year of the estimate  
- **mehoinusa672n**: Median household income in chained 2023 dollars  

To ensure compatibility with our integrated dataset, we applied the following transformations:

- Standardized column names to lowercase, underscore-separated format  
- Converted date fields to datetime objects and extracted the **Year**  
- Merged the income data with the real estate dataset using a left join on Year  

This produced a unified table where each real estate transaction includes the median household income for that year, enabling direct comparison and correlation analysis.

### Ethical and Legal Constraints

Both datasets are **public and open-license**, but ethical considerations still apply:

**1. Privacy and Identifiability**  
The real estate data includes street addresses and geographic coordinates, but the dataset is not considered personally identifying because ownership information is not provided. All transactions are already public records in Connecticut. However, our project does not publish or analyze data at the address level. All results are aggregated to the year level, minimizing any privacy concerns.

**2. Terms of Use and Attribution**  
- The Connecticut dataset is licensed for open public use but requires attribution to the Office of Policy and Management.  
- FRED data is free to use with attribution, and the README will include correct citations.  

**3. No redistribution of restricted data**  
Both datasets allow redistribution, but to maintain reproducibility best practices, the project provides instructions for programmatic download and hosts processed outputs (not raw files) in a Box folder for TAs.

### Summary of Data Integration

The final curated dataset is a year-level table containing:

- Mean raw sale price  
- Mean inflation-adjusted sale price (2023 USD)  
- Median household income  
- Year indicator  

This dataset reflects multiple cleaning, validation, and merging steps and serves as the foundation for all subsequent analysis presented in the Findings section.

Overall, the two datasets complement each other and collectively support a comprehensive exploration of housing affordability trends before, during, and after the COVID-19 pandemic.

## Data Quality

Ensuring the quality, consistency, and reliability of the datasets used in this project was a critical component of preparing the integrated analytical dataset. Because the Connecticut real estate dataset is large, heterogeneous, and collected over many years, it contains numerous quality challenges ranging from missing values to mixed data types and inconsistent formatting. Our goal was not only to clean the data but also to document the underlying issues and justify the decisions made in the quality assessment process. This section outlines the data quality problems identified, the steps taken to address them, and the residual limitations that users of the dataset should be aware of when interpreting the results.

### 1. Completeness and Missing Data

One of the most prominent quality issues in the Connecticut real estate dataset involved missing values in key classification variables. In particular:

- **Property Type**
- **Residential Type**

These fields are essential for distinguishing between residential and non-residential properties. Since our research questions focus specifically on residential housing affordability, complete classification is important. Upon inspection, 41,212 out of ~462,000 records in the 2015–2023 subset had at least one missing value, and 20,525 records were missing *both* Property Type and Residential Type.

Because rows missing both values could not reliably be categorized, we removed them (`dropna` with `subset=["Property Type", "Residential Type"]` and `how="all"`). This step ensured that the resulting dataset contained only well-defined residential property sales or partially incomplete but still classifiable records.

Missing values in other fields—such as address records, assessor remarks, and OPM remarks—were considered non-essential for our analysis and therefore did not require removal. The Date field occasionally failed to parse due to formatting inconsistencies but was handled by forcing conversion with `errors="coerce"`, after which null dates were evaluated for relevance. Since year-level grouping was based on the List Year variable, missing Date values did not obstruct analysis.

The income dataset from FRED had no missing values after filtering to the years of interest (2015–2023), ensuring complete temporal alignment with the real estate dataset.

### 2. Accuracy and Validity

To evaluate accuracy, we examined whether the numeric fields adhered to expected ranges:

- **Sale Amount** values generally fell within plausible residential price ranges for Connecticut.  
- **Assessed Value** and **Sales Ratio** fields were internally consistent, though not used for final modeling.  
- **Year** (renamed from “List Year”) ranged correctly from 2015–2023 after filtering.

We performed additional checks:

- Outliers were inspected visually and statistically; extremely high values corresponded to legitimate high-value residential properties rather than data entry errors.
- The income series presented no anomalies, as FRED performs internal validation before publication.

Thus, the datasets were deemed factually consistent and valid for analytical use.

### 3. Consistency and Standardization

Several variables required standardization to ensure consistency:

- **Date Recorded** was originally stored in inconsistent mm/dd/yyyy string formats. We converted all records using `pd.to_datetime`.
- **observation_date** in the income dataset was standardized in the same way and converted to a Year variable for merging.
- Column names were normalized (lowercase, underscores, removal of special characters) to ensure compatibility with automated processing and reproducibility scripts.

Cross-dataset consistency was also addressed. Since the real estate dataset contains one row per sale while the income dataset contains one row per year, the merge introduced income values at the individual-transaction level—but all income values per year were identical. This was expected and validated.

### 4. Integrity and Join Quality

The integrity of the merge between real estate and income data was assessed by checking:

- Whether all years in the filtered real estate dataset existed in the income dataset. They did (2015–2023).
- Whether any unexpected nulls appeared post-merge. None did for the income field.

We also validated that after cleaning and filtering:

- 442,354 records remained,
- All belonged to the correct temporal range,
- All retained valid sale amounts and year values.

The merge thus preserved referential integrity and ensured consistent year mapping.

### 5. Transformation Quality (Inflation Adjustment)

To compare prices meaningfully across years, we applied CPI-based inflation adjustments using a manually curated CPI dictionary:

price_2023 = raw_sale_price * (CPI_2023 / CPI_year)

Data quality considerations for this step included:

- Ensuring CPI values were accurate and correctly matched to the year.
- Confirming no sale records were missing CPI values.
- Verifying inflation-adjusted prices aligned with raw prices in expected ways (e.g., earlier-year sales increased more dramatically after adjustment).

Checks were performed at both the transaction and year-aggregated levels. The inflation adjustment passed all validation steps.

### 6. Aggregation Quality

All final analysis relied on a year-level dataset derived from the cleaned transaction-level dataset. To ensure aggregation quality:

- We computed mean nominal and inflation-adjusted home prices per year.
- We computed mean household income per year from the merged real estate-income dataset.
- We validated that means were consistent with raw distributions and showed no unexpected discontinuities.

The resulting table for 2015–2023 contained accurate and reproducible summaries.

### 7. Residual Limitations

Despite cleaning, several structural limitations remain:

- Missing data in classification fields required dropping some records, which may slightly bias results if omissions were not random.
- The dataset does not separate property types beyond broad residential categories (e.g., single-family vs. condo), limiting granularity.
- Income data reflects national estimates, not Connecticut-specific income trends.
- The dataset cannot account for unrecorded private sales or discrepancies in municipal record keeping.

Nevertheless, these limitations do not materially affect the year-level trends the project aims to study.

### Conclusion

The data quality assessment process ensured that the final dataset used for analysis is consistent, accurate, and reproducible. Despite necessary filtering and cleaning steps, the remaining data provides a reliable basis for studying the relationship between income trends and home prices before, during, and after the COVID-19 pandemic.

## Findings

Our analysis provides empirical answers to the four research questions guiding this project, using a curated dataset of Connecticut residential property sales (2015–2023) and national real median household income. By integrating these sources, adjusting prices for inflation, and constructing a year-level analytical dataset, we identify clear trends in home values, income growth, and affordability during the COVID-19 pandemic.

### 1. Connecticut Home Prices Increased Dramatically During the COVID-19 Period

Inflation-adjusted home prices in Connecticut increased sharply between the pre-pandemic period (2015–2019) and the COVID-era (2020–2023). The mean real price across 2015–2019 was:

- **$425,482 (2023 USD)**

During the pandemic, the mean surged to:

- **$609,405 (2023 USD)**

This represents a **43.2% increase**, even after correcting for inflation. Visualizations confirm that the largest jumps occurred in 2020 and 2021, coinciding with historically low mortgage rates, remote work adoption, and heightened relocation activity. The increase reflects substantial demand-side pressure, reduced inventory, and shifts in household behavior.

### 2. Median Household Income Increased Only Modestly

Real median household income followed a very different trajectory. The average income in the pre-pandemic period was:

- **$77,168**

Compared to **$81,260** during the pandemic period, a change of only:

- **5.3%**

Income declined in 2020 and 2021 due to labor market disruptions, then recovered in 2023, but overall growth remained minimal relative to housing prices. This divergence—rapid appreciation in home prices vs. stagnation in income—points to an expanding affordability gap.

### 3. Income and Home Prices Show Moderate Correlation but Weak Predictive Power

The correlation between year-level median household income and inflation-adjusted home prices from 2015–2023 is:

- **0.587**, indicating a moderate positive relationship.

However, a simple linear regression shows weak explanatory power:

- **Regression equation:**  
  *Price = 18.58 × Income – 960,292.71*

- **R² = 0.3447**

This means that **only ~34% of the variation in home prices** can be explained by income changes alone. During the pandemic, prices rose far more quickly than income, producing a widening disconnect. Non-income factors—including supply shortages, investor activity, pandemic mobility, and historically low interest rates—likely played much stronger roles in the observed price surge.

### 4. Broader Conclusions: Affordability Declined and Economic Inequality Increased

Synthesizing these results, the post-pandemic housing market appears to have diverged significantly from traditional income-based affordability patterns. Home prices increased by over 40% while incomes grew by just 5%, meaning that:

- Housing became substantially less affordable for first-time buyers.  
- Wealth inequality likely increased, as existing homeowners gained equity while new buyers faced higher barriers.  
- Real estate values during COVID-19 did not reflect improved household economic strength but rather structural pressures in the housing market.

These findings indicate that the pandemic period did not represent a uniform economic recovery; rather, it amplified disparities between asset-owning and non–asset-owning households. Despite strong housing market performance, the underlying income data suggest uneven financial resilience.

### Summary

The evidence shows a clear imbalance: home prices surged rapidly, incomes stagnated, and affordability declined. While income and home prices share a moderate long-term relationship, pandemic-era price dynamics were driven by forces outside household earnings. This mismatch offers a critical insight into the broader economic landscape of the post-COVID era—one marked by increased financial strain for prospective homeowners and heightened inequality in housing accessibility.

## Future Work

This project provided meaningful insights into the relationship between Connecticut residential home prices and U.S. median household income during the years surrounding the COVID-19 pandemic. While the analysis revealed a moderate long-run positive correlation between income and housing prices, the findings also made clear that income alone cannot account for the dramatic surge in inflation-adjusted home prices between 2020 and 2023. The linear regression model explained only about one-third of the variation in real home prices, indicating that a large share of housing market behavior was driven by factors not represented in our income variable. This key takeaway shapes several important directions for future research, broader methodological improvements, and lessons learned about studying housing markets.

### 1. Incorporating Additional Economic Variables

One of the most significant areas for future work involves expanding the set of explanatory variables. Housing markets are influenced by a complex combination of macroeconomic, demographic, and policy-driven forces. Among these, **interest rates** are especially crucial. During the early pandemic period, mortgage rates fell to historic lows, fundamentally altering borrowing conditions and increasing households’ purchasing power. Lower financing costs often allow buyers to afford higher prices, even when incomes remain stagnant. By adding mortgage rate data (e.g., the average 30-year fixed rate from Freddie Mac), future research could quantify how much of the price escalation was driven by favorable borrowing conditions rather than underlying economic growth.

Alongside interest rates, future models should also integrate measures of **inflation, wage growth distribution, and consumer sentiment**, which may influence housing demand. Forecast-oriented datasets—such as expectations of future home prices—could also help disentangle the behavioral dynamics that emerged during the pandemic.

### 2. Accounting for Housing Supply Dynamics

A second major direction for future work is analyzing the **supply side of the housing market**. Rising prices can be caused either by increased demand or by restricted supply—and in many cases, both. Connecticut has historically exhibited slow housing development due to zoning constraints, limited new construction, and an aging housing stock. COVID-19 further disrupted building activity through labor shortages, material delays, and supply-chain breakdowns.

Future analysis could incorporate:

- **Building permits (U.S. Census Building Permit Survey)**
- **Vacancy rates**
- **Annual housing inventory levels**
- **Time-on-market data**
- **Construction cost indices**

These variables would allow researchers to measure whether Connecticut’s price surge reflected structural constraints in supply rather than traditional economic growth.

### 3. Investigating Migration and Demographic Change

The pandemic altered migration patterns across the United States. Densely populated urban centers saw outflows, while suburban and rural areas experienced increases in demand as households sought more space and work-from-home flexibility. Given Connecticut’s proximity to major cities like New York and Boston, it is very likely that pandemic-era migration contributed significantly to increased housing pressure.

Future work should integrate:

- **IRS county-to-county migration flows**
- **Census Bureau’s ACS migration estimates**
- **Change-of-address data from USPS**

A richer demographic perspective would help determine whether population shifts played a meaningful role in housing demand, particularly in specific Connecticut counties or towns.

### 4. Improving Modeling Techniques

The simple linear regression used in this project served as an interpretable starting point but may not capture nonlinear or interactive effects that characterize real-world housing systems. Future modeling approaches could include:

- **Multiple linear regression with additional covariates**
- **Time-series analysis (e.g., ARIMA or structural break models)**
- **Panel data models if regional disaggregation becomes available**
- **Machine learning methods** such as random forests, gradient boosting, or neural networks

These approaches could identify more nuanced relationships, interactions between variables, and potentially more accurate predictive models. Housing markets often exhibit nonlinear dynamics—thresholds, tipping points, and delayed reactions—making advanced modeling techniques especially valuable.

### 5. Using Finer-Grained Temporal and Spatial Data

This project used annual data, which is appropriate for long-run comparisons but conceals short-term volatility. Housing markets often respond rapidly to policy changes, interest rate adjustments, or economic shocks. Future work should consider:

- **Monthly or quarterly data for both prices and income proxies**
- **Sub-state geographic breakdowns**, such as county-level or ZIP code-level property data
- **Comparisons across states** to contextualize Connecticut trends regionally

More granular analysis would allow a deeper understanding of when price spikes occurred, how quickly markets responded to shocks, and which communities experienced the greatest changes.

### 6. Event-Based and Mixed-Methods Analysis

Finally, future work could contextualize quantitative findings with **event-based timelines** or **qualitative approaches**. Events such as state lockdowns, federal stimulus checks, eviction moratoriums, the shift to remote work, and global supply-chain disruptions may have shaped housing market behavior in ways that purely numerical datasets cannot capture. Combining quantitative models with qualitative timeline analysis—or even interviews with real estate professionals—could produce a more complete narrative of the pandemic housing market.

### Summary

In summary, this project demonstrates that household income explains only a small portion of the dramatic growth in Connecticut housing prices during the COVID-19 period. Future research should broaden the analytical scope by integrating interest rates, supply constraints, migration patterns, and more complex statistical techniques. Expanding the dataset and refining the modeling framework would help identify which variables were most influential and develop a more comprehensive understanding of how pandemic-era dynamics reshaped housing affordability and economic resilience.


## Reproducing
This section explains how to fully reproduce our analysis from raw data acquisition through inflation adjustment, dataset integration, visualization, and statistical modeling. The workflow was executed in VSCode using a Jupyter Notebook.

---
### Step 0. Data Acquisition
Download the datasets from the website links given either in data profile or citations
Download the xlsx file from U.S. Median Household Income series (MEHOINUSA672N) from the Federal Reserve Bank of St. Louis (FRED)
Download the csv file from the Connecticut Real Estate Sales dataset from Data.gov

### Step 1. VSCode
We used **VSCode** with the **Jupyter Notebook extension**.  
Open the project notebook:
is477_project.ipynb
Run each cell sequentially.

### Step 2 — Imports

The following libraries are required to run the project:

```python
import pandas as pd
import numpy as np
import os
import openpyxl
import matplotlib.pyplot as plt
from sklearn.metrics import r2_score
from sklearn.linear_model import LinearRegression
```
If any dependencies are missing, install them using:
pip install pandas numpy openpyxl matplotlib scikit-learn

### Step 3 — Convert Excel and CSV Data into DataFrames

The function below loads an Excel file, standardizes its column names, and converts all columns to appropriate data types.  
We then use the function to load the FRED income dataset and `pandas.read_csv()` to load the Connecticut real estate dataset.

```python
# Function to convert an Excel file into a clean pandas DataFrame
def excel_to_df(excel_file: str, sheet_name: str = None) -> pd.DataFrame:
    df = pd.read_excel(excel_file, sheet_name=sheet_name)

    # Standardize column names
    df.columns = (
        df.columns
        .str.lower()
        .str.strip()
        .str.replace(" ", "_")
        .str.replace(r"[^0-9a-zA-Z_]", "", regex=True)
    )

    df = df.convert_dtypes()
    return df

# Convert FRED Excel file into a DataFrame
xl_df = excel_to_df("MEHOINUSA672N.xlsx", sheet_name="Annual")

# IMPORTANT: Replace the filename above with your own local file path if needed.

# Load Connecticut housing sales CSV
csv_df = pd.read_csv("Real_Estate_Sales_2001-2023_GL.csv", encoding="utf-8")
```

### Step 4. Cleaning
```python
#Changing the dates into the same format for both dataframes as well as renaming a few columns
csv_df["Date Recorded"] = pd.to_datetime(csv_df["Date Recorded"], format="%m/%d/%Y", errors="coerce")
xl_df["observation_date"] = pd.to_datetime(xl_df["observation_date"], errors="coerce")
xl_df["Year"] = xl_df["observation_date"].dt.year	
csv_df = csv_df.rename(columns={"List Year": "Year"})


#Merge the two datasets based of the year with left join
merged_df = csv_df.merge(
    xl_df[["Year", "mehoinusa672n"]],
    on="Year",
    how="left"
)

#Sorting out which columns are needed and not needed and then sorting by year
merged_df["Date"] = merged_df["Date Recorded"]
merged_df = merged_df.drop(columns=["Non Use Code", "Assessor Remarks", "OPM remarks", "Location", "Date Recorded"])
merged_df = merged_df.sort_values("Year")

#Since we are mostly focusing on pre an during covid, we will be focusing only on 2015 to 2023
filtered_df = merged_df[(merged_df["Year"] >= 2015) & (merged_df["Year"] <= 2023)]

#cleaning step and we dropped the missing values
Cleaned_Df = filtered_df.dropna(subset=["Property Type", "Residential Type"], how="all")
```

### Step 5. CPI Data and Inflation Adjustment

The following code creates a CPI lookup table, merges it into the cleaned dataset, and computes inflation-adjusted home prices in 2023 dollars.

```python
# CPI index values from 2015–2023
cpi_dict = {
    2015: 237.017,
    2016: 240.007,
    2017: 245.120,
    2018: 251.107,
    2019: 255.657,
    2020: 258.811,
    2021: 270.970,
    2022: 292.655,
    2023: 305.109
}

# Convert CPI dictionary into DataFrame
cpi_df = pd.DataFrame(list(cpi_dict.items()), columns=['year', 'cpi'])

# Merge CPI values into cleaned dataset
adj_df = Cleaned_Df.merge(cpi_df, left_on='Year', right_on='year', how='left')

# Inflation-adjust to 2023 dollars
cpi_2023 = cpi_dict[2023]
adj_df['price_2023'] = adj_df['Sale Amount'] * (cpi_2023 / adj_df['cpi'])

# Compute average inflation-adjusted price per year
mean_price_year = (
    adj_df.groupby('Year')['price_2023']
          .mean()
          .reset_index()
          .rename(columns={'price_2023': 'mean_residential_price_2023usd'})
)

# Merge the per-year mean back into the dataset
adj_df = adj_df.merge(mean_price_year, on='Year', how='left')

# Create final year-level summary dataset
final_year_df = (
    adj_df.groupby('Year')
          .agg({
              'price_2023': 'mean',            # inflation-adjusted home price
              'Sale Amount': 'mean',           # raw home price
              'mehoinusa672n': 'mean'          # median household income
          })
          .reset_index()
)

# Rename for clarity
final_year_df = final_year_df.rename(columns={
    'price_2023': 'mean_residential_price_2023usd',
    'Sale Amount': 'mean_raw_sale_amount',
    'mehoinusa672n': 'median_household_income'
})
```

### Step 6. Answer Research Questions / Analysis

**Research Question 1:** How did Connecticut home prices change during COVID (2019–2023) vs. pre-pandemic (2015–2019)?

```python
# Focus only on CT home prices
# Create two different dataframes based on pre- and during-COVID periods

df = final_year_df.copy()

pre = df[(df["Year"] >= 2015) & (df["Year"] <= 2019)]
during = df[(df["Year"] >= 2020) & (df["Year"] <= 2023)]

pre_mean = pre["mean_residential_price_2023usd"].mean()
during_mean = during["mean_residential_price_2023usd"].mean()

pct_change = ((during_mean - pre_mean) / pre_mean) * 100

print("Pre-pandemic mean CT home price (2015–2019):", pre_mean)
print("COVID-period mean CT home price (2020–2023):", during_mean)
print("Percent change:", pct_change, "%")
```
Pre-pandemic mean CT home price (2015–2019): 425481.53910530685  
COVID-period mean CT home price (2020–2023): 609405.3387548988  
Percent change: 43.22721028892177 %

```python
#Home prices Graph with covid line
import matplotlib.pyplot as plt
plt.figure(figsize=(10,5))
plt.plot(df["Year"], df["mean_residential_price_2023usd"], marker="o")
plt.axvline(2020, color="red", linestyle="--", label="COVID Begins")
plt.title("Connecticut Home Prices (Inflation-Adjusted to 2023 USD)")
plt.ylabel("Mean Price (2023 USD)")
plt.xlabel("Year")
plt.legend()
plt.grid()
plt.show()
```

<img width="876" height="470" alt="image" src="https://github.com/user-attachments/assets/c7e90321-ee99-4906-b7d2-d09561b114e4" />


Connecticut home prices experienced a substantial and sustained real increase during the COVID-19 years. This supports the idea that the pandemic fundamentally reshaped the housing market, with demand surges and limited inventory driving prices well above pre-pandemic levels. Affordability pressures likely intensified as price growth outpaced typical income gains.


## Research Question 2: How did real median household income change?
# Split into pre-pandemic (2015–2019) and COVID-era (2020–2023)
# Calculate means and percent changes


df = final_year_df.copy()


pre = df[(df["Year"] >= 2015) & (df["Year"] <= 2019)]
during = df[(df["Year"] >= 2020) & (df["Year"] <= 2023)]


pre_income = pre["median_household_income"].mean()
during_income = during["median_household_income"].mean()


income_pct_change = ((during_income - pre_income) / pre_income) * 100


print("Pre-pandemic mean median household income (2015–2019):", pre_income)
print("COVID-period mean median household income (2020–2023):", during_income)
print("Percent change:", income_pct_change, "%")
Pre-pandemic mean median household income (2015–2019): 77168.0
COVID-period mean median household income (2020–2023): 81260.0
Percent change: 5.3027161517727555 %

#Income Graph with covid line

plt.figure(figsize=(10,5))
plt.plot(df["Year"], df["median_household_income"], marker="o", color="green")
plt.axvline(2020, color="red", linestyle="--", label="COVID Begins")
plt.title("U.S. Real Median Household Income (Inflation-Adjusted)")
plt.xlabel("Year")
plt.ylabel("Median Household Income (USD)")
plt.grid()
plt.legend()
plt.show()


<img width="868" height="470" alt="image" src="https://github.com/user-attachments/assets/1e88ef56-8c4b-48c5-81d9-7bcdc3db08f1" />


Unlike home prices, which surged rapidly during the pandemic, real median household income showed only a small positive change across the COVID period. In fact:

Income peaked just before the pandemic (2019)

Declined in 2020–2022 due to labor market disruptions

Rebounded in 2023, but still grew only modestly overall

This suggests that while the housing market experienced extreme upward pressure, household earnings did not grow proportionally. The gap between housing costs and income likely intensified affordability challenges for many families during and after the pandemic.


## Research Question 3: What relationship exists between changes in income and changes in home prices during and after the pandemic?

# Correlation between household income and inflation-adjusted home prices
corr = df["median_household_income"].corr(df["mean_residential_price_2023usd"])
print("Correlation:", corr)
Correlation: 0.5871509255866934

According to correlation, income influences housing prices, but income alone cannot explain dramatic price shifts, especially the pandemic spike in 2020.

#Linear Regression: Income vs. Housing Price


X = df["median_household_income"].values.reshape(-1, 1)
y = df["mean_residential_price_2023usd"].values.reshape(-1, 1)


model = LinearRegression()
model.fit(X, y)


slope = model.coef_[0][0]
intercept = model.intercept_[0]
r2 = model.score(X, y)


print("Regression Equation: price = {:.2f} * income + {:.2f}".format(slope, intercept))
print("R-squared:", r2)
Regression Equation: price = 18.58 * income + -960292.71
R-squared: 0.34474620941731093


#Regression Model of income vs housing prices
#Generates prediction line, and each dot on the graph represents a year
#Use mean because that is the data we want to explain
#Use median because of its earning


x_range = np.linspace(X.min(), X.max(), 200).reshape(-1, 1)
y_pred = model.predict(x_range)


plt.figure(figsize=(8,6))
plt.scatter(X, y, color="purple", label="Actual Data", alpha=0.7)
plt.plot(x_range, y_pred, color="orange", linewidth=2.5, label="Regression Line")


plt.title("Linear Regression: Income vs. Home Prices", fontsize=14)
plt.xlabel("Median Household Income (USD)", fontsize=12)
plt.ylabel("Mean Residential Home Price (2023 USD)", fontsize=12)


plt.grid(True, alpha=0.3)
plt.legend()
plt.show()


<img width="725" height="552" alt="image" src="https://github.com/user-attachments/assets/226bb2e0-10b3-4170-b53e-ec761395b21b" />


#Slope = 18.579314981810274
#For every $1 increase in median household income, the mean residential price increases by ~$18.58


While income and home prices have a moderate long-term positive relationship, income does not account for the dramatic surge in housing prices during COVID-19.
The pandemic housing market was influenced primarily by non-income factors, leading to a widening affordability gap.

This disconnect reinforces the idea that rising home prices during COVID-19 did not reflect improved household economic conditions—but instead structural shifts in housing demand and supply.


## Research Question 4: What broader conclusions can we draw about post-pandemic affordability and economic resilience?

The combined trends in housing prices and household income reveal that the post-pandemic economy experienced a significant imbalance between property values and earnings. While home prices rose sharply during the COVID-19 period—far outpacing inflation—median household income grew only modestly. This widening gap indicates that housing affordability declined substantially, suggesting that rising property values did not reflect genuine improvements in household financial strength. Instead, the rapid escalation in home prices points to structural pressures in the housing market rather than broad-based economic recovery.

Overall, the evidence suggests that the post-pandemic period was characterized by increased economic inequality and a decline in affordability, as income growth failed to keep pace with the surging cost of homeownership. These findings highlight vulnerabilities in economic resilience, especially for households attempting to enter or remain in the housing market after the pandemic.





Milestone 4: Final Project Submission 

Title: Impact of COVID-19 on the Economy: Home Prices and Household Earnings

Contributors: Alevtyna Rypninska (ar83) & Seongwook Min (sm116)

Summary: [500-1000 words] Description of your project, motivation, research question(s), and any findings.

Data profile: [500-1000 words] Description of each dataset used including all ethical/legal constraints.

Data quality: [500-1000 words] Summary of the quality assessment and findings.

Findings: [~500 words] Description of any findings including numeric results and/or visualizations.

Future work: [~500-1000 words] Brief discussion of any lessons learned and potential future work.
This project helped give insight into the picture of the relationship between household income and Connecticut home prices during the years surrounding the COVID pandemic. While our analysis showed that income had a moderate, positive correlation with housing prices over the long run, it also became clear that income alone cannot account for the price surge between 2020 and 2023. A regression model with income as the only variable explained only about 1/3 of the adjusted home prices, leaving most of the housing market’s movement unexplained. This outcome suggests several other factors along with real world events could help explain this change.
Housing markets respond to many forces at once, and income, especially when capturing only one part of household economics. Future work should include variables that reflect the other aspects of housing. For example, interest rates, as interest rates reached historic lows during this period, making borrowing cheaper and enabling buyers to bid more aggressively. Incorporating monthly or quarterly data could help quantify how much of the price spike was made by changes in financing conditions.
Another important area that could be looked at in the future, involves housing supply. Prices can rise for two very different reasons: because demand increases, or because supply remains limited or both. Connecticut, like many other states, faced constraints on new construction long before the pandemic due to many zoning restrictions, aging housing stock, and slow rates of development. The pandemic also contributed to the ongoing problems by creating construction delays and supply-chain interruptions that further tightened supply. Future work could integrate datasets on building permits, vacancy rates, or total residential inventory to try and understand the supply side of constraints that contributed to price appreciation.
Migration could also be a potential angle to consider. During covid, densely populated cities would have many residents seeking more space and lower density living areas, while suburban and rural areas saw increases in housing demand. Connecticut may have been involved in these trends, especially given how close it is to New York. Incorporating migration data such as data from the Census Bureau could help determine whether population shifts played a significant role in bidding up home prices during the pandemic.
Another possible future work could be improving the analysis. A simple linear regression is useful for interpretation, but housing markets are complex and may follow nonlinear patterns. As such, using techniques such as multiple regression or even machine learning models like random forests could uncover better relationships between variables. These models may better capture how multiple factors income, interest rates, supply measures, and demographic change work together to shape the housing market.


Finally, future work could include event based analysis to contextualize the findings. Events such as statewide lockdowns, shifts to remote work, or any global events related to money or houses that may have influenced the housing market in a way that the data alone cannot capture. Maybe trying to combine quantitative and qualitative together would better explain the work.
In summary, the project demonstrated that income is only one piece of the explanation. Future research should integrate additional economic, demographic, and policy variables to develop a better explanation for the post pandemic housing prices. With greater data and more detailed modeling, it should be possible to understand what variables were directly and greatly important to the pricing changes due to covid. 





Reproducing: Sequence of steps required for someone else to reproduce your results.

References: Formatted citations for any papers, datasets, or software used in your project.

For the real-estate dataset: 
  Office of Policy and Management. (2025, September 14). Real Estate Sales 2001-2023 GL [Dataset]. Data.gov. https://catalog.data.gov/dataset/real-estate-sales-2001-2018 
  
For the median household income data: 
  U.S. Census Bureau. (n.d.). Real Median Household Income in the United States [MEHOINUSA672N]. FRED – Federal Reserve Bank of St. Louis. https://fred.stlouisfed.org/series/MEHOINUSA672N

Visual Studio Code (version 3.11.7 or 3.13.7). Microsoft Corporation. Used for data cleaning, coding, and visualization.

