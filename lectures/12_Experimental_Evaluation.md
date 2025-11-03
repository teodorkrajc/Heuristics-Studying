# 2IRR60 Heuristic Algorithms
### 2025-26 Q1 Lecture 12 – Experimental Evaluation

## Heuristic Algorithms
Heuristics compute approximate solutions to optimization problems, typically without guarantees on optimality or runtime.

**Categories:**
- Greedy algorithms
- Local search (hill climbing, tabu, simulated annealing)
- Population-based (GA, PSO, ACO)
- Metaheuristics – general-purpose, problem-independent strategies
- Exact solvers – rely on heuristics internally (branch & bound)

---

## No Free Lunch Theorem (NFLT)
> “Over all possible problems, all algorithms perform equally well.”

Meaning:
- For every problem where algorithm A outperforms B, there exists another where B outperforms A.
- There is **no universally best heuristic**.

Implication:
- Must test algorithms on specific problem classes and datasets.

---

## Experimental Evaluation of Algorithms

### Step 1: Choose Heuristics
Compare multiple algorithms or parameter variants.

Requirements:
- Same problem instance sets
- Same parameter settings throughout runs
- Include **baseline** (simple) and **target** (best-known/optimal) algorithms

---

### Step 2: Choose Datasets
Two main types:

**Real-world datasets**
- Measured data from real applications
- Typically messy (noise, missing values)
- Best for domain-specific evaluation

**Synthetic datasets**
- Generated computationally
- Easier control over parameters, distributions
- Must mimic real-world data (uniform random often unrealistic)

**Benchmark datasets**
- Curated collections for reproducibility (e.g., TSPLIB, SATLIB)

---

### Step 3: Analyze Dataset Parameters
Performance depends on **hidden parameters** like:
- Problem size (scalability)
- Graph density
- Data uniformity
- Weight or profit ranges
- Clause-variable ratio (for SAT)

Average performance across all datasets often meaningless.

---

### Step 4: Define Performance Measures

Two main aspects:
1. **Running time** (wall clock, CPU time, etc.)  
2. **Solution quality** (objective function value, relative improvement, etc.)

Multi-objective trade-offs: speed vs accuracy.

---

### Step 5: Run Experiments
Ensure **identical runtime environments**:
- Same hardware and software
- Same random seed handling
- Repeated trials (≥5) for averaging

Example setup:
```
CPU: Intel i7-6700K @ 4GHz (8 cores)
RAM: 16 GB
OS: Windows 10
Language: Java 21
Single-threaded
```
Each run repeated 5×, averages reported.

---

### Step 6: Present Results

**Option 1: Tables**
- Exact values per dataset  
- Precise but trends hard to spot

**Option 2: Line plots**
- Show performance vs parameter (e.g., instance size)

**Option 3: Bar charts**
- Compare algorithms visually (add variance/error bars)

**Option 4: Scatter plots**
- Show trade-offs (quality vs runtime)

---

## Example: Benchmark Analysis

- Tables of solution costs and runtimes per dataset.  
- Line plots showing runtime scaling on random data.  
- Bar charts comparing relative solution quality vs baseline.  
- Scatter plots displaying runtime vs relative cost.

---

## Multi-Objective Optimization

### Definition
Optimization involving multiple conflicting objectives.

Examples:
- Taxi routing: minimize #taxis **and** total distance.
- Tournament scheduling: maximize fairness **and** diversity.

---

### Pareto Optimality
A solution is **Pareto optimal** if no objective can improve without worsening another.

**Pareto front** = set of all non-dominated solutions.

Goals:
- Quantify trade-offs
- Compute representative Pareto set
- Enable decision maker to choose preference

---

### Methods for Multi-Objective Optimization

| Method Type | Description |
|:--|:--|
| No preference | Solve once, decision afterward |
| A priori | Weight objectives before solving |
| A posteriori | Compute Pareto set, decide later |
| Interactive | Iteratively refine preferences |

---

### A Posteriori Methods
Extend (meta)heuristics to maintain Pareto sets.

**Option 1:** Compute Pareto solutions one-by-one  
**Option 2:** Compute entire Pareto front using population-based heuristics.

Examples:
- Multi-objective evolutionary algorithms (MOEA)
- Particle Swarm variants
- Novelty search algorithms

---

### Example – Tournament Optimization
Find optimal match assignments balancing **skill fairness** and **diversity of opponents**.

Approach: scalarize multiple objectives or evolve Pareto set of team configurations.

---

**End of Lecture 12**
