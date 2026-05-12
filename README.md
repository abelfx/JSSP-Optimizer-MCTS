# MCTS-Based Job Shop Scheduling Optimizer

An implementation of Monte Carlo Tree Search (MCTS) to solve the Job Shop Scheduling Problem (JSSP), demonstrating the transition from vanilla random rollouts to heuristic-guided simulations.

## Problem Statement (The One-Pager)

**Domain:** Operations Research & Combinatorial Optimization
**Problem:** The Job Shop Scheduling Problem (JSSP)

In a Job Shop environment, multiple jobs must be processed on specific machines in a strict, sequential order. The primary objective is to minimize the **Makespan** ($C_{max}$)—the total time elapsed from the start of the first operation to the completion of the last. 

**The Challenge:**
JSSP is notoriously NP-hard due to the **combinatorial explosion** of possible operation sequences. For even a small number of jobs and machines, the state space becomes astronomical. Traditional greedy algorithms (like "Shortest Processing Time First") often fall into local optima, creating bottlenecks where several machines sit idle while waiting for a single job to finish an earlier stage. Because designing an accurate, static evaluation function for a partially completed schedule is nearly impossible, traditional heuristic searches struggle to find optimal sequences.

**The Solution:**
This project treats schedule generation as a sequential decision process. By deploying **Monte Carlo Tree Search (MCTS)**, the agent explores the massive scheduling tree without needing a perfect human-written heuristic for partial states. Instead, it approximates the value of scheduling decisions through rapid, simulated rollouts to the end of the factory day, organically discovering the critical paths that minimize machine idle time.

---

## How MCTS Solves This (The 4 Processes)

The algorithm builds an asymmetrical search tree where each Node is a partial schedule, and each Edge is a valid operation assignment. The agent iterates through four distinct phases:

### 1. Selection (Strategic Navigation)
The algorithm navigates the partial schedule tree using the **Upper Confidence Bound applied to Trees (UCT)** formula. It prioritizes sequences that previously resulted in high factory efficiency (Exploitation) while occasionally branching out to unvisited job sequences to avoid local optima (Exploration). 

### 2. Expansion (Constraint-Aware Growth)
When the search reaches an unexpanded node, it identifies all "Ready" operations—those whose precedence constraints are met and whose required machines are available. It adds these as new child nodes, ensuring the search tree only grows within the physical constraints of the Job Shop.

### 3. Simulation (Heuristic-Guided Rollout)
From a newly expanded node, the agent simulates the remainder of the schedule until all jobs are completed. To maximize the algorithm's potential, this implementation uses an **$\epsilon$-greedy policy**. 80% of the time, it selects the job with the "Most Work Remaining," and 20% of the time, it selects randomly. This reduces the variance of the Monte Carlo estimates, providing a high-fidelity forecast of the node's true potential.

### 4. Backpropagation (Value Informing Action)
Once the simulation concludes, the final Makespan is converted into a continuous reward signal (`Reward = 1000 / Makespan`). This value is passed back up the tree, updating the average efficiency score of every decision made along that path. Over thousands of iterations, the optimal starting sequence naturally emerges with the highest visit count.

---

## 📊 Empirical Validation & Results

The MCTS optimizer was benchmarked against a baseline random scheduler on a 3-Job, 3-Machine bottleneck environment. 

*   **Theoretical Lower Bound:** 10 time units (dictated by the maximum workload on Machine 1).
*   **Random Baseline Makespan:** 14 time units.
*   **MCTS Optimized Makespan:** 11 time units.

**Conclusion:** 
The MCTS agent successfully reduced the baseline makespan by ~21.4%. By achieving a makespan of 11, the algorithm operated at **90.9% efficiency** relative to the absolute mathematical limit of the factory configuration. It successfully identified the bottleneck and routed jobs to minimize idle time.

### Optimized Schedule Visualization
*(Ensure you save your matplotlib chart to the assets folder and it will render here)*

![Gantt Chart](assets/optimal_gantt_chart.png)

---

## 🚀 Getting Started

To run this project locally or evaluate the MCTS agent:

1. **Clone the repository:**
   ```bash
   git clone https://github.com/abelfx/JSSP-Optimizer-MCTS.git
   cd JSSP-Optimizer-MCTS

2. Install Dependencies

- You can check out the result of the optimization in the assets folder
```
```
   ip install -r requirements.txt
```

3.```
3. Lunch the Jupyter Notebook:
```
```
jupyter notebook MCTS_Job_Shop_Optimizer.ipynb
```
```

- You can check out the result of the optimization in the assets folder
