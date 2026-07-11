# DCF-Valuation-Model
# TAMO – Financial Statement & Valuation Analysis (README)

**File:** `TAMO-_FS_Analysis__1_.xlsx`
**Subject Company:** Tata Motors Ltd. (NSE: TATAMOTORS)
**Data source:** Screener.in (raw financial data export) and manually sourced market comps
**Purpose:** End‑to‑end DCF (Discounted Cash Flow) valuation of Tata Motors — from raw historicals to a per‑share intrinsic value estimate.

---

## 1. What this workbook does

This is a self-contained equity valuation model. It takes Tata Motors' historical financial statements, derives operating and return metrics, estimates a discount rate (WACC) using peer comparables, projects future free cash flows, and discounts them back to arrive at an intrinsic **equity value per share**, which is then compared against the current market price to flag a potential discount/premium.

---

## 2. How the sheets fit together (recommended reading order)

| Order | Sheet | Role |
|---|---|---|
| 1 | **Data Sheet** | Master input sheet pulled from Screener.in — company metadata, current share price, share count, face value. *Locked/reference — not meant to be edited.* |
| 2 | **RawFS** | Raw financial statement line items as scraped from source, before cleanup. |
| 3 | **Historical Data** | Cleaned, structured historical Income Statement, Balance Sheet, and Cash Flow Statement (FY2013–FY2022 + LTM), with common-size (% of Sales) ratios computed alongside each line. |
| 4 | **Cash Flow Data** | Supplementary historical cash flow breakdown (Operating activities: profit, receivables, inventory, payables, etc.), FY2011–FY2018. |
| 5 | **Ratio Analysis** | Growth and profitability ratios (Sales Growth, EBITDA Growth, EBT Growth, etc.) derived from the historical financials. |
| 6 | **Intrinsic growth** | Calculates ROIC (Return on Invested Capital), Reinvestment Rate, and the resulting **Intrinsic Growth Rate**, which feeds the DCF's near-term growth assumption. |
| 7 | **Beta comp** / **DATA1** | Peer company data (Debt, Debt/Equity, Market Cap) for Cummins India, Hitachi Energy, CG Power, ABB, Polycab, used to derive an industry Beta. |
| 8 | **WACC** | Full cost-of-capital build: peer-based unlevered/relevered Beta, Cost of Debt, Cost of Equity (CAPM), capital structure (current vs. target), and the final **Weighted Average Cost of Capital**. |
| 9 | **Rm** | Historical Nifty 50 annual returns (2000–2022) used to compute the **Return on Market / Equity Risk Premium** input for Cost of Equity in the WACC sheet. |
| 10 | **DCF** | The valuation engine — projects EBIT, tax-effects it, deducts reinvestment to get Free Cash Flow to Firm (FCFF), discounts each year at WACC (mid-year convention), computes Terminal Value, and rolls everything up to **Enterprise Value → Equity Value → Value per Share**, compared to the current market share price. |

> Sheets named with a trailing **`>`** (`DCF>`, `Financials>`, `Data>`) are empty section-divider/navigation tabs used to visually group the sheets that follow them — they contain no data.

---

## 3. Key outputs

| Metric | Located in | What it represents |
|---|---|---|
| WACC | `WACC` sheet | Discount rate applied to future cash flows |
| Intrinsic Growth Rate | `Intrinsic growth` sheet | Near-term reinvestment-driven growth assumption for FCFF projections |
| Terminal Value | `DCF` sheet | Value of cash flows beyond the explicit forecast period (Gordon Growth) |
| Equity Value per Share | `DCF` sheet | Model's estimate of intrinsic value per Tata Motors share |
| Discount / Premium | `DCF` sheet | Gap between model's intrinsic value and the actual market share price |

---

## 4. Methodology notes

- **WACC** is built off peer-comparable unlevered Betas (auto companies + electricals peer set), relevered to Tata Motors' target capital structure, combined with CAPM-based Cost of Equity (Risk-Free Rate + Beta × Equity Risk Premium) and post-tax Cost of Debt.
- **Cost of Equity / Equity Risk Premium** is derived from historical Nifty 50 annual total returns (`Rm` sheet, 2000–2025) plus an assumed dividend yield.
- **Growth rate** for the forecast period is derived intrinsically: `Growth = ROIC × Reinvestment Rate`, computed from 4-year historical averages (`Intrinsic growth` sheet), rather than assumed arbitrarily.
- **FCFF** is projected as `EBIT × (1 - Tax Rate) - Reinvestment`, discounted using a **mid-year convention** to reflect cash flows arriving throughout the year rather than at year-end.
- **Terminal Value** uses the Gordon Growth (perpetuity) method: `FCFF(n+1) / (WACC - Terminal Growth Rate)`.
- **Equity Value** = Enterprise Value (PV of FCFF + PV of Terminal Value) **+ Cash − Debt**, then divided by shares outstanding.

---

## 5. Important caveats / things to check before relying on this model

- Several **negative Free Cash Flow years** and a negative resulting Enterprise Value appear in the current `DCF` sheet output — this typically signals either (a) genuinely depressed near-term profitability for Tata Motors in the base year used, or (b) an assumption (growth rate, reinvestment rate, or tax rate) that needs revisiting. Treat the current per-share output as a **working draft**, not a final number.
- The **Reinvestment Rate** and **Intrinsic Growth Rate** in FY2019–FY2022 are volatile/negative in places, driven by swings in EBIT and working capital — worth sanity-checking against Tata Motors' actual capex and business cycle (e.g., JLR performance, COVID-19 impact) during those years.
- Peer comp sets differ slightly between the `Beta comp`, `DATA1`, and `WACC` sheets (company lists don't fully match) — worth reconciling to a single consistent peer group.
- The `Data Sheet` tab is sourced directly from Screener.in and is explicitly marked "please do not make any changes to this sheet" — treat it as a locked input.
- All figures are in **INR**, generally in ₹ Crores, unless stated otherwise in a given sheet.

---

## 6. Suggested next steps if extending this model

1. Reconcile the peer comp lists across `Beta comp`, `DATA1`, and `WACC`.
2. Sensitize the DCF output to WACC and Terminal Growth Rate (build a 2-way data table).
3. Add a scenario toggle (Bull/Base/Bear) for the growth and margin assumptions.
4. Cross-check the negative FCFF years against Tata Motors' actual reported cash flow statements to confirm the base-year figures are appropriate for a forward projection.
