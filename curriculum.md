# Curriculum roadmap & progress

Source of truth for "where we are". The daily agent reads **Progress**, teaches `Roadmap[last_lesson_index + 1]`, then updates Progress and the Log in the same commit as the lesson file.

## Rules for the daily agent

1. Today's lesson = the next roadmap item after `last_lesson_index`. One roadmap item per day; if an item is marked `(2 days)`, split it across two consecutive days (`part 1/2`, `part 2/2`) and only advance the index after part 2.
2. Every lesson must explicitly **build on the previous one**: open by recalling the key result from yesterday and show where it is used today. Reuse notation and running examples (the running example is a stock `S` with `S₀ = 100`, `μ = 0.08`, `σ = 0.2`, `r = 0.03` unless a lesson needs otherwise).
3. **Follow Hull** (*Options, Futures, and Other Derivatives*). Audience: assume **only basic knowledge of options** (calls, puts, payoffs, long/short) **and basic probability** (random variables, mean, variance, the normal distribution). Do not assume anything else. When a lesson first needs any of the following, explain it in 2–4 plain lines with a numeric example, and give a one-line reminder the next few times it comes up:
     - Calculus: derivatives, partial derivatives, Taylor expansion, integrals, e^x and ln x
     - Finance: continuous compounding and discounting, forwards, put–call parity, no-arbitrage, short selling
     - Python: keep code beginner-friendly. Use plain NumPy, comment every line that isn't obvious, and say what output to expect. Never assume pandas or SciPy knowledge without explaining it.
   Build up one step at a time. If a derivation needs more than about three new ideas, split it across days. Teach at Hull's level: intuition, discrete-time approximations (Δz = ε√Δt), riskless-portfolio arguments and numerical examples. **No measure theory**: no σ-algebras, atoms, Radon–Nikodym derivatives or formal proofs. Say "the information available at time t" in words, and only write E[· | Fₜ] or E_t[·] when Hull does.
   - **Use Hull's notation**: Wiener process `z` with `dz` (not W/dW); `dS = μS dt + σS dz`; `ΔS/S = μΔt + σε√Δt`; Itô's lemma for `G(x, t)`; derivative price `f`; portfolio `Π`; `N(d₁)`, `N(d₂)`; `Ê` for risk-neutral expectation; λ for the market price of risk.
   - Each lesson names the matching Hull chapter by **title** and section (e.g. "Hull — *Wiener Processes and Itô's Lemma*, 'The Process for a Stock Price'"), not by number, since chapter numbers change between editions. Where Hull has a worked example, mirror its style with fresh numbers.
   - One-off note for Day 2: say in one line that the course now follows Hull. The atom bookkeeping from Day 1 is optional scaffolding; only the idea "decisions at time t use only information up to t" carries forward.
4. If `feedback.md` has open entries, add one short reinforcement item for each (max 2) before the new material.
5. If the learner's replies show the pace is too fast (2+ consecutive struggles), insert a consolidation day: re-teach the weak concept from a new angle and do not advance `last_lesson_index`. Record it in the Log as `Day N — date — Consolidation: <topic>`.

## Progress

- `day_number`: 7
- `week_number`: 2
- `last_lesson_index`: 7
- `part`: (none)
- `last_sent_date`: 2026-10-28
- `last_topic`: L7 American options on trees; u = e^{σ√Δt}; more steps
- `last_lesson_file`: lessons/2026-10-28.md

## Log

(newest at the bottom; e.g. `Day 1 — 2026-10-20 — L1 Probability spaces, filtrations & information`)

Day 1 — 2026-10-20 — L1 Probability spaces, σ-algebras as information & filtrations
Day 2 — 2026-10-21 — L2 Normal & lognormal distributions; simple vs continuously compounded returns
Day 3 — 2026-10-22 — L3 Expectations given today's information, martingales, discounting
Day 4 — 2026-10-23 — L4 One-step binomial tree: no-arbitrage, riskless portfolio, Δ
Day 5 — 2026-10-26 — L5 Risk-neutral valuation; real world vs risk-neutral world
Day 6 — 2026-10-27 — L6 Two-step trees: backward induction, Δ through the tree
Day 7 — 2026-10-28 — L7 American options on trees; u = e^{σ√Δt}; more steps

## Roadmap (follows Hull's chapter order; chapter titles in *italics*)

### Module A — Foundations Hull takes for granted, then binomial trees
1. Information up to time t (done on Day 1, taught with more formality than the rest of the course)
2. Normal & lognormal distributions; simple vs continuously compounded returns; E and Var of a lognormal (*The Black–Scholes–Merton Model*: lognormal property preview)
3. Expectations "given today's information" and the fair-game (martingale) idea, intuitively; discounting
4. One-step binomial tree: no-arbitrage, riskless portfolio, Δ = (f_u − f_d)/(S₀u − S₀d) (*Binomial Trees*)
5. Risk-neutral valuation: p = (e^{rΔt} − d)/(u − d), why μ drops out, the real world vs risk-neutral world (*Binomial Trees*)
6. Two-step trees, European puts/calls by backward induction; delta changing through the tree (*Binomial Trees*)
7. American options on trees; matching volatility u = e^{σ√Δt}, d = 1/u; increasing the number of steps (*Binomial Trees*)
8. Module review: from trees to continuous time

### Module B — *Wiener Processes and Itô's Lemma*
9. The Markov property and continuous-time stochastic processes
10. The Wiener process: Δz = ε√Δt, properties, simulate paths
11. Generalized Wiener process dx = a dt + b dz; Itô process dx = a(x,t) dt + b(x,t) dz
12. The process for a stock price dS = μS dt + σS dz; discrete-time model; Monte Carlo simulation of the stock (Hull's spreadsheet example in NumPy)
13. Why (Δz)² behaves like Δt — the heart of Itô (Hull's technical note / appendix argument)
14. Itô's lemma: statement and Taylor-series derivation (Hull's appendix)
15. Applications: forward contracts F = S e^{r(T−t)}; the lognormal property via G = ln S
16. Correlated processes and Itô's lemma for several variables; module review

### Module C — *The Black–Scholes–Merton Model*
17. Lognormal distribution of S_T; expected return μ vs μ − σ²/2; confidence intervals for S_T
18. Volatility: estimating from historical data; trading days vs calendar days
19. Deriving the BSM differential equation with a riskless portfolio (2 days)
20. Risk-neutral valuation and the BSM pricing formulas; interpreting N(d₁) and N(d₂) (2 days)
21. Implied volatility; dividends (known cash dividends; continuous dividend yield)
22. Module review: BSM three ways (tree limit, PDE, risk-neutral expectation)

### Module D — *The Greek Letters*
23. Delta hedging; stop-loss strategy; simulate discrete delta-hedging P&L
24. Theta and gamma; Θ + rSΔ + ½σ²S²Γ = r Π
25. Vega and rho; making a portfolio delta-, gamma- and vega-neutral
26. Hedging in practice, scenario analysis; module review

### Module E — *Volatility Smiles* and *Basic Numerical Procedures*
27. Volatility smiles: why put and call smiles match, equity skew, FX smile, volatility surfaces
28. Monte Carlo simulation for option pricing; antithetic variates and control variates
29. Finite difference methods (explicit and implicit) for the BSM equation
30. Module review

### Module F — *Martingales and Measures*
31. Market price of risk λ = (μ − r)/σ, from a riskless-portfolio argument
32. Martingales and the equivalent martingale measure result; choice of numeraire
33. Alternative numeraires: money market account, zero-coupon bond (forward risk-neutral world), annuity
34. Multiple independent factors; Black's model revisited; the option to exchange one asset for another
35. Change of numeraire and drift adjustments; module review

### Module G — *Exotic Options*
36. Binary options: cash-or-nothing and asset-or-nothing
37. Barrier options (knock-in/out; in–out parity)
38. Asian and lookback options with Monte Carlo
39. Module review

### Module H — *Interest Rate Derivatives: Models of the Short Rate* and *HJM, LMM*
40. Equilibrium short-rate models: Rendleman–Bartter, Vasicek, CIR; mean reversion
41. Bond prices in Vasicek and CIR: P(t,T) = A(t,T)e^{−B(t,T)r}
42. No-arbitrage models: Ho–Lee and Hull–White; trinomial trees
43. HJM and the LIBOR market model (intuition); module review

### Module I — *More on Models and Numerical Procedures*
44. Merton's jump-diffusion model
45. Stochastic volatility models and how they generate smiles
46. Implied volatility function (local volatility) model
47. American options by Monte Carlo (Longstaff–Schwartz least-squares)
48. Capstone: price and hedge a product end-to-end (2 days)
49. Course review & where to go next

After item 49, start **Cycle 2: practice problems**: one Hull end-of-chapter style or interview-style problem per day, cycling through Modules A–I. Append the planned items here before teaching them.
