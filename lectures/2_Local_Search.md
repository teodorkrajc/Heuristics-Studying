# 2IRR60 Heuristic Algorithms
### 2025-26 Q1 Lecture 2 – Local Search

---

## Local Search

**Scenario:**  
You are lost in a foggy forest. You want to find the **highest point**, so that you can look over the clouds.  
How do you find the highest point?

> *(Image: cartoon person in foggy forest, climbing hills and evaluating local maxima.)*

---

## Optimization Problem

We want to find the *best* (highest-value) solution in a given **solution space**.

---

### Solution Space Examples

- **Bitstrings** – binary optimization  
- **Permutations** – combinatorial optimization problem  
- **Continuous domains** – e.g., function optimization  

> *(Image: diagram with points labeled a → f on a hilly terrain showing local peaks.)*

---

## Solution Representations

Examples of different ways to represent a solution:

| Example | Representation | Comment |
|----------|----------------|----------|
| Bitstring | 010101... | Easy to manipulate |
| Permutation | (a, b, c, d, e) | Order matters |
| Assignment | {(a, 4), (b, 1), (c, 3), (d, 2), (e, 5)} | General mapping form |

**Good representation should:**
- Make all possible solutions representable  
- Require few/simple constraints  
- Allow easy updates  

---

### Example Representation

{(a, 4), (b, 1), (c, 3), (d, 2), (e, 5)}
W = 18  
*(Image: simple diagram showing mapping between letters and numbers.)*

---

## Neighborhoods

A **neighborhood** N(s) defines which solutions are “close” to s.

Typical operations:
- Flip one bit  
- Swap two elements in a permutation  
- Move a single component to a new value  

> *(Image: graph showing nodes as solutions connected to their neighbors.)*

---

### Example – Max-Ones Problem

- Objective: maximize number of 1’s in a bitstring.  
- **Bad** solution → few 1’s (“Terrible!”)  
- **Good** solution → many 1’s (“Great!”)

*(Slide showed “Terrible!” vs “Great!” labels.)*

---

## Constraints

Some solution spaces have additional constraints.  
Example: assignment must be valid (no duplicates, capacity limits, etc.).  
Neighborhood moves must keep feasibility or use repair heuristics.

---

## Local Search Methods

### Single-Solution Approaches
- **Random Search / Random Walk**
- **Iterative Improvement (Hill Climbing)**
  - Includes gradient descent
- **Probabilistic Hill Climbing**
- **Iterated Local Search**
- **Variable Neighborhood Search**

---

### Random Search & Random Walk

Start with random solutions, evaluate repeatedly.  
No guarantee of improvement.  
Used as baseline or diversification.

---

### Iterative Improvement (Hill Climbing)

Start with random solution s  
→ repeatedly move to the best neighbor if it improves the objective.

- Stops when no neighbor is better → **local optimum**.  
- Exploits local structure, but can get stuck.  

*(Image: hill-climber moving uphill, stops at local peak.)*

---

### Gradient Descent (continuous variant)

Move in direction of steepest descent (minimization) or ascent (maximization).

---

### Probabilistic Hill Climbing

Instead of always taking the best move, take better moves with high probability and sometimes worse moves with small probability → more exploration.

---

### Iterated Local Search

Combine repeated local searches with random perturbations to escape local optima.

---

### Variable Neighborhood Search

Systematically change the neighborhood structure during search.  
- Alternate between small and large neighborhoods.  
- Reduces risk of stagnation.

---

## Examples

### Example – Traveling Salesperson Problem (TSP)

Algorithm: Iterative Improvement  
Neighborhood: Swap adjacent nodes  

> *(Images: a → h labeled cities connected in routes)*

| Iteration | Path Length | Comment |
|------------|-------------|----------|
| 0 | 33 | Initial solution |
| 1 | 32.7 | Slight improvement |
| 2 | 31.8 | Better route |
| 3 | 29 | Continued improvement |
| 4 | 25.7 | Still improving |
| 5 | 24.5 | Near optimum |
| 6 | 22.3 | Best found |
| 7 | 31.4 | Moved to worse neighbor (local minimum) → stuck ! |

*(Series of diagrams: each shows route and length improving, final one highlights a local minimum.)*

---

### Local Minimum ?!

Sometimes the algorithm gets trapped—no improving moves available even though better solutions exist elsewhere.

---

### Example – TSP with 2-Opt Neighborhood

**Algorithm:** Iterative Improvement  
**Neighborhood:** 2-Opt (edge exchange)

- Removes two edges and reconnects paths differently.  
- Often yields shorter routes.  

| Iteration | Length | Note |
|------------|--------|------|
| 0 | 31.4 | Initial |
| 1 | 28.1 | Improved route |

> *(Image: diagram illustrating 2-Opt swap.)*

---

### Example – N-Queens Problem

**Problem:** Place N queens on a chessboard so that none attack each other.  
Not originally an optimization problem → turn into one.

**Objective function:**
- f = number of conflicts (minimize)  
- 0 means valid solution.

**Neighborhood:** Move a queen by one square.

| Step | #Conflicts | Comment |
|------|-------------|----------|
| 0 | 6 | Initial layout |
| 1 | 4 | Improved |
| ... | → 0 | Goal: no conflicts |

*(Images: board showing queens and attack lines decreasing.)*

---

### Other Techniques (overview)

- Random Restart Local Search  
- Greedy Search  
- Adaptive Neighborhoods  
- Hybrid Methods (e.g., Simulated Annealing, Tabu Search)

---

**Summary:**
Local search explores the neighborhood of a current solution and iteratively improves it.  
Strengths – simple and effective on many problems.  
Weakness – risk of getting stuck in local optima.

---

End of Lecture 2.
