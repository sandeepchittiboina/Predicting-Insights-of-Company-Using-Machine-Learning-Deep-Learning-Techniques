# Predicting Insights of Company Using Machine Learning & Deep Learning Techniques
### LSTM-based Stock Price Forecasting + Power BI Visualisation

> MSc Data Science dissertation project (University of Greenwich) by **Sai Sandeep Chittiboina**

![banner](./assets/banner.png)

## Overview
This project uses **Long Short‑Term Memory (LSTM)** networks to forecast the **future closing price** of equities and to explore cross‑company relationships through exploratory data analysis (EDA). It also includes **Power BI** visuals to present the insights interactively.

The analysis focuses on four automobile companies — **Tesla (TSLA)**, **Ford (F)**, **General Motors (GM)** and **Toyota (TM)** — with the final LSTM model trained on **Toyota (TM)** closing prices. The work includes moving‑average trend analysis, daily returns, correlation/risks, and a reproducible deep‑learning pipeline.

> **Disclaimer**: This repository is for research and educational purposes only. It is **not** financial advice.

## Key Features
- 🧩 **Data ingestion** from Yahoo Finance via `yfinance`
- 🔎 **EDA**: moving averages (10/20/30), daily returns, pair plots, correlations
- ⚖️ **Risk vs. expected return** comparison across the four automakers
- 🧠 **LSTM model** (Keras/TensorFlow) with Adam optimiser for 1‑step ahead closing‑price prediction (trained on Toyota)
- 📈 **Visualisations** with Matplotlib/Seaborn; **Power BI** dashboard for business‑friendly reporting
- 📊 **Metrics**: RMSE (example run ≈ **3.16** on TM)
- 🧪 **Reproducible notebooks** and scriptable pipeline
- ✅ **Ethics & compliance** checklist

## Project Structure
```
.
├── notebooks/
│   ├── 01_eda.ipynb
│   ├── 02_risk_returns.ipynb
│   └── 03_lstm_tm.ipynb
├── src/
│   ├── data/
│   │   ├── download_data.py          # yfinance downloader
│   │   └── preprocess.py             # cleaning, scaling, windowing
│   ├── features/
│   │   └── indicators.py             # moving avgs, returns, etc.
│   ├── models/
│   │   ├── build_lstm.py             # model architecture
│   │   └── train_lstm.py             # training loop & eval
│   └── utils/
│       └── io.py
├── data/
│   ├── raw/                          # raw Yahoo data (csv)
│   └── processed/                    # scaled/windowed datasets
├── reports/
│   ├── figures/                      # exported plots
│   └── dissertation.pdf              # optional: add your PDF here
├── powerbi/
│   └── stock_forecasting.pbix
├── requirements.txt
├── LICENSE
└── README.md
```

> The above structure is suggested; rename/move files to match your actual code. If you include your dissertation, place it as `./reports/dissertation.pdf` and update the link below.

## Getting Started

### 1) Prerequisites
- Python 3.9+
- pip (or uv/poetry/conda)
- Power BI Desktop (optional, for `.pbix`)

### 2) Setup
```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>

python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

pip install -r requirements.txt
```

A sample `requirements.txt`:
```
pandas
numpy
yfinance
matplotlib
seaborn
scikit-learn
tensorflow
keras
jupyter
```

### 3) Download data
```bash
python src/data/download_data.py \
  --tickers TSLA F GM TM \
  --start 2018-01-01 --end 2023-01-01 \
  --out data/raw
```

### 4) Preprocess and feature engineering
```bash
python src/data/preprocess.py \
  --input data/raw --output data/processed \
  --window 60 --scaler standard
```

### 5) Train LSTM (Toyota example)
```bash
python src/models/train_lstm.py \
  --ticker TM \
  --input data/processed \
  --epochs 50 --batch-size 32 \
  --save-model models/tm_lstm.keras \
  --export-fig reports/figures/tm_prediction.png
```

> Tip: Notebooks in `./notebooks` reproduce the steps interactively.

## Methodology

### Data
Historical OHLCV time‑series pulled with `yfinance` (note: `yfinance` is a community package and not an official Yahoo API).

### EDA
- Moving averages (10/20/30) to smooth trends
- Daily returns distributions and **pair plots** to inspect inter‑company relations
- **Correlation matrix** and a **risk vs. expected return** scatter to compare assets

### Modelling
- Sliding‑window **supervised** framing of the time series
- **Keras** LSTM: one or more LSTM layers followed by Dense output
- **Adam** optimiser; evaluate with **RMSE**, MAE, MAPE
- Hold‑out/temporal split for validation/testing

### Result (example)
- Toyota (TM) 1‑step ahead close prediction with **RMSE ≈ 3.16** (see `reports/figures/tm_prediction.png`).

## Power BI
Open `powerbi/stock_forecasting.pbix` to explore KPIs: closing‑price trends, volume, returns, and model prediction overlays. Replace the data source paths if needed.

## Figures (suggested exports)
Place rendered images here so the README can display them:

- `reports/figures/moving_averages_tm.png`
- `reports/figures/daily_returns_hist.png`
- `reports/figures/pairplot.png`
- `reports/figures/correlation_heatmap.png`
- `reports/figures/risk_vs_return.png`
- `reports/figures/tm_prediction.png`

You can then reference them like:

```md
![Risk vs. Return](./reports/figures/risk_vs_return.png)
```

## Ethics & Professional Considerations
- No insider information; avoid market manipulation
- Be transparent about methods, assumptions, and limitations
- Treat outputs as *experimental* and *educational*

## How to Cite
If you include your dissertation/PDF inside this repo under `./reports/dissertation.pdf`, you can cite it as:

> Chittiboina, S. S. (2023). *Predicting Insights of Company Using Machine Learning & Deep Learning Techniques and Visualising These Outcomes in Power BI*. University of Greenwich. DOI/URL: (add if applicable).

## Roadmap
- [ ] Multi‑step forecasting (horizon > 1)
- [ ] Hyperparameter search (Optuna/KerasTuner)
- [ ] Model ensembling (LSTM + XGBoost/Prophet)
- [ ] Live data refresh / scheduled retraining
- [ ] Dockerfile for reproducible runs

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License
This project is licensed under the **MIT License** — see [`LICENSE`](./LICENSE).

## Acknowledgements
- Supervisor: **Mohammad Al‑Antary**
- University of Greenwich — Computing & Mathematical Sciences
- Open‑source community maintainers (yfinance, pandas, TensorFlow, etc.)

---

*Made with ❤️ for data science and learning.*
