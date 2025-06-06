# Predicting Baseball Pitcher's Earned Run Average (ERA)

A comprehensive statistical analysis project that develops predictive regression models to forecast a baseball pitcher's Earned Run Average (ERA) using various performance metrics and advanced regularization techniques.

## 📊 Project Overview

This project analyzes 2023 MLB pitching data to identify the most significant predictors of pitcher performance and build robust predictive models. Using a dataset with 106+ potential predictors, we employ multiple regression techniques to address challenges like multicollinearity and overfitting.

### Key Objectives
- Identify the most significant predictors of pitcher ERA
- Develop models balancing accuracy and interpretability  
- Address multicollinearity using advanced regression techniques
- Validate models through comprehensive diagnostic testing

## 🎯 Research Questions

1. Which performance metrics are the most significant predictors of a pitcher's ERA?
2. How do advanced regression techniques (Ridge, LASSO, Elastic Net) improve model performance?
3. What are the potential issues of multicollinearity in the dataset, and how can they be mitigated?
4. How well does the final model generalize to new data based on diagnostic assessments?

## 📈 Dataset

### Data Sources
- **Pitching Data 2023** (`pitching_data_2023.csv`): Comprehensive pitching statistics for the 2023 MLB season
- **Additional Stats** (`additional_stats.csv`): Supplementary performance metrics

### Key Variables
- **Target Variable**: `p_era` (Pitcher's Earned Run Average)
- **Key Predictors**:
  - `k_percent`: Strike/strikeout percentage
  - `bb_percent`: Walk percentage  
  - `whiff_percent`: Swing-and-miss percentage
  - `woba`: Weighted on-base average
  - `xba`: Expected batting average
  - `player_age`: Pitcher's age
  - `swing_percent`, `hard_hit_percent`: Batting quality metrics

## 🔬 Methodology

### Models Tested

1. **Model 1**: `p_era ~ k_percent + bb_percent`
   - Hypothesis: Basic strikeout/walk stats affect performance

2. **Model 2**: `p_era ~ woba + whiff_percent` ⭐ **Best Initial Model**
   - Hypothesis: Preventing strong batting and inducing misses impacts effectiveness
   - **AIC: 91.89** (lowest)

3. **Model 3**: `p_era ~ player_age + xba * woba`
   - Hypothesis: Age and expected batting performance influence ERA

4. **Model 4**: `p_era ~ swing_percent + hard_hit_percent + whiff_percent`
   - Hypothesis: Swing behavior and contact quality explain performance

5. **Model 5**: `p_era ~ player_age * k_percent + bb_percent`
   - Hypothesis: Control, strikeouts, and age impact ERA

### Advanced Techniques

#### Regularization Methods
- **Ridge Regression**: Handles multicollinearity by adding L2 penalty
- **LASSO Regression**: Performs feature selection via L1 penalty  
- **Elastic Net**: Combines Ridge and LASSO for optimal balance ⭐ **Final Model**

#### Model Validation
- Residual analysis and QQ-plots
- Variance Inflation Factor (VIF) analysis
- Cook's Distance and leverage analysis
- Durbin-Watson and Ljung-Box tests for autocorrelation
- Cross-validation for parameter tuning

## 🏆 Key Results

### Final Model Performance
- **Correlation Coefficient**: 0.8086 (R² ≈ 0.65)
- **Final Predictors**: k_percent, bb_percent, woba, xba, and woba:xba interaction
- **Key Insights**:
  - `whiff_percent` and `woba:xba` interaction emerged as most crucial predictors
  - Regularization techniques significantly improved model stability
  - Multicollinearity successfully addressed (VIF values within acceptable ranges)

### Notable Outliers
Elite pitchers identified as influential points:
- Shohei Ohtani (extreme innings pitched)
- Blake Snell (exceptional performance profile)
- Spencer Strider (high strikeout/walk combination)
- Michael Kopech (unique statistical profile)

## 🚀 Getting Started

### Prerequisites
```r
# Required R packages
library(tidyverse)
library(glmnet)
library(car)
library(broom)
library(ggplot2)
library(lmtest)
library(caret)
library(Metrics)
```

### Installation & Usage
1. Clone the repository:
```bash
git clone https://github.com/[username]/baseball-era-prediction
cd baseball-era-prediction
```

2. Load the data:
```r
# Update file paths to your local directory
file_path <- "data/pitching_data_2023.csv"
file_path1 <- "data/additional_stats.csv"
data <- read.csv(file_path)
data1 <- read.csv(file_path1)
merged_data <- merge(data, data1, by = "last_name..first_name")
```

3. Run the analysis:
```r
source("Final410.Rmd")
```

## 📁 Repository Structure

```
baseball-era-prediction/
├── README.md
├── Final410.Rmd                 # Main analysis file
├── data/
│   ├── pitching_data_2023.csv
│   └── additional_stats.csv
├── docs/
│   ├── presentation.pdf         # Project presentation slides
│   └── final_report.pdf         # Comprehensive project report
└── results/
    ├── model_outputs/
    └── visualizations/
```

## 📊 Key Visualizations

- **Coefficient Plots**: Show predictor importance and effect direction
- **Residual Analysis**: Validate model assumptions
- **Cross-Validation Curves**: Optimal lambda selection for regularization
- **Influence Plots**: Identify outliers and leverage points

## 🔮 Future Work

- **Multi-Season Analysis**: Expand to include temporal trends
- **Additional Metrics**: Incorporate pitch velocity and movement data
- **Parameter Tuning**: More granular grid search for lambda optimization
- **Outlier Modeling**: Specialized approaches for elite performers
- **Player Clustering**: Identify different pitcher archetypes

## 👥 Team Members

- **Aaron Wu** - Lead Data Analyst & Model Development
- **Ruchi Tiwari** - Data Processing & Validation
- **Edwin Muñoz** - Model Validation & Diagnostics  
- **Shakty Juarez** - Regularization Techniques & Parameter Tuning

## 📚 References

- [2023 MLB Player Stats - Kaggle](https://www.kaggle.com/datasets/vivovinco/2023-mlb-player-stats)
- [Baseball Stats for Beginners](https://www.blessyouboys.com/2019/1/9/18172095/baseball-stats-for-beginners-earned-run-average-field-independent-pitching-explained)
- [MLB Glossary - WHIP](https://www.mlb.com/glossary/standard-stats/walks-and-hits-per-inning-pitched)
- [Baseball Savant - Player Stats](https://baseballsavant.mlb.com/)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

**Note**: This project was completed as part of STAT 410 coursework. The analysis demonstrates practical applications of advanced statistical methods in sports analytics and provides insights valuable for team management, player development, and fantasy sports.
