# Session 1 — Lecture Notes: Returns, and Why Prices Lie

> Companion to `session01_returns.ipynb` and `Quant_Finance_20h_Plan.md`.
> Structure: ~50 min theory (this doc + readings) → ~55 min notebook → 15 min closed-book review.
> **For the next Claude/model session:** act as professor/guide. When I paste my four review answers, grade them against the "Review answers rubric" at the bottom.

---

## Hour 1 theory, condensed

### 1. Simple vs log returns

- **Notation:** P₀ = price at the start of the period (e.g., yesterday's close); P₁ = price at the end (e.g., today's close). In time-series form: Pₜ and Pₜ₋₁, i.e. `px / px.shift(1)` in pandas.
- **Simple return:** R = P₁/P₀ − 1 — what you actually earn.
- **Log return:** r = ln(P₁/P₀) — what quants model.

Why quants prefer log returns (two reasons):

1. **Time-additive:** a month's log return = sum of daily log returns. Sums of many small random variables are what statistics handles well.
2. Simple returns are **cross-sectionally additive**: portfolio return = weighted average of simple returns.

Rule of thumb: **log for time-series modeling, simple for portfolio aggregation.** For small moves they're nearly identical (ln(1+x) ≈ x); on a −20% day they diverge badly.

Worked example: SPY closes 500 → 510. Simple = 510/500 − 1 = 2.00%. Log = ln(510/500) ≈ 1.98%.

### 2. Annualization

- Mean return scales **linearly** with time: × 252 (trading days).
- Volatility scales with **√time**: × √252 — because *variances* add under independence, not standard deviations.
- This √t scaling appears everywhere: option pricing, VaR horizons, position sizing. Annualizing vol by ×252 instead of ×√252 is a disqualifying error.

### 3. Stylized facts of returns

The empirical fingerprint of nearly every asset — why "prices lie":

- **Fat tails.** Daily returns have excess kurtosis far above 0 (SPY typically 10+; Normal = 0). The 1987 crash was a ~20σ event under Gaussian assumptions. Any model assuming normality underprices disaster. → Sets up Session 2 (VaR/CVaR).
- **Volatility clustering.** Large moves follow large moves. Returns are ~uncorrelated (direction unpredictable) but |returns| are strongly autocorrelated (magnitude IS predictable). This asymmetry explains where quant effort goes. → Sets up Session 4 (GARCH).
- **Aggregational Gaussianity.** Monthly returns look more normal than daily. Tail risk lives at short horizons.

### Readings (rest of theory hour)

- Wikipedia: "Stylized facts"
- QuantStart: returns basics article
- [MIT 18.S096 Lecture 1](https://ocw.mit.edu/courses/18-s096-topics-in-mathematics-with-applications-in-finance-fall-2013/) — first 20 min at 1.5× is enough

---

## Hour 2 — Notebook

`session01_returns.ipynb` (same folder). Parts: A simple vs log returns · B annualization + naive Sharpe · C fat tails (histogram vs Normal, QQ-plot, kurtosis, 4σ-day count) · D vol clustering (rolling 21d vol, autocorr of r vs |r|). Fill the TODOs yourself — no copy-pasting solutions.

---

## Review (15 min, closed book)

Answer from memory, then get graded:

1. Why do quants prefer log returns? (two reasons)
2. Why is assuming normality of returns dangerous? Cite a number from your own Part C output.
3. What is volatility clustering, and which plot proved it?
4. Why does volatility annualize with √252 and not 252?

### Review answers rubric (for the grader)

1. Time-additivity for modeling + (simple returns handle) portfolio aggregation; bonus: ln(1+x)≈x for small moves.
2. Fat tails / excess kurtosis ≫ 0; empirical 4σ-day count far exceeds Normal prediction (~0.02 expected in a 10y sample); 1987 ≈ 20σ.
3. Large moves cluster; |returns| autocorrelated while returns aren't. Proof: rolling-vol plot spikes (2018, 2020, 2022) and the autocorrelation bar chart asymmetry.
4. Variances add under independence, so vol grows with √t.

**After passing:** tick Session 1 in `Quant_Finance_20h_Plan.md`. Next up: Session 2 — Risk: Volatility, Drawdown, VaR & CVaR.
