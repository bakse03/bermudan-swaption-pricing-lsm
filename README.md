# Bermudan Swaption Pricing in the Hull-White Model via Longstaff-Schwartz Method (LSM)

This repository features a complete quantitative finance implementation in Python for pricing European and Bermudan Payer Swaptions. The engine utilizes Hull-White short-rate paths generated via Monte Carlo simulations and applies the Longstaff-Schwartz Method (Least-Squares Monte Carlo - LSM) to evaluate optimal early exercise boundaries.

---

## 🔬 Theoretical Background & Model Setup

### 1. Hull-White Short Rate Model
The instantaneous risk-free interest rate $r_t$ is assumed to follow the stochastic differential equation (SDE) under the risk-neutral measure:

$$dr_t = (\theta(t) - a r_t) dt + \sigma dW_t$$

Where:
* $a$ is the mean-reversion speed parameter.
* $\sigma$ represents the instantaneous volatility.
* $\theta(t)$ is a deterministic function calibrated to perfectly fit the initial market zero-coupon bond curve.

### 2. Bermudan Swaption Valuation (LSM)
A Bermudan Payer Swaption grants the holder the right (but not the obligation) to enter into a fixed-for-floating Interest Rate Swap (IRS) at predefined exercise anniversary windows $T_i$. 

Since American/Bermudan-style options depend on path-dependent early exercise choices, the script implements the **Longstaff-Schwartz Algorithm**:
* At each exercise date, the immediate exercise value (Intrinsic Value) is compared against the **Continuation Value**.
* The Continuation Value is estimated by regressing the discounted future payoffs against current state variables (the short rate $r_t$) using ordinary least squares (OLS) quadratic polynomials.
* Backward induction is then performed across all simulated Monte Carlo interest rate paths to determine the optimal exercise timeline.

---

## 🚀 Project Features & Workflow

The Jupyter Notebook is structured into clear computational phases:
1. **Analytical Calibration:** Computing time-dependent $\theta(t)$ parameters and pricing analytical Zero-Coupon Bonds (ZCB) to establish the yield framework.
2. **Monte Carlo Short-Rate Simulator:** Simulating correlated short-rate paths over the swap's lifespan using exact transition distributions.
3. **European Swaption Baseline:** Implementing an analytical baseline and a standard Monte Carlo pricing routine for European swaptions to validate model stability.
4. **Longstaff-Schwartz Pricing Engine:** Running the backward regression loop to price the Bermudan derivative variant.
5. **Sensitivity Analysis & Disruption Breakdown:** Evaluating option premium shifts against starting short rates $r_0$ and charting early exercise histograms across the target time windows.

---

## 📁 Repository Structure

```text
bermudan-swaption-pricing-lsm/
├── ProjektOPiHWM.ipynb      # Main Jupyter Notebook containing calculations and visualizations
└── README.md                # Comprehensive project documentation
```

---

## 🛠️ Requirements & Quick Start

### Prerequisites
Ensure your Python execution environment includes the standard quantitative and data science libraries:

* **numpy**
* **pandas**
* **scipy**
* **matplotlib**

---

### How to Run via Google Colab

1. **Upload the Notebook:** Upload the `ProjektOPiHWM.ipynb` file directly into your Google Drive or link it straight to your GitHub repository.
2. **Initialize Runtime:** Initialize the runtime environment using a standard Python 3 kernel.
3. **Execute Cells:** Execute all cells sequentially (`Ctrl + F9`). 

> 💡 **What happens next:** The notebook will run the Monte Carlo loops, execute the polynomial regressions, output the final option premiums, and render diagnostic charts (short rate path simulations and exercise distribution histograms).
