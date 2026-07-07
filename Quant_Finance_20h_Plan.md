# Quant Finance in 20 Hours — The 80/20 Plan

> **Goal:** Quant finance literacy that strengthens your Bangkok banking/finance DS profile and front-loads FRM Part 1 concepts. Not a quant-career pivot — a force multiplier for the plan you already have.
>
> **Format:** 10 sessions × 2h. Each session ≈ 50 min theory → 55 min hands-on Python → 15 min review. Weekday-only pace: 2–3 sessions/week → done in ~4 weeks.
>
> **The 20% that matters:** returns & risk, portfolio theory, backtesting without fooling yourself, time series, and why ML in finance fails naively. You already have pandas/sklearn — this plan spends zero time re-teaching Python.

---

## Setup (15 min, before Session 1)

- [ ] `pip install yfinance pandas numpy matplotlib scipy statsmodels backtesting`
- [ ] Verify data pull works: `yf.download("SPY", start="2015-01-01")` (if flaky, use `yahooquery`)
- [ ] Create a `quant_finance/` folder with one notebook per session — this becomes portfolio evidence

**Core free resources used throughout:**

| Resource | Use for |
|---|---|
| [MIT OCW 18.S096 — Math with Applications in Finance](https://ocw.mit.edu/courses/18-s096-topics-in-mathematics-with-applications-in-finance-fall-2013/) | Rigorous but accessible lectures |
| [EDHEC: Introduction to Portfolio Construction with Python (Coursera)](https://www.coursera.org/learn/introduction-portfolio-construction-python) | Audit free — portfolio theory in code |
| [QuantStart articles](https://www.quantstart.com/articles/) | Practitioner-level explainers |
| [Patrick Boyle (YouTube)](https://www.youtube.com/@PBoyle) | Finance professor; best short derivative/risk videos |
| [Investopedia](https://www.investopedia.com/) | Fast concept lookups |
| [backtesting.py docs](https://kernc.github.io/backtesting.py/) | The backtesting framework we'll use |

---

## Session 1 — Returns, and Why Prices Lie

**Why first:** every quant concept is built on returns, not prices. Getting log vs simple returns and "stylized facts" right unlocks everything after.

- [ ] **Theory (50m):** Simple vs log returns; annualization; stylized facts of returns — fat tails, volatility clustering, near-zero autocorrelation. Read: QuantStart on [returns basics] + Wikipedia "Stylized facts". Skim MIT 18.S096 Lecture 1.
- [ ] **Code (55m):** Pull 10 years of SPY + 3 stocks. Compute daily/monthly log returns. Plot histogram vs fitted normal — see the fat tails yourself. QQ-plot. Rolling 21-day volatility plot — see clustering.
- [ ] **Review (15m):** Write from memory: why log returns? Why is normality assumption dangerous? What is vol clustering? Check answers against notes.

## Session 2 — Risk: Volatility, Drawdown, VaR & CVaR

**Why:** risk measurement is *the* overlap between quant finance, your credit-risk project, and FRM Part 1. Highest-ROI session for your CV.

- [ ] **Theory (50m):** Volatility (rolling, EWMA), max drawdown, Value-at-Risk (historical, parametric, Monte Carlo), Expected Shortfall/CVaR and why regulators prefer it (Basel connection). Patrick Boyle's VaR video + Investopedia CVaR.
- [ ] **Code (55m):** Implement all three VaR methods + CVaR on your Session 1 data from scratch (no libraries). Compare them. Compute max drawdown function.
- [ ] **Review (15m):** Explain to an imaginary stakeholder: "our 1-day 99% VaR is X" — what does that mean and what does it *not* mean? Where does VaR break?

## Session 3 — Portfolio Theory: Diversification, Sharpe, Markowitz

**Why:** Markowitz + Sharpe ratio is the grammar of every conversation about performance. Interviewers assume it.

- [ ] **Theory (50m):** Diversification math (correlation → portfolio variance), efficient frontier, Sharpe/Sortino ratios, CAPM & beta in 15 minutes (concept only). EDHEC Coursera Week 1–2 videos at 1.5×.
- [ ] **Code (55m):** Build a 5-asset portfolio. Simulate 5,000 random weight allocations, plot the efficient frontier (return vs vol, colored by Sharpe). Find max-Sharpe weights with `scipy.optimize`.
- [ ] **Review (15m):** Why does an asset with *worse* returns can still improve a portfolio? What are Markowitz's failure modes in practice (estimation error)?

## Session 4 — Time Series for Finance: Stationarity, ARIMA, GARCH

**Why:** direct synergy with your Project 3 (time-series forecasting) and the single most transferable topic back to your DS plan.

- [ ] **Theory (50m):** Stationarity & ADF test, ACF/PACF, random walk hypothesis, ARIMA intuition, GARCH for volatility forecasting (concept + when it's used). QuantStart's time-series article series (parts on stationarity, ARMA, GARCH).
- [ ] **Code (55m):** ADF test on prices vs returns. Fit ARIMA on returns (see how little it predicts — that's the lesson). Fit GARCH(1,1) with `arch` package; plot conditional volatility vs realized.
- [ ] **Review (15m):** Why can't you forecast returns easily but *can* forecast volatility? What does that imply about where quant effort goes?

## Session 5 — Backtesting I: Your First Strategy

**Why:** backtesting is the core quant workflow — hypothesis → simulation → evaluation. It's also where your ML instincts transfer directly.

- [ ] **Theory (50m):** Momentum & trend-following (why they persist), moving-average crossover logic, transaction costs, slippage. Backtest evaluation: CAGR, Sharpe, max drawdown, win rate. Read backtesting.py Quick Start + QuantStart "Successful Backtesting" parts 1–2.
- [ ] **Code (55m):** Implement SMA crossover on SPY with `backtesting.py`. Add 0.1% transaction costs — watch performance change. Compare vs buy-and-hold honestly.
- [ ] **Review (15m):** List every way this backtest could be lying to you. (Aim for 5+: costs, survivorship, one asset, one period, parameter choice…)

## Session 6 — Backtesting II: How to Fool Yourself (Overfitting)

**Why:** the #1 differentiator between amateurs and professionals is understanding backtest overfitting. This is also a killer interview talking point that maps to ML overfitting.

- [ ] **Theory (50m):** Look-ahead bias, survivorship bias, data snooping, multiple testing (→ this is your stats deep-dive knowledge applied!), walk-forward validation, in-sample vs out-of-sample. Read: QuantStart "Successful Backtesting" parts 3–4 + skim López de Prado's "The 7 Reasons Most Machine Learning Funds Fail" (free SSRN paper).
- [ ] **Code (55m):** Grid-search SMA parameters in-sample (2015–2020) → test out-of-sample (2021–2025). Watch the "best" parameters fall apart. Implement simple walk-forward split.
- [ ] **Review (15m):** Map each backtesting sin to its ML equivalent (look-ahead = data leakage, parameter mining = overfitting…). This mapping IS your interview answer.

## Session 7 — Fixed Income & Derivatives: The Minimum Viable Set

**Why:** Thai banking DS roles touch bonds and options pricing indirectly; FRM Part 1 tests this heavily. Concept-level only — no stochastic calculus.

- [ ] **Theory (65m — theory-heavy session):** Bond pricing, yield, duration & convexity (intuition). Options: calls/puts, payoff diagrams, put-call parity, Black-Scholes *inputs and intuition* (not derivation), the Greeks in one paragraph each, implied volatility. Patrick Boyle's options playlist + Investopedia.
- [ ] **Code (40m):** Price a bond and compute duration in numpy. Implement Black-Scholes formula (it's 10 lines with `scipy.stats.norm`); plot option price vs volatility and vs time to expiry.
- [ ] **Review (15m):** Draw payoff diagrams for long call, short put, covered call from memory. What happens to option value when vol rises? Why?

## Session 8 — ML in Finance: Why Naive Approaches Fail

**Why:** this is YOUR edge. A DS who knows why financial ML is hard is rare and credible. Directly reusable in interviews for banking DS roles.

- [ ] **Theory (50m):** Why financial data breaks sklearn defaults: non-stationarity, low signal-to-noise, non-IID samples, regime change. Fractional labels/triple-barrier (concept), purged cross-validation, feature importance pitfalls. Read López de Prado paper properly this time + QuantStart ML articles.
- [ ] **Code (55m):** Build features (lagged returns, vol, RSI) → train your beloved XGBoost to predict next-day direction. Use proper time-series CV. Observe ~51% accuracy. Compute what Sharpe that actually implies with costs. The disappointment is the lesson.
- [ ] **Review (15m):** Write 5 bullet answers to: "Why doesn't your credit-default modeling approach transfer directly to return prediction?"

## Session 9 — Market Structure, Strategy Types & Position Sizing

**Why:** rounds out the vocabulary — how markets actually work and how pros size bets. Makes you conversant, not just technical.

- [ ] **Theory (60m):** Market microstructure lite: order books, bid-ask spread, market vs limit orders, market makers, why HFT exists. Strategy taxonomy: momentum, mean reversion, stat arb/pairs, carry, market making. Position sizing: fixed fractional, Kelly criterion (concept + why pros use fractional Kelly), vol targeting.
- [ ] **Code (45m):** Pairs trading mini-demo: find two correlated stocks, compute spread z-score, backtest simple mean-reversion on the spread. Add vol-targeted position sizing to your Session 5 strategy.
- [ ] **Review (15m):** For each strategy type, one sentence: what's the hypothesized edge and who's on the other side of the trade?

## Session 10 — Capstone: Ship It

**Why:** 20 hours of learning is invisible unless it's on GitHub and your CV. This session converts knowledge into career assets.

- [ ] **Build (75m):** One polished notebook: "Systematic Strategy Research: Momentum vs Mean Reversion on [assets]" — data → stylized facts → strategy → honest backtest with costs → walk-forward validation → risk metrics (Sharpe, VaR, max DD) → limitations section. Reuse Sessions 1–9 code.
- [ ] **Publish (30m):** Push to GitHub with a strong README (problem framing, methodology, *limitations* — your signature style). Add one CV bullet + one LinkedIn post draft.
- [ ] **Review (15m):** Final self-test — the 10 questions below, closed-book.

---

## Final self-test (Session 10 review)

1. Why log returns, and what are the three stylized facts of asset returns?
2. Define VaR and CVaR; why do regulators prefer CVaR?
3. How does correlation drive diversification benefit? What breaks Markowitz in practice?
4. Why is volatility forecastable but returns mostly aren't?
5. Name five backtest biases and their ML-world equivalents.
6. What are the Black-Scholes inputs? What do vega and theta measure?
7. Why does 51% directional accuracy usually fail after costs?
8. What is walk-forward validation and why not plain k-fold CV in finance?
9. Explain fractional Kelly in two sentences.
10. Pairs trading: what's the edge hypothesis and the main risk?

**Pass bar:** 8/10 confident answers. Redo the review sections of weak sessions.

---

## How this feeds your existing plan

| This plan | Feeds into |
|---|---|
| Sessions 2, 7 (risk, VaR, bonds, options) | FRM Part 1 (Nov 2026) — you'll enter prep with ~30% of Valuation & Risk Models pre-learned |
| Session 4 (ARIMA/GARCH) | Project 3 time-series option — directly reusable |
| Sessions 6, 8 (overfitting, ML pitfalls) | Interview differentiator for banking DS roles |
| Session 10 capstone | Optional 4th GitHub portfolio piece |

**Deliberately excluded (the other 80%):** stochastic calculus, C++, exotic derivatives pricing, HFT infrastructure, crypto, order-book modeling. None of it moves your Bangkok banking DS applications.
