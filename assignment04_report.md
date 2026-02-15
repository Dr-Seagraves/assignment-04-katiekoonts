# Assignment 04 Interpretation Memo

**Student Name:** Katie Koonts
**Date:** February 15, 2026
**Assignment:** REIT Annual Returns and Predictors (Simple Linear Regression)

---

## 1. Regression Overview

You estimated **three** simple OLS regressions of REIT *annual* returns on different predictors:

| Model | Y Variable | X Variable | Interpretation Focus |
|-------|------------|------------|----------------------|
| 1 | ret (annual) | div12m_me | Dividend yield |
| 2 | ret (annual) | prime_rate | Interest rate sensitivity |
| 3 | ret (annual) | ffo_at_reit | FFO to assets (fundamental performance) |

For each model, summarize the key results in the sections below.

---

## 2. Coefficient Comparison (All Three Regressions)

**Model 1: ret ~ div12m_me**
- Intercept (β₀): 0.1082 (SE: 0.006, p-value: 0.000)
- Slope (β₁): -0.0687 (SE: 0.032, p-value: 0.035)
- R²: 0.002 | N: 2,527

**Model 2: ret ~ prime_rate**
- Intercept (β₀): 0.1998 (SE: 0.016, p-value: 0.000)
- Slope (β₁): -0.0194 (SE: 0.003, p-value: 0.000)
- R²: 0.016 | N: 2,527

**Model 3: ret ~ ffo_at_reit**
- Intercept (β₀): 0.0973 (SE: 0.009, p-value: 0.000)
- Slope (β₁): 0.5770 (SE: 0.567, p-value: 0.309)
- R²: 0.000 | N: 2,518

*Note: Model 3 has 9 fewer observations because ffo_at_reit has some missing values.*

---

## 3. Slope Interpretation (Economic Units)

**Dividend Yield (div12m_me):**
- A 1% point increase in dividend yield is associated with a -0.0687 change in annual return.
- This is a bit counterintuitive—higher dividends are actually linked to lower future returns. This could mean that high dividend-paying REITs are mature or slower growing, so they don't deliver as much capital. Investors buying for current yield might miss out on the total return.

**Prime Loan Rate (prime_rate):**
- A 1% point increase in the year-end prime rate is associated with a -0.0194 change in annual return.
- This makes economic sense, when interest rates rise, REIT returns tend to fall. Higher rates mean higher borrowing costs for REITs and lower property valuations. It's the clearest relationship of the three models.

**FFO to Assets (ffo_at_reit):**
- A 1 unit increase in FFO/Assets is associated with a 0.5770 change in annual return.
- The sign is positive (which makes intuitive sense more profitable REITs should generate better returns), but it's not statistically significant and the standard error is huge relative to the coefficient. So this relationship is pretty weak.

---

## 4. Statistical Significance

For each slope, at the 5% significance level:
- **div12m_me:** Significant (p = 0.035) higher dividend yield is statistically significantly linked to lower subsequent returns.
- **prime_rate:** Significant (p < 0.001) the prime rate is the strongest predictor, with very strong statistical evidence of a negative relationship with REIT returns.
- **ffo_at_reit:** Not significant (p = 0.309) there's no statistically significant relationship between FFO/Assets and returns in this simple regression.

**Which predictor has the strongest statistical evidence of a relationship with annual returns?** Prime rate, the t-stat is -6.487 , and the p-value is almost zero.

---

## 5. Model Fit (R-squared)

Compare R² across the three models:
- Prime rate has the highest R² at 0.016 (1.6% of variation explained)
- Dividend yield has R² = 0.002 (0.2%)
- FFO/Assets has R² ≈ 0.000 (essentially nothing)

All three R^2 values are really low. This tells us that simple one variable models don't explain much of what drives REIT returns. Most of the variation comes from other factors we're not capturing here, maybe interest rate expectations, sector rotation, property valuations, leverage, or just market sentiment. It's a good reminder that real world returns are complicated and driven by lots of different pieces.

---

## 6. Omitted Variables

By using only one predictor at a time, we might be omitting:
- **Other interest rates or yield curve slope:** We're only using the prime rate, but futures rates, 10-year yields, or the spread between long and short rates might matter for REIT valuations.
- **REIT sector composition:** Different property types (apartments, office, retail, industrial) respond differently to economic cycles. Our model treated all REITs the same.
- **Leverage/debt levels:** REITs with more debt might be more sensitive to interest rate changes and could be driving the prime_rate relationship.
- **Market-wide risk factors:** Beta, momentum, or broader market returns could drive REIT performance and might be correlated with our X variables.

**Potential bias:** If we're omitting variables correlated with both X and ret, our slopes could be biased. For example, if REITs with high leverage tend to also have high FFO/Assets, and leverage is negatively correlated with returns, we might be understanding the true effect of profitability on returns.

---

## 7. Summary and Next Steps

**Key Takeaway:**
Prime rate is clearly the best single predictor of REIT returns among these three options, with a statistically significant negative relationship that makes economic sense. Dividend yield also matters, but in a counterintuitive way. FFO to assets doesn't have enough predictive power on its own. Collectively, these results suggest that interest rate environment and market maturity are the main drivers of REIT returns, not just fundamental profitability.

**What we would do next:**
- Build a multiple regression model with all three predictors (or more) to see if we can explain more variation
- Test whether the relationships are stable over different time periods (recessions vs. expansions)
- Look at heteroskedasticity, since REITs might show more volatility in some market conditions
- Break out results by REIT sector (apartment vs. industrial vs. retail) to see if sensitivities differ

---

## Reproducibility Checklist
- [ ] Script runs end-to-end without errors
- [ ] Regression output saved to `Results/regression_div12m_me.txt`, `regression_prime_rate.txt`, `regression_ffo_at_reit.txt`
- [ ] Scatter plots saved to `Results/scatter_div12m_me.png`, `scatter_prime_rate.png`, `scatter_ffo_at_reit.png`
- [ ] Report accurately reflects regression results
- [ ] All interpretations are in economic units (not just statistical jargon)
