# 2IRR60 Heuristic Algorithms
### 2025-26 Q1 Lecture 10 – SMT Solving and Linear Programming (LP)

## Exact Solvers – Outline
9. Branch and Bound and SAT Solving  
10. SMT Solving and Linear Programming  
11. Integer Linear Programming  
12. Experimental Evaluation  

Topics today:
- DPLL Branching Heuristics  
- Satisfiability Modulo Theories (SMT)  
- Linear Programming (LP)  

## DPLL Heuristics

### Branching Heuristics
Let **C** be the current CNF clause set during DPLL.

**Simple heuristics**
- **Pure Literal Elimination (PLE):** pick literal `ℓ` if only `ℓ` (and not `¬ℓ`) appears in any clause of C  
- Only return literals that appear in clauses (others irrelevant)  
- Prefer literals from small clauses → more unit propagation, fewer recursive calls  

**Other successful heuristics**
At each step, pick `ℓ` that maximizes a measure function:

- **DLIS (Dynamic Largest Individual Sum):**  
  `DLIS(C, ℓ) = |{ c ∈ C : ℓ ∈ c }|`  
- **Jeroslow–Wang (JW):**  
  `JW(C, ℓ) = Σ_{c∈C, ℓ∈c} 1 / 2^{|c|}`  

## Satisfiability Modulo Theories (SMT)

### Motivation
SAT solves Boolean logic only. SMT extends SAT with **theory solvers** for arithmetic, arrays, etc.

**Example formula:**
```
(a > 3 ∨ b = 2) ∧ (a + b < 10)
```

## Theory Solvers in SMT Solvers
Modern solvers (e.g., Z3) include:

- Linear real arithmetic (LIA)  
- Non-linear arithmetic (NIA)  
- Equalities and Uninterpreted Functions (EUF)  
- Array theory  
- Bit-vectors  
- Floating-point, strings, data types, ODEs, etc.

## Heuristics in SMT Solvers
Interface via **tactics**

| Command | Description |
|:--|:--|
| simplify | rewrite formulas |
| solve-eqs | Gaussian elimination |
| bit-blast | reduce to SAT |
| propagate-values | propagate equalities |
| split-clause | split into sub-goals |

Example:
```java
Tactic t = ctx.MkTactic("simplify");
t.Apply(g);
```

## SMT Optimization
Optimization via repeated solving or dedicated branch-and-bound.

```java
for (int i = 0; i < M; i++) {
  obj = ctx.mkAdd(obj, ctx.mkITE(x[i], ctx.mkInt(c[i]), ctx.mkInt(0)));
}
Optimize opt = ctx.mkOptimize();
opt.MkMinimize(obj);
```

## Linear Programming (LP)

### Definition
Optimize a **linear cost function** under **linear constraints**.

Example:
```
x₁ + x₂ ≤ 12
x₁ + 5x₂ ≤ 35
x₁ ≥ 0, x₂ ≥ 0
maximize 2x₁ + 4x₂
```

Convex feasible region → unique optimal solution.

## Standard Form
maximize **cᵀx** subject to **A·x ≤ b**, **x ≥ 0**

## LP Rewriting
- Minimization → maximize −f(x)  
- Equalities → two inequalities  
- x = x⁺ − x⁻ for negatives  
- Strict → approximate with ≤ ε

## Modeling Procedure
1. Define decision variables  
2. Add linear constraints  
3. Define objective  
4. Convert to standard form  

## Example – Max-Flow
Variables: fᵢⱼ  
Constraints: fᵢⱼ ≤ cᵢⱼ, flow conservation  
Objective: maximize Σ fₛⱼ  

## Example – Shortest Path
Distance variables or flow variables encoding.  

## Duality in LP
Primal: maximize **cᵀx** s.t. A·x ≤ b, x ≥ 0  
Dual: minimize **bᵀy** s.t. Aᵀ·y ≥ c, y ≥ 0  

**Strong Duality:** cᵀx = bᵀy if feasible.

## LP Algorithms

| Algorithm | Inventor | Behavior | Complexity |
|:--|:--|:--|:--|
| Simplex | Dantzig | boundary walk | Exponential worst-case |
| Ellipsoid | Khachiyan | encloses region | Polynomial, slow |
| Interior-Point | Karmarkar | inside feasible region | Polynomial, fast |

→ **Linear Programming ∈ P**.

## LP Variants
- Quadratic Programming  
- Convex Programming  
- Integer Linear Programming (NP-hard)

**Rule of Thumb:**  
Single local optimum → P  
Multiple → NP-hard  

**End of Lecture 10**
