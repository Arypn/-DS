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

