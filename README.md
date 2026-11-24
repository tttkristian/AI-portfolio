[← Projects](../../pages/3-technical-projects.md) · [Home](../../README.md)

# Local Search on the 8-Puzzle and 8-Queens

**ICOM5015 · AIMA Exercise 4.4 · [[Date]]**
**Course outcome:** CO1 → **SO1** · **Also supports:** optional SO6 (Experimentation)

| | |
|---|---|
| **Activity** | Group assignment (Group B), Chapter 4 |
| **My role** | [[ ]] |
| **Tools** | Python, aima-python (`hill_climbing`, `simulated_annealing`, …), NumPy, pandas, Matplotlib |
| **Evidence** | [[Notebook link, if permitted]] |

## 1. The problem
Compare four local-search algorithms on two problems: steepest-ascent hill climbing (HC), first-choice (FC), random-restart (RR) and simulated annealing (SA).

## 2. Decisions
- **Objective functions:** 8-puzzle maximizes −(Manhattan distance); 8-queens uses a complete-state formulation, since AIMA's version is incremental.
- **Ground truth:** BFS backwards from the goal gave the exact optimal cost for all **181,440** reachable 8-puzzle states. Checked against A\* and the solvability test.
- **Fair test set:** 8-puzzle instances stratified by optimal cost (1–31), then re-weighted to the true population. 1,000 random 8-queens boards.
- **SA schedule** tuned on separate tuning instances only.
- **Reproducibility:** each run gets its own seed derived from a CRC-32 hash, so results don't depend on run order.

## 3. Results and verification
7,208 runs in the main experiment.

| Success rate | HC | FC | RR | SA |
|---|---|---|---|---|
| 8-queens | 12.9% | 11.3% | **100%** | 97.9% |
| 8-puzzle (population-weighted) | 0.2% | 0.3% | **94.9%** | 75.0% |

**Validation against the textbook:** AIMA reports HC solves about 14% of 8-queens boards in about 4 steps. This experiment got **12.9%** and **4.19 steps**, which confirms the setup is correct.

**Something I didn't expect:** AIMA's `simulated_annealing` has no goal test. On the 8-puzzle it *visited* a goal in 98.5% of runs but *ended* at one in only 72.2%. It wandered away while the temperature was still high.

[[Add the success-rate figure from the notebook.]]

## 4. What I learned
[[e.g. Why plain hill climbing fails (local maxima, plateaus); why restarts fix it; why reproducing a known number first matters.]]

## 5. Outcome connection
**CO1 → SO1 / SO6.** [[Explain how the formulation, experiment design and validation show problem solving and experimentation.]]

## 6. Gen AI disclosure
I used [[tool/model, date]] to [[purpose]] in [[part]]. I revised [[changes]], rejected [[issue]], and checked the result through [[tests/sources/reasoning]]. My own contribution was [[specific work]].
