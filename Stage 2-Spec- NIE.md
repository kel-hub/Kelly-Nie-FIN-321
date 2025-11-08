# Technical Specification (Scenario #2)

**Created by:** [Kelly Nie]  
**Updated by:** [Kelly Nie]  
**Date Created:** [November 7, 2025]  
**Date Updated:** [November 7, 2025]  
**Version:** [0.0]
**LLM Used:

**Role:** Financial Analyst / Treasury Analyst  
**Audience:** CFO or Director of Treasury  

**Purpose:** Provide a professional, quantitative specification outlining the analytical structure for evaluating FX hedging alternatives.

---

## 1. Problem Statement

Our company expects to receive a €8,000,000 foreign‑currency receivable in 12 months from a European customer. Because we report in USD, we are exposed to FX risk from potential movements in the EURUSD exchange rate. A weaker euro reduces the USD value of proceeds, creating a potential revenue shortfall. This Stage 2 specification defines the technical modeling framework for quantifying, comparing, and evaluating hedging alternatives, including a forward, a money‑market hedge, and a EUR put option to support treasury decision‑making. The firm’s objective is to protect USD value while preserving upside when feasible and determine which hedge structure best aligns with risk management goals.

---

## 2. Inputs (Known Variables)

Create a clean, professional input table. This will become the foundation for your spreadsheet and future AI prompts.

| Variable | Description | Unit | Example | Source |
|-----------|-------------|------|----------|--------|
| `FC_AMT` | Foreign-currency receivable | EUR | 8,000,000 | Company data |
| `S₀` | Current EURUSD spot rate | USD/EUR | [1.0850] | Market data |
| `F₀` | 1-year EURUSD forward rate | USD/EUR | 1.0890 | Provided |
| `r_USD` | USD 1-year interest rate | % | [4.00%] | Market data |
| `r_EUR` | EUR 1-year interest rate | % | [3.00%] | Market data |
| `t` | Time to maturity | Years | 1 | Derived |
| `K_put` | EUR Put strike | USD/EUR | [1.0850] | Analyst choice |
| `K_call` | EUR Call strike | USD/EUR | [1.0850] | Analyst choice |
| `Premium_put` | Put premium | USD per contract | 0.021 | Scenario |
| `Premium_call` | Call premium | USD per contract | 0.026 | Scenario |

---

## 3. Assumptions & Constraints

We assume interest rates are simple annual yields and that the quoted forward represents a one‑year maturity. Exchange rates are quoted as USD per EUR. Option premiums are paid upfront in USD. Transaction costs, counterparty credit risk, margin requirements, early exercise, and liquidity effects are excluded. No interim cash flows are assumed. This framework is static and does not incorporate dynamic hedging. All inputs are treated as known and constant for modeling purposes.


---

## 4. Calculation Flow

1. Forward Hedge
   - Use the 1‑year forward rate (F₀) to lock in the USD value of €8,000,000.
   - Compute: €8,000,000 × F₀.
   - This gives a fixed USD amount to compare against other methods.

2. Money Market Hedge
   - Discount the €8,000,000 receivable using the EUR interest rate (r_EUR).
   - Convert the discounted euros to USD at today’s spot rate (S₀).
   - Invest the USD amount at the USD interest rate (r_USD) until maturity.
   - Use the final USD amount for comparison.

3. Option Hedge
   - Buy a EUR put with strike price K_put.
   - For each possible future EURUSD rate (S_T), calculate the payoff: max(K_put – S_T, 0).
   - Add the payoff to the unhedged proceeds and subtract the premium.
   - Compare across different future EURUSD scenarios.

4. Unhedged Case
   -  For each S_T, estimate USD outcome as €8,000,000 × S_T.
   -  Use this as the baseline for comparison.

5. Compare Results
   - Put all USD values from each method into a summary table.
   - Chart results to show differences in risk, cost, and upside.
---

## 5. Outputs

| Output | Description | Format | Purpose |
|---------|--------------|---------|----------|
| `USD_forward` | USD proceeds from forward hedge | Numeric | Certainty benchmark |
| `USD_mm` | USD proceeds from money market hedge | Numeric | Cross-check against forward |
| `USD_put` | USD proceeds from EUR put hedge | Table | Sensitivity & protection |
| `USD_call` | USD proceeds from EUR call hedge | Table | Optional upside case |
| `Chart_1` | Hedge outcomes vs. S_T | Line chart | Visual comparison |
| `Summary` | Written conclusion | 1–2 paragraphs | Executive-ready takeaway |


---

## 6. Sensitivity Plan
We will change the EURUSD rate at maturity (S_T) in a range around today’s rate, for example, from 0.95×S₀ to 1.05×S₀ in small steps. For each S_T, we will calculate how much USD we would get with each hedge strategy and put the results in a comparison table. We will also make a simple line chart to show how each hedge performs at different exchange rates. This helps us see which strategies protect against risk and which allow some upside.

---

## 7. Limitations & Next Steps
We are not including trading fees, early option exercise, or credit risk. We also assume no other cash flows before maturity. These simplifications make the model easier but less realistic. Next, we will build the spreadsheet using this plan, test different exchange rate scenarios, and see which hedge works best. Finally, we will prepare the results to share with management.

