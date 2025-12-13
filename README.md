# Predicting NFL Player Contract Values Using Position-Specific Regression Models

**Michael Nichols**  
**Jake Cohen**  
**DS 340W – Data Modeling and Prediction**  
**Penn State University**

---

## Project Overview

The National Football League (NFL) operates under a hard salary cap, making accurate player valuation essential for roster construction, contract negotiation, and long-term competitive success. While prior research has examined salary distributions and team-level payroll effects, there remains a gap in predictive modeling at the **individual player level**, particularly across different position groups.

This project introduces a **position-specific multiple linear regression framework** to estimate NFL player contract values using on-field performance metrics and demographic characteristics. By tailoring predictors to each position group, the models reduce statistical noise and more accurately reflect how different roles are valued in the modern NFL.

The full modeling pipeline is implemented in **R** and follows a reproducible, interpretable, and statistically grounded workflow consistent with the methodology and findings presented in the accompanying research paper :contentReference[oaicite:0]{index=0}.

---

## Research Question

**To what extent can measurable on-field performance metrics predict NFL player contract values, and how does this relationship vary across position groups?**

---

## Methodological Framework

This project follows a **position-specific regression strategy**, motivated by the idea that different positions contribute value in fundamentally different ways.

Key design principles:
- Separate regression models for each position group
- Linear regression for interpretability and transparency
- Log-transformed contract values to address right-skewed salary distributions
- Standardized predictors for comparability across variables
- Train / test / validation split to ensure robust evaluation

The workflow follows the **CRISP-DM** framework:
1. Data understanding  
2. Data preparation  
3. Model development  
4. Model evaluation  
5. Interpretation and discussion  

---

## Data Sources and Description

### Data Sources
- **Spotrac**: Contract values, salary details
- **Pro Football Reference**: Player performance statistics

Data spans **2013–2024 NFL seasons**, ensuring relevance to the modern salary-cap environment.

---

### Offensive Dataset
**`merged_players_offense_yearly_combined.csv`**

Includes season-level variables such as:
- Passing yards, touchdowns, interceptions (QB)
- Rushing attempts, rushing yards, receiving usage (RB)
- Receptions, receiving yards, touchdowns (WR/TE)
- Age and experience
- Total contract value (log-transformed in modeling)

---

### Defensive Dataset
**`merged_players_defense_yearly_combined.csv`**

Includes:
- Tackles
- Sacks
- Quarterback hits
- Interceptions
- Games played
- Contract value

Defensive players are currently modeled as a single group.

---

## Modeling Approach

### Position Groups Modeled
- Quarterbacks (QB)
- Running Backs (RB)
- Wide Receivers / Tight Ends (WR/TE)
- Defensive Players

Each model predicts **log(total contract value)** using position-relevant performance metrics and demographic controls.

Although regularization methods (Ridge, LASSO) were explored for stability testing, **ordinary least squares (OLS)** regression was selected due to its interpretability and sufficient predictive performance.

---

## Model Evaluation Metrics

Model performance is assessed using:
- **R-squared (R²)**: Variance explained
- **Root Mean Squared Error (RMSE)**: Predictive accuracy
- **Adjusted R²**: Comparison across models with different predictors

Evaluation is conducted on both **test and validation datasets** to reduce overfitting risk.

---

## Key Results Summary

- **Quarterbacks**  
  - Strongest performance-to-salary relationship  
  - High R² and low RMSE  
  - Passing yards, touchdowns, and completion percentage are strong positive predictors  
  - Interceptions negatively impact salary

- **Running Backs**  
  - Moderate predictive performance  
  - Rushing volume and receiving involvement both matter  
  - Reflects league preference for versatile, dual-threat backs

- **Wide Receivers / Tight Ends**  
  - Weakest model performance  
  - Negative R² values indicate box-score stats alone do not explain salaries  
  - Likely driven by non-quantified traits (route running, athleticism, scheme fit, market timing)

- **Defense**  
  - Moderate predictive strength  
  - Pass-rush metrics (sacks, QB hits) are strongest predictors  
  - Tackles and interceptions show weaker effects

These results reinforce the importance of **position-specific modeling** and highlight the limitations of traditional statistics for certain roles.

---

## How to Run the Project

### Prerequisites
- R (version 4.0+)
- RStudio (recommended)

### Required Packages
```r
install.packages(c(
  "tidyverse",
  "caret",
  "broom",
  "ggplot2",
  "knitr"
))
```

### How to run
  1. Clone or download this repository from GitHub.
  2. Open **RStudio**.
  3. Set your working directory to the project folder.
  4. Open `NFL_Salary_Model_Clean_Linear_Only.Rmd`.
  5. Make sure the following files are in the same directory:
     - `merged_players_offense_yearly_combined.csv`
     - `merged_players_defense_yearly_combined.csv`
  6. Install required R packages if needed.
  7. Click **Knit** to run the full analysis.
