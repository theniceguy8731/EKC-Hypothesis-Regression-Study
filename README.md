# Analysis of Evironmental Kuznets Curve on Groundwater Quality in India
This project focuses on the analysis of State Domestic Product (SDP) and Ground Water Quality (GWQ) data across various states in India, examining economic and environmental factors from 2000 to 2011. Our goal is to identify trends, outliers, and potential data discrepancies that could influence policy-making and economic strategy.

## Table of Contents
- [Analysis of Evironmental Kuznets Curve on Groundwater Quality in India](#analysis-of-evironmental-kuznets-curve-on-groundwater-quality-in-india)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
    - [Background](#background)
    - [Objective](#objective)
  - [Data Description](#data-description)
    - [Sources](#sources)
      - [Groundwater Quality Data](#groundwater-quality-data)
      - [State Economic Output Data](#state-economic-output-data)
      - [Inequality Data](#inequality-data)
      - [Additional References](#additional-references)
    - [Description](#description)
      - [Groundwater Quality (GWQ) Data](#groundwater-quality-gwq-data)
      - [State Domestic Product (SDP) Data](#state-domestic-product-sdp-data)
      - [Gini Index Data](#gini-index-data)
      - [Data Issues and Adjustments](#data-issues-and-adjustments)
        - [Missing Entries](#missing-entries)
        - [Outliers](#outliers)
        - [Missing Data Handling](#missing-data-handling)
    - [Preprocessing](#preprocessing)
      - [Data Cleaning and Integration](#data-cleaning-and-integration)
        - [Fixing Telangana Entries](#fixing-telangana-entries)
        - [Excluding Incomplete Entries](#excluding-incomplete-entries)
        - [Standardizing State Names](#standardizing-state-names)
      - [Handling Missing Data](#handling-missing-data)
        - [Analyzing and Addressing Missing Values](#analyzing-and-addressing-missing-values)
      - [Outlier Detection and Management](#outlier-detection-and-management)
        - [Identifying Outliers](#identifying-outliers)
      - [Merging Data Sources](#merging-data-sources)
  - [Methodology](#methodology)
    - [Tools and Technologies Used](#tools-and-technologies-used)
      - [Python Libraries](#python-libraries)
    - [Analytical Methods](#analytical-methods)
  - [Results](#results)
    - [Summary of Findings](#summary-of-findings)
      - [Regression Analysis](#regression-analysis)
        - [Analysis With Outliers](#analysis-with-outliers)
        - [Analysis Without Outliers](#analysis-without-outliers)
        - [Analysis with Complete Model](#analysis-with-complete-model)
        - [Analysis Over Time](#analysis-over-time)
        - [Regional Analysis](#regional-analysis)
        - [Summary Statistics](#summary-statistics)
  - [Discussions](#discussions)
    - [Interpretation of Results](#interpretation-of-results)
    - [Limitations and Future Directions](#limitations-and-future-directions)
  - [Conclusion](#conclusion)

## Introduction

### Background
The Environmental Kuznets Curve (EKC) hypothesis is a fascinating economic theory that suggests a specific relationship between environmental degradation and economic development. Initially proposed in the 1990s, the EKC posits that as an economy grows, environmental degradation increases until a certain level of average income is attained, after which it starts to decline. This forms what is described as an inverted U-shaped curve. This theory has sparked significant academic debate, particularly concerning its applicability across different environmental metrics.

In India, groundwater quality is a critical issue, influenced by both natural and human factors. As the backbone of India’s agricultural and domestic water supply, maintaining groundwater quality is crucial yet challenging due to the impacts of industrialization, agriculture, and urban expansion.

### Objective
The purpose of this project is to examine whether the Environmental Kuznets Curve holds true for groundwater quality across various states in India. This analysis will integrate data on statewise GDP, income inequality(GINI indexes), and indicators of groundwater contamination(particularly nitrate levels) to investigate the correlation between economic growth, income inequality and environmental quality. By exploring these relationships, this project aims to shed light on the broader implications of the EKC in the context of sustainable development and environmental policy in India.

## Data Description
### Sources

#### Groundwater Quality Data
- **Data Description:** Groundwater quality (GWQ) data, measured in milligrams per liter, covering all Indian districts from 2000 to 2019.
- **Source:** 

#### State Economic Output Data
- **Data Description:** State-year wise economic output, specifically net state domestic product (SDP) at constant prices.
- **Source:** Reserve Bank of India (RBI), accessed through the Database for the Indian Economy (DBIE) portal.
  - **Link:** [DBIE - RBI](https://dbie.rbi.org.in/DBIE/dbie.rbi?site=publications#!2)

#### Inequality Data
- **Data Description:** District-level Gini index.
- **Source:** Derived from the paper by Mohanty et al. (2016), which provides an extensive analysis of economic disparities.
  - **Link to Paper:** [Research Gate](https://www.researchgate.net/publication/304613066_Estimates_of_Poverty_and_Inequality_in_the_Districts_of_India_2011-2012)

#### Additional References
- **RBI Regional Definitions:** Definitions of states belonging to each region in India as specified by the RBI.
  - **Link to Document:** [RBI Regional Definitions](https://www.rbi.org.in/upload/Publications/PDFs/58914.pdf)

### Description

#### Groundwater Quality (GWQ) Data
- **Coverage:** All Indian districts
- **Period:** 2000 to 2019
- **Details:** This dataset includes measurements of groundwater quality indicator(nitrate) across all districts in India. It provides a comprehensive look at water quality trends and regional disparities. The data points cover a wide range of pollutants and are crucial for assessing the environmental impact at a granular level.

#### State Domestic Product (SDP) Data
- **Coverage:** All Indian states
- **Period:** 2000 to 2019
- **Details:** The dataset comprises annual economic output figures for each state, measured as the Net State Domestic Product (SDP) at constant prices. This data is essential for analyzing economic growth patterns in relation to changes in environmental quality.

#### Gini Index Data
- **Coverage:** District-level
- **Period:** Corresponds with GWQ and SDP data periods
- **Details:** The Gini index data is used to measure income inequality within districts. This socioeconomic indicator helps to explore how wealth distribution affects environmental outcomes, providing a deeper understanding of the social dimensions involved in the Environmental Kuznets Curve.

#### Data Issues and Adjustments

##### Missing Entries
- **States with Incomplete Data:** Initial analysis revealed missing GWQ data for states including Mizoram, Lakshadweep, Manipur, and Sikkim. These gaps were noted for consideration in the analysis phase to avoid biased interpretations.

##### Outliers
- **Detection Method:** Utilized the Interquartile Range (IQR) Method to identify outliers.
- **Approach:** Applied the IQR method separately on state-wise and overall data points. Approximately 2% of the dataset was identified as outliers, which were handled carefully to maintain the integrity of statistical analyses.

##### Missing Data Handling
- **Nitrate Values:** A significant portion of the dataset (about 4612 out of 11651 data points) lacked nitrate values, with some states missing more than 70% of their data. The approach to managing these missing values was critical for maintaining the robustness of the project's findings.

### Preprocessing

#### Data Cleaning and Integration

##### Fixing Telangana Entries
- **Problem:** SDP data for Telangana was missing from 2000 to 2004.
- **Solution:** Used average ratios of SDP between Andhra Pradesh and Telangana from 2004 to 2011 to estimate Telangana's SDP for the missing years, ensuring that potential biases from diverging growth rates post-2011 were minimized.

##### Excluding Incomplete Entries
- **Action:** Entries for Dadra and Nagar Haveli and Daman and Diu were dropped from the GWQ dataset due to the absence of corresponding SDP data.

##### Standardizing State Names
- **Purpose:** Facilitated data handling and consistency across datasets by converting full state names to their official abbreviations.

#### Handling Missing Data

##### Analyzing and Addressing Missing Values
- **Details:** Identified significant gaps in nitrate values, with 4612 out of 11651 data points missing. Some states had more than 70% of their data missing. Decisions on how to handle these missing values were crucial for the integrity of the analysis.
- **Approaches:**
  - **Complete Case Analysis:** Created one dataset where all missing data points were dropped.
  - **Mean Imputation:** Formed a second dataset where missing values were replaced with the state-wise means for each respective state. And states with more than 66% of missing data were excluded.
  - **District Level Mean Imputation:** Created a third dataset where districts with more than 66% missing data were excluded, and remaining missing points were imputed using district-level averages.

#### Outlier Detection and Management

##### Identifying Outliers
- **Method Used:** Applied the Interquartile Range (IQR) method separately on state-wise and pooled data points to detect outliers.
- **Handling Strategy:** Instead of excluding outliers directly, they were flagged with a dummy variable in the dataset to assess their impact during regression analysis without losing potentially valuable information.

#### Merging Data Sources
- **Procedure:** Merged GWQ, SDP, and Gini data into three comprehensive datasets prepared under different assumptions for handling missing data and outliers.


## Methodology

### Tools and Technologies Used

#### Python Libraries
- **Pandas:** For data manipulation and cleaning.
- **NumPy:** For numerical operations.
- **Matplotlib & Seaborn:** For data visualization.
- **Statsmodels:** For econometric analyses.
- **Jupyter Notebook:** As the development environment for interactive computing and presentation.

### Analytical Methods

1. **Regression Analysis:** 
   - **Linear Regression:** Used to explore relationships between variables like State Domestic Product (SDP) and Groundwater Quality (GWQ), including additional factors such as the Gini index.
   - **Non-linear Regression:** To assess the Environmental Kuznets Curve hypothesis, incorporating polynomial terms (SDP squared and cubed) to capture potential non-linear effects.

2. **Outlier Detection:**
   - Employed the Interquartile Range (IQR) method to identify and address outliers, ensuring that the regression analysis remains robust and reliable.

3. **Data Imputation:**
   - Various strategies to handle missing data:
     - Complete case analysis (dropping all missing data).
     - Mean imputation at different levels (state and district) to maintain data integrity without significant data loss.

4. **Dummy Variable Creation:**
   - Introduced dummy variables in regression models to consider outliers and categorical variables such as regions or specific years, enhancing model accuracy and interpretability.

5. **Time Series Analysis:**
   - Incorporated time-specific dummy variables to analyze temporal trends and changes over the years.

6. **Hypothesis Testing:**
   - Conducted hypothesis tests to statistically validate the results obtained from regression analyses, such as testing the significance of coefficients to understand their impact on dependent variables.

7. **Geographical Analysis:**
   - Analyzed geographical variations by including region-specific dummy variables in regression models. This helped in understanding how environmental and economic variables interact differently across various regions of India.

## Results
### Summary of Findings
<div align="center">

![](./Assets/Pasted%20image%2020240429011859.png)

</div>

#### Regression Analysis
##### Analysis With Outliers
<div align="center">

![](./Assets/Pasted%20image%2020240429015810.png)

</div>

| Variable Name | Coefficient | Standard Error | T-stat | Confidence Interval   | R-squared | Observations | F-stat |
| ------------- | ----------- | -------------- | ------ | --------------------- | --------- | ------------ | ------ |
| const         | 39.5958     | 0.808          | 49.020 | 38.012 41.179         | 0.470     | 6761<br>     | 2992   |
| SDP           | 7.299e-06   | 1.53e-06       | 4.756  | (4.29e-06) (1.03e-05) |           |              |        |
| Outlier       | 175.9017    | 2.274          | 77.338 | 171.443 180.360       |           |              |        |
*Dataset 1*

| Variable Name | Coefficient | Standard Error | T-stat | Confidence Interval | R-squared | Observations | F-stat |
| ------------- | ----------- | -------------- | ------ | ------------------- | --------- | ------------ | ------ |
| const         | 40.9483     | 0.731          | 56.048 | 39.516 42.380       | 0.462     | 7349         | 3149   |
| SDP           | 0.0086      | 0.001          | 5.972  | 0.006<br>0.011      |           |              |        |
| Outlier       | 174.6020    | 2.203          | 79.270 | 170.284 178.920     |           |              |        |
*Dataset 2*

| Variable Name | Coefficient | Standard Error | T-stat | Confidence Interval | R-squared | Observations | F-stat |
| ------------- | ----------- | -------------- | ------ | ------------------- | --------- | ------------ | ------ |
| const         | 40.5251     | 0.771          | 52.568 | 39.014 42.036       | 0.444     | 7346         | 2929   |
| SDP           | 8.201e-06   | 1.51e-06       | 5.423  | 5.24e-06 1.12e-05   |           |              |        |
| Outlier       | 8.201e-06   | 2.289          | 76.473 | 170.574 179.549     |           |              |        |
*Dataset 3*

From the high value of the t statistic it is evident that in our case the outliers are affecting the results as the confidence interval suggested that we can reject the null hypothesis, and so we use trimming to solve the issue of Outliers. One could also use winsorizing to tackle such problems.

##### Analysis Without Outliers

<div align="center">

![](./Assets/Pasted%20image%2020240429020824.png)

</div>

> **Note:** We achieve somewhat similar results results in our basic regression analysis and so we decide to move forward only with the dataset 2 because of the fact that it has the highest number of observation as well as it will help us in interpretation as we see later on.

| Variable Name | Coefficient | Standard Error | T-stat | Confidence Interval | R-squared | Observations | F-stat |
| ------------- | ----------- | -------------- | ------ | ------------------- | --------- | ------------ | ------ |
| const         | 41.0345     | 0.624          | 65.722 | 39.811 42.258       | 0.007     | 7041         | 46.05  |
| SDP           | 0.0084      | 0.001          | 6.786  | 0.006<br>0.011      |           |              |        |
*Dataset 2*

##### Analysis with Complete Model
| Variable Name | Coefficient | Standard Error | T-stat  | Confidence Interval | R-squared | Observations | F-stat |
| ------------- | ----------- | -------------- | ------- | ------------------- | --------- | ------------ | ------ |
| const         | 35.4741     | 2.206          | 16.084  | 31.151 39.798       | 0.074     | 7041         | 141.1  |
| SDP           | 0.1453      | 0.007          | 20.071  | 0.131    0.160      |           |              |        |
| SDP-squared   | -0.0002     | 1.18e-05       | -16.361 | -0.000 -0.000       |           |              |        |
| SDP-cubed     | 6.78e-08    | 5.1e-09        | 13.305  | 5.78e-08 7.78e-08   |           |              |        |
| GINI          | -55.0448    | 6.636          | -8.295  | -68.053 -42.037     |           |              |        |
*Dataset 2*

<div align="center">

![](./Assets/Pasted%20image%2020240429023528.png)

</div>

##### Analysis Over Time
- To quantify the effect of years on the the model we will consider a new dummy variable by the name time and set it's value to year-200 for that respective data point. 
- This will effectively set the values of outliers ranging from 0 to 18.
- After this we will just run a regression to test the statistical significance of this variable.

| Variable Name | Coefficient | Standard Error | T-stat  | Confidence Interval | R-squared | Observations | F-stat |
| ------------- | ----------- | -------------- | ------- | ------------------- | --------- | ------------ | ------ |
| const         | 39.3809     | 2.203          | 17.873  | 35.062 43.700       | 0.095     | 7041         | 147.0  |
| SDP           | 0.1582      | 0.007          | 21.874  | 0.144    0.172      |           |              |        |
| SDP-squared   | -0.0002     | 1.17e-05       | -16.878 | -0.000 -0.000       |           |              |        |
| SDP-cubed     | 6.784e-08   | 5.04e-09       | 13.459  | 5.8e-08 7.77e-08    |           |              |        |
| GINI          | -53.4313    | 6.564          | -8.140  | -66.299 -40.564     |           |              |        |
| time          | -0.9488     | 0.076          | -12.565 | -1.097 -0.801       |           |              |        |
| sdp*time      |  0.0047     | 0.001          |  4.920  |  0.003  0.007       |           |              |        |
| gini*time     | -0.8652     | 1.190          | -0.727  | -3.198  1.468       |           |              |        |
| sdp^2*time    | -3.227e-06  | 9.62e-07       | -3.354  | -5.11e-06 -1.34e-06 |           |              |        |


##### Regional Analysis
- To model the data on geographical basis we will be using the method of categorical dummy variables.
- We will assign a binary dummy variable to each region except one.
- This is done as the gain in linear relationship is not constant from each region to the other region.
- Now we just run a regression analysis to quantify our results.

| Variable Name | Coefficient | Standard Error | T-stat  | R-squared | Observations | F-stat |
| ------------- | ----------- | -------------- | ------- | --------- | ------------ | ------ |
| const         | 25.0010     | 3.611          | 6.923   | 0.224     | 7041         | 203.4  |
| SDP           | 0.1601      | 0.007          | 22.090  |           |              |        |
| SDP-squared   | -0.0002     | 1.13e-05       | -16.984 |           |              |        |
| SDP-cubed     | 6.601e-08   | 4.82e-09       | 13.685  |           |              |        |
| GINI          | -66.6524    | 6.137          | -10.860 |           |              |        |
| time          | -1.0732     | 0.078          | -13.728 |           |              |        |
| north         | 25.5117     | 3.488          | 7.315   |           |              |        |
| east          | -20.0382    | 3.783          | -5.297  |           |              |        |
| central       | 14.4271     | 3.491          | 4.133   |           |              |        |
| west          | 11.0725     | 3.770          | 2.937   |           |              |        |
| south         | 25.2794     | 3.596          | 7.031   |           |              |        |

- Here the baseline is represented by the north-eastern states.
- From our regression analysis we can infer that most geographical regions show an increase in nitrate levels with respect to north eastern regions except for the the eastern region.

##### Summary Statistics
| Index      | Count    | Mean               | Std               | Min         | Max               |
| ---------- | -------- | ------------------ | ----------------- | ----------- | ----------------- |
| Nitrate    | 7041     | 44.3817622809      | 32.2242300243     | 0           | 145.5             |
| SDP        | 7041<br> | 398.8264137196     | 309.5532614022    | 1.373       | 1728.578          |
| SDP-square | 7041<br> | 254872.120605286   | 440275.0137812615 | 1.885129    | 2987981.902084    |
| SDP-cubic  | 7041<br> | 228931752.67689428 | 651794044.5076435 | 2.588282117 | 5164959780.340556 |
| GINI       | 7041<br> | 0.2807853998       | 0.0558248539      | 0.17        | 0.48              |

| Index      | 25%               | 50%               | 75%                | 95%              |
| ---------- | ----------------- | ----------------- | ------------------ | ---------------- |
| Nitrate    | 17.6709141117     | 38.150002         | 62.20414           | 108.25           |
| SDP        | 188.93            | 325.739           | 510.787            | 1024.622         |
| SDP-square | 35694.5449        | 106105.896121     | 260903.359369      | 1049850.242884   |
| SDP-cubic  | 6743770.367957001 | 34562828.49655841 | 133266044.22201338 | 1075699655.56429 |
| GINI       | 0.24              | 0.27              | 0.32               | 0.39             |

## Discussions

### Interpretation of Results
Our findings indicate that nitrate levels are generally higher in most regions compared to the northeastern states, except for the eastern region which shows lower levels. This variation could be attributed to differences in industrial activities, agricultural practices, and urbanization levels across regions.

The increasing trend in nitrate levels over time suggests that economic development initially leads to greater environmental degradation. However, the varied impact across regions hints at the influence of local policies, environmental regulations, and the economic structure of each region on pollution levels.

The results align with the Environmental Kuznets Curve hypothesis, which predicts that pollution will rise with economic growth up to a certain income level, after which it will begin to decline. The reason behind this pattern could be that higher income levels enable better infrastructure for pollution control and greater public awareness about environmental issues.

### Limitations and Future Directions
- We can see that we already do not have any data for the following states:
	- Mizoram
	- Lakshadweep
	- Manipur
	- Sikkim
- From a basic analysis we see that the data for 17 districts is missing from the data and 
- 8 of these belong to Jammu and Kashmir and the other belong to various other states.
- Also in our dataset due to the missing data we have to exclude the following states:
  - Nagaland
  - Bihar
  - Jharkhand
  - Meghalaya
  - Arunachal Pradesh
  - Odisha
  - Uttar Pradesh
  - Assam
- And therefore our results or interpretations are not applicable to these states.
## Conclusion
In summary, our analysis supports the idea that while economic growth is often accompanied by environmental challenges, the extent of these challenges can vary significantly based on regional characteristics and developmental stages.
