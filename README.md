# Volatility Modeling for Nifty 50

---

## Introduction
This project focused on modeling and forecasting the one-day-ahead volatility of the Nifty 50 index using an ARCH–GARCH framework. The forecasts of conditional variance were further translated into 99% Value-at-Risk (VaR) estimates, offering a risk-management lens on short-term stock market fluctuations. The project demonstrates how financial time-series techniques can quantify volatility clustering and provide forward-looking measures of downside risk.

---

## Background
Equity indices like the Nifty 50 exhibit stylized facts that challenge traditional constant-variance models. Market returns are generally mean-reverting around zero, but volatility tends to cluster: tranquil periods alternate with sudden spikes driven by shocks. To capture such dynamics, Engle’s ARCH and Bollerslev’s GARCH models allow variance to evolve conditionally on past innovations. This makes them especially suited for volatility forecasting and for risk metrics such as Value-at-Risk. The project applied this methodology to Indian equity markets, focusing on the Nifty 50 index.

---

## Problem Statement
The objective was to develop a robust model that could forecast one-day-ahead volatility of the Nifty 50 index, while effectively capturing volatility clustering and short-memory effects. A second goal was to translate conditional variance into a forward-looking measure of downside risk through 99% Value-at-Risk. Finally, the project sought to evaluate the relative performance of ARCH and GARCH specifications in terms of forecasting accuracy.

---

## Terminologies
- **ARCH (Autoregressive Conditional Heteroskedasticity):** A volatility model where conditional variance depends on past squared shocks, capturing volatility clustering in returns.  
- **GARCH:** An extension of ARCH that includes lagged variances in addition to lagged squared shocks, allowing persistence in volatility.
- **Value-at-Risk (VaR):** A widely used financial risk metric that estimates the maximum expected loss over a given time horizon at a chosen confidence level (99% in this project).
- **ARCH-LM Test:** A statistical test used to detect ARCH effects in residuals. Rejection of the null hypothesis indicates the presence of volatility clustering.

---

## Dataset
The dataset comprised daily closing prices of the Nifty 50 between 29 May 2021 and 29 May 2025, amounting to roughly 995 trading days. The first 985 days were used as the training set for model fitting and diagnostics, while the last 10 days were reserved for testing and evaluation. Daily log-returns were computed from closing prices, sourced from the National Stock Exchange. The series showed an overall uptrend with occasional corrections, mean-reverting returns around zero, and distinct volatility clustering during episodes such as early 2022 and mid-2024.

---

## Data Analysis & PreProcessing
Stationarity was confirmed using the Augmented Dickey-Fuller test, which yielded a test statistic of -31.59 with a p-value below 0.01. A t-test for the mean indicated that the average daily return was not significantly different from zero, supporting the choice of a constant mean specification. Autocorrelation analysis showed no significant ARMA structure in returns, but the squared residuals displayed strong autocorrelation at lag one, pointing to ARCH effects. This confirmed the need for volatility models beyond constant variance.

---

## Methodology
The ARCH-LM test revealed highly significant ARCH effects, with an LM statistic of 101.55 and a p-value close to zero. On this basis, two models were fitted. The ARCH(1) model specified conditional variance as a function of the previous shock squared, while the GARCH(1,1) model allowed variance to depend on both the lagged squared shock and lagged variance, capturing persistence in volatility. Both models were evaluated using Root Mean Squared Error (RMSE) and Mean Absolute Error (MAE), and their one-day-ahead forecasts were converted into 99% Value-at-Risk estimates for market risk assessment.

---

## Diagnostics
Before finalizing the volatility models, diagnostic checks were performed to validate assumptions. The residuals of the mean equation were subjected to the ARCH-LM test, which strongly rejected the null hypothesis of no ARCH effects. The LM statistic of 101.55 with a p-value close to 0 confirmed the presence of volatility clustering, justifying the use of ARCH-family models.

The autocorrelation function of squared residuals exhibited a sharp spike at lag 1 followed by rapid decay, indicating short-memory volatility dynamics. This pattern suggested that a low-order ARCH or GARCH model would suffice. Residual plots from both ARCH(1) and GARCH(1,1) specifications confirmed that the conditional variance models effectively absorbed much of the heteroskedasticity, though small clusters of volatility remained visible.

Comparing models, the ARCH(1) residuals showed cleaner white-noise behavior than GARCH(1,1), which retained slightly more persistence. Together, these diagnostics supported the choice of ARCH(1) as a parsimonious yet effective specification for forecasting Nifty 50 volatility.

---

## Results & Discussion
The ARCH(1) model achieved lower prediction errors, with RMSE of 0.003 and MAE of 0.0018, compared to the GARCH(1,1) model, which recorded RMSE of 0.004 and MAE of 0.0036. This suggests that short-memory volatility captured by ARCH was sufficient for this dataset, whereas GARCH introduced persistence but at the cost of slightly higher error. Importantly, the volatility forecasts provided meaningful risk measures. For instance, on 15 May 2025, the 99% Value-at-Risk was estimated at -2.802%, implying that there is only a 1% chance of experiencing a daily loss greater than this value.

---

## Conclusion & Future Scope
The project demonstrated that ARCH and GARCH models are effective tools for capturing volatility clustering in Indian equity markets and for producing forward-looking risk metrics. The ARCH(1) model, in particular, offered superior forecasting accuracy for this dataset, while both models highlighted the importance of accounting for conditional variance dynamics. In the future, extending the testing horizon, incorporating asymmetric volatility models, and enriching the feature set with macroeconomic indicators could improve predictive power. Further work could also expand into multi-day horizon VaR forecasting and stress-testing under market shocks, strengthening the relevance of this approach for portfolio and risk management. Expanding the testing window and experimenting with variants such as EGARCH or GJR-GARCH would also provide a more comprehensive assessment.

---

## Contributors
- Anirudh A
- Kowshik M
- Moneesh B
- Anushka

---
