# Curriculum roadmap & progress

Source of truth for "where we are". The daily agent reads **Progress**, teaches `Roadmap[last_lesson_index + 1]`, then updates Progress and the Log in the same commit as the lesson file.

## Rules for the daily agent

1. Today's lesson = the next roadmap item after `last_lesson_index`. One roadmap item per day; if an item is marked `(2 days)`, split it across two consecutive days (`part 1/2`, `part 2/2`) and only advance the index after part 2.
2. Every lesson must explicitly **build on the previous one**: open by recalling the key result from yesterday and show where it is used today. Reuse notation and running examples (the running example is a stock `S_t` with `S_0 = 100`, `μ = 0.08`, `σ = 0.2`, `r = 0.03` unless a lesson needs otherwise).
3. Audience: a working quant/analyst comfortable with Python, NumPy, pandas, undergraduate calculus and probability. Rigour level: "Shreve Vol II lite" — state results precisely, prove the key ones in sketch form, prefer intuition + simulation over measure-theoretic detail.
4. If `feedback.md` has open entries, add one short reinforcement item for each (max 2) before the new material.
5. If the learner's replies show the pace is too fast (2+ consecutive struggles), insert a consolidation day: re-teach the weak concept from a new angle and do not advance `last_lesson_index`. Record it in the Log as `Day N — date — Consolidation: <topic>`.

## Progress

- `day_number`: 0
- `week_number`: 0
- `last_lesson_index`: 0
- `part`: (none)
- `last_sent_date`: (none yet)
- `last_topic`: (none yet)
- `last_lesson_file`: (none yet)

## Log

(newest at the bottom; e.g. `Day 1 — 2026-10-20 — L1 Probability spaces, filtrations & information`)

## Roadmap

### Module A — Probability foundations (refresher with a finance lens)
1. Probability spaces, σ-algebras as "information", filtrations, adapted processes
2. Random variables, expectation, variance, normal & lognormal distributions (moment generating functions)
3. Conditional expectation — definition, tower property, "taking out what is known", independence
4. Martingales in discrete time; the fair-game intuition; martingale transforms (discrete stochastic integrals)
5. Binomial asset pricing model: one-period replication and risk-neutral probabilities
6. Multi-period binomial model; discounted prices as martingales under Q; pricing a European call by backward induction
7. Week review & synthesis: from binomial trees to continuous time (why we need a limit)

### Module B — Brownian motion
8. Symmetric random walk → scaled random walk → Brownian motion (Donsker intuition, simulate it)
9. Definition and properties of Brownian motion: independent Gaussian increments, covariance `min(s,t)`
10. Brownian motion as a martingale; `W_t² − t` and `exp(θW_t − θ²t/2)` are martingales
11. Quadratic variation: `[W,W]_t = t`; why `dW·dW = dt`; first variation is infinite (simulate it)
12. Path properties: continuity, nowhere differentiability, reflection principle, distribution of the running maximum
13. First passage times and the Markov property; barrier-hitting probabilities
14. Module review: Brownian motion toolkit

### Module C — The Itô integral
15. Why Riemann–Stieltjes fails; Itô integral for simple (step) integrands; left-endpoint evaluation
16. Itô integral for general adapted integrands; martingale property; Itô isometry (2 days)
17. Computing `∫ W dW = (W_t² − t)/2` from first principles; Itô vs Stratonovich
18. Itô processes `dX = μ dt + σ dW` and their quadratic variation; `∫ Δ dS` as trading gains
19. Module review: integrals, isometry, quadratic variation

### Module D — Itô's lemma
20. Itô's lemma for functions of Brownian motion `f(W_t)` — derivation via Taylor + `dW² = dt`
21. Itô's lemma for `f(t, X_t)` with an Itô process; the box calculus (`dt·dt = 0`, `dt·dW = 0`, `dW·dW = dt`)
22. Geometric Brownian motion: solving `dS = μS dt + σS dW`; lognormal distribution of `S_T`; simulate and check
23. Multidimensional Itô's lemma; correlated Brownian motions; Itô product rule
24. Applications: `d(log S)`, `d(1/S)`, `d(S·B)`, quotient rule, exchange rates
25. Module review: Itô's lemma drills

### Module E — SDEs
26. Existence & uniqueness (Lipschitz, growth) — statement and intuition; strong vs weak solutions
27. Ornstein–Uhlenbeck / Vasicek: solve by integrating factor; mean reversion; stationary distribution
28. CIR process, Feller condition; other SDEs used in finance (brief)
29. Numerical schemes: Euler–Maruyama and Milstein; strong vs weak convergence (simulate convergence orders)
30. Feynman–Kac theorem: link between SDEs and PDEs (2 days)
31. Module review: SDEs & simulation

### Module F — Black–Scholes
32. Self-financing portfolios in continuous time; delta-hedging argument
33. Deriving the Black–Scholes PDE; boundary/terminal conditions
34. Solving the BS PDE (change of variables to heat equation) and the BS formula (2 days)
35. The Greeks: delta, gamma, vega, theta, rho; gamma–theta relationship from the PDE
36. Implied volatility, the smile, and what BS gets wrong
37. Module review: Black–Scholes from three angles (PDE, replication, expectation)

### Module G — Change of measure & risk-neutral pricing
38. Radon–Nikodym derivative, equivalent measures — discrete example first
39. Girsanov's theorem (one-dimensional) — statement, intuition, simulation check (2 days)
40. Risk-neutral measure; market price of risk; discounted assets are Q-martingales
41. Martingale representation theorem; completeness and hedging
42. Fundamental theorems of asset pricing (no-arbitrage ⇔ EMM; completeness ⇔ uniqueness)
43. Change of numéraire; forward measure; pricing exchange options (Margrabe)
44. Module review: pricing via expectation under Q, Monte Carlo pricing in Python

### Module H — Exotic options & applications
45. Digital options and the pricing of indicator payoffs
46. Barrier options via reflection principle
47. Asian & lookback options (Monte Carlo + variance reduction: antithetic, control variates)
48. American options: optimal stopping, early exercise, Longstaff–Schwartz (2 days)
49. Module review

### Module I — Interest rates
50. Short-rate models: Vasicek, CIR, Hull–White; bond pricing PDE
51. Affine term structure; zero-coupon bond formulas
52. HJM framework and the drift condition
53. LIBOR/forward market model intuition, caps/floors and Black's formula
54. Module review

### Module J — Beyond Black–Scholes
55. Jump processes: Poisson process, compound Poisson, Merton jump-diffusion
56. Stochastic volatility: Heston model, correlation and the smile
57. Local volatility and Dupire's formula
58. Characteristic functions & Fourier pricing (Carr–Madan) intro
59. Capstone: price and hedge a product end-to-end (model choice, calibration sketch, MC vs PDE, hedge P&L simulation) (2 days)
60. Course review & where to go next (Shreve, Björk, Øksendal, rough volatility, ML in pricing)

After item 60, start **Cycle 2: problem-solving**: one interview-style or exam-style problem per day (e.g. "compute E[W_t⁴]", "price a power option", "find the SDE for X_t = W_t³"), cycling through Modules A–J; append the planned items here before teaching them.
