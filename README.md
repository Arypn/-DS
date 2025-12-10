# Impact of COVID-19 on the Economy: Home Prices and Household Earnings  

## Contributors
- **Alevtyna Rypninska** – Data Analysis & Visualization Lead  
- **Seongwook Min** – Data Integration & Cleaning Lead  

---

## Summary

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



Milestone 4: Final Project Submission 

Title: Impact of COVID-19 on the Economy: Home Prices and Household Earnings

Contributors: Alevtyna Rypninska (ar83) & Seongwook Min (sm116)

Summary: [500-1000 words] Description of your project, motivation, research question(s), and any findings.

Data profile: [500-1000 words] Description of each dataset used including all ethical/legal constraints.

Data quality: [500-1000 words] Summary of the quality assessment and findings.

Findings: [~500 words] Description of any findings including numeric results and/or visualizations.

Future work: [~500-1000 words] Brief discussion of any lessons learned and potential future work.
We learned through our analysis that income, while somewhat helps explain the housing prices, doesn't truly explain the reason. As such, future work should include more variables that seem to be related in someway to housing. Also maybe specific events that happened aroudn the time covid started could also be a reason to why the prices changed. With many other variables, our R^2 may be able to be closer to 1, and we could better explain the changes.

Reproducing: Sequence of steps required for someone else to reproduce your results.

References: Formatted citations for any papers, datasets, or software used in your project.

For the real-estate dataset: 
  Office of Policy and Management. (2025, September 14). Real Estate Sales 2001-2023 GL [Dataset]. Data.gov. https://catalog.data.gov/dataset/real-estate-sales-2001-2018 
  
For the median household income data: 
  U.S. Census Bureau. (n.d.). Real Median Household Income in the United States [MEHOINUSA672N]. FRED – Federal Reserve Bank of St. Louis. https://fred.stlouisfed.org/series/MEHOINUSA672N

Visual Studio Code (version 3.11.7 or 3.13.7). Microsoft Corporation. Used for data cleaning, coding, and visualization.

