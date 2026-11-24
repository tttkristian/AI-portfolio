[← Projects](../../pages/3-technical-projects.md) · [Home](../../README.md)

# Python vs NumPy: When Is Fast Actually Fast?

**ICOM5015 · Programming Assignment 1 · [[Date]]**
**Course outcome:** optional **SO6** (Experimentation & engineering judgment)

| | |
|---|---|
| **Activity** | Group assignment (Group B) |
| **My role** | [[ ]] |
| **Tools** | Python, NumPy, `timeit`, Matplotlib |
| **Evidence** | [[Notebook link, if permitted]] |

## 1. The problem
At what problem size does NumPy's advantage over pure Python become measurable, substantial (≥10×), and very large (≥100×)? Is NumPy ever slower?
**Hypothesis:** for tiny inputs, NumPy's fixed per-call overhead dominates.

## 2. Method
- Element-wise vector product and matrix product, pure Python loops vs NumPy (`np.multiply`, `A @ B`).
- One untimed warm-up call, `timeit.autorange()` so each sample lasts over 0.2 s, and a correctness check on every result.

## 3. Results
- **Hypothesis confirmed:** for very small inputs NumPy is *slower* (0.3–0.6× at n = 1–3).
- Matrix speedups reach about **2,270×**, roughly 15 times the vector peak, because the Python version grows as n³.
- **Two methodology mistakes, reproduced on purpose:**

| Mistake | Correct speedup | Flawed speedup |
|---|---|---|
| No warm-up (matrix, n = 100) | 1,265× | 22.9× |
| List-to-array conversion inside the timer (vector, n = 100,000) | 91.6× | **0.8×** (NumPy looks slower!) |

[[Add the speedup plot.]]

## 4. What I learned
Python's arithmetic isn't slow; its per-element overhead is. More importantly, **the measurement setup can flip the conclusion**. [[Your reflection.]]

## 5. Outcome connection
**SO6.** [[Hypothesis → controlled experiment → analysis → conclusion supported by evidence, plus deliberately testing the methodology itself.]]

## 6. Gen AI disclosure
I used [[tool/model, date]] to [[purpose]] in [[part]]. I revised [[changes]], rejected [[issue]], and checked the result through [[tests/sources/reasoning]]. My own contribution was [[specific work]].
