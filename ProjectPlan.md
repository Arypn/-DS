#ProjectPlan.md

Project Title: Impact of COVID-19 on the Economy — Home Prices and Earnings

Overview
The COVID-19 pandemic triggered unprecedented changes in the U.S. economy, particularly within the housing and labor markets. While home prices surged to record highs, many households faced stagnant earnings and financial instability. This project seeks to explore how the pandemic influenced both real estate prices and median household income from 2015 through 2023, focusing on the question of whether income growth kept pace with rapidly rising property values.

By integrating two government datasets — one from the Connecticut Office of Policy and Management (OPM), which reports real estate sales across the state, and another from the U.S. Census Bureau via FRED, which tracks national real median household income — this project will illustrate both local and national economic shifts during and after the pandemic. The work will demonstrate concepts from the data lifecycle, including acquisition, organization, integration, cleaning, analysis, and documentation, while also emphasizing ethical and reproducible data-handling practices.

Research Questions
This project is guided by four central research questions:
How did Connecticut home prices change during the COVID-19 period (2019–2023) compared to the pre-pandemic years (2015–2019)?


How did real median household income in the United States evolve across the same period?


What relationship exists between changes in income and changes in home prices during and after the pandemic?


What broader conclusions can we draw about post-pandemic affordability and economic resilience?


Together, these questions aim to uncover whether rising property values reflected genuine economic recovery or growing inequality between income and housing costs.

Team
This project is a collaboration between Alevtyna Rypninska and Seongwook Min. Working as a two-person team allows a clear division of responsibilities while maintaining accountability through a shared GitHub repository.
Alevtyna Rypninska – Project Manager & Data Integration Lead:
 Alevtyna is responsible for coordinating the project timeline, organizing the GitHub structure, acquiring and cleaning the datasets, merging them by year, and documenting the data workflow to ensure reproducibility.


Seongwook Min – Data Analysis & Visualization Lead:
 Seong will perform exploratory data analysis, generate descriptive statistics and visualizations, carry out correlation and regression testing, and assist in interpreting and communicating findings in the final report.


Both team members will contribute to the writing of reports and notebooks. All code and markdown files will be version-controlled, with regular branch merges and review meetings to maintain consistency and equal contribution, as reflected in the Git commit history.

Datasets
1. Connecticut Real Estate Sales Dataset (Office of Policy and Management, Data.gov)
The first dataset originates from the Office of Policy and Management (OPM) and provides a comprehensive listing of all real estate transactions in Connecticut with a sales price of $2,000 or greater, collected annually between October 1 and September 30. The data are mandated by Connecticut General Statutes §§ 10-261a and 10-261b and include variables such as town, property address, date of sale, property type (residential, apartment, commercial, industrial, or vacant land), sales price, and property assessment.
Each year of data is referred to as a Grand List year. For instance, the 2018 GL represents sales occurring between October 2018 and September 2019. The dataset covers multiple years from 2001 to 2023, although a few municipalities may not report data immediately following property revaluations.
This dataset will form the foundation of the housing-market analysis. Prices will be adjusted for inflation to 2023 U.S. dollars using the Consumer Price Index (CPI-U). By grouping the data by year and property type, we can track how median and average prices evolved before, during, and after the COVID-19 pandemic. The cleaned and processed files will be stored in /data/processed/ for reproducibility.

2. Real Median Household Income in the United States (U.S. Census Bureau via FRED)
The second dataset, accessed through the Federal Reserve Bank of St. Louis (FRED), is titled Real Median Household Income in the United States (MEHOINUSA672N). It contains annual values from 1984 through 2024 and represents household income measured in 2024 C-CPI-U dollars (not seasonally adjusted). The underlying source is the U.S. Census Bureau’s Income and Poverty in the United States release.
Because the data are already inflation-adjusted, they allow for straightforward comparison across decades. The dataset includes two main columns — DATE, representing the year, and MEHOINUSA672N, the corresponding real median household income value. These figures will provide the national earnings context for comparison against Connecticut’s housing trends.
For the integration step, the project will align income data and real-estate data by calendar year (2015–2023). This will enable the creation of time-series visualizations showing how the trajectory of income compares with housing prices during the COVID era.

Integration and Analysis Plan
After collecting both datasets, the first phase will focus on cleaning and preparation. Dates will be standardized, and inflation adjustments will be applied to ensure both datasets share a consistent value base (2023 USD). Once prepared, the datasets will be merged by the year variable, producing a combined table containing annual median sale prices for Connecticut and national median household income.
The integrated data will support three analytical stages:
Descriptive Trend Analysis: Identify pre-, during-, and post-pandemic patterns in both prices and income.


Correlation Testing: Calculate the correlation coefficient to assess whether annual income changes are associated with home-price movements.


Regression Modeling: Use a simple linear model to estimate how changes in household income relate to variations in real estate prices.


Visualization will play an important role. Line graphs will illustrate both series on a shared timeline, and scatterplots will visualize the relationship between percentage changes in income and housing prices. The entire workflow will be automated in Python (using Pandas, NumPy, and Matplotlib) to ensure reproducibility.

Timeline and Milestones
The project will be completed through a series of structured milestones aligned with the course deadlines. Both team members, Alevtyna Rypninska and Seongwook Min, will share equal responsibility for the project’s progress and deliverables. While Alevtyna will focus more on data analysis, identifying trends, and interpreting results, Seong will take the lead on data structure, cleaning, and integration to ensure the datasets are accurate and well-organized. All writing, documentation, and presentations will be completed collaboratively.

By October 16, 2025: Complete and submit the Project Plan (Milestone 2) including all required sections: overview, research questions, datasets, timeline, constraints, and gaps. Both Alevtyna and Seong will contribute equally to writing and editing the plan.

By October 21, 2025: Acquire the two datasets — Connecticut Real Estate Sales (Data.gov) and Real Median Household Income (FRED). Seong will focus on data collection, formatting, and cleaning, while Alevtyna will verify data accuracy and begin preliminary exploration.

By October 28, 2025: Apply inflation adjustments using CPI-U, standardize date formats, and merge the datasets by year. Seong will manage data integration and transformation, with Alevtyna assisting in checking alignment and data completeness.

By November 11, 2025: Submit the Interim Status Report (Milestone 3) summarizing progress, challenges, and preliminary results. Both members will draft and review the report together, ensuring a balanced reflection of technical and analytical progress.

By November 19, 2025: Conduct exploratory data analysis (EDA), identify trends, and generate initial visualizations that compare income and housing price changes. Alevtyna will lead the analysis and visualizations, while Seong ensures data accuracy and assists with coding support.

By December 3, 2025: Draft the final report, integrate findings, and refine visuals and interpretations. Both Alevtyna and Seong will contribute equally to writing, editing, and formatting the report for clarity and consistency.

By December 10, 2025: Submit the Final Project Release (Milestone 4) on GitHub, including all cleaned datasets, analysis notebooks, Markdown reports, and a tagged release. Both members will review the repository, confirm reproducibility, and finalize documentation.

Constraints
Time will be the most significant constraint since each milestone must be completed within a two-week window. The housing dataset is Connecticut-specific, while the income dataset is national, so conclusions must account for regional variation. Some towns may have missing or incomplete sales data due to property revaluations. Another technical constraint is ensuring consistent inflation adjustments, because the income dataset already uses 2024 C-CPI-U dollars while the real-estate data will be converted using CPI-U indexes. Finally, defining the “COVID-19 period” presents an interpretive challenge; for this project, 2020 and 2021 will represent the acute pandemic phase, with 2022–2023 treated as recovery years.

Gaps and Areas for Additional Input
At this stage, the primary gap involves the granularity of income data. While the Census dataset provides national figures, state-level median income data (from the American Community Survey) could offer better alignment with the Connecticut housing dataset. We will consult the instructor about whether adding that third dataset is encouraged or beyond scope.
 Another open decision is the analytical model: depending on feedback, the project may employ either a simple correlation or an interrupted time-series approach to highlight the structural break at 2020. We will also seek guidance on best practices for visualization aesthetics and report formatting to align with course expectations.

Summary
In summary, this project will provide a data-driven examination of how the COVID-19 pandemic influenced housing prices and earnings in the United States. By combining the Connecticut real-estate dataset with the Census Bureau’s national income data, we aim to determine whether wage growth supported or lagged behind the rapid escalation of housing costs. The project will apply key concepts from the data lifecycle, including ethical handling, integration, quality assessment, and reproducibility.
The resulting workflow will not only address the research questions but also serve as a transparent example of best practices in data management and analysis — from acquisition to final reporting — as required by the course project milestones.

