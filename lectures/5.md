# 2IRR60 Heuristic Algorithms
### 2025-26 Q1 Lecture 5 – Ant Colony Optimization

---

## Quick Recap
Building solutions step-by-step by making **choices**.

Examples of representations:
- **Bitstring:** choose next bit 0 or 1  
- **Permutation:** choose next element in order  

---

## Greedy Algorithms
Always make the *best* choice based on the current partial solution.  

- Usually not optimal  
- Often a good heuristic  
- Not a metaheuristic but widely used  

*(Not covered in the book.)*

---

## Local Search
Improves a single solution using neighborhood moves.  

---

## Iterative Improvement
Repeatedly move to better neighbors until no improvement is possible.  

---

## Tabu Search
Remembers which solutions were already visited.  
Next → best unvisited solution.  
Effectively **changes the neighborhood** based on memory.  

---

## Simulated Annealing
Accepts worse moves with a small probability.  
Balances exploration (escaping local minima) and exploitation.  

---

## Population-Based Metaheuristics
Ant Colony Optimization (ACO) is part of this family.  

---

## Why Ant Colonies?
An individual ant is not very intelligent (tiny brain)...  
…but together, they can solve complex problems.  

→ Emergent collective behavior  
→ Great for optimization  

*(Slides showed ants forming a shortest-path trail between nest and food source.)*

---

## Ant Colonies
Ants communicate indirectly via pheromones — chemical trails that evaporate over time.  
Paths with stronger pheromone concentrations are more attractive.

This collective mechanism leads to discovering shortest or most efficient paths.

---

## Simulation
*(Illustrations of ants exploring multiple paths and eventually converging on the shortest one.)*

---

## Ant Colony Optimization – Ant System
Each ant constructs a path (solution) step by step, influenced by:
- **Pheromone level (τ):** memory of past successful paths  
- **Visibility (η):** heuristic desirability (e.g., 1/distance)

After completing all tours, pheromone trails are updated based on path quality.

---

### Optimal Path Example
Slides illustrated several paths with different lengths (6, 7, 4),  
showing convergence toward the shortest (length 4).

---

### Example of Pheromone and Visibility
Ant chooses next node `j` from `i` with probability:

`P(i,j) = [τ(i,j)]^α * [η(i,j)]^β / Σ([τ(i,k)]^α * [η(i,k)]^β)`

where:  
- τ(i,j): pheromone trail strength  
- η(i,j): visibility (e.g., 1/distance)  
- α, β: parameters controlling influence

*(Tables in slides compared pheromone values and visibilities.)*

---

## Minimization Problem
ACO typically used for minimization (e.g., shortest path, minimal cost).  

---

## Variants / Extensions
Different versions of the algorithm modify pheromone update rules:  
- Ant System (AS)  
- Ant Colony System (ACS)  
- Max-Min Ant System (MMAS)

---

## Convergence
Some variants can be proven to converge to the **globally optimal solution**,  
but there are no practical bounds on the speed of convergence.

In general:
- Convergence is not guaranteed for all problems.  
- Algorithm performance is sensitive to parameter settings.

---

## Properties
- Essentially a **probabilistic greedy algorithm** with added feedback.  
- Produces fairly good solutions (not always optimal).  
- Works well in **dynamic environments** (e.g., changing graphs).  

---

## Implementation
- Each ant builds a path independently → **easy parallelization**.  
- Pheromones updated globally after all ants complete their tours.  
- Stop after:
  - Fixed number of iterations, or  
  - Pheromone levels stabilize.

*(Slides showed several algorithm execution snapshots.)*

---

## Parameter Choices
Important parameters:
- α: influence of pheromone trails  
- β: influence of visibility  
- ρ: pheromone evaporation rate  
- m: number of ants per iteration

Performance strongly depends on these settings.

---

## When to Use Ant Colony Optimization?
**Advantages**
- Adapts to dynamic changes (e.g., real-time routing)  
- Provides distributed, robust search  
- Easy to parallelize  

**Disadvantages**
- Slower convergence than greedy or local search  
- Sensitive to parameter tuning  
- Computationally expensive for large graphs  

---

## A Short Tangent: Beam Search and Related Methods
**Greedy algorithm:**  
Finds a single best path in the construction tree.

**Backtracking:**  
Explores the entire tree with pruning.

**Dynamic Programming:**  
Reuses overlapping subproblems.

**Beam Search:**  
Explores multiple best partial paths simultaneously (width = number of paths per level).

---

### Incremental Construction Comparison

| Approach | Exploration | Memory | Parallelism |
|-----------|--------------|---------|--------------|
| Greedy | Low | Low | Single path |
| Backtracking | High | High | Sequential |
| Beam Search | Medium | Moderate | Parallel |
| Ant Colony Optimization | Medium–High | Moderate | Highly parallel |

---

**End of Lecture 5**
