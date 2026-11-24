[← Projects](../../pages/3-technical-projects.md) · [Home](../../README.md)

# Team Domino AI: Playing Well When You Can't See the Other Hands

**ICOM5015 · Chapter 5 project (Adversarial Search) · [[Date]]**
**Course outcome:** CO2 → **SO2** (Design) · **Also supports:** CO1 → SO1, optional SO5, SO6

| | |
|---|---|
| **Activity** | Group project (Group B): double-six domino, 4 players in 2 teams, 7 tiles each, no boneyard |
| **My role** | [[Exactly what you built: engine, agents, belief sampler, experiments, …]] |
| **Tools** | Python, [OpenSpiel](https://github.com/google-deepmind/open_spiel) (rules reference and referee), NumPy, pandas, Matplotlib |
| **Evidence** | [[Notebook link, if permitted]] · [[demo video]] |

## 1. The problem
Domino is adversarial **and** partially observable: you know your own 7 tiles but not the other 21. Minimax and alpha-beta assume you can see the whole state. [[Design requirements you set: e.g. legal play under the official rules, decision time under X ms, beat a strong heuristic team.]]

## 2. Design decisions
- **Approach: averaging over clairvoyance (Perfect-Information Monte Carlo).** Sample complete deals consistent with what's known, solve each one as a fully observable game, and average the move values. [[Why this over alternatives you considered: e.g. pure rollouts, full information-set search, CFR.]]
- **Belief sampler with pass inference.** When a player passes, they can't hold either open end. Without this inference, about **23%** of sampled worlds contradicted known facts.
- **Own engine, verified against OpenSpiel.** OpenSpiel was too slow inside the search, so we wrote a faster engine: **14.5× faster** per random game.
- **Model selection.** A self-play league plus an external check picked **AB-K32** (32 sampled worlds, alpha-beta to depth 5) as the final agent.

## 3. Results and verification
| Check | Result |
|---|---|
| Engine matches OpenSpiel rules | 3,000 games, 67,198 moves, **0 mismatches** |
| Same outcomes with OpenSpiel as referee | **150 / 150** hands |
| AI team vs. Heuristic team (per hand) | **59.6%** hand win rate |
| Matches to 100 points | about **82%** match win rate |
| Statistical significance | AI team outscored the Heuristic team in 270 of 385 decided deals; sign test p = 1.75 × 10⁻¹⁵ |
| Robustness | Rankings held under Latin-American rules |

[[Add 1–2 figures from the notebook: tournament results, ablation over number of samples K.]]

**Team experiments.** [[One sentence on how much the AI helps a random or heuristic partner.]]

## 4. What I learned
- [[e.g. Why "guess the hands and play as if true" (K = 1) is weak, and how strength grows with K.]]
- **Instructive negative result:** self-play tuning accepted six "improved" heuristics with margins of only 0.1–1.1 points. [[What you concluded.]]
- **Limitations:** [[human evaluation (Section 11) incomplete / compute cost per decision / …]]

## 5. Outcome connection
**CO2 → SO2.** [[Requirements → alternatives → design rationale → evaluation against those requirements. Mention any economic/social considerations honestly, e.g. compute cost per decision, or "not applicable beyond…".]]
**Optional SO5 (Teamwork).** [[How tasks were split and integrated. Keep it factual and professional.]]

## 6. Gen AI disclosure
I used [[tool/model, date]] to [[purpose]] in [[part]]. I revised [[changes]], rejected [[issue]], and checked the result through [[tests/sources/reasoning]]. My own contribution was [[specific work]].

## References
- Russell, S., & Norvig, P. *Artificial Intelligence: A Modern Approach*, Ch. 5.
- Lanctot, M., et al. (2019). OpenSpiel: A framework for reinforcement learning in games. arXiv:1908.09453.
- [[ ]]
