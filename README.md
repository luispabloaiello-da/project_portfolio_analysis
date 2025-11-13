# Portfolio Analysis — Clean Report

## Executive Summary
- The portfolio delivers **~11.5% annualized return** with **~8.5% annualized volatility** over the observed period.  
- Correlations show a **cluster of assets that often move together**, balanced by at least one asset that **moves differently (low or slightly negative correlation)**—this provides some diversification but also reveals **areas of concentration risk**.  
- Allocation charts suggest that **how weights evolve over time** (rebalancing vs drift) is a key driver of the portfolio’s risk/return behavior.

---

## Slides

- [Portfolio Analysis](https://www.canva.com/design/DAG4nAOf_ZM/P5gfJ1I6I9TJ7e2aWbTpEQ/edit?utm_content=DAG4nAOf_ZM&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)

---

## 1) Normalized Price Index (Chart & Table)
**What it shows**  
- Each asset’s price series is re-scaled so they all **start at the same value (e.g., 100)**. From that common starting line, we can compare **relative growth** fairly across assets.

**How to read it**  
- If a line ends at **130**, that asset gained **+30%** since the start; **90** means **−10%**.  
- **Steeper, choppier** lines → potentially **higher risk** (more ups and downs).  
- **Crossovers** (one line overtaking another) show **changes in leadership** over time.

**What it tells us here**  
- You can quickly see **which asset(s) outperformed** over the full period, and which lagged.  
- Look for **regime shifts** (e.g., an asset trending up that later flattens or declines). These often map to macro events or company news.

---

## 2) Daily Percentage Returns (Table)
**What it shows**  
- The **day-to-day % change** in each asset’s price.

**How to read it**  
- The **average** daily return (mean) hints at typical gain per day.  
- The **standard deviation** of daily returns measures **daily volatility**—how “bouncy” the asset is.  
- **Outliers** (very large up/down days) flag events worth investigating.

**What it tells us here**  
- Which assets are **steady vs. jumpy**.  
- Days with unusually large moves help explain short-term portfolio swings and can guide **risk controls** (position limits, hedges).

---

## 3) Correlation Matrix (Daily Returns)
**What it shows**  
- How similarly pairs of assets move **each day** (−1 to +1).

**How to read it**  
- **+1**: move together; **−1**: move in opposite directions; **0**: unrelated.  
- **Clusters** of high positive correlation indicate **concentration** (many eggs in one behavioral basket).  
- **Low/negative correlations** are **diversifiers** that can **soften drawdowns**.

**What it tells us here**  
- The notebook shows, for example, **Asset5 has slight negative correlation with Asset1 (~−0.11)**—that’s a mild **hedge**.  
- **Asset5 is moderately positively correlated** with **Asset2 (~0.59)**, **Asset3 (~0.56)**, and **Asset4 (~0.42)**—a **cluster** that can amplify moves (good in rallies, painful in sell-offs).  
- Net: **some diversification exists**, but **cluster risk** is present.

---

## 4) Scatter Plot of Returns (Two Assets)
**What it shows**  
- Each point is a day. **X = returns of Asset X**, **Y = returns of Asset Y**.

**How to read it**  
- **Upward slanted, tight band** → strong positive correlation (move together).  
- **Downward slanted band** → negative correlation (hedge).  
- **Round, diffuse cloud** → low/near-zero correlation (good diversifier).  
- **Outliers** far from the cloud = shock days worth noting.

**What it tells us here**  
- Confirms visually what the correlation number says, and **highlights outlier days** that drive risk.

---

## 5) Portfolio Analysis

### (a) Area Chart of Asset Weights
**What it shows**  
- A **stacked area** where each band is an asset’s **weight** in the portfolio (weights sum to ~100% per day).

**How to read it**  
- **Thicker band** = larger allocation.  
- **Changing thickness over time** shows **rebalancing or tactical tilts**.  
- **Drift** (a band keeps getting thicker because it outperforms) can raise risk unintentionally.

**Key takeaway here**  
- Check whether weights **stay near targets** (disciplined) or **drift** (potentially riskier). Regular rebalancing usually improves **risk control**.

### (b) Chart of Historical Cumulative Returns (Portfolio)
**How it’s built**  
1. Compute daily portfolio return = **sum(weights × asset daily returns)**.  
2. Convert to growth of 1: **(1 + rₜ).cumprod()**.

**How to read it**  
- Rising line = wealth growth; **flat** = stagnation; **drawdowns** = peak-to-trough declines.  
- Look for **speed of recovery** after drawdowns (resilience).

**What it tells us here**  
- You can see **the journey**, not just the destination: whether returns came steadily or in bursts and how tough the drawdowns were.

### (c) Annualized Return & (d) Annualized Volatility
**Results in your notebook**  
- **Annualized Return ≈ 11.5%**  
- **Annualized Volatility ≈ 8.5%**

**How they’re calculated** (261 trading days/year)  
- **Annualized Return**: take total growth `∏(1+rt​)`, raise to 261/n, minus 1.  
- **Annualized Volatility**: **std dev of daily returns × √261**.

**Why they matter**  
- Return answers, “**How much did we make, annualized?**”  
- Volatility answers, “**How bumpy was the ride?**”  
- Together they describe **risk-adjusted quality** (e.g., return/vol ≈ **1.35** here—solid for a diversified mix).

### (e) Area Chart of Asset Weights Grouped by Family
**What it shows**  
- The same weight idea but **grouped** (e.g., **Equity**, **Fixed Income**, **Alternatives**).

**How it’s created**  
- Use the info table to map each asset → family, **sum weights by family per day**, and plot as a stacked area.

**Why it matters**  
- Gives a **top-down view** of risk buckets, helps check **policy bands** (e.g., 60/40), and reveals **drift or tactical tilts** at the family level.

---

## Bottom-Line Assessment

### Performance & Risk
- **Return (~11.5% annualized)** is **healthy** for a multi-asset portfolio.  
- **Volatility (~8.5% annualized)** is **moderate**. Combined, this is a **solid risk-return profile** for the period.

### Diversification
- You have **useful diversification** (e.g., Asset1 vs Asset5 shows slight negative link),  
- but also a **correlated cluster** (Asset2/3/4/5) that can **concentrate risk** in certain regimes.

### Allocation Discipline
- The **weights** (and family weights) over time will reveal if you **rebalance** (good risk control) or **drift** (risk can creep up). If drift is visible, codify a rebalancing rule.

---

## Recommendations (Actionable)

1) **Manage cluster risk**  
   - Cap exposures where assets are **moderately/highly correlated** (e.g., Asset2/3/4/5).  
   - Increase allocations to **lower/negatively correlated** assets to **stabilize drawdowns**.

2) **Enforce rebalancing**  
   - Use **bands (±5%)** or a **monthly/quarterly** cadence. This controls unintended risk increases when winners run.

3) **Track drawdowns explicitly**  
   - Add a **drawdown curve** and monitor **max drawdown** and **time to recover**. If painful, consider **true diversifiers** (quality bonds, managed futures, tail hedges) or **smaller positions** in the jumpiest assets.

4) **Add risk-adjusted KPIs**  
   - Report **Sharpe** (or Sortino) and **Calmar** (ann. return / max drawdown) alongside return and vol. They help judge the **quality** of returns.

5) **Regime & attribution checks**  
   - Split the sample into **calm vs stress** windows: correlations often **rise in stress**.  
   - Do a simple **attribution** to see whether **allocation** or **selection** drove most of the return.

---

## What needs special attention next?
- **Correlation cluster (Asset2/3/4/5):** Great in good times, risky in bad—**size it consciously**.  
- **Weight drift:** If present, it can stealthily lift portfolio risk—**rebalance** to policy targets.  
- **Shock days:** Outliers in the returns table—**review those dates** and decide on **controls** (limits, hedges) to reduce future damage.

---

### One-slide takeaway
> “Our portfolio earned **~11.5%** per year with **~8.5%** volatility, a solid risk-adjusted profile. We benefit from **some diversification**, but a **correlated asset cluster** concentrates risk in certain regimes. The fastest improvements are to **enforce rebalancing**, **size down correlated bets**, and **add diversifiers** that hold up in stress—reducing drawdowns while keeping return potential.”
