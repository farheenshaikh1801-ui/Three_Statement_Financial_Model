# NIKE, Inc. (NYSE: NKE) — 3-Statement Financial Model

A fully linked three-statement financial model (Income Statement, Balance Sheet and Cash Flow Statement) for **NIKE, Inc.**, built in Excel. It covers **five years of actuals (FY2022–FY2026)** and **five years of forecasts (FY2027–FY2031)**, with a segment-level revenue build and a **Bear / Base / Bull scenario switch**.

> All figures are in **USD millions** unless stated otherwise. Nike's fiscal year ends on **May 31**.

---

## Contents

| File | Description |
|---|---|
| `Nike_3-_Statement_Model_Farheen_Ahmed.xlsx` | The Excel model (3 worksheets, fully formula-driven) |
| `README.md` | This document |

---

## Model Structure

The workbook has three tabs that feed into each other:

```
Notes (assumptions & scenario switch)
   │
   ├──► Revenue_Build (segment revenue forecast)
   │          │
   │          ▼
   └──► 3_statement_model (IS ► BS ► CF ► schedules ► charts)
```

### 1. `Notes` — Assumptions & Scenario Control
The single place where forecast drivers live.

- **Scenario selector** (cell `C5`): `1 = Bear`, `2 = Base`, `3 = Bull`. Every scenario-sensitive driver uses `CHOOSE()` to pick the active case.
- **Revenue growth by segment**: North America, EMEA, Greater China, APLA and Converse, set separately for FY2027, FY2028 and FY2029–31.
- **Margins & opex**: gross margin, demand creation expense and operating overhead as % of revenue.
- **D&A, capex & stock-based compensation** as % of revenue.
- **Working capital**: DSO, DIO, DPO, prepaid/other current assets, accrued liabilities and taxes payable.
- **Tax**: effective tax rate.
- **Debt & interest**: cost of debt (FY26 cash interest ÷ average debt) and interest income on cash and short-term investments.
- **Capital returns & shares**: dividend-per-share growth, share buybacks, repurchase price, employee share issuance, dilution and option proceeds.

Each driver records its unit and its basis (e.g. "5-yr average", "FY25–26 average", "Management guidance").

### 2. `Revenue_Build` — Segment Revenue Forecast
- Builds total NIKE, Inc. revenue bottom-up from geographic segments: **North America, EMEA, Greater China, APLA, Global Brand Divisions, Converse and Corporate**.
- Shows YoY growth and % of total revenue by segment.
- Includes a historical **product view** (Footwear, Apparel, Equipment) taken from the 10-K revenue note.
- Built-in checks reconcile segment totals to the income statement and to the product-view total.

### 3. `3_statement_model` — Integrated Financial Statements
| Section | What it contains |
|---|---|
| **Assumptions summary** | Historical ratios computed from the actuals next to forecast drivers pulled from `Notes` |
| **Income Statement** | Revenue → COGS → Gross Profit → Demand creation & overhead → EBIT → Interest & other → Pre-tax income → Tax → Net income; EPS (basic and diluted), share count, dividends per share |
| **Balance Sheet** | Cash, ST investments, AR, inventory, PP&E, leases, intangibles, goodwill; debt, AP, accrued liabilities, taxes payable; equity roll-forward |
| **Cash Flow Statement** | Operating (net income + non-cash items + working capital changes), investing (capex), financing (debt, buybacks, dividends); free cash flow, FCF margin, FCF conversion |
| **Supporting schedules** | Working capital schedule, PP&E/depreciation roll-forward, debt and interest schedule |
| **Charts** | Revenue vs. gross margin; operating, investing and financing cash flows |

---

## How the Statements Link

- **Net income** from the Income Statement flows into **Retained earnings** (less dividends and buybacks) and is the starting line of the **Cash Flow Statement**.
- **Working capital** balances are driven by days metrics (`AR = Revenue × DSO / 365`, `Inventory = COGS × DIO / 365`, `AP = COGS × DPO / 365`), and their year-over-year changes flow into operating cash flow.
- **PP&E** rolls forward: `Opening + Capex − D&A = Closing`.
- **Debt** rolls forward through the debt schedule (scheduled repayments of $2.0bn in FY2027 and $1.5bn in FY2030). **Interest expense** is calculated on opening debt, net of interest income on opening cash and short-term investments, so the model has **no circular references**.
- **Ending cash** from the Cash Flow Statement becomes **Cash** on the Balance Sheet.

### Integrity Checks
| Check | Location | Expected |
|---|---|---|
| Total Assets = Total Liabilities + Equity | `3_statement_model` row 99 | `TRUE` for every year |
| CF ending cash − BS cash | `3_statement_model` row 138 | `0` for every year |
| Segment revenue − IS revenue | `Revenue_Build` row 18 | `0` |
| Product-view revenue − segment Nike Brand revenue | `Revenue_Build` row 40 | `0` |

All checks pass in every scenario.

---

## Scenario Summary

| Metric | Bear | **Base** | Bull |
|---|---:|---:|---:|
| Revenue FY2027 ($mm) | 41,562 | **42,952** | 44,343 |
| Revenue FY2031 ($mm) | 45,240 | **50,510** | 56,254 |
| Gross margin (forecast) | 43.4% | **43.9%** | 44.4% |
| EBIT margin FY2031 | 8.2% | **9.2%** | 10.2% |
| Net income FY2031 ($mm) | 2,968 | **3,871** | 4,986 |
| Diluted EPS FY2027 ($) | 1.74 | **2.16** | 2.63 |
| Diluted EPS FY2031 ($) | 1.96 | **2.79** | 3.95 |
| Free cash flow FY2031 ($mm) | 3,581 | **4,477** | 5,590 |

**How the scenarios differ:** Bear and Bull move revenue growth by ±3 pts in FY2027 and ±2 pts in FY2028–31, and margins by ±0.5 pts, relative to Base. Inventory days, the tax rate, dividend growth and buybacks are also flexed by scenario (for example, Bear freezes the dividend and pauses buybacks).

### Base-Case Snapshot
| | FY2026A | FY2027E | FY2031E |
|---|---:|---:|---:|
| Revenue ($mm) | 46,398 | 42,952 | 50,510 |
| Revenue growth | 0.2% | −7.4% | 4.7% |
| EBIT margin | 8.2% | 9.2% | 9.2% |
| Net income ($mm) | 3,108 | 3,183 | 3,871 |
| Diluted EPS ($) | 2.10 | 2.16 | 2.79 |
| Free cash flow ($mm) | 2,184 | 4,904 | 4,477 |

---

## Key Base-Case Assumptions

- **FY2027 reset:** Greater China (−25%), Converse (−30%), EMEA (−10%) and APLA (−6%) decline, while North America is flat. These figures are guided by Q1 FY2027 results and management commentary.
- **Recovery (FY2029–31):** North America +5%, EMEA +4.5%, Greater China +2.5%, APLA +6%, Converse flat.
- **Gross margin:** 5-year average (FY22–26).
- **Operating overhead and demand creation:** FY25–26 average as % of revenue.
- **Capital returns:** dividend per share grows 2.5% a year and buybacks run at $1.0bn a year at $35.30/share (NKE close on 14-Oct-2026).
- **Held flat at FY2026 levels:** short-term investments, lease ROU assets and liabilities, intangibles, goodwill, and deferred taxes and other assets/liabilities. These are non-operating or not reliably forecastable.

---

## How to Use

1. Download the `.xlsx` file and open it in **Microsoft Excel** (LibreOffice Calc and Google Sheets also work).
2. Go to the **`Notes`** tab and set cell **`C5`** to `1` (Bear), `2` (Base) or `3` (Bull).
3. To test your own views, change the inputs in the **Bear / Base / Bull columns (G:I)** or the single-value drivers in column **C**.
4. Review the results in **`3_statement_model`** and confirm the balance and cash checks still pass.

**Note:** historical columns (FY2022–FY2026) hold reported figures. Forecast columns (FY2027–FY2031) are entirely formula-driven, so change the inputs in `Notes` rather than editing the forecast cells.

---

## Data Sources

- NIKE, Inc. **Form 10-K** filings (FY2022–FY2026)
- NIKE **FY2027 Q1** earnings results and press releases
- Management guidance and *Business Today* coverage
- 3-month U.S. T-bill rate (4.28%), used as the reference for interest income on cash

**Basis of preparation:** historical figures for FY2022–FY2026 come from reported financials. Estimates are guided by Q1 FY2027 results, press releases and management guidance.

---

## Skills Demonstrated

- Integrated three-statement financial modelling
- Segment-level (bottom-up) revenue forecasting
- Working capital, PP&E and debt schedules
- Scenario analysis with `CHOOSE()`-driven switches
- Model integrity checks and reconciliation
- Financial data visualisation in Excel

---

## Author

**Farheen Ahmed**

---

## Disclaimer

This model is an independent educational and portfolio project. It is **not investment advice** and is not affiliated with or endorsed by NIKE, Inc. Forecasts are based on the author's assumptions and may differ materially from actual results.
