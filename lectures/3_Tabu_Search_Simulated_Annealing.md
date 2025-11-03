# 2IRR60 Heuristic Algorithms
### 2025-26 Q1 Lecture 3 – Tabu Search & Simulated Annealing

---

## Quick Recap
Local Search → Iterative Improvement → risk of getting stuck in local optima.

---

## Local Search and Neighborhoods

**Common techniques**
- Random Search & Random Walk  
- Iterative Improvement (hill climbing, gradient descent)  
- Probabilistic Hill Climbing  
- Iterated Local Search  
- Variable Neighborhood Search

---

## When to Use Iterative Improvement
Good for smooth landscapes with many improving moves, but fails with many local optima.

**Advantages**
- Simple  
- Fast on small or smooth problems  

**Disadvantages**
- Gets stuck in local optima  
- No diversification

---

## Tabu Search

**Problem 1:** Stuck in a local optimum → Allow non-improving moves.  
**Problem 2:** Repeated cycling back to the same solutions → Remember where you’ve been.

---

### Core Idea
“Remember” which solutions we’ve already visited.  
Next solution = best non-tabu neighbor.  

This effectively changes the neighborhood based on memory.

---

## Memory Concept

### Simple Tabu List
List of visited solutions – prevents revisiting the same points.

### Smarter Memory
Forbid specific moves or attributes instead of whole solutions.

### Memory Types
- **Short-term memory:** prevents cycling (recent moves).  
- **Long-term memory:** promotes diversification and exploration.

---

## Tabu List Mechanism
- Storing entire solutions is expensive.  
- Instead store moves (e.g., “swap a ↔ b”).  
- Forbid undoing those moves for several iterations.  

**Goal:** Avoid cycles and maintain exploration.

---

### Example Move
swap g and h
This move becomes tabu for *k* iterations.

---

## Aspiration Criteria
Sometimes a tabu move can be allowed again if it leads to a better solution than any found so far.

---

## Example – Assignment Problem

**Neighborhood:** Swap assignments  
**Tabu list:** Store assignment edges

| Iteration | Cost | Comment |
|------------|------|----------|
| 0 | 31 | Initial solution |
| 1 | 30 | Improvement |
| 2 | 26 | Continued improvement |
| 3 | 23 | Better |
| 4 | 22 | Best found |

*(Slides showed a 6×6 assignment matrix, with highlighted tabu edges.)*

---

## Simulated Annealing

Hill climbing is deterministic → stuck in local optima.  
We allow probabilistic acceptance of worse moves to escape.

---

### Analogy
Based on annealing in metallurgy:  
- Material is heated and slowly cooled to reach a low-energy state.  

**Optimization analogy:**  
- Start with high temperature → explore broadly.  
- Slowly cool → converge to near-optimal solution.

---

### Simplified Algorithm

SimulatedAnnealing(s₀, T₀):
s ← s₀
best ← s
while not terminated:
s′ ← random neighbor of s
Δ ← f(s′) − f(s)
if Δ > 0 → accept s′
else accept with probability exp(Δ / T)
T ← cool(T)
if f(s′) > f(best) → best ← s′
return best


---

### Temperature
- High T → more exploration  
- Low T → more exploitation  

*(Graph on slides: probability curve dropping from 1.0 to 0.0 as temperature decreases.)*

---

## Why Simulated Annealing?
- Generalization of random iterative improvement  
- Allows escape from local optima  
- Simple algorithm  
- Combines exploration and exploitation  
- Stochastic rather than deterministic

---

## Deterministic Variant – Threshold Accepting
Accept moves with Δ ≥ −θ (threshold).

**Pros:** Simple, deterministic  
**Cons:** Less adaptive

---

## Markov Chain Interpretation
The search process forms a **Markov chain**:
- States = candidate solutions  
- Transitions = move probabilities depending on temperature  

Eventually converges to a stationary distribution,  
where the probability of a state s is proportional to `exp(−f(s)/T)`.

*(Slides showed 4-node example: A, B, C, D with transition probabilities.)*

---

## Summary

| Method | Key Idea | Memory | Exploration | Stochastic | Escape Mechanism |
|:--|:--|:--|:--|:--|:--|
| Tabu Search | Avoid cycles via memory | Yes | Medium | No | Tabu list |
| Simulated Annealing | Accept worse moves probabilistically | No | High (early) | Yes | Probabilistic |

---

**End of Lecture 3**
