# **World Happiness Index Analysis**

## Project Overview
This project investigates the factors associated with national happiness using data from the World Happiness Report. The analysis combines exploratory data analysis (EDA), multiple linear regression (MLR), interaction modeling, and diagnostic testing to identify the strongest predictors of happiness while ensuring the validity of statistical assumptions.
The primary objective was to determine whether economic prosperity, human development, unemployment, population density, inequality, crime, literacy, and firearm ownership contribute to differences in happiness level across countries.
### Research Question: 
**Which socio-economic factors most strongly influence national happiness, and how can happiness be explained using a multiple linear regression?**
<br></br>

## Tools and Libraries
- Pandas
- Numpy
- Seaborn
- Matplotlib.pyplot
- Stats
- Multiple Linear Regression (OLS)
- Breusch-Pagan Test
- Variance Inflation Factor (VIF)
- Cook's Distance
- Regression Diagnostics

<br></br>

## Dataset Summary

The dataset contains 114 countries and includes measures of income, unemployment, population density, inequality, education, crime, firearm ownership, human development, and happiness.

| Variable|	Mean|	Std. Deviation|	Min|	Max |
|----------|-----|------------|-------|-------|
| Income|	17 725|	22 101|	508|	117 182|
| Population Density	| 283.87	|985.22|	2 | 8 041|
| Crime Rate	| 44.50|	14.22|	15.23 |	83.76 |
| Unemployment| 7.74	| 5.64	| 0.70 |	35.30 |
| Human Development Index (HDI)	| 0.782	|0.123|	0.49	|0.96 |
| Happiness Index	| 5.748 |	1.025|	2.52|	7.84 |
| Literacy Rate	| 0.900	| 0.139	|0.38	|1.00 |
| Gini Index	| 37.09 |	9.58 |	0.36|	69.30 |
| Weapons per 100 Persons | 12.35	| 14.31	| 0.00 |	120.50 |

<br></br>

## Exploratory Data Analysis
#### Distribution Characteristics
Several predictors exhibited noticeable positive skewness.
|Variable	|Skewness|	Interpretation|
|-----------|--------|-----------| 
|Population Density	|6.90|	A small number of countries exhibit extremely high population density.|
|Weapons per 100 Persons	| 4.15|	Most countries have low firearm ownership, while a few are extreme outliers.|
|Unemployment|	2.08	| A limited number of countries report exceptionally high unemployment rates.|
|Income|	1.91	|Wealth is concentrated among a smaller number of high-income countries.|

<br></br>

## Best Interpretable Linear Regression Model
The best interpretable model explaining national happiness was:

**Happiness = β₀ + β₁·Log(Income) + β₂·Population Density + β₃·Unemployment + β₄·HDI + β₅·(HDI × Unemployment)**

Happiness Index = -0.590 + 0.498 ln(Income)- 0.00014 Population Density- 0.005 Unemployment+ 2.451 HDI + 0.291(HDI × Unemployment)
<br></br>

**Model Performance:**
| Metric | Value|
|--------|------|
|R² | 0.725 |
|Adjusted R² | 0.712|
|F-Statistic | 56.90|
|Prob(F-Statistic) | 1.05 × 10⁻²⁸|
|Number of Observations |114|
| AIC |193.0|
|BIC | 209.5|
|Durbin-Watson | 2.047|

<br></br>

## Model Interpretation
#### Income
- Higher income is associated with higher happiness.
- The relationship is nonlinear, hence the logarithmic transformation.
- Happiness increases with income, but at a decreasing rate, reflecting diminishing marginal returns.
- #### Population Density
- More densely populated countries tend to exhibit slightly lower happiness levels after controlling for other variables.
- #### Unemployment
- For every 1 percentage-point increase in unemployment, happiness decreases by approximately 0.021 points, holding other variables constant.
- The effect of unemployment is moderated by HDI.
#### Human Development Index (HDI)
- HDI emerged as one of the strongest predictors of happiness.
- Holding all other variables constant, a 0.10 increase in HDI increases predicted happiness by approximately 0.58 points.
#### Interaction Effect: HDI × Unemployment
- Happiness is strongly associated with income and population density, but the relationship between unemployment and happiness is moderated by human development. **Countries with higher levels of human development appear better able to mitigate the adverse effects of unemployment on well-being.**
<br></br>

## Model Diagnostics
Diagnostics evaluation indicates:
- Residuals are scattered around the horizontal zero line.
- No systematic curvature is present.
- Residuals remain distributed above and below zero throughout the range of fitted values.
- Residual variance appears relatively constant.
<br></br>

<img width="200" height="200" alt="qqplot of residuals" src="https://github.com/user-attachments/assets/612efc1b-dab0-41ac-94e1-b7d6d92ab70c" />


<img width="200" height="200" alt="residuals_vs_fitted" src="https://github.com/user-attachments/assets/e32df326-c982-454d-ad6d-d02bcb2cfa83" />


<br></br>
## Multicollinearity Assessment
Variance Inflation Factors (VIF) were computed for all predictors.

|Criterion | Interpretation|
|----------|----------------|
| VIF < 5 | Acceptable |
| VIF > 10 | Serious concern|

#### Conclusion
- All predictors had VIF values below 5.
- No evidence of problematic multicollinearity was detected.
- Multicollinearity is not a major concern.
<br></br>
  
## Breusch-Pagan Test
The Breusch-Pagan test was used to evaluate heteroscedasticity.

#### Hypotheses
Null Hypothesis (H₀): Residuals exhibit homoscedasticity (constant variance).
Alternative Hypothesis (H₁): Residuals exhibit heteroscedasticity (non-constant variance).

|Test Statistic | Value|
|----------------|-----------|
|LM Statistic |10.96|
|LM p-value |0.204|
|F Statistic |1.396|
|F p-value | 0.207|

#### Conclusion

Since the p-value exceeds 0.05:

- Fail to reject the null hypothesis.

-  There is insufficient evidence of heteroscedasticity.

-  The assumption of constant error variance appears satisfied.
  <br></br>
  
## Influential Observation Analysis
Influence diagnostics identified four notable countries:

| Country | Reason for Influence|
|------------|---------------------|
|Singapore | Extremely high population density and strong socioeconomic indicators|
|Hong Kong |Extremely high population density and strong socioeconomic indicators|
|Afghanistan | Large prediction error relative to model expectations|
|United States | Exceptional civilian firearm ownership rate|

#### Cook's Distance Assessment

Although these observations exert noticeable influence on model estimates:
- No country exhibited a Cook's Distance greater than 1.
- No single observation excessively dominated the regression results.
Conclusion: The model is not driven by any individual country.
<br></br>

## Key Findings

- Income is a major determinant of happiness.

- Logarithmic income consistently emerged as one of the strongest predictors.

- Human Development Index (HDI) is a primary driver of well-being.

- Countries with higher development levels tend to report substantially higher happiness scores.

- Population density is negatively associated with happiness.

- Unemployment reduces happiness. However, highly developed countries appear better able to offset its negative effects.

- Economic prosperity (Income per Capita) remains the strongest overall predictor.

<br></br>

## Author

[Carl Legros](https://www.linkedin.com/in/carllegros/)


