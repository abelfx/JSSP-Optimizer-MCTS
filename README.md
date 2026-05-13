# MCTS-Based Job Shop Scheduling Optimizer

An implementation of Monte Carlo Tree Search (MCTS) to solve complex Job Shop Scheduling Problems (JSSP) using heuristic-guided simulations.

## Overview

The Job Shop Scheduling Problem requires assigning multiple multi-step jobs to a set of specialized machines in a strict order. The goal is to minimize the **Makespan**—the total time it takes to finish every job. Because of the combinatorial explosion of possible schedules, traditional greedy algorithms often fail, creating massive bottlenecks on the factory floor.

This project treats schedule generation as a sequential game. It uses **Monte Carlo Tree Search (MCTS)** to navigate the massive search space. By simulating thousands of possible factory futures (rollouts) using an $\epsilon$-greedy policy ("Most Work Remaining"), the AI agent naturally discovers parallel machine utilization and optimal routing without needing a hardcoded, static heuristic.

## Performance & Results

The MCTS optimizer was benchmarked on a highly constrained **5-Job, 5-Machine** environment. The theoretical physical limit for this specific factory configuration is 20 time units.

* **Random Baseline Makespan:** 47 time units
* **MCTS Optimized Makespan:** 25 time units

**Conclusion:** The MCTS agent reduced the total factory processing time by **~46.8%** compared to the baseline. It successfully untangled the web of job constraints, identifying critical paths to run machines in parallel and significantly reduce idle time.

## Getting Started

To run this project locally or evaluate the MCTS agent:

1. **Clone the repository:**
   ```bash
   git clone https://github.com/abelfx/JSSP-Optimizer-MCTS.git
   cd JSSP-Optimizer-MCTS
   ```

2. Install Dependencies
   ```
   pip install -r requirements.txt
   ```
3. Lunch the Jupyter Notebook:
   
   ```
   jupyter notebook MCTS_Job_Shop_Optimizer.ipynb
   ```
**You can check out the result of the optimization in the assets folder**
