[← 5. Learning with Gen AI](5-learning-with-genai.md) · **6. Lessons Learned** · [7. Professional Outlook →](7-professional-outlook.md)

# 6. Lessons Learned

## 6.1 A failed approach
**Self-play tuning that didn't pay off ([Domino AI](../projects/domino-ai/README.md), Section 10).**
Six versions of the heuristic were each accepted because they beat the previous one in self-play, but by margins of only 0.1–1.1 points. [[Describe what the final comparison showed and what you concluded, e.g. that small self-play wins aren't evidence of real improvement without a significance test against a fixed opponent.]]

## 6.2 A correction
**Measuring the wrong thing ([Python Performance](../projects/python-performance/README.md)).**
- Without a warm-up call, NumPy's matrix speedup looked like **22.9×** instead of **1,265×**.
- Timing the list-to-array conversion made NumPy look **slower** (0.8×) instead of **91.6×** faster.

**Lesson:** the timed region must contain only the operation under study. I now check the measurement setup before trusting any number. [[Did you make one of these mistakes first, or design the test on purpose? Say which.]]

## 6.3 Another correction
**Repeated states ([PA3](../projects/pa3-search/README.md)).** Depth-first tree search on Missionaries and Cannibals never terminates; adding an explored set solved it in 11 expansions. [[Your own bug or wrong assumption while coding PA3.]]

## 6.4 Remaining limitations
- PA3 treats the robot as a point among static convex obstacles.
- Domino AI hasn't been fully evaluated against human players yet. [[update if finished]]
- [[ ]]

## 6.5 What I'd do differently
[[2–3 bullets, e.g. "Write the evaluation plan before writing the agent", "Run significance tests before accepting an improvement", "Commit code to Git from day one."]]

---
[← 5. Learning with Gen AI](5-learning-with-genai.md) · [7. Professional Outlook →](7-professional-outlook.md)
