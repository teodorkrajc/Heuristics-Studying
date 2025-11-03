# 2IRR60 Heuristic Algorithms
### 2025-26 Q1 Lecture 9 – Branch and Bound (B&B) and DPLL

---

## Overview
Two classic **complete search algorithms**:
- **Branch and Bound (B&B)** – for optimization problems.  
- **DPLL (Davis–Putnam–Logemann–Loveland)** – for satisfiability problems (SAT).  

Both are systematic search methods that prune parts of the search tree that cannot yield better or feasible solutions.

---

## Branch and Bound (B&B)

### Key Idea
- Systematically explore the solution space using a **search tree**.
- Each node represents a **partial solution**.
- Use **bounds** to avoid exploring unpromising branches.

---

## Example – Traveling Salesperson Problem (TSP)
Goal: find the shortest tour visiting all cities once.

1. Start with a partial path.  
2. Compute a **lower bound** (minimum possible total length).  
3. If lower bound ≥ best known tour, prune the branch.  
4. Otherwise, expand further.

---

### Step-by-Step Example

1. Initial node: no cities visited.  
   - Bound: 0.  
2. Add next city → update bound.  
3. If bound < current best → keep exploring.  
4. Otherwise, backtrack.

*(Slides illustrated a tree expanding partial tours, with subtrees pruned when bounds exceeded current best.)*

---

## Components of B&B

| Component | Description |
|:--|:--|
| **Branching** | Split the problem into subproblems (divide search space). |
| **Bounding** | Compute upper/lower bounds on possible solutions. |
| **Pruning** | Discard subproblems whose bounds show they cannot improve the best solution. |
| **Search Strategy** | DFS, BFS, best-first, or heuristic ordering. |

---

## Pseudocode

best ← ∞
procedure BnB(node):
if node is complete:
if f(node) < best:
best ← f(node)
return
bound ← lower_bound(node)
if bound ≥ best:
return # prune
for child in expand(node):
BnB(child)


---

## Bound Computation
The **quality of the bound** is crucial for efficiency.

- Tight bounds → strong pruning → faster convergence.  
- Weak bounds → more exploration → slower runtime.  

---

## Example: Knapsack Problem
Maximize total value without exceeding capacity.

- **Branch:** choose whether to include an item.  
- **Bound:** fractional (LP-relaxed) upper bound on achievable value.  
- **Prune:** if bound < current best.

---

## Visualization
*(Slide diagram showed a binary tree, with branches labeled “include item” and “exclude item.” Some branches cut off early when bounds insufficient.)*

---

## Search Strategies
- **Depth-first:** uses less memory, may find good solutions early.  
- **Best-first:** explores nodes with best bound first (more pruning).  
- **Breadth-first:** level-order search, systematic but expensive.  

---

## Advantages and Disadvantages

**Advantages**
- Guarantees optimal solution.  
- Can drastically reduce search compared to brute force.  
- Applicable to many discrete optimization problems.

**Disadvantages**
- Still exponential in worst case.  
- Performance depends on bound strength.  
- Hard to parallelize efficiently.

---

## Relation to Metaheuristics
- Metaheuristics (GA, ACO, SA, etc.) are **incomplete** → find good solutions quickly.  
- Branch and Bound is **complete** → guarantees optimality.  
- Hybrid approaches: use heuristic solutions as initial bounds.

---

## DPLL – SAT Solving

### Problem
Given a Boolean formula in CNF (Conjunctive Normal Form),  
determine if it can be satisfied (True assignment exists).

---

## Example CNF
(¬x₁ ∨ x₂) ∧ (¬x₂ ∨ x₃) ∧ (x₁ ∨ ¬x₃)

Goal: assign True/False to x₁, x₂, x₃ so that all clauses are True.

---

## Backtracking Search for SAT
1. Choose a variable.  
2. Assign True or False.  
3. Simplify formula.  
4. If contradiction → backtrack.  
5. Repeat until solution found or all assignments tried.

---

## DPLL Algorithm
An optimized backtracking SAT solver.

### Enhancements
- **Unit propagation:**  
  If a clause has only one literal left, force it to satisfy the clause.  

- **Pure literal elimination:**  
  If a literal appears with one polarity only, fix it accordingly.

- **Backtracking:**  
  If a conflict arises, undo last decisions.

---

## Pseudocode
function DPLL(Φ):
Φ ← unit_propagate(Φ)
Φ ← pure_literal_assign(Φ)
if Φ contains empty clause:
return False
if Φ is satisfied:
return True
choose variable x
return DPLL(Φ ∧ x) or DPLL(Φ ∧ ¬x)


---

## Example Step-by-Step

1. Start with `(¬x₁ ∨ x₂) ∧ (x₁ ∨ ¬x₃) ∧ (¬x₂ ∨ x₃)`  
2. Choose x₁ = True → simplify.  
3. Unit clause forces x₃ = True.  
4. All clauses satisfied → SAT.

---

## Search Tree Representation
Each node = partial variable assignment.  
Branches correspond to setting a variable True/False.  
Pruning occurs when a contradiction (empty clause) appears.

*(Slide diagram showed binary SAT search tree with some branches pruned early.)*

---

## Relation Between B&B and DPLL

| Aspect | Branch & Bound | DPLL |
|:--|:--|:--|
| Problem Type | Optimization | Decision (SAT) |
| Uses Bounds | Yes | No (logical pruning instead) |
| Guarantees | Optimal solution | Satisfiability / UNSAT proof |
| Structure | Search tree | Search tree |
| Pruning | Bound-based | Clause-based |

---

## Modern Extensions
- **CDCL (Conflict-Driven Clause Learning):** adds learned constraints to prevent repeating conflicts.  
- **Hybrid SAT/Optimization Solvers:** integrate bounding strategies with logical reasoning.  

---

## When to Use
- **B&B:** combinatorial optimization (TSP, Knapsack, scheduling).  
- **DPLL:** satisfiability, verification, model checking.

---

## Summary
Branch and Bound and DPLL are foundational **systematic search algorithms**:
- B&B: uses bounds to prune.  
- DPLL: uses logic and propagation to prune.  
Both provide complete solutions and inspire hybrid and modern metaheuristic techniques.

---

**End of Lecture 9**
