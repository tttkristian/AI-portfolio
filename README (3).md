[← Projects](../../pages/3-technical-projects.md) · [Home](../../README.md)

# Search Under the Microscope: Robot Paths and River Crossings

**ICOM5015 – Artificial Intelligence · Programming Assignment 3 (Chapter 3: Search) · November 2026**
**Course outcome:** CO1, *Describe, analyze and apply different AI techniques* → **ABET SO1** (Engineering Problem Solving)
**Also supports:** CO4 → SO3 (video presentation), optional SO6 (experimentation)

<!-- Lines marked [[ ... ]] are for you to fill in or confirm. Delete this comment before publishing. -->

| | |
|---|---|
| **Activity** | Group programming assignment (Group B, 4 members), AIMA Exercises 3.7 and 3.9 |
| **My role** | I wrote all of the code and ran all of the experiments in the notebook. [[Add what teammates did, if anything, e.g. "Teammates reviewed the write-up and recorded part of the video."]] |
| **Tools** | Python, [aima-python](https://github.com/aimacode/aima-python) `search` module, NumPy, Matplotlib, NetworkX |
| **Evidence** | [Video presentation](https://youtu.be/eSlmu0yrgq4) · [[Notebook link, only if the instructor allows publishing it]] |

---

## 1. The problem

Chapter 3 is about **problem-solving agents** that find a sequence of actions by searching a state space. The assignment asks two questions that, I learned, are really the same question:

1. **Exercise 3.7: shortest path for a robot among convex polygon obstacles.** A robot's position is any point in the plane, so there are infinitely many states. *Can this be turned into a finite graph that still contains the shortest path, and which search algorithm finds it best?*
2. **Exercise 3.9: Missionaries and Cannibals.** *What is the smallest correct formulation, how do we solve it optimally, and is checking for repeated states worth it?*

Before running anything, I wrote down predictions from the lectures so the experiments could confirm or refute them:
- BFS should **not** be optimal in 3.7, because step costs are segment lengths, not equal.
- A\* with straight-line distance should be optimal **and** expand fewer nodes than uniform-cost search.
- In 3.9, every crossing is reversible, so a search without an explored set should loop forever.

## 2. Decisions: formulation first, algorithm second

### Exercise 3.7: from an infinite plane to 35 states

![Figure 3.31 scene](figures/fig31-scene.png)

Gridding the plane doesn't fix the problem. The finer the grid, the more states (70 states at spacing 40, 14,643 at spacing 2.5), and the count never stops growing. Instead I used the **"taut string" argument**: a shortest path is straight wherever it is free, so it can only bend at obstacle corners. That means the only states that matter are **S, G and the polygon vertices**:

| Formulation | States |
|---|---|
| Every point (x, y) in the plane | uncountably infinite |
| Visibility graph (S + G + 33 vertices) | **35 states**, 117 edges, average branching factor 6.69 |

I implemented it as a subclass of `aima.search.Problem`. `ACTIONS(s)` returns every vertex reachable by a straight segment that doesn't cross an obstacle interior. Edges along a polygon are allowed; diagonals through it are not.

![Visibility graph](figures/visibility-graph.png)

### Exercise 3.9: names don't matter, counts do

People of the same type are interchangeable, so a state is just **(M, C, B)**: missionaries and cannibals on the start bank, and which side the boat is on. Of the 32 possible triples, 20 are safe and **16 are reachable**.

![Missionaries and Cannibals state space](figures/mc-state-space.png)

The diagram shows the reachable space is almost a straight line, which gives exactly **4 distinct optimal solutions** of 11 crossings.

For A\*, I derived my own heuristic. Each round trip moves at most one person *net*, so with *n* people left on the start bank, at least 2n − 3 crossings are needed (boat on the start side). The code checks admissibility against the true distance for all 16 states (h(start) = 9 ≤ h\*(start) = 11).

## 3. Results and verification

### Six algorithms on Figure 3.31

![Paths found by six algorithms](figures/six-algorithms-paths.png)

| Algorithm | Path length | × optimal | Nodes expanded |
|---|---|---|---|
| Breadth-first | 624.0 | 1.200 | 19 |
| Depth-first | 689.4 | 1.325 | 20 |
| Iterative deepening | 624.0 | 1.200 | 113 |
| Uniform-cost | 520.1 | **1.000** | 33 |
| Greedy best-first | 593.1 | 1.140 | **5** |
| **A\*** | 520.1 | **1.000** | 17 |

### One scene isn't enough: 60 random scenes

To check that this wasn't a fluke of one picture, I generated 15 random scenes each with 5, 10, 20 and 30 convex obstacles (convex hulls via Andrew's monotone chain).

![Scaling with number of obstacles](figures/random-scenes-scaling.png)

- **Uniform-cost and A\* were optimal in all 60 scenes.** Every other algorithm missed the optimum at least once.
- With 30 obstacles, **A\* expanded about 15× fewer nodes** than uniform-cost (8.9 vs 133.9 on average).
- Greedy best-first was cheapest but found the optimum in only 1 of 30 scenes with 20+ obstacles; DFS paths reached 6.47× the optimal length.

### Missionaries and Cannibals: is the explored set worth it?

| Search | Result | Nodes expanded |
|---|---|---|
| BFS, tree search (no repeated-state check) | 11 crossings | 10,963 |
| BFS, graph search (explored set) | 11 crossings | **13** |
| DFS, tree search | **never terminates** (stopped at 200,000) | 200,000 |
| DFS, graph search | 11 crossings | 11 |

A set lookup per node turns an infinite search tree into a 16-state graph.

### How I verified correctness
- **Automated sanity checks** on `ACTIONS`: polygon edges are always successors, polygon diagonals never are, and the heuristic is **consistent** on every edge.
- **Admissibility check** of the 3.9 heuristic against true goal distances for all reachable states.
- **Cross-check of optimality:** the two algorithms that theory says are optimal (UCS and A\*) agreed on every scene.
- **Fixed random seeds**, so every number above is reproduced by *Restart & Run All*.

## 4. What I learned

- **The formulation matters more than the algorithm.** Both problems became easy once the state space was abstracted correctly (35 and 16 states). This was my biggest takeaway. [[Optional: one sentence on what you believed before, e.g. "I expected the choice of algorithm to be the hard part."]]
- **Cheaper is not better.** BFS returned the path with the *fewest segments* (4) but it was 20% longer than optimal. BFS minimizes the number of actions, not their total cost, which is exactly what the lecture predicted.
- **Heuristics only help when there's something to prune.** In Missionaries and Cannibals, A\* and UCS both expanded 14 nodes. The space is nearly a line, so the heuristic had nothing to cut.
- **Why humans find 3.9 hard:** the solution requires a move that looks like going backwards (bringing two people back at step 6). That is hill-climbing reasoning getting stuck, which connects to the local-search work in Chapter 4.

### Mistakes, limitations and what I'd do differently
- [[Describe one thing that went wrong while you coded it and how you found/fixed it, e.g. a visibility test bug, an inadmissible first heuristic, a DFS run that hung. This is the most valuable sentence on the page.]]
- **Unfair comparison I found:** aima's BFS tests for the goal when a node is *generated*, while UCS and A\* test when it is *expanded*, so BFS's expansion counts look smaller than they really are.
- **Iterative deepening was dropped** from the random-scene experiment because, as a tree search on a dense graph, its cost explodes (113 expansions vs 19 for BFS on one scene).
- **Simplifying assumptions:** the robot is a point, obstacles are static and convex, and the Figure 3.31 coordinates were estimated from the picture.
- **Next time:** grow obstacles by the robot's size before building the graph, split non-convex obstacles into convex pieces, and measure run time fairly, including the cost of *building* the visibility graph versus searching it.

## 5. Outcome connection

**CO1 → SO1 (Engineering Problem Solving).** I *identified* that the given formulation was unusable (infinite states), *formulated* a finite one and justified it with a geometric argument, *solved* it with six algorithms, and *verified* the result with automated checks, an admissibility proof and 60 random test scenes. The evidence is the comparison tables and figures above. Where it stops being valid: everything was tested on small, static, 2-D scenes with a point robot.

**CO4 → SO3 (Communication).** The results were presented in a [video](https://youtu.be/eSlmu0yrgq4) and written up with figures and tables. [[Mention which part of the video you presented.]]

## 6. Gen AI disclosure

I used **Claude (Anthropic, claude.ai)** in November 2026 to [[confirm each item]]:
- plan the notebook's structure against the assignment instructions and rubric;
- review the finished notebook, including re-running the cells to check that every number in the text matched the code output;
- draft the Introduction and References, add in-text citations, and reorganize my comments on 3.7(d) into observations, interpretation and implications;
- [[code and figures: the submitted disclosure says it "was used for the code, and the visuals." State exactly what that meant, e.g. debugging help, plotting code, or explanations, so it is consistent with the submitted notebook.]]

**What I changed or rejected:** [[e.g. a suggestion you didn't use, or text you rewrote.]]
**How I verified it:** every reported number comes from code output in the notebook; heuristic properties are checked by code, not taken on trust; algorithm behavior was checked against Russell & Norvig (2010, Sec. 3.4–3.5).
**My own contribution:** the problem formulations, the implementation of the search problems and heuristic, and all of the experiments.

## References
- aimacode. (n.d.). *aima-python* [Computer software]. GitHub. https://github.com/aimacode/aima-python
- Amarel, S. (1968). On representations of problems of reasoning about actions. In D. Michie (Ed.), *Machine Intelligence 3* (pp. 131–171). Edinburgh University Press.
- Andrew, A. M. (1979). Another efficient algorithm for convex hulls in two dimensions. *Information Processing Letters, 9*(5), 216–219.
- Russell, S., & Norvig, P. (2010). *Artificial Intelligence: A Modern Approach* (3rd ed.). Pearson.
