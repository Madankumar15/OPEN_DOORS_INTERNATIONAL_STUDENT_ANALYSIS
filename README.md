# OPEN_DOORS_INTERNATIONAL_STUDENT_ANALYSIS

Comprehensive analysis of international student enrollment trends in US higher education institutions (1980-2025) with time series forecasting using Facebook Prophet.

## Overview

This project performs a multi-dimensional exploratory data analysis on the Open Doors International Student Census dataset, encompassing 45 years of enrollment data across 190+ countries, 4,000+ institutions, and 20+ fields of study. The analysis integrates descriptive, comparative, trend, and predictive components to provide actionable insights for institutional planning.

## Dataset

- **Source**: Open Doors Institute for International Education Census (1980-2025)
- **Observations**: 1.18M international students (current)
- **Time Period**: 45 academic years
- **Geographic Coverage**: 190+ countries and regions
- **Institutional Coverage**: 4,000+ degree-granting institutions across 4 types
- **Fields Analyzed**: 20+ major fields of study
- **Funding Categories**: 8+ distinct funding source types

## Analysis Structure

### 1. Descriptive Analysis (5 visualizations)

Examines data distributions, trends, and fundamental characteristics:

| Chart | Finding |
|-------|---------|
| Total enrollment trend (1980-2025) | 2,326% growth (49K → 1.18M); 4 structural breaks at 1985, 2001, 2016, 2020 |
| YoY enrollment & growth rates | COVID-19 induced -8% decline (2020/21); recovery by 2022/23 |
| Category composition over time | Graduates dominate (40%+); OPT fastest-growing (20%+) |
| Academic level distribution | Current: 35% UG, 40% Grad, 5% Non-Degree, 20% OPT |
| Institution type distribution | Right-skewed; Doctoral institutions host 45%; Gini: 0.634 (high concentration) |

### 2. Comparative Analysis (8 visualizations)

Identifies patterns across geographic, demographic, and financial dimensions:

| Chart | Finding |
|-------|---------|
| Top 15 countries by enrollment | India (363K) + China (266K) = 54% of total |
| Country growth rates (YoY) | Nepal 48.7%, Vietnam 15.9% (high-growth); China -4.1% (declining) |
| Regional distribution | Asia 70%+; Latin America 15%; Europe 10% |
| Country × degree heatmap | India: Masters+OPT heavy; Mexico: balanced |
| Funding source composition | 50% self-funded, 25% employment, 20% university-supported |
| Funding by academic level | Undergrads: more university support; Grads: self/employment-funded |
| Institution type growth | Doctoral +2.5% YoY; Master's expanding faster |
| Regional growth | Latin America 3.2% YoY; Asia 1.5%; Europe 0.8% |

### 3. Trend & Correlation Analysis (3 visualizations)

Reveals structural patterns and field-level relationships:

| Chart | Finding |
|-------|---------|
| Field specialization heatmap | STEM-dominant for India/China; Business-dominant for Europe/Middle East |
| Enrollment-field correlation | Engineering & Business show highest positive correlation |
| Lorenz curves + Gini | High concentration (Gini 0.634): top 20 institutions = 45% of students |

### 4. Machine Learning Forecasting (2 visualizations)

Applies Bayesian time series methodology:

| Chart | Finding |
|-------|---------|
| Prophet forecast (2025-2030) | 1.26M projected by 2029/30; annual growth 1.4% (slowing from 4.5% historical) |
| Model performance | MAPE: 12.06% (acceptable for planning); MAE: ±130K |

## Methodology

### Data Processing

- Hierarchical structure removal from Census tables
- Categorical encoding for academic levels, regions, funding types
- Temporal alignment: academic year parsing ("2024/25" → "2024-07-01")
- Null handling: forward-fill for trends; deletion for specific analysis

### EDA Techniques

**Descriptive**: Summary statistics, distribution analysis (box plots, CDF), concentration metrics (Lorenz, Gini)

**Comparative**: Cross-tabulation, heatmaps, percentage composition, YoY growth calculations

**Trend**: Time series decomposition, COVID-19 impact assessment, field correlation

### Time Series Forecasting

**Algorithm**: Facebook Prophet (Bayesian additive model)

**Configuration**:
- Trend: Piecewise linear with automatic changepoint detection (prior scale: 0.05)
- Seasonality: Additive yearly component (prior scale: 10)
- Uncertainty: 95% confidence intervals via posterior sampling
- Inference: MCMC (PyMC backend)

**Validation**:
- Split: 80/20 (2015-2024 train; 2015-2025 test)
- Metrics: MAPE 12.06%, MAE ±130K, RMSE ±145K
- Backtesting: 10-year period

**Assumptions**:
- Historical patterns persist (no structural shocks)
- Univariate model (no causal inference)
- Stationarity via trend + seasonality decomposition

## Key Findings

### Market Structure
- **Concentration**: Gini 0.634; top 20 institutions host 45%
- **Geographic**: Asia 70%+; India + China = 54%
- **Institutional**: Doctoral-led (45%); Master's expanding

### Growth Dynamics
- **Overall**: 2,326% over 45 years; slowing from 4.5% to 1.4% annually
- **Heterogeneous**: Nepal/Vietnam high-growth; China/South Korea declining
- **COVID**: -8% shock (2020/21); 12-18 month recovery lag

### Demographics
- **Academic**: Graduates 40%+; OPT fastest-growing
- **Funding**: 50% self-funded (economically sensitive); 25% employment-sponsored
- **Field**: STEM for Asia; Business for Europe/Middle East

### Forecast (2025-2030)
- **Point**: 1.26M (+7.2% by 2030)
- **Annual**: 1.4% growth (±0.5% CI)
- **Accuracy**: MAPE 12.06% (acceptable for 3-5 year horizon)
- **Interpretation**: Market maturation; stabilizing at low single-digit growth

## Technical Stack

```
Python 3.10+
├── Data: Pandas, NumPy
├── Visualization: Matplotlib, Seaborn
├── Time Series: Prophet (PyMC)
├── ML Validation: Scikit-learn
├── Office: python-pptx
└── Utilities: Openpyxl
```

## File Structure

```
international-student-eda/
├── README.md
├── data/
│   └── OD25_Intl-Student-Census_Tables__1_.xlsx
├── notebooks/
│   └── Open_doors_EDA.ipynb
├── src/
│   ├── step1_data_loading.py
│   ├── step2_enhanced_charts.py
│   ├── step3_new_visualizations.py
│   ├── final_step_prophet_forecasting.py
│   └── visualization_utilities.py
├── outputs/
│   ├── charts/ (16+ visualizations)
│   ├── presentations/ (editable PowerPoint slides)
│   └── reports/ (documentation)
└── requirements.txt
```

## Model Performance

| Metric | Value | Interpretation |
|--------|-------|-----------------|
| MAPE | 12.06% | Good; acceptable for 3-5 year forecasts |
| MAE | ±130,265 | ~11% of mean enrollment |
| RMSE | ±145,130 | ~12% of mean; symmetric distribution |
| R² | ~0.90 | Explains 90% of variance |

### Performance by Period
- **2015-2019**: MAPE 8-10% (excellent)
- **2020-2021**: MAPE 20-25% (structural break)
- **2022-2025**: MAPE 10-12% (good)

## Usage

```bash
# Clone
git clone https://github.com/yourusername/international-student-eda.git
cd international-student-eda

# Install
pip install -r requirements.txt

# Run EDA
jupyter notebook notebooks/Open_doors_EDA.ipynb

# Generate forecasts
python src/final_step_prophet_forecasting.py
```

## Limitations

### Univariate Approach
- No causal inference; correlation ≠ causation
- Cannot quantify policy impacts (visa restrictions, economic cycles)
- Relies on historical patterns only

### Data Constraints
- Annual aggregation (no seasonal variation)
- Survivorship bias (enrolled students only; application pipeline excluded)
- No demographic/psychographic data (motivations, decision factors)
- No integration of exchange rates, visa policy, GDP

### Forecast Risk
- 95% CI widening: ±160K by 2030
- Assumes no structural breaks post-2025
- Vulnerable to pandemic-scale disruptions

## Future Work

### Model Enhancement
1. **External Regressors**: Add visa policy, GDP, exchange rates, mobility index → MAPE 9-10%
2. **Segmented Models**: Separate forecasts by country (India, China, Mexico) and academic level → MAPE 7-9%
3. **Ensemble**: Combine Prophet + ARIMA + Exponential Smoothing → Robustness improvement

### Advanced Analytics
4. **Causal Analysis**: Quantify policy impacts via regression discontinuity
5. **Scenario Planning**: What-if models for policy changes, economic shocks
6. **Anomaly Detection**: Early warning system for enrollment anomalies

### Operational
7. **Continuous Monitoring**: Quarterly updates and MAPE tracking
8. **Decision Tools**: Interactive dashboards for enrollment and budget planning
9. **Benchmarking**: Peer institution comparison framework

## References

- Open Doors Institute. (2025). *International Student Census*. https://www.iie.org/opendoors
- Taylor, S. J., & Letham, B. (2018). Forecasting at scale. *The American Statistician*, 72(1), 37-45.
- Box, G. E. P., & Jenkins, G. M. (1970). *Time Series Analysis: Forecasting and Control*.

## License

MIT License - see LICENSE file for details.

---

**Status**: Analysis Complete | Model Operational  
**Last Updated**: March 2026
