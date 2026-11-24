[← 3. Technical Projects](3-technical-projects.md) · **4. Critical Thinking & Communication** · [5. Learning with Gen AI →](5-learning-with-genai.md)

# 4. Critical Thinking & Communication

Evidence for **CO3 → SO7** (acquiring new knowledge) and **CO4 → SO3** (communication).

## 4.1 Literature review (CO3 → SO7)
**Artifact:** [Is Artificial Intelligence Real Intelligence? A Debate and Literature Review](../projects/intelligence-essay/README.md) · November 13, 2026 · group essay and recorded debate

- **What I read and why:** six sources from philosophy, cognitive science and ML research (Searle, Puccetti, Harnad, Legg & Hutter, Bender & Koller, Li et al.) used to argue whether built systems can be genuinely intelligent. I argued Position A (intelligence is defined by function).
- **How I evaluated the claims:** sorted each source by kind of evidence: empirical, theoretical or philosophical. Only Li et al. (2023) is an experiment. Its *intervention* (editing the model's internal board and watching its moves change) is what separates a causal representation from a correlation a probe happens to find.
- **Source check:** re-reading for this portfolio, I found that the submitted essay's in-text citation numbers don't match its reference list, and that Turing and Chollet are cited but not listed. [Details](../projects/intelligence-essay/README.md#3-source-check-errors-i-found-when-re-reading).
- **What was new to me and how it connects to the course:** a learned model can *build* its own state representation. In PA3 and Domino, my team and I designed those representations by hand.
- **What I applied:** the debate's "check the process, not just the output" matches the verification in my projects (UCS/A\* agreement in PA3, the move-by-move engine check against OpenSpiel in Domino).
- **What I still want to learn:** [[ ]]

## 4.2 Technical paper demonstration (CO4 → SO3)
**Artifact:** Li et al. (2023), *Emergent world representations: Exploring a sequence model trained on a synthetic task* (ICLR), presented in Round 5 of the [intelligence debate](https://www.youtube.com/watch?v=sORd6XOfe7U) · November 2026 · [essay page](../projects/intelligence-essay/README.md)

- **What I presented:** a GPT-style model trained only to predict the next legal Othello move, never shown a board or the rules. Probes recovered the board state from its activations. When the researchers *edited* that internal board, the model switched to moves that are legal on the edited board. That shows the representation is part of how it decides, not just a correlation.
- **Audience and how I adapted:** the debate was for the team and the professor, so I presented the experiment verbally, without slides or figures. [[Optional: how you made probing clear without a picture.]]
- **Figures I used:** none. It was a spoken debate.
- **Questions I was asked and how I answered:** Position B accepted the result but argued that a game representation isn't understanding. I answered that in Round 2 they had asked us to look at the internal process instead of only the output, and this experiment does exactly that.
- **Feedback received → what I changed:** [[ ]]

## 4.3 Other communication evidence
| Artifact | Type | What it shows |
|---|---|---|
| [PA3 video](https://youtu.be/eSlmu0yrgq4) | Recorded presentation | Explaining search results to an audience. [[Which part you presented]] |
| [Intelligence debate](https://www.youtube.com/watch?v=sORd6XOfe7U) | Recorded six-round debate | Arguing Position A live, presenting the Othello paper (Round 5, see 4.2) and answering rebuttals |
| [[Forum post]] | Discussion | [[A claim you questioned or a classmate you helped]] |
| [[ ]] | [[ ]] | [[ ]] |

---
[← 3. Technical Projects](3-technical-projects.md) · [5. Learning with Gen AI →](5-learning-with-genai.md)
