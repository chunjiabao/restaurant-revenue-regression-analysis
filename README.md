# Restaurant Revenue Analysis Using Multiple Linear Regression

A statistical analysis identifying the key drivers of monthly restaurant revenue, using Multiple Linear Regression (MLR) on a dataset of 100 restaurants, complemented by an interactive Excel dashboard.

## Overview

Restaurant revenue is influenced by many factors — location, pricing, marketing, service quality — but it's not always clear which of these actually matter once the others are accounted for. This project uses MLR to isolate the statistically significant drivers of monthly revenue and translates the results into actionable business recommendations for restaurant owners.

Three models were built and compared, each improving on the last:

| Model | Description | Adjusted R² | Standard Error | Residual Behavior |
|---|---|---|---|---|
| **Model 1** | Quantitative variables only | 0.2509 | 34,640.7 | Heteroscedastic |
| **Model 2** | Full model (quantitative + dummy-coded categorical variables) | 0.8462 | 15,696.7 | Heteroscedastic |
| **Model 3** | Log-transformed revenue, insignificant predictors removed | 0.90935 | 0.1393 | Randomly distributed  |

Model 3 satisfies all MLR assumptions (linearity, homoscedasticity, no multicollinearity) and is the final model used for interpretation.

## Dataset

- **File:** `Dashboard.xlsx` → `rawdata` sheet
- **Records:** 100 restaurants, no missing values
- **Dependent variable:** `monthly_revenue`
- **Quantitative predictors:** `seating_capacity`, `avg_meal_price`, `years_in_business`, `staff_count`, `marketing_spend`, `customer_rating`
- **Qualitative predictors (dummy-coded):** `location_type`, `cuisine_type`, `restaurant_size`, `has_parking`, `has_delivery`

`seating_capacity` was dropped after Model 1 due to high correlation with `staff_count` (r = 0.78), which created a multicollinearity issue.

## Key Findings

- **Location matters most:** restaurants in **Downtown** areas earn ~38% more revenue than Suburban locations; **Mall** locations earn ~22% more; **Strip Mall** locations earn ~26% less.
- **Customer ratings drive revenue:** each 1-point increase in rating is associated with a ~21% increase in monthly revenue.
- **Marketing spend and meal pricing** both have statistically significant positive effects on revenue.
- All 14 predictors retained in the final model (Model 3) are statistically significant (p < 0.05).

## Repository Contents

```
restaurant-revenue-regression-analysis/
├── Dashboard.xlsx                                  # Raw data, dashboard, and all 3 regression models
├── Restaurant_Revenue_Analysis.docx                # Full written report
└── README.md
```

### About `Dashboard.xlsx`

This workbook contains the full working analysis:
- **`rawdata`** — the original 100-restaurant dataset
- **`Dashboard`** — an interactive Excel dashboard (KPI cards, revenue by cuisine/location, restaurant-size revenue split, customer rating vs. revenue scatter plot)
- **`Model_1_Quantitative`**, **`Model_2_Full`**, **`Model_3_Improved`** — regression output (coefficients, p-values, confidence intervals, residual diagnostics) for each of the three models described above

## Methodology

1. Converted qualitative variables into dummy variables (one reference category dropped per variable to avoid multicollinearity)
2. Built Model 1 using only quantitative predictors; identified heteroscedasticity and insignificant variables
3. Built Model 2 adding all qualitative variables; removed `seating_capacity` due to multicollinearity with `staff_count`
4. Built Model 3 by log-transforming `monthly_revenue` and removing remaining insignificant predictors (`cuisine_type_Italian`, `has_parking_Yes`), producing a model that satisfies all MLR assumptions
5. Compared models using Adjusted R², standard error, and residual diagnostics (since Adjusted R² isn't comparable across models with a transformed dependent variable)

## Tech Stack

- Microsoft Excel (Regression Analysis Toolpak, dashboarding)

## Author

Chun Jia Bao
