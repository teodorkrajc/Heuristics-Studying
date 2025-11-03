# 2IRR60 Heuristic Algorithms
### 2025-26 Q1 Lecture 8 – Evolutionary Algorithms II

---

## Quick Recap
Evolutionary algorithms simulate natural evolution:
- Populations of individuals (solutions)
- Fitness-based selection
- Crossover and mutation  
Goal: evolve increasingly fit solutions.

---

## Example: Genetic Algorithm (Recap)
Each solution is encoded as a **chromosome** (bit string or numeric vector).

**Basic Steps:**
1. Initialize population  
2. Evaluate fitness  
3. Select parents  
4. Apply crossover and mutation  
5. Replace old population  
6. Repeat until termination condition

---

## The Need for Diversity
Evolutionary search relies on diversity to explore.  
If all individuals are too similar:
- The algorithm converges prematurely.
- Local optima are difficult to escape.  

**Mechanisms to maintain diversity:**
- Mutation  
- Random immigrant strategies  
- Fitness sharing  
- Niching methods  

---

## Fitness Sharing
Encourage multiple subpopulations (niches) by reducing fitness in crowded areas.

**Formula:**
f’(i) = f(i) / Σ sh(d(i, j))

where:
- `sh(d)` is a sharing function that decreases with distance  
- `d(i, j)` = distance between individuals i and j  

Effect: individuals close together compete for shared resources → population spreads out.

---

## Niching
Method for maintaining multiple stable subpopulations in multimodal landscapes.

Applications:
- Finding multiple local optima simultaneously.  
- Preserving genetic variety.  

Common techniques:
- **Fitness sharing**
- **Crowding**
- **Speciation (grouping similar individuals)**

---

## Selection Pressure
Controls how strongly fitter individuals dominate reproduction.

- High pressure → fast convergence, less exploration.  
- Low pressure → more exploration, slower convergence.

Trade-off determines algorithm’s success.

---

## Elitism
Always keep the best k individuals unchanged in the next generation.

**Pros:** prevents loss of best solutions  
**Cons:** may reduce diversity  

---

## Genetic Drift
Random loss of alleles (traits) due to finite population size.

Causes:
- Stochastic selection  
- Strong elitism  
- Small population size  

**Result:** population becomes homogeneous even without high selection pressure.

---

## Balancing Parameters
- **Population size (N):** exploration capacity  
- **Mutation rate (pm):** exploration level  
- **Crossover rate (pc):** exploitation level  
- **Selection pressure:** convergence rate  

All interact → parameter tuning is essential.

---

## Example: Parameter Impact
Too small a population → stagnation.  
Too high mutation → random search.  
Too strong selection → premature convergence.  
Balanced parameters → steady improvement.

*(Slides showed fitness vs. generation graphs with varying mutation/selection strengths.)*

---

## Hybrid Evolutionary Algorithms
Combine EAs with other optimization techniques.

Examples:
- **Memetic Algorithms:** combine EA with local search.  
- **Hybrid GA + Gradient Descent:** refine best solutions locally.  
- **Simulated Annealing hybrids:** probabilistic mutation control.

Goal: exploit global search (EA) + local refinement (deterministic).

---

## Example – Memetic Algorithm
for each generation:
evolve population using GA
apply local search to best few individuals
replace population partially or fully

Improves convergence speed and solution quality.

---

## Real-Coded Evolutionary Algorithms
Instead of bitstrings, use vectors of real numbers.

Advantages:
- Natural representation for continuous optimization.  
- Avoids encoding/decoding overhead.  
- Supports arithmetic crossover and Gaussian mutation.

---

## Crossover for Real-Valued Chromosomes
Examples:
- **Arithmetic crossover:**  
  `child = α * parent1 + (1 - α) * parent2`  
- **Blend crossover (BLX-α):**  
  Generates offspring within an interval expanded by α beyond parents.  
- **Simulated Binary Crossover (SBX):**  
  Mimics binary crossover behavior in continuous domains.

---

## Mutation for Real-Valued Chromosomes
Common choices:
- Add Gaussian noise: `x' = x + N(0, σ²)`  
- Scale perturbation: `x' = x * (1 + N(0, σ²))`  

Mutation step size σ often adapts dynamically (self-adaptation).

---

## Evolution Strategies (Recap)
Notation (μ, λ)-ES:  
- μ = parents  
- λ = offspring  
- Next generation = best μ of λ offspring  

Mutation standard deviation σ evolves alongside solution vector x.

**Self-adaptation rule:**
σ' = σ * exp(τ * N(0,1))
x' = x + σ' * N(0, I)


---

## Covariance Matrix Adaptation Evolution Strategy (CMA-ES)
A state-of-the-art ES for continuous optimization.

### Key Concepts:
- Uses full covariance matrix for mutation sampling.  
- Learns correlations between variables.  
- Adapts step size and orientation automatically.

### Algorithm Outline:
1. Sample offspring from multivariate Gaussian.  
2. Evaluate fitness.  
3. Update mean and covariance matrix.  
4. Repeat until convergence.

### Benefits:
- Excellent for non-separable, multimodal problems.  
- Requires little parameter tuning.  
- Scales well to high dimensions.

---

## Visualization of CMA-ES
*(Slides showed contour plots with elliptical sampling clouds adapting to the problem shape over generations.)*  

---

## Evolutionary Programming (EP)
- Similar to ES but focuses purely on mutation (no crossover).  
- Often used in control and prediction problems.  
- Mutation distribution adapts over time.

---

## Genetic Programming (GP)
Evolves **programs or expressions** instead of fixed-length strings.

### Representation
- Trees instead of bitstrings.  
- Nodes = operators/functions; leaves = variables or constants.  

### Operations
- Crossover = subtree exchange.  
- Mutation = random node replacement.  

### Example
f(x) = (x + 3) * sin(x)

Mutated or recombined with other expressions to evolve better-performing formulas.

---

## Applications of GP
- Symbolic regression  
- Controller design  
- Automated code generation  
- Evolving decision trees or neural network topologies

---

## Summary of Evolutionary Algorithm Types

| Type | Representation | Variation | Notes |
|:--|:--|:--|:--|
| Genetic Algorithm (GA) | Binary / discrete | Crossover + Mutation | General-purpose |
| Evolutionary Strategy (ES) | Real-valued | Self-adaptive mutation | Continuous optimization |
| Evolutionary Programming (EP) | Real-valued / structures | Mutation only | Adaptive systems |
| Genetic Programming (GP) | Tree-based | Subtree crossover | Symbolic regression, programs |

---

## Strengths and Limitations

**Strengths**
- Very flexible and parallelizable  
- Suitable for complex, nonlinear, non-differentiable problems  
- Global search capability  

**Limitations**
- Computationally expensive  
- Sensitive to parameter tuning  
- Difficult to analyze theoretically  

---

## Future Directions
- Adaptive parameter control  
- Multi-objective optimization  
- Hybridization with ML and reinforcement learning  
- Neuroevolution (evolving neural networks)  

---

**End of Lecture 8**
