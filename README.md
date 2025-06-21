# 📈 AdEase Wikipedia Page Views Forecasting Case Study

## 🏢 About AdEase
**AdEase** is a cutting-edge digital advertising company leveraging AI to optimize ad placement. With the help of its Design, Dispense, and Decipher AI modules, it delivers effective, efficient, and affordable digital ads. The goal is to maximize engagement (clicks) while minimizing advertising costs.

## 🎯 Objective
The task is to forecast Wikipedia page views to assist AdEase in optimizing ad placements across multilingual content. With 145,000+ Wikipedia articles tracked over 550 days, we aim to:

- Forecast daily page views for articles in **seven languages**.
- Use advanced time series models (ARIMA, SARIMAX, Prophet).
- Incorporate **exogenous events** (like marketing campaigns) into the forecast.
- Compare language-wise forecasting accuracy for strategic ad decisions.

## 📁 Dataset Description

### 🗂️ Files:
- [`train_1.csv`](https://drive.google.com/file/d/1jf-KeOpyQBD40FgmhBxkoB7Yb2qV_RQN/view?usp=drive_link): Daily view counts for 145,000+ Wikipedia pages.
- [`Exog_Campaign_eng.csv`](https://drive.google.com/file/d/1-faQjZ8WBqxHVZUgtqb-m0u-7I_5oqQR/view?usp=drive_link): Binary indicator of campaign days (exogenous variable for English pages only).

### 🧾 Page Name Format:
Each row name is formatted as:  
`Page_Title_Language.wikipedia.org_AccessType_AccessAgent`  
From this, we extracted:
- **Page Title**
- **Language** (e.g., en, fr, ja)
- **Access Type** (desktop/mobile)
- **Access Agent** (all-access/spider/user)

## 🔬 Exploratory & Modeling Approach

### 1. 📊 EDA & Feature Engineering
- Parsed page strings into structured columns.
- Analyzed access type, device usage, and origin agents.
- Created `long-format` time series for modeling.
- Handled nulls via interpolation; removed sparse columns.
- Detected and addressed non-stationarity using **ADF Test** and differencing.

### 2. ⏳ Time Series Decomposition
- Seasonal and trend components identified, especially in English and Japanese data.
- Decomposed series using STL for Prophet and SARIMAX insights.

### 3. 📈 Modeling
- **ARIMA**: Classical baseline forecasting.
- **SARIMAX**: Integrated external campaign data for English pages.
- **Prophet**: Used for high-seasonality pages across languages.

### 4. 📌 Hyperparameter Tuning
- Performed grid search for optimal `(p, d, q)` and seasonal orders in SARIMAX.
- Evaluated using **MAPE**, **AIC**, and **visual residual diagnostics**.

## 📊 Key Insights

- **English Dominance**: English pages received the highest views—ideal for ad placement.
- **Access Origin**: 76% of access came via agents (real users), not spiders.
- **Access Type**: Over 75% of views were via **mobile-web** and **all-access** devices.
- **wikipedia.org Relevance**: ~88% of traffic came from `wikipedia.org` domains.
- **Stationarity**: Languages like Russian and Spanish were already stationary; others needed differencing.
- **Seasonality Detected**: Clear patterns in English, Japanese, and Chinese time series.
- **Best Forecasting Models**:
  - English (SARIMAX + Campaign): MAPE = **4.05%**
  - Chinese: MAPE = **3.07%**
  - Russian: MAPE = **4.16%**
  - Spanish: MAPE = **8.56%** (needs improvement)
- **Campaign Influence**: Campaign days spiked traffic significantly on English pages.

## 💡 Recommendations

1. **Prioritize English Pages**  
   High traffic + low forecasting error make them optimal for ad targeting.

2. **Target All-Access & Mobile Users**  
   These two types contribute to 75%+ of total views—ideal for ad strategy alignment.

3. **Leverage Seasonality**  
   Embed seasonal trends in models (e.g., Prophet, SARIMAX) for improved accuracy.

4. **Use SARIMAX for Campaign Integration**  
   Proven effective with exogenous campaign events, especially in English forecasts.

5. **Retrain Models Regularly**  
   Keep forecasts updated with latest behavior to ensure reliability.

6. **Improve Spanish Forecasting**  
   High MAPE (~8.56%) suggests need for deeper seasonal analysis or campaign overlays.

7. **Optimize Ad Timing During Campaigns**  
   Focused content placement during traffic spikes can yield higher engagement.


## 🛠️ Tools & Libraries Used

- **Python**: `pandas`, `numpy`, `matplotlib`, `seaborn`
- **Forecasting**: `statsmodels (ARIMA, SARIMAX)`, `prophet`
- **Tuning**: `itertools`, `grid search`
- **Diagnostics**: `ADF Test`, `ACF/PACF`, `MAPE`, `AIC`

## 📄 Final Report

All model code, visualizations, and detailed analysis are included in the PDF below:  
📎 [`AdEase_case_study_akansha_saini.pdf`](https://github.com/AkanshaSaini761/AdEase_Time_Series_Case_Study/blob/main/AdEase_case_study_akansha_saini.pdf)
