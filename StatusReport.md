# Milestone 3: Interim Status Report  
### Impact of COVID-19 on the Economy: Home Prices and Household Earnings  
### IS 477 – Fall 2025  
### Team: Alevtyna Rypninska & Seongwook Min  

---

## Introduction

The goal of this project is to investigate how the COVID-19 pandemic reshaped economic well-being by analyzing two key indicators: residential housing prices and real median household income. By integrating Connecticut’s residential property sales data with the Census Bureau’s national household income dataset (accessed through FRED), we aim to determine whether income growth kept pace with the rapid rise in home prices between 2015 and 2023. This question is especially important because many households felt financial pressure throughout the pandemic, and understanding economic reality requires comparing housing costs and earnings on equal terms.

Milestone 3 represents a major turning point in our project. While earlier milestones focused on acquiring datasets, organizing the repository, and cleaning preliminary fields, this milestone centered on producing analytically ready data. Most importantly, we implemented inflation adjustments to ensure that prices across different years can be compared directly. We also cleaned, merged, and aggregated the dataset into a final year-level structure that will serve as the foundation for exploratory analysis, correlation testing, and regression modeling in Milestone 4.

This interim report provides an update on every major task listed in the Project Plan. It documents the work completed, summarizes changes to the plan, evaluates timeline progress, and includes each team member’s contribution summary. The report showcases our progress while laying out a clear path for the remaining work needed to complete the project.

---

## Progress on Project Tasks

### 1. Data Acquisition

All data acquisition tasks outlined in our Project Plan have been fully completed. We collected the Connecticut Office of Policy and Management (OPM) Real Estate Sales dataset covering 2001–2023 and imported it into the project repository. This dataset includes sale price, town, assessment value, property type, sale year, and date recorded. We also acquired the national Real Median Household Income dataset from the Federal Reserve Economic Data (FRED) system, which provides annual household income in inflation-adjusted dollars.

Both datasets were incorporated into the Jupyter notebook (`is477_project.ipynb`) for processing. Files are stored in the repository under appropriate folders, ensuring traceability. No additional data sources were needed, and acquisition required no revisions.  

---

### 2. Data Cleaning and Preprocessing

Much of our early progress depended on correctly cleaning and structuring the raw OPM data, which contained hundreds of thousands of property records. Cleaning involved removing rows with missing sale prices, standardizing numeric formats, correcting inconsistent capitalization in property types, and ensuring that the “Year” field was properly extracted.

Seong led this portion of the project, preparing the `Cleaned_Df` dataframe. His work included:

- filtering out non-residential property categories (e.g., commercial, industrial, vacant land),
- converting date formats to a consistent standard,
- validating numeric fields,
- checking for anomalies such as extreme outliers,
- and merging the income dataset so each property record aligned with the correct Year.

As a result of this work, `Cleaned_Df` contained only valid residential property sales from 2015 to 2023 with clean attributes and corresponding median household income already merged in. This cleaned dataset provided a reliable input for all subsequent steps.

---

### 3. Inflation Adjustment Using CPI-U

One major objective of this milestone was adjusting all housing prices into constant 2023 dollars. Without inflation adjustment, a $200,000 home sale in 2015 cannot be meaningfully compared to the same amount in 2023. Alevtyna implemented this inflation adjustment using the Consumer Price Index for All Urban Consumers (CPI-U), published by the Bureau of Labor Statistics.

To streamline the process, instead of loading CPI values from a separate file, CPI values for each year (2015–2023) were stored directly in a Python dictionary. This minimized file dependencies and ensured a reproducible workflow. The adjustment formula used was:

Adjusted Price in 2023 Dollars = Original Sale Price × (CPI for 2023 divided by CPI for the year the home was sold)

Explanation:
- Original Sale Price = the amount the home sold for in that year  
- CPI for the year = the Consumer Price Index for the sale year  
- CPI for 2023 = the Consumer Price Index for 2023 (our base year)

This calculation converts every home sale into its 2023 equivalent. A new column, `price_2023`, was added to the dataframe. This inflation-adjusted value is essential for accurate trend analysis.

This step was completed smoothly and served as one of the most analytically important components of the milestone.

---

### 4. Creation of the Year-Level Analytical Dataset

The most significant achievement of Milestone 3 was transforming the cleaned and inflation-adjusted data into a summarized year-level dataset appropriate for analysis. Since the goal is to compare economic attributes across years rather than individual homes, we aggregated the data to produce one row per year.

Alevtyna generated the final year-level dataset (`final_year_df`) by grouping the data by Year and computing:

- **mean nominal sale amount**,  
- **mean inflation-adjusted sale price (2023 USD)**,  
- **mean household income for that year**.

The resulting dataset provides a concise representation of how average housing costs and household income changed over time. This format greatly simplifies the analytical steps planned for Milestone 4, such as trend visualizations, year-to-year percent changes, correlation analysis, and regression modeling.

The creation of this year-level dataset marks a key milestone because it transitions the project from data preparation into analysis.

---

### 5. Exploratory Data Analysis (In Progress)

Preliminary exploratory data analysis has begun. Early descriptive summaries show a clear upward trend in both nominal and inflation-adjusted housing prices across the COVID years. Even after adjusting for inflation, the spike in home prices in 2020–2021 is unmistakable. In contrast, household income demonstrates a flatter trajectory, with smaller year-to-year changes and even a slight decline at the onset of the pandemic.

These early insights reinforce the project’s central question: housing prices have accelerated faster than household income. Visualizations and statistical summaries in Milestone 4 will further confirm these patterns.

---

### 6. Statistical Analysis (Upcoming)

Correlation and regression analysis are planned for Milestone 4. With the year-level dataset prepared, we will examine whether changes in income correlate with changes in real housing prices and test whether income is a statistically significant predictor of price changes over time.

These tests will help determine whether the widening gap between home prices and income reflects a fundamental shift in affordability.

---

## Updated Timeline

The project remains fully on schedule. No major timeline adjustments were necessary.

| Task | Status | Original Deadline | Updated Completion |
|------|--------|-------------------|---------------------|
| Data Acquisition | Complete | Oct 21 | Completed on time |
| Data Cleaning | Complete | Oct 28 | Completed on time |
| Inflation Adjustment | Complete | Nov 11 | Completed early |
| Final Year-Level Dataset | Complete | Nov 11 | Completed |
| EDA | In Progress | Nov 19 | On track |
| Correlation & Regression | Not Started | Dec 3 | Scheduled |
| Final Report | Not Started | Dec 3 | Scheduled |
| Final Release | Not Started | Dec 10 | On track |

---

## Changes to the Project Plan

Several refinements were made during Milestone 3:

1. **Switched to a year-level analytical framework**  
   Originally, we expected to analyze property-level data. However, aggregating the data by year provided a clearer view and aligned better with the research questions.

2. **Streamlined inflation methodology**  
   Instead of loading CPI from a file, we embedded CPI values in the notebook. This simplification improved reproducibility.

3. **Earlier integration of the income dataset**  
   Income was merged before inflation adjustment, simplifying downstream tasks.

These changes improved efficiency without altering the project’s goals.

---

## Team Member Contributions

### **Seongwook Min — Data Integration Lead**

Seong led all data preparation tasks. He cleaned and organized the OPM dataset, filtered the data to include only residential properties, and merged it with income data. His work resulted in the `Cleaned_Df` dataset, which provided a reliable basis for further analysis. He ensured consistency in the dataset, handled formatting issues, and prepared the structural foundation for inflation adjustment and aggregation.

### **Alevtyna Rypninska — Data Analysis & Visualization Lead**

During this milestone, I focused on preparing the analytical foundation of the project by implementing the CPI-U–based inflation adjustment and converting all residential sale prices into constant 2023 dollars. I developed a clean and reproducible workflow that adjusted each sale amount and added the new price_2023 variable to the dataset. I then created the final year-level analytical dataset by aggregating residential home sales by year and computing mean nominal prices, mean inflation-adjusted prices, and median household income. This year-level table will be used for all trend analysis, correlation tests, and regression modeling in the next milestone. I also began preliminary exploratory analysis to validate our patterns and contributed to organizing and formatting the Status Report to meet all rubric requirements.

---

## Conclusion

Milestone 3 represents a major step forward in the project. With the datasets fully cleaned, inflation-adjusted, and aggregated, we are now equipped to explore deeper analytical questions. The year-level dataset built during this milestone provides a strong foundation for investigating whether household income growth kept pace with the dramatic rise in housing prices during the COVID-19 pandemic. Our project remains on schedule, and we are well-prepared to begin the statistical modeling and analysis planned for Milestone 4.

---

