# 2IRR60 Heuristic Algorithms
### 2025-26 Q1 Lecture 6 – Swarm Optimization

---

## Quick Recap
Population-based metaheuristics involve multiple candidate solutions cooperating or competing.

---

## Swarm Intelligence
**Why ant colonies?**  
An individual ant is not very intelligent (tiny brain),  
but collectively they can solve complex problems — an example of **emergent behavior**.  

Swarm intelligence uses such principles for optimization.

---

## Exploration vs. Exploitation
**Exploration:** searching new regions of the solution space.  
**Exploitation:** refining known good regions.  
Swarm-based methods balance both through shared information among agents.

---

## Ant Colony Optimization
Review of ACO: cooperative search using pheromone communication to discover optimal paths.

---

## Swarm Optimization
Swarm optimization is inspired by the behavior of flocks, herds, and colonies.  
The idea is to solve optimization problems by emulating these collective behaviors.

---

## Swarm Intelligence – Definition
The collective behavior of decentralized, self-organized systems.  

### Properties
- Population of agents.  
- Agents follow simple rules.  
- Interaction is local (no central control).  
- Emergence of global intelligent behavior.

---

## Applications of Swarm Intelligence
- **Swarm robotics:** coordination of robots, self-assembly.  
- **Data science:** clustering and pattern detection.  
- **Optimization:** finding near-optimal solutions to hard problems.

---

## Examples of Swarm Behavior
- Ants building trails.  
- Bee colonies allocating resources.  
- Bird flocks aligning flight patterns.  
- Fish schools synchronizing movement.  
- Bacteria or slime molds adapting to environments.

---

## Emergence
Complex, adaptive, and coordinated behavior arises from simple local interactions.  

*(Slide image: birds flocking, fish schooling, ants forming trails.)*

---

## Swarm Optimization – Concept
Emulate swarm behavior to move through the solution space.

### Global Idea
The swarm is guided by one or more individuals with the best-known solution.  

Each agent (particle) moves in the solution space and updates its position based on:
- Its own experience.
- Information from neighbors or the global best.

---

## Particle Swarm Optimization (PSO)
Particles move around a continuous solution space.  
They are accelerated toward good solutions based on velocity and position updates.

### Characteristics
- Works in continuous spaces.  
- Balances exploration and exploitation.  
- Can converge quickly for smooth functions.

---

## Very Basic Swarm Example
Particles initialized at random positions explore the landscape.  
Each is influenced by its own best position and the best position found by the swarm.

*(Slides illustrated particles moving toward an optimum.)*

---

## Particle Swarm Dynamics
Each particle has:
- A **position** vector (current solution).  
- A **velocity** vector (direction of change).

Velocity update combines:
1. Inertia (previous movement).  
2. Cognitive component (pull toward own best).  
3. Social component (pull toward swarm best).

---

## Generic Velocity Update Formula
`v[i] = w * v[i] + c1 * r1 * (p_best[i] - x[i]) + c2 * r2 * (g_best - x[i])`  
`x[i] = x[i] + v[i]`

where:  
- `w`: inertia weight  
- `c1`, `c2`: learning factors  
- `r1`, `r2`: random factors  
- `p_best[i]`: best position found by particle i  
- `g_best`: best position found by the swarm  

---

## Example Visualization
Slides showed particles moving through a landscape, with arrows indicating:
- Direction toward own best (local).  
- Direction toward global best.  

---

## Different Samples per Particle and Component
Each particle samples new positions and velocities independently, increasing diversity.

---

## Although the Solution Space Is Continuous…
The simulation itself is **discrete**: each iteration updates all positions and velocities.

*(Slide animation showed convergence of particles over time.)*

---

## Convergence
Particles gradually gather near an optimal region.  
Convergence speed depends on inertia, learning factors, and randomization.  

---

## Extensions of PSO

### Adaptive Particle Swarm Optimization
Parameters (inertia, learning rates) are adjusted dynamically during execution.

### Bare Bones Particle Swarm Optimization
Eliminates explicit velocities; new positions are drawn from Gaussian distributions around p_best and g_best.

### Hybrid Variants
Combine PSO with other techniques such as **gradient descent** for faster convergence.

---

## Algorithm & Implementation
1. Initialize population (positions and velocities).  
2. Evaluate fitness of all particles.  
3. Update personal and global bests.  
4. Update velocities and positions.  
5. Repeat until convergence or iteration limit.

Can easily be executed **in parallel** for each particle.

---

## Termination Conditions
- Fixed number of iterations.  
- Convergence criterion (positions change little).  

---

## When to Use Particle Swarm Optimization
**Advantages**
- Simple to implement.  
- Few parameters.  
- Works well on continuous and multimodal problems.  
- Can exploit parallel computing.

**Disadvantages**
- May converge prematurely (to local optimum).  
- Sensitive to parameter settings.  
- Not ideal for discrete or combinatorial problems.

---

## Random Walks
A **random walk** is a stochastic process consisting of successive random steps.

### Example
1D grid with steps ±1 from the origin.  
Used to model exploration behavior of individual agents.

---

## 2D and 3D Random Walks
Particles move in multidimensional spaces.  
Can simulate exploration of the solution space.

---

## Relevance for Swarm Optimization
- Random walks explore local neighborhoods.  
- Help avoid premature convergence.  
- Provide controlled randomness for movement.

---

## What Is a Good Random Walk?
- Choose a neighbor randomly from local neighborhood.  
- Neighborhood size affects exploration vs exploitation.

---

## Lévy Walk
A variation of random walk with occasional long jumps (heavy-tailed distribution).  
Encourages wide exploration while maintaining local search ability.

---

## Comparison
| Type | Behavior | Exploration | Convergence |
|:--|:--|:--|:--|
| Simple Random Walk | Small random steps | Moderate | Slow |
| Lévy Walk | Occasional long steps | High | Faster |

---

## Generic Swarm Optimization – Template

**Algorithm outline:**
1. Initialize a swarm of agents with random positions.  
2. Each agent performs a random step according to a walk model (simple or Lévy).  
3. Evaluate all agents.  
4. Share information (global best).  
5. Adjust movement parameters to balance exploration/exploitation.  
6. Repeat until termination.

---

## Parameters
Constants or adaptive parameters determine balance:
- Step size  
- Probability of long jumps  
- Neighborhood size  

---

## Optimization Direction
Use the algorithm to **minimize** or **maximize** objective functions as needed.

---

## Metaphor-Based Metaheuristics
Many metaheuristics are inspired by natural or physical processes.

Examples:
- Simulated Annealing  
- Ant Colony Optimization  
- Particle Swarm Optimization  
- Harmony Search  
- Artificial Bee Colony Algorithm  
- Glowworm Swarm Optimization  
- Shuffled Frog Leaping Algorithm  
- Cat Swarm Optimization  
- Gravitational Search Algorithm  
- Cuckoo Search  
- Bat Algorithm  
- Spiral Optimization Algorithm  
- Flower Pollination Algorithm  
- River Formation Dynamics  
- Intelligent Water Drops  
- Artificial Ecosystem Algorithm  
- Cooperative Group Optimization  

*(Slides listed over a dozen metaphor-based algorithms.)*

---

## Summary
Swarm Optimization leverages collective behavior of agents to explore solution spaces.  
It’s robust, parallelizable, and adaptable, making it a core component of modern metaheuristics.

---

**End of Lecture 6**
