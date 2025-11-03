# 2IRR60 Heuristic Algorithms
### 2025-26 Q1 Lecture 7 – Evolutionary Algorithms

---

## Quick Recap
Population-based metaheuristics combine cooperation and competition to explore and exploit the solution space.  

Previous topics:  
- Swarm intelligence (cooperation)  
- Ant Colony Optimization  
- Particle Swarm Optimization  

Now: **Evolutionary Algorithms (competition + reproduction)**

---

## Metaphor-Based Metaheuristics
Metaheuristic methods are based on metaphors of natural or man-made processes.  

**Criticism:**  
- Many “new” methods are merely rebranded variants without true novelty.  
- Good paradigms should introduce genuinely new mechanisms.  

**Goal:**  
- Introduce new mechanisms for effective search.  
- Reduce parameter count while maintaining solution quality.

---

## Evolution – Biological Inspiration
> “The process by which different kinds of living organisms are believed to have developed from earlier forms during Earth’s history.”

### Three Main Processes
1. **Natural Selection:**  
   Not all individuals reproduce equally.  
   Fitter individuals have a higher chance to pass on their traits.  

2. **Reproduction:**  
   Offspring inherit traits from their parents.  

3. **Mutation:**  
   New random traits occasionally appear.

Together, these processes generate diversity and adaptation in populations.

---

## Exploration vs. Exploitation
A balance is needed between:
- **Exploration:** discovering new traits or adapting to changing conditions.  
- **Exploitation:** reinforcing traits that yield success in current conditions.  

---

## Evolutionary Concepts
**Selection (Survival of the Fittest):**  
Individuals with higher fitness reproduce more often.

**Reproduction:**  
Two parents produce new offspring through:
- **Crossover:** mixing traits of both parents.  
- **Mutation:** introducing random variation.

Note: Asexual reproduction involves mutation but no crossover.

---

## Evolution Acts on Populations
- Takes place *across generations*, not within individuals.  
- Population evolves by replacing old generations with new ones.

---

## Evolutionary Algorithms
Algorithms inspired by biological evolution that optimize a given fitness function.

Variants include:
- **Genetic Algorithms (GA)**
- **Evolutionary Strategies (ES)**
- **Genetic Programming (GP)**

---

## Why Evolutionary Algorithms Work
- Nature’s evolutionary process is effective at optimizing survival.  
- Mechanisms balance exploration and exploitation.  
- Algorithms simulate evolution under controlled conditions for faster optimization.

---

## Historical Success
- Evolutionary algorithms mimic nature’s efficiency.  
- In computational contexts, we can:
  - Evaluate fitness directly.
  - Skip the slow biological growth phase.
  - Handle smaller, well-defined solution spaces.

---

## Genetic Algorithms (GA)
Inspired by genetics and DNA encoding.

**DNA:** blueprint for individuals containing many traits.  
Encoded as a **string of bases** (A, C, G, T).  
Subsections form **genes**.

---

### Example Representation
AACGTAACCGTTACTA
AACG TAAC CGTTAC TA

**Reproduction:**
- Each individual has 2 DNA strings.
- Two parents donate one each to the offspring.
- DNA may break and exchange pieces → **crossover**.
- Random changes in DNA → **mutation**.

---

### Example of Crossover and Mutation
Parent 1: AACGTAACCGTTACTA
Parent 2: GTAGCGATCCATGGAA
Crossover:
AACGTAACCGT | TACTA
GTAGCGATCCA | TGGAA
Mutation:
AACGTA G CCGT TGGAA

Offspring inherit mixed and possibly mutated traits.

---

## Mapping to Optimization Problems
- **Individual/Solution:** element of solution space.  
- **Population P(t):** set of individuals at generation t.  
- **Fitness:** quality measure of the solution.  

---

### General Procedure
1. Initialize population `P(0)`.  
2. Evaluate fitness of all individuals.  
3. Repeat until termination:
   1. Select parents from `P(t)` based on fitness.  
   2. Apply crossover to generate offspring.  
   3. Apply mutation to offspring.  
   4. Form new population `P(t+1)`.

---

### Simple Genetic Algorithm Example

Representation: bit-strings of length *k*.  
Fitness function: number of 1s in the string.  
Goal: maximize f(s).

| Individual | String | Fitness |
|:--|:--|:--|
| 1 | 0110110101 | 6 |
| 2 | 0101010101 | 5 |
| 3 | 1010110110 | 6 |
| 4 | 1110010000 | 5 |

*(Slides showed evolving bitstrings with increasing fitness over generations.)*

---

## Selection Methods
Different ways to choose parents:

- **Roulette Wheel Selection:** probability ∝ fitness.  
- **Tournament Selection:** pick best among random subset.  
- **Rank-Based Selection:** fitness scaled by rank.  
- **Elitism:** best individuals always survive.

---

## Crossover Operators
Combine traits from two parents.

Common types:
- **Single-point crossover:** split at one position.  
- **Two-point crossover:** split at two positions.  
- **Uniform crossover:** randomly choose bits from each parent.

---

## Mutation Operators
Introduce diversity by flipping random bits or perturbing values.

Typical mutation rate: small (e.g., 1% per bit).  

Prevents premature convergence.

---

## Parameter Control
- **Population size:** affects exploration ability.  
- **Mutation rate:** too high = random search; too low = stagnation.  
- **Crossover rate:** controls mixing intensity.  

---

## Convergence
Evolutionary algorithms may converge to a local optimum if diversity is lost.

To counter this:
- Use diversity-preserving strategies (e.g., mutation, crowding).  
- Restart or inject random individuals.

---

## Evolutionary Strategies (ES)
Focus on **real-valued optimization** and **self-adaptation**.

Key difference from GA:
- Mutation rates themselves evolve.
- Selection is often deterministic (best μ individuals survive).

Notation: **(μ, λ)-ES**  
μ = parents, λ = offspring per generation.

---

## Example of (μ, λ)-ES
- Generate λ offspring by mutating μ parents.  
- Evaluate fitness.  
- Select μ best offspring for next generation.  

This process repeats until convergence.

---

## Genetic vs Evolutionary Strategies
| Aspect | Genetic Algorithm | Evolutionary Strategy |
|:--|:--|:--|
| Representation | Binary strings | Real-valued vectors |
| Reproduction | Crossover + mutation | Mutation dominant |
| Selection | Probabilistic | Deterministic |
| Adaptation | Fixed parameters | Self-adaptive mutation rates |

---

## Balance of Exploration and Exploitation
- **Crossover:** promotes exploitation (combine good traits).  
- **Mutation:** promotes exploration (new traits).  
- **Selection pressure:** determines convergence speed.

---

## Strengths and Weaknesses
**Strengths**
- Applicable to many optimization problems.  
- Does not require derivatives or gradient info.  
- Flexible representation.

**Weaknesses**
- Computationally expensive.  
- Sensitive to parameter tuning.  
- May converge prematurely.

---

## Summary
Evolutionary algorithms model the process of natural evolution:  
- Populations evolve over generations.  
- Selection, crossover, and mutation guide adaptation.  
- Balancing exploration and exploitation is key.

Variants such as Genetic Algorithms and Evolutionary Strategies offer different trade-offs between randomness and control.

---

**End of Lecture 7**
