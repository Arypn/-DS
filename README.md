# Impact of COVID-19 on the Economy: Home Prices and Household Earnings  

## Contributors
- **Alevtyna Rypninska** – Data Analysis & Visualization Lead  
- **Seongwook Min** – Data Integration & Cleaning Lead  

---

## Summary

The COVID-19 pandemic reshaped economic life in ways that were especially visible in the housing market. News headlines described bidding wars, low mortgage rates, and rapidly rising home prices, while many households simultaneously faced job loss, income instability, or stagnant wages. This project asks a simple but important question: **Did household earnings keep up with the surge in housing prices during and after the pandemic, or did the gap between income and housing costs widen?**

To investigate this question, we focus on the relationship between **Connecticut residential home prices** and **U.S. real median household income** from 2015 through 2023. Connecticut provides a useful case study because it reported detailed property-level data across many years, while national income data offers a broad measure of household economic well-being. By integrating these two perspectives—local housing prices and national income trends—we can assess whether the post-pandemic economy reflected genuine recovery for typical households or primarily benefited those already positioned to participate in a rising housing market.

The project is guided by four research questions. First, we examine **how Connecticut home prices changed during the COVID-19 years (2020–2023) compared to the pre-pandemic period (2015–2019)**. We restrict our analysis to **residential properties only**, filtering the statewide real-estate dataset to keep records where the property could be classified using the `Property Type` or `Residential Type` fields. Second, we ask **how real median household income in the United States evolved over the same period**, using an annual series from the Federal Reserve Bank of St. Louis (FRED) based on U.S. Census Bureau data. Third, we investigate **the statistical relationship between income and home prices**, using correlation and linear regression to test whether increases in income can explain observed changes in housing prices. Finally, we explore **what broader conclusions we can draw about post-pandemic affordability and economic resilience**, particularly for households trying to enter or remain in the housing market.

Our workflow follows the data lifecycle emphasized in IS 477. We began by acquiring two trustworthy datasets from public government sources. The **Real Median Household Income** dataset (MEHOINUSA672N) was downloaded as an Excel file and converted into a tidy table with one row per year. The **Connecticut Real Estate Sales** dataset was imported from CSV and cleaned to correct data types, standardize column names, and handle missing values. Because this project is specifically about households and their living situations, we removed rows where both `Property Type` and `Residential Type` were missing, ensuring that our analysis focused only on clearly identifiable residential properties.

We then integrated the datasets by year. The real-estate data originally contained nominal sale prices, so we adjusted every residential sale into **2023 dollars** using the Consumer Price Index for All Urban Consumers (CPI-U). This step ensured that a sale in 2015 could be fairly compared to a sale in 2023. After computing an inflation-adjusted price for each transaction, we aggregated the data to a **year-level dataset** with three key variables: the mean residential sale price in 2023 USD, the mean nominal sale price, and real median household income for that year.

The resulting year-level dataset allowed us to summarize trends and answer our research questions. We found that **Connecticut home prices increased dramatically in real terms during the COVID period**. The average inflation-adjusted residential sale price rose from roughly \$425,000 in the pre-pandemic years (2015–2019) to more than \$609,000 in 2020–2023—a **43% increase** even after controlling for inflation. Visualizations showed a sharp spike in 2020 followed by elevated prices in 2021–2023, suggesting that the pandemic created a structural shift rather than a temporary blip.

In contrast, **real median household income grew only modestly**. Across the same two periods, income increased from about \$77,000 to \$81,000, a gain of just over **5%**. Income peaked in 2019, fell during the first years of the pandemic, and only partially recovered by 2023. When we compared income and housing prices directly, the divergence was striking: home prices climbed many times faster than income, implying that residential property became substantially less affordable for the typical household.

Statistical analysis confirmed that this disconnect was not simply noise. A correlation of about **0.59** indicated a moderate long-run positive relationship between income and home prices—years with higher income tended to also have higher prices. However, a linear regression model using income to predict inflation-adjusted home prices explained only about **34%** of the variation in prices (R² ≈ 0.345). This means that most of the change in home prices, especially during the COVID years, must be attributed to other factors such as low interest rates, limited housing supply, migration patterns, or speculative demand.

Taken together, these results suggest that **rising property values during and after the pandemic did not reflect broad-based improvements in household economic strength**. Instead, the housing market and household earnings moved along increasingly different paths. The surge in Connecticut home prices—combined with relatively slow income growth—points to **worsening affordability and growing inequality**. Households without existing housing assets faced greater barriers to homeownership, while those who already owned property benefited disproportionately from capital gains. In this sense, the post-pandemic housing boom reveals not just economic resilience but also structural vulnerabilities in how the benefits of recovery were distributed.

Milestone 4: Final Project Submission 

Title: Impact of COVID-19 on the Economy: Home Prices and Household Earnings

Contributors: Alevtyna Rypninska (ar83) & Seongwook Min (sm116)

Summary: [500-1000 words] Description of your project, motivation, research question(s), and any findings.

Data profile: [500-1000 words] Description of each dataset used including all ethical/legal constraints.

Data quality: [500-1000 words] Summary of the quality assessment and findings.

Findings: [~500 words] Description of any findings including numeric results and/or visualizations.

Future work: [~500-1000 words] Brief discussion of any lessons learned and potential future work.

Reproducing: Sequence of steps required for someone else to reproduce your results.

References: Formatted citations for any papers, datasets, or software used in your project.

