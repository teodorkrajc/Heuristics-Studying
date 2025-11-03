# 2IRR60 Heuristic Algorithms
### 2025-26 Q1 Lecture 4 – Simulated Annealing II

---

## Quick Recap
Avoiding local optima → Tabu Search and Simulated Annealing.

---

## Tabu Search Memory
**Idea:** “Remember” which solutions we’ve already visited to avoid cycling.

### Memory Types
- **Short-term:** recent solutions or moves (tabu list).  
- **Long-term:** promotes exploration and diversification.

### Tabu List
- Simple version – list of visited solutions.  
- Smarter version – forbid specific moves or attributes.  
- Helps balance exploration and exploitation.

---

## Simulated Annealing
**Probabilistic hill-climbing**: accept worse moves with some probability.

Acceptance probability ≈ `exp(−Δ/T)` (for minimization).

- High T → more exploration  
- Low T → strong exploitation  

*(Slide graph showed acceptance dropping from 1.0 to 0.0 as T decreases.)*

---

## Why Use Simulated Annealing?
- Generalization of random iterative improvement  
- Performs more exploration  
- Can escape local optima  
- Simple and robust  
- Not deterministic → more adaptive  

---

## Deterministic Variant – Threshold Accepting
Replace probabilistic rule with a fixed threshold θ: accept if Δ ≥ −θ.

**Pros:** simpler, deterministic  
**Cons:** less adaptive to landscape  

---

## Performance Analysis
The search process forms a **stochastic Markov chain**.

- States = solutions  
- Transitions = probabilistic moves depending on temperature  
- Goal → probability of reaching a global optimum  

---

### Markov Chain View
Homogeneous Markov chain example (A, B, C, D) with transition probabilities.

Eventually, probabilities stabilize → **stationary distribution**  

At equilibrium: `P(s) ∝ exp(−f(s)/T)`  

As T → 0, probability mass concentrates on global optima.  

---

## Takeaways

| Aspect | Tabu Search | Simulated Annealing |
|:--|:--|:--|
| Memory | Yes (short + long term) | No |
| Exploration | Moderate | High (initially) |
| Determinism | Deterministic | Stochastic |
| Escapes local optima | Via tabu list | Via probabilistic acceptance |
| Analysis basis | Empirical | Markov-chain theory |

---

**End of Lecture 4**
