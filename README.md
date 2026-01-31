# Repo-Rate-VAR-analysis
VAR analysis of repo rate, inflation, GDP, and money supply in India



### 🟢 Situation
The Reserve Bank of India (RBI) uses the repo rate as its primary monetary policy tool to control inflation, influence economic growth, and manage liquidity. However, macroeconomic variables such as repo rate, inflation, GDP growth, and money supply are dynamic, policy-driven, and interdependent.

Initial attempts to model these relationships using traditional regression and machine-learning techniques failed. The repo rate exhibited sharp policy-driven changes, and the data violated key regression assumptions such as normality, homoscedasticity, and independence.

---

### 🔵 Task
The main objective of this project was to build a **statistically valid and economically meaningful model** that can:

- Capture dynamic and lagged interactions among macroeconomic variables  
- Properly model the behavior of a policy instrument like the repo rate  
- Analyze how monetary policy shocks propagate through inflation, GDP growth, and money supply in India  


## ❓ Research Questions

This project is guided by the following research questions:

1. How does India’s repo rate dynamically interact with key macroeconomic variables such as inflation, GDP growth, and money supply?

2. Does a monetary policy shock to the repo rate significantly influence inflation in the short run?

3. What is the impact of repo rate changes on real economic activity, measured through GDP growth?

4. How does money supply (M3) respond to changes in the repo rate over time?

5. To what extent is the repo rate influenced by its own past values, indicating policy inertia?

These questions aim to understand the effectiveness and transmission mechanism of monetary policy in India using a dynamic time-series framework.

---

## 🧪 Hypotheses

Based on monetary theory and prior empirical evidence, the following hypotheses are tested:

- **H1:** The repo rate responds positively to inflation shocks, reflecting inflation-targeting behavior by the Reserve Bank of India.

- **H2:** A positive shock to the repo rate leads to a decline in GDP growth in the short run, indicating a contractionary effect of monetary tightening.

- **H3:** An increase in the repo rate reduces money supply (M3), leading to tighter liquidity conditions in the economy.

- **H4:** The repo rate is strongly influenced by its own lagged values, indicating gradual and inertial monetary policy adjustments.

These hypotheses are evaluated using a Vector Autoregression (VAR) framework along with impulse response and variance decomposition analysis.



## 📁 Data Collection & Preparation

All datasets used in this project were collected from official publications of the **Reserve Bank of India (RBI)**. RBI data ensures reliability, consistency, and direct relevance to Indian monetary policy analysis.

## 🛠️ Data Consolidation Method

RBI publishes macroeconomic indicators across multiple tables and formats. These raw files could not be directly used for econometric analysis.

Steps followed:

1. A master **monthly timeline** was created in Excel  
2. Individual RBI datasets were merged using **VLOOKUP**
3. Matching was done using **Month–Year keys**
4. All variables were aligned to a common monthly frequency

## 📊 Variables Used in Analysis

| Column Name | Description | Source |
|------------|------------|--------|
| d_repo_rate | Monthly change in repo rate | RBI – Select Economic Indicators |
| d_cpi_inflation | Monthly CPI inflation change | RBI – Select Economic Indicators |
| d_gdp_growth_rate | Monthly GDP growth rate | GDP Components |
| dlog_m3 | Log difference of money supply (M3) | RBI – Money Stock Measures |


## 🔄 Data Transformation

Macroeconomic time series typically exhibit trends and persistence. To ensure stationarity:

- First differencing was applied to:
  - Repo rate
  - Inflation
  - GDP growth
- Log-difference transformation was applied to:
  - Money supply (M3)
 
## 🧠 Methodology

This project follows a structured econometric workflow designed to correctly model the dynamic behavior of monetary policy variables in India.

---

### 1️⃣ Initial Modeling Attempt: Regression Framework

As a baseline, traditional regression and regularized machine-learning models were first applied:

- Ordinary Least Squares (OLS)
- Ridge Regression
- Lasso Regression
- Elastic Net

These models were estimated using transformed macroeconomic variables.

**Outcome:**
- Negative or near-zero R² values
- Non-normal and heteroskedastic residuals
- High sensitivity to policy-driven outliers
- Poor explanatory power

**Inference:**  
Static regression-based approaches are unsuitable for modeling the repo rate, which behaves as a discrete policy instrument rather than a smooth economic variable.

---

### 2️⃣ Stationarity Testing

Macroeconomic time series often exhibit trends and persistence. To ensure valid inference, stationarity was tested using the **Augmented Dickey-Fuller (ADF) test**.

- Variables were transformed using:
  - First differencing
  - Log-differencing (for money supply)
- ADF test results confirmed that all transformed variables are stationary

This step validated the use of time-series models.

---

### 3️⃣ Vector Autoregression (VAR) Model

After confirming stationarity, a **Vector Autoregression (VAR)** model was implemented.

**Why VAR?**
- Treats all variables as endogenous
- Captures dynamic and lagged interactions
- Does not impose restrictive theoretical structure
- Widely used in macroeconomic policy analysis

---

### 4️⃣ Lag Length Selection

The optimal lag length was selected using standard information criteria:

- Akaike Information Criterion (AIC)
- Bayesian Information Criterion (BIC)
- Hannan–Quinn Information Criterion (HQIC)

Based on these criteria, a **VAR with 8 lags** was selected to best capture the underlying dynamics.

---

### 5️⃣ Dynamic Analysis Tools

To interpret the estimated VAR model, two standard tools were used:

- **Impulse Response Functions (IRF):**  
  To analyze how shocks to the repo rate affect inflation, GDP growth, and money supply over time.

- **Forecast Error Variance Decomposition (FEVD):**  
  To measure the contribution of each variable’s shocks to the forecast uncertainty of other variables.

---


## 📈 Results

The Vector Autoregression (VAR) model provides meaningful insights into the dynamic interactions between the repo rate, inflation, GDP growth, and money supply in India. The key findings from the estimated VAR model, impulse response analysis, and variance decomposition are summarized below.

---

### 1️⃣ Repo Rate Dynamics

- The repo rate is strongly influenced by its own past values.
- Multiple lagged values of the repo rate are statistically significant.
- This indicates **high policy inertia**, where the Reserve Bank of India adjusts policy rates gradually rather than abruptly.

**Interpretation:**  
Monetary policy decisions are smooth and persistent, reflecting deliberate and cautious adjustments.

---

### 2️⃣ Impact on Inflation (CPI)

- Inflation is highly persistent and mainly driven by its own past values.
- Repo rate shocks have a **weak and short-lived effect** on inflation.
- No strong immediate disinflationary impact of repo rate hikes is observed.

**Interpretation:**  
Short-run inflation dynamics in India appear to be influenced more by structural and supply-side factors than by policy rate changes.

---

### 3️⃣ Impact on GDP Growth

- A positive shock to the repo rate leads to a **decline in GDP growth** in the short run.
- The contractionary effect persists for several periods before fading.

**Interpretation:**  
Monetary tightening effectively slows real economic activity, confirming the real-sector impact of interest rate policy.

---

### 4️⃣ Impact on Money Supply (M3)

- Money supply responds negatively to increases in the repo rate.
- Liquidity tightens following a policy rate hike.
- Money supply also shows strong persistence due to its own past values.

**Interpretation:**  
Monetary policy influences liquidity conditions, though the response occurs gradually over time.

---

### 5️⃣ Impulse Response Function (IRF) Summary

- Repo rate shocks lead to:
  - Immediate increase in the repo rate followed by gradual normalization
  - Small negative response of inflation
  - Noticeable decline in GDP growth
  - Reduction in money supply (M3)

These responses confirm the contractionary nature of monetary tightening.

---

### 6️⃣ Forecast Error Variance Decomposition (FEVD) Summary

- Over 80% of the variation in the repo rate is explained by its own shocks.
- Inflation variance is dominated by its own past shocks.
- GDP growth variance is influenced by both repo rate and inflation shocks.
- Money supply variance is largely self-driven, with a measurable contribution from repo rate shocks.

---

