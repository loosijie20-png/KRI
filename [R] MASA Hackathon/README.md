# MASA Hackathon: Structural Climate Risk in the Reinsurance Layer

## Project Background

**Context**

Submitted for the MASA Hackathon, the flagship event of the Malaysian Actuarial Student Association (MASA). A group project by team OnzLah from Universiti Malaya, involving 5 members.

**Problem statement**

Historical loss data can no longer adequately capture climate risk in the reinsurance industry, as greenhouse gas (GHG) emissions shift the frequency, severity and geographic distribution of natural-disaster losses. The project models GHG emissions intensity as an upstream climate-pressure signal for Thailand and Viet Nam, and traces its implications through reinsurance pricing and accumulation strategy.

## Objectives

1. Model GHG emissions intensity (Mt CO₂e per billion USD GDP) for Thailand and Viet Nam from structural drivers, and predict its 2024 value.
2. Compare the two countries' natural-disaster loss profiles in frequency, severity and loss per event, using EM-DAT economic losses as a proxy for insured-loss pressure.
3. Stress-test 2030 emissions intensity under baseline, mitigation and adverse energy-transition scenarios.
4. Translate the results into a scenario-based reinsurance strategy covering pricing, treaty capacity and risk transfer.

## Data Sources

| Dataset | Source / Link | Size (rows × cols) | Time period |
| --- | --- | --- | --- |
| World Development Indicators extract: 31 indicators for 11 ASEAN countries | [World Bank WDI](https://databank.worldbank.org/source/world-development-indicators) | 286 × 35 | 1999–2024 |
| World Development Indicators extract: land area | [World Bank WDI](https://databank.worldbank.org/source/world-development-indicators) | 286 × 5 | 1999–2024 |
| Annual natural-disaster events and economic losses, Thailand and Viet Nam | [EM-DAT, CRED (UCLouvain)](https://public.emdat.be/) | 25 × 11 | 2000–2024 |

## Key Findings

- **Renewable energy and energy intensity drive emissions intensity.** Higher renewable energy consumption lowers GHG/GDP (coefficient −0.005), while higher energy intensity raises it (coefficient 0.113); both are significant.
- **The two countries have different catastrophe-risk profiles.** Thailand is severity-driven, dominated by the 2011 floods (over USD 40 billion in economic losses), while Viet Nam is frequency-driven, with recurring storm and flood losses and a 2015 spike of about USD 6.95 billion.
- **Transition progress measurably changes 2030 emissions intensity.** The mitigation scenario lowers it by 5.82% for Thailand and 5.45% for Viet Nam, while the adverse scenario raises it by 5.65% and 5.09%.

**Model comparison**: validation period 2019–2023, sorted by MAPE.

| Model | RMSE | MAE | MAPE | R² |
| --- | --- | --- | --- | --- |
| **Dynamic Panel Fixed Effects** | 0.0464 | 0.0394 | **3.32%** | 0.9931 |
| Log-Linear Panel Fixed Effects | 0.0527 | 0.0444 | 3.60% | 0.9924 |
| ARIMA (country-wise) | 0.0896 | 0.0778 | 7.43% | 0.9681 |

**2030 stress test**: GHG/GDP in Mt CO₂e per billion USD GDP, with the Transition Risk Index (TRI) anchored at 100 under the baseline.

| Country | Baseline 2030 | Mitigation 2030 | Adverse 2030 | Mitigation TRI | Adverse TRI |
| --- | --- | --- | --- | --- | --- |
| Thailand | 0.7961 | 0.7498 (−5.82%) | 0.8411 (+5.65%) | 94.18 | 105.65 |
| Viet Nam | 1.2479 | 1.1799 (−5.45%) | 1.3115 (+5.09%) | 94.55 | 105.09 |

## Project Structure

```
[R] MASA Hackathon/
├── analysis.Rmd                                              # Code: cleaning, EDA, catastrophe analysis, modelling
├── analysis.html                                             # Knitted output of analysis.Rmd
├── P_Data_Extract_From_World_Development_Indicators-6.xlsx   # Raw WDI extract: 31 indicators
├── P_Data_Extract_From_World_Development_Indicators-7.xlsx   # Raw WDI extract: land area
├── thailand_vietnam_emdat_annual_disaster_trends.xlsx        # EM-DAT annual disaster events and losses
├── WDI_cleaned.xlsx                                          # Cleaned WDI dataset
├── report.pdf                                                # Submission report
└── README.md
```

## Skills I Learned

**Technical skills**

- Exploratory data analysis: year-on-year growth, energy-mix and renewable-energy trends, and catastrophe frequency and severity analysis
- Time-series modelling: log-linear and dynamic panel fixed-effects regression with an ARIMA benchmark, using a strict time-based train, validation and forecast split
- Scenario stress testing: 2030 projections under mitigation and adverse scenarios.

## My Contribution

- Built and compared three models (log-linear panel fixed effects, dynamic panel fixed effects and a country-wise ARIMA benchmark) on a strict time-based split: 1999–2018 training, 2019–2023 validation and 2024 forecast.

* Built and deployed an interactive Shiny dashboard that forecasts 2030 GHG/GDP emissions intensity for Thailand and Viet Nam from the dynamic panel model. Live at [loosijie.shinyapps.io/masa2](https://loosijie.shinyapps.io/masa2/).

## Challenges & Lessons Learned

| Challenge | How it was addressed |
| --- | --- |
| No public insured-claims data for Thailand or Viet Nam | Used EM-DAT economic losses as a proxy for insured-loss pressure, filtered to climate-related disasters only |
| Uneven missing data across WDI countries and indicators | Dropped Timor-Leste, Brunei Darussalam and indicators above 40% missing; imputed the rest within each country |
| Large difference in economic size between Thailand and Viet Nam | Used GHG emissions per billion USD GDP as the target instead of absolute emissions |
| Risk of data leakage in time-series forecasting | Used a time-based split (1999–2018 train, 2019–2023 validation, 2024 forecast) and within-country lags |
