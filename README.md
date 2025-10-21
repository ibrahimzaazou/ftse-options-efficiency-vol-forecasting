# SPY Option Efficiency & Volatility Forecasting

This project analyzes SPY (S&P 500 ETF) option efficiency by testing the **put–call parity rule** for mispricings and modeling volatility with **realized, EWMA, and GARCH** approaches.  
Using **Black–Scholes pricing**, it compares forecasted vs. market prices to reveal how volatility shocks drive pricing errors and overall market efficiency.

---

## 🔍 Project Overview
This is an end-to-end quantitative research workflow built in Python + Jupyter:

1. **Data acquisition:** Fetches SPY option chains and interest rates from Yahoo Finance.  
2. **Parity analysis:** Tests put–call parity and computes synthetic forwards.  
3. **Vol forecasting:** Builds rolling volatility models (RV21, EWMA λ = 0.94, GARCH(1,1)).  
4. **Pricing:** Applies Black–Scholes with forecasted σ to price each option.  
5. **Integration:** Joins forecasts and prices across all maturities/moneyness buckets.  
6. **Summary report:** Automatically generates visuals + performance leaderboard.

---

## 📁 Repository Structure
│
├── 01_data_fetch_and_pairs.ipynb # Fetch & clean SPY options
├── 02_put_call_parity.ipynb # Parity checks and synthetic forwards
├── 03_vol_forecasting_and_pricing.ipynb # Realized/EWMA/GARCH σ̂ + BS pricing
├── 04_integration_and_report.ipynb # Merge forecasts and build pricing panel
├── 05_summary.ipynb # Final analysis & HTML report
│
├── data/ # Raw + processed data
├── reports/ # Figures + summary_overview.html
├── requirements.txt # Dependencies
├── LICENSE
└── README.md


---

## 🧠 Key Results (SPY sample)
| Model | MAE | RMSE | Median |error| |
|--------|------|------|-------------|
| **sig_rv21** | 0.9538 | 1.276 | 0.74 |
| sig_rv63 | 1.09 | 1.456 | 0.84 |
| sig_garch | 1.20 | 1.61 | 0.91 |
| sig_ewma | 1.37 | 1.86 | 0.97 |

- **Best model:** 21-day realized volatility (`sig_rv21`)  
- **Errors increase with tenor:** short maturities are most accurate  
- **Hardest moneyness bucket:** (0.9, 1.0] (ATM)  
- **Easiest:** (0.8, 0.9] (slightly ITM/OTM)

---

## 🖥 Final Report
**HTML summary (auto-generated):**  
📄 [`reports/summary_overview.html`](reports/summary_overview.html)

Includes:
- Leaderboard of model errors
- Error distributions & scatter plots
- Per-tenor and per-moneyness tables
- Key takeaways

---

## ⚙️ How to Reproduce
```bash
# 1️⃣ Clone repo
git clone https://github.com/ibrahimzaazou/ftse-options-efficiency-vol-forecasting.git
cd ftse-options-efficiency-vol-forecasting

# 2️⃣ Create env (Python 3.11)
python -m venv venv311
venv311\Scripts\activate      # or: source venv311/bin/activate
pip install -r requirements.txt

# 3️⃣ Launch Jupyter
jupyter lab

Then open notebooks sequentially (01_… → 05_…).
All outputs (figures + summary) appear in /reports.

📦 Dependencies
pandas, numpy, matplotlib, seaborn
statsmodels, arch, pyarrow
yfinance, scipy
Jupyter Lab ≥ 4.0

Future Extensions -->
Walk-forward out-of-sample validation
IV vs HV comparisons
Transaction-cost adjusted parity tests
Cross-asset generalization (FTSE 100, SPX, QQQ)

