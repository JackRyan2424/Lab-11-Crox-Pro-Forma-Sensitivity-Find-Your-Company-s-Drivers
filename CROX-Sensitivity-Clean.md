# CROX Sensitivity — Individual Submission

## 1. Model, inputs and method

This analysis uses my existing CROX pro forma and changes two independent operating inputs one at a time: revenue growth and gross margin. Each scenario starts from a fresh copy of the base assumptions and reruns all five years of linked statements. All other independent assumptions remain at base.

Sources: [Step 1 and range rationale](CROX-Sensitivity-Step-1.md), [full sensitivity report](CROX-Operating-Sensitivity.md), [audit data](CROX-Operating-Sensitivity-Data.json), and [model](crox_proforma.py).

| Independent input | Lower | Base | Higher | Affected years and units |
|---|---|---|---|---|
| Revenue growth | -2%, -1%, 0%, 0.5%, 0.5% | 0%, 1%, 2%, 2.5%, 2.5% | 2%, 3%, 4%, 4.5%, 4.5% | Annual growth for 2026–2030, respectively; +/-2 percentage points from base each year |
| Gross margin | 56.0% | 57.5% | 59.0% | Percentage of revenue in every year, 2026–2030; +/-1.5 percentage points from base |

These are judgment ranges informed by CROX history, not probabilities. Saved 2023–2025 revenue growth was 11.46%, 3.53%, and -1.50%; gross margin was 55.78%, 58.76%, and 58.33%. The growth range tests weaker and stronger recovery. The margin range approaches the historical low and modestly exceeds the historical high.

## 2. Visible sensitivity results

All statement outputs are USD millions; value is USD/share. Free cash flow is **FCFE**, defined as CFO minus capital expenditures plus net borrowing. Changes equal scenario minus base and are calculated before rounding.

| Run | 2030 EBIT | Change | 2030 FCFE | Change | Value/share | Change | Accounting checks |
|---|---:|---:|---:|---:|---:|---:|---|
| Lower revenue growth | 857.382 | -89.619 | 587.979 | -58.492 | 113.505 | -9.290 | PASS |
| Base revenue growth | 947.001 | 0.000 | 646.471 | 0.000 | 122.795 | 0.000 | PASS |
| Higher revenue growth | 1,043.961 | +96.960 | 709.380 | +62.909 | 132.727 | +9.931 | PASS |
| Lower gross margin | 922.296 | -24.704 | 627.846 | -18.626 | 119.188 | -3.607 | PASS |
| Base gross margin | 947.001 | 0.000 | 646.471 | 0.000 | 122.795 | 0.000 | PASS |
| Higher gross margin | 971.705 | +24.704 | 665.097 | +18.626 | 126.402 | +3.607 | PASS |

Every forecast FCFE is positive in these cases. Value per share is available under the existing model's conditional valuation assumptions: 12% cost of equity, 2.5% terminal growth, and 50.220 million shares. This is not an updated market valuation.

## 3. Compare output spans

Span means maximum minus minimum across valid lower/base/higher results, using unrounded values.

| Output | Revenue-growth span | Gross-margin span | Larger driver over these ranges |
|---|---:|---:|---|
| 2030 operating profit, EBIT (USD millions) | 186.579 | 49.409 | Revenue growth |
| 2030 FCFE (USD millions) | 121.401 | 37.252 | Revenue growth |
| Value per share (USD/share) | 19.221 | 7.214 | Revenue growth |

**Over these ranges, revenue growth produces the larger span for operating profit, FCFE, and value per share.** This does not establish that growth is inherently more important than margin. The growth test covers a 4-percentage-point lower-to-higher spread in each annual rate, while the margin test covers a 3-percentage-point spread. Growth also compounds over five years. Different reasonable ranges could change the ranking.

### Causal link using actual results

Increasing annual revenue growth by 2 percentage points in each forecast year raises 2030 EBIT by **$96.960 million**, FCFE by **$62.909 million**, and value by **$9.931 per share**. Revenue compounds from year to year, raising gross profit and operating profit. Taxes and reinvestment absorb part of the profit increase: capex remains 2% of revenue, and operating working-capital balances recalculate with sales and cost of sales. Depreciation also adjusts through the PP&E schedule.

Increasing gross margin from 57.5% to 59.0% raises 2030 EBIT by **$24.704 million** and FCFE by **$18.626 million**. The model links SG&A to gross profit at approximately 62.34%, so SG&A rises with gross profit and absorbs part of the benefit. Higher final-year FCFE also increases terminal value under the unchanged valuation assumptions.

## 4. Restored-base check and verification

| Output | Base before | Base after | Difference |
|---|---:|---:|---:|
| 2030 EBIT (USD millions) | 947.001 | 947.001 | 0.000 |
| 2030 FCFE (USD millions) | 646.471 | 646.471 | 0.000 |
| Value per share (USD/share) | 122.795 | 122.795 | 0.000 |
| Accounting checks | PASS | PASS | No change |

**Restored base: PASS.** Inputs and all five years of forecast statements match exactly before rounding. Display precision is 0.001 in the stated output units; independently rounded displayed values can differ from displayed changes by 0.001.

Checks performed:

- Only the selected independent input changes in each lower/higher case; linked quantities recalculate.
- Assets equal liabilities plus equity in each forecast year.
- Cash and equity rollforwards, CFO, and FCFE reconcile within 0.0000001 USD million.
- Cash remains at or above the $100 million floor.
- All 40 annual accounting checks across the initial base, six cases, and restored base pass.
- Independent arithmetic verifies EBIT, FCFE, signed DCF values, changes, and spans; 10 automated tests pass.
- The saved report agrees with the underlying audit data.

Invalid runs are excluded from spans. Negative cash flows would remain signed, and value would be unavailable if the existing valuation could not defensibly handle them. None of the prescribed cases was invalid.

## 5. Sensitivity — Learn on your own

### What is one-at-a-time sensitivity?

It changes one independent model assumption while holding all other independent assumptions at base, then recalculates the full linked model. This isolates that input's effect within the model. Calculated quantities such as revenue, inventory, taxes, and cash flow are allowed to change. It does not measure the combined effect of several assumptions changing together.

### How does the chosen input range affect the ranking?

A wider tested range can create a larger output span, even when the output's response to a small input change is modest. The timing and compounding of changes matter too. Here, growth varies by 4 percentage points from lower to higher in each of five years; gross margin varies by 3 percentage points. The conclusion therefore applies **over these ranges**, not to all possible scenarios.

### Why is a sensitivity table not a forecast probability?

A sensitivity table gives conditional answers: what the model calculates if specified inputs occur. It does not assign likelihoods to those inputs or outcomes. Lower, base, and higher are scenario labels, not confidence intervals; the base is not automatically the most likely outcome. A probability forecast would require a supported distribution of assumptions and their relationships, which this one-at-a-time analysis does not estimate.

## 6. Prediction and comparison with actual results

**Prediction:** Increasing CROX's gross margin from **57.5% to 59.0% in every year from 2026?2030**, holding all other independent inputs constant, would increase 2030 operating profit by approximately **$25 million**, FCFE by **$20 million**, and value per share by **$4**. Higher gross profit would be partly offset by higher SG&A and taxes.

*Written after reviewing the results; this is not a pre-run locked prediction.*

| Output | Predicted change from base | Actual change from base | Actual minus prediction |
|---|---:|---:|---:|
| 2030 operating profit, EBIT (USD millions) | +25.000 | +24.704 | -0.296 |
| 2030 FCFE (USD millions) | +20.000 | +18.626 | -1.374 |
| Value per share (USD/share) | +4.000 | +3.607 | -0.393 |

All three actual changes are positive, matching the stated direction, but smaller than the approximate prediction. The model lets only about 37.66% of incremental gross profit reach EBIT because SG&A remains 62.34% of gross profit. Taxes and linked working-capital movements then affect FCFE. Value reflects all five years of FCFE and terminal value under the unchanged discount-rate and terminal-growth assumptions. Differences are calculated before rounding.
