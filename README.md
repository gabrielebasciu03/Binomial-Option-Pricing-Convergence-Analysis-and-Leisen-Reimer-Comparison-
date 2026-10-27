# Binomial-Option-Pricing-Convergence-Analysis-and-Leisen-Reimer-Comparison-
 Binomial Option Pricing: CRR vs Leisen–Reimer Convergence  A numerical study of how fast two binomial trees converge to the Black–Scholes price of a European call: the Cox–Ross–Rubinstein (CRR) model and the Leisen–Reimer (LR) model with Peizer–Pratt 2 (PP2) inversion. Both are implemented as Excel VBA functions.


## Setup

| Parameter | Value |
|-----------|-------|
| Spot S | 100 |
| Strike K | 100 |
| Risk-free rate r | 1% |
| Volatility σ | 20% |
| Maturity T | 1 year |
| Black–Scholes price | 8.433319 |

## Methods

- **Black–Scholes:** the analytical benchmark.
- **CRR:** `u = e^(σ√Δt)`, `d = 1/u`, with backward induction. Theoretical convergence of order 1.
- **Leisen–Reimer:** the tree parameters come from inverting normal approximations to the binomial distribution. The strike sits at the tree centre (odd n), which removes the oscillations of CRR. Convergence of order ~2.

## VBA Implementation

`LR_OptionPrice(S, K, T, r, σ, n, method, type, style)` supports:
- Inversion methods: CP, PP1, PP2
- Calls and puts
- European and American exercise

Implementation details: n is forced odd, the up-factor uses a separate `R_factor = exp(r·Δt)` variable, and the inversion helpers clamp probabilities to [0.0001, 0.9999].

## Results

| n | CRR error | LR error |
|-----|-----------|----------|
| 1 | 1.981403 | 0.167874 |
| 10 | 0.195613 | 0.002919 |
| 50 | 0.039810 | 0.000251 |
| 100 | 0.019814 | 0.000039 |

**Observed order of convergence** (log–log slope of the error):
- CRR: **−0.996** (theory: −1)
- Leisen–Reimer: **−1.857** (theory: ≈ −2)

## Key Findings

- CRR converges with order 1 but oscillates, because the strike's position relative to the tree nodes keeps changing.
- LR converges smoothly and monotonically, with an error below 0.001 from n ≥ 25.
- At n = 100, the LR error is about **500× smaller** than the CRR error.

## Files

- `GabrieleBasciuReport3.xlsm`: VBA functions and calculations
- Report (PDF): methodology, convergence plots and discussion

## Reference

Leisen, D. & Reimer, M. (1995). *Binomial models for option valuation: examining and improving convergence.*

## Tech

Excel VBA, numerical methods, option pricing theory.
