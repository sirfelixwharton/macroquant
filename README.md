# macroquant
Institutional-grade macro quant model: regime classification, intermarket correlation, fair value logic, volatility banding, mispricing signal detection.

# 🧠 Institutional Macro Flow Valuation Model

> Macro regime → Correlation structure → Fair value modeling → Mispricing residuals → Flow confirmation → Signal classification.

This repository houses a complete, institutional-grade macro quant strategy engineered for precision mispricing detection and intelligent signal execution. It integrates top-down macroeconomic logic with intermarket data to uncover inefficiencies at both swing and intraday levels.

---

## ⚙️ Core Architecture

### 1. 🔍 **Macro Regime Engine**
- Classifies current economic conditions using YoY GDP and benchmark interest rates.
- Regime tags shape correlation expectations and model weightings.

### 2. 📈 **Rolling Correlation Matrix (DCC-GARCH)**
- Intermarket relationships adaptively tracked via DCC-GARCH.
- Highlights shifts in leading assets and lagging reactions (e.g., oil → XOM).

### 3. 💰 **Fair Value Modeling Suite**
- Ensemble of valuation models conditioned on correlation:
  - Linear regression
  - Polynomial regression
  - XGBoost
  - LassoCV
  - Volatility-conditioned residual model
- Model weights dynamically selected per regime.

### 4. 📊 **Realized Volatility Bands**
- Adaptive quantile regression on rolling realized volatility.
- Predicts expected move ranges for fair value, dynamically adjusts per macro regime and flow condition.

### 5. 📉 **Residual Mispricing Detector**
- Mispricing = Actual price – Fair Value
- Z-score of residual used as signal input
- Adjusted for band width and volatility context

### 6. 🧠 **Macro Flow Overlay (Surprise Engine)**
- CPI, PPI, PMI Surprise Index computed via trailing z-score of (Actual - Forecast).
- Surprise-weighted sentiment overlay adjusts mispricing thresholds.
- Flow timing logic aligns signal strength to release windows (pre, during, post).

### 7. 📬 **Signal Classification System**
- 4-tier signal output:
  1. **Regime alignment**
  2. **Mispricing strength (z-score)**
  3. **Volatility confidence band position**
  4. **Macro flow confirmation (Surprise Index)**
- Each signal carries a **judgment score** from 0–100 to guide discretionary or semi-auto execution.

---

## 📂 Files

- `macro_model.ipynb`: Full notebook of the model.
- `macro_regime.py`: GDP + interest-rate regime tagging logic.
- `dcc_garch.py`: DCC-GARCH correlation tracking.
- `valuation_models.py`: Fair value modeling suite.
- `residual_detector.py`: Residual mispricing scoring.
- `macro_flow.py`: Surprise index + macro timing overlay.
- `signal_engine.py`: Final signal classification logic.

---

## 🛠 Installation & Usage

```bash
git clone https://github.com/YOUR_USERNAME/macro-flow-valuation-model.git
cd macro-flow-valuation-model
pip install -r requirements.txt
jupyter notebook macro_model.ipynb

