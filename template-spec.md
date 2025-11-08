# [Spec ] – Technical Specification Template

**Created by:** [Kelly Nie]  
**Updated by:** [Kelly Nie]  
**Date Created:** [November 7, 2025]  
**Date Updated:** [November 7, 2025]  
**Version:** [0.0]
**LLM Used:"" [LLM] (optional if LLm used)

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

> *Tip:* Keep labels short and standardized. Think like a financial modeler — these names should become variable names, spreadsheet inputs, or prompt parameters later.

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

List expected results from the model. These become your **spreadsheet outputs**, **AI prompt targets**, and **Stage 5 discussion points**.

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

Define how you will test and visualize FX outcomes.

Example:
> Vary EURUSD spot at maturity \(S_T\) from 0.95×S₀ to 1.05×S₀ in increments of 0.01.  
> For each value, compute USD proceeds under all hedge strategies.  
> Present results as a comparison table and line chart.

> *Professional analysts always test sensitivity — it shows how robust their recommendations are.*

---

## 7. Limitations & Next Steps

Briefly note any analytical limits (e.g., volatility ignored, credit risk excluded) and outline your immediate next step (e.g., model build in Stage 3).

Example phrasing:
> This specification does not incorporate implied volatility or transaction costs. The next phase will involve constructing an Excel model implementing this logic to quantify results under each hedge structure.

---

# 🧭 Writing a Strong Specification

**Your spec should:**
- **Communicate like a professional:** clear, structured, and jargon-free.  
- **Think one stage ahead:** your spec should feed directly into your Excel build or AI prompt.  
- **Be internally consistent:** variables, labels, and steps must align.  
- **Be reproducible:** a new analyst should be able to implement your plan without your help.  
- **Be executive-relevant:** the CFO should understand *what you’re doing* and *why it matters*.

---

## 🔗 How This Sets You Up for Later Stages

| Stage | What This Spec Enables |
|-------|------------------------|
| **Stage 3** | Each “Input” and “Output” becomes a spreadsheet cell or named range. |
| **Stage 4** | Your “Calculation Flow” becomes an AI prompt instruction block. |
| **Stage 5** | Your “Outputs” drive the interpretation and recommendation. |

> *Treat your specification as the bridge between business insight and technical execution — the CFO should be confident your plan is sound even before seeing the numbers.*
