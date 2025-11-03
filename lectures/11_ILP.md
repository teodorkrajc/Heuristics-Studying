# 2IRR60 Heuristic Algorithms
### 2025-26 Q1 Lecture 11 – Integer Linear Programming (ILP)

## Overview
- ILP Modeling
- ILP Formulations and Big-M Method
- Performance of ILP Solvers
- Branch and Cut

---

## Integer Linear Programming (ILP)
An **integer linear program** is a linear optimization problem where some or all variables are constrained to take **integer values**.

Example problem:  
Maximize or minimize a linear cost function under linear constraints where at least one variable is integer.

---

## Example: Knapsack Problem
**Input:** n items, each with weight wᵢ and profit pᵢ, maximum capacity W.  
**Output:** subset of items maximizing profit without exceeding capacity.

1. **Variables:** xᵢ – amount or inclusion of item i  
2. **Constraints:**
   - xᵢ ≤ 1 for all i
   - Σ wᵢxᵢ ≤ W
   - xᵢ ∈ ℤ
3. **Objective:** maximize Σ pᵢxᵢ

| Item i | 1 | 2 | 3 | 4 | 5 | 6 |
|:--|:--|:--|:--|:--|:--|:--|
| Weight wᵢ | 5 | 7 | 5 | 8 | 11 | 6 |
| Profit pᵢ | 6 | 7 | 4 | 10 | 14 | 5 |

Fractional variant = LP, Integer variant = ILP.

---

## ILP vs LP Example
Study scheduling example:
```
x₁ + x₂ ≤ 12
x₁ + 5x₂ ≤ 35
x₁, x₂ ≥ 0
x₁, x₂ ∈ ℤ
maximize 2x₁ + 4x₂
```
- LP: continuous solution space → convex polytope.
- ILP: discrete lattice points → NP-hard.
- Two optima: (5,6) and (7,5).

---

## ILP Modeling and Solving

### Modeling
1. Choose real/integer variables to represent feasible solutions.
2. Add linear constraints to enforce feasibility.
3. Define optimization goal (max/min).

### Solving
- Common solvers: **Gurobi, CPLEX, GLPK, SCIP**.  
- Use **branch-and-bound**, **LP relaxations**, and **symmetry reduction**.
- Performance depends on model structure (#variables, encoding, constraints).

---

## ILP Formulations: Boolean Constraints

Propositional constraints become linear integer constraints.

For each Boolean x: add
```
x ≥ 0,  x ≤ 1,  x ∈ ℤ
```

CNF → ILP translation: convert disjunctions to linear inequalities.

### Example: SAT encoding
Formula: ϕ = (x₁ ∨ x₂) ∧ x₃ ∧ (x₁ ∨ x₂ ∨ x₃)

Variables: x₁, ¬x₁, x₂, ¬x₂, x₃, ¬x₃ ∈ {0,1}

Constraints:
```
x₁ + ¬x₁ = x₂ + ¬x₂ = x₃ + ¬x₃ = 1
x₁ + x₂ ≥ 1
x₃ ≥ 1
x₁ + x₂ + x₃ ≥ 1
```
Shows NP-hardness of ILP (reduces SAT to ILP).

---

## SAT Encoding Example – 3-Coloring
Goal: color graph vertices with 3 colors so adjacent vertices differ.

**SAT Encoding:**
```
xᵢ₁ ∨ xᵢ₂ ∨ xᵢ₃   (each vertex has a color)
¬xᵢ₁ ∨ ¬xᵢ₂, etc.  (at most one color)
¬xᵢₖ ∨ ¬xⱼₖ       (edges have different colors)
```

**ILP Encoding:**
```
xᵢ₁ + xᵢ₂ + xᵢ₃ = 1
xᵢₖ + xⱼₖ ≤ 1
xᵢⱼ ∈ {0,1}
```

---

## ILP Formulations: Logic Constraints

| Logic Formula | ILP Formulation |
|:--|:--|
| x ↔ ¬y | x + y = 1 |
| x₁ ∨ x₂ ∨ … ∨ xₙ | x₁ + x₂ + … + xₙ ≥ 1 |
| z ↔ (x₁ ∨ … ∨ xₙ) | z ≥ xᵢ ∀i, z ≤ Σxᵢ |
| x₁ ∧ … ∧ xₙ | xᵢ = 1 ∀i |
| z ↔ (x₁ ∧ … ∧ xₙ) | z ≤ xᵢ ∀i, z ≥ Σxᵢ − n + 1 |
| x ↔ y | x = y |
| z ↔ (x ↔ y) | z ≤ x−y+1, z ≤ y−x+1, z ≥ x+y−1, z ≥ 1−x−y |
| x → y | x ≤ y |
| z ↔ (x → y) | z ≤ y−x+1, z ≥ 1−x, z ≥ y |

---

## ILP Formulations: Arithmetic Constraints

| Arithmetic Constraint | ILP Formulation |
|:--|:--|
| x is odd | x − 2w = 1, w ∈ ℤ |
| x is even | x − 2w = 0, w ∈ ℤ |
| x ≡ y (mod n) | x − nw = y, w ∈ ℤ |
| z = max(x₁,…,xₙ) | z ≥ xᵢ ∀i, minimize z |
| z = min(x₁,…,xₙ) | z ≤ xᵢ ∀i, maximize z |
| z = |x − y| | z ≥ x−y, z ≥ y−x, minimize z |

---

## The Big-M Method

### Idea
Introduce a large constant **M** and binary variable z to model conditional constraints.

| Conditional | ILP Formulation |
|:--|:--|
| z = 0 → f(x) ≤ b | f(x) − Mz ≤ b |
| f₁(x) ≤ b₁ ∨ f₂(x) ≤ b₂ ∨ f₃(x) ≤ b₃ | fᵢ(x) − Mzᵢ ≤ bᵢ, z₁ + z₂ + z₃ ≤ 2 |

Choosing M:
- Use problem-specific upper bounds.
- Tighter M → better performance.

---

## Big-M Example – Square 3-Center Problem

Input: points (a₁,b₁)…(aₙ,bₙ)  
Output: smallest r such that all points covered by 3 r×r squares.

**Variables:**
- xₖ,yₖ – centers of squares
- zᵢₖ ∈ {0,1} – point i covered by square k
- r > 0 – size

**Constraints:**
```
zᵢ₁ + zᵢ₂ + zᵢ₃ ≥ 1
xₖ − r/2 − (1−zᵢₖ)M ≤ aᵢ ≤ xₖ + r/2 + (1−zᵢₖ)M
yₖ − r/2 − (1−zᵢₖ)M ≤ bᵢ ≤ yₖ + r/2 + (1−zᵢₖ)M
```
**Goal:** minimize r.

---

## Big-M Example – Graph 3-Coloring

Variables:
- xᵢ ∈ {1,2,3} (vertex colors)
- zᵢⱼ ∈ {0,1} (alternative condition for edges)

Constraints:
```
xⱼ + 1 − M(1−zᵢⱼ) ≤ xᵢ ≤ xⱼ − 1 + Mzᵢⱼ
```
Goal: any (feasible coloring).

---

## Alternative Encoding – Chromatic Number
Minimize m (≤ K colors) such that no adjacent vertices share a color.

Variables:  
xᵢ ∈ {1..K}, zᵢⱼ ∈ {0,1}, m ∈ ℕ

Constraints:
```
xᵢ ≠ xⱼ  ∀(i,j)∈E
m ≥ xᵢ  ∀i
```
Goal: minimize m.

---

## Encoding Comparison

| Encoding | Variables | Constraints | Notes |
|:--|:--|:--|:--|
| 0/1 Encoding | 3|V| | |V|+3|E| | Simple, intuitive |
| Big-M Encoding | |V|+|E| | 2|E| | Fewer variables, tighter formulation |

---

## Performance of ILP Solvers
Modern ILP solvers rely on:
- **Branch & Bound / Branch & Cut**
- **Cutting planes**
- **Preprocessing and symmetry detection**
- **LP relaxations**

Performance depends on formulation, bounds, and tightness of constraints.

---

**End of Lecture 11**
