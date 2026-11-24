[← Critical Thinking](../../pages/4-critical-thinking.md) · [Home](../../README.md)

# Is Artificial Intelligence Real Intelligence? A Debate and Literature Review

**ICOM5015 · Debate essay · November 13, 2026**
**Course outcome:** CO3 → **SO7** (Acquiring and applying new knowledge) · **Also supports:** CO4 → SO3 (recorded debate), optional SO5 (Teamwork)

<!-- Lines marked [[ ... ]] are for you to fill in or confirm. Delete this comment before publishing. -->

| | |
|---|---|
| **Activity** | Group debate and written essay (Group B, 4 members split into two opposing subgroups of 2). Position A: Ricardo and me. Position B: Jose and Leonardo. |
| **My role** | Argued **Position A** (intelligence is defined by function, not biological material) in the rounds defending that AI can have actual intelligence, and **presented the Othello paper (Li et al., 2023) in Round 5**, the debate's main empirical evidence. In the essay, I wrote the descriptions of the debate and the Conclusion. |
| **Sources** | 6 peer-reviewed works, 1980–2023 (see [References](#references)) |
| **Evidence** | [Recorded debate](https://www.youtube.com/watch?v=sORd6XOfe7U) · [[Essay PDF, only if the instructor and teammates allow publishing it]] |

---

## 1. The question

*Can intelligence be genuine when humans build it instead of evolution?* The hard part is that intelligence has no agreed definition, and the definition you pick mostly decides the answer. The essay compares three:

| Definition | Source | Asks |
|---|---|---|
| Capability | Turing; Legg & Hutter [1] | Does the system achieve goals across many environments? |
| Understanding | Searle [3]; Harnad [5] | Do its internal states mean something *to the system*? |
| Skill-acquisition efficiency | Chollet | How quickly does it learn tasks it hasn't seen? |

Our working definition: intelligence is the capacity to achieve goals and adapt across varied, partly new environments. It is *genuine* when that capacity depends on internal states that are about the world for the system itself. The definition deliberately doesn't say what the system has to be made of.

## 2. What I read and how I evaluated it

We sorted every source by the **kind of evidence** it gives, because a thought experiment and an experiment can't support a claim in the same way.

| Source | Type | Claim | Where it stops being valid |
|---|---|---|---|
| Legg & Hutter (2007) [1] | Theoretical | Intelligence = goal achievement across environments; nothing about neurons | Measures performance, says nothing about understanding |
| Searle (1980), Chinese Room [3] | Philosophical | Running a program isn't enough to understand | A thought experiment, not proof that machines *can't* understand |
| Puccetti (1980) [4] | Philosophical | Superhuman chess doesn't show understanding | Based on 1980 chess programs |
| Harnad (1990) [5] | Theoretical | Symbols defined only by other symbols never reach meaning | Doesn't show that grounding has to be biological |
| Bender & Koller (2020) [6] | Theoretical | A model trained only on the *form* of language can't learn its *meaning* | Argued from a thought experiment (the octopus) |
| **Li et al. (2023) [2]** | **Empirical** | A GPT-style model trained only on Othello move lists builds an internal board state, and editing that state changes its moves | One closed, synthetic domain |

**The deciding evidence was Li et al.** It was the only experiment in the debate, and the intervention is what makes it convincing. A probe that *reads* a board state out of the activations could just be finding a correlation. *Changing* that state and watching the model switch to moves that are legal on the edited board shows the representation is part of how the model decides. Both sides accepted the result. What they disagreed on was what it shows: a world representation, or understanding.

**Main conclusion:** the two positions were less opposed than they looked. Both accepted that artificial systems could in principle be intelligent. The real disagreement was about **what evidence would be enough** to show genuine understanding, and nobody has an accepted test for that yet.

## 3. Source check: errors I found when re-reading

Re-checking the essay's citations for this portfolio, I found problems in the submitted version:

- **Section 1's citation numbers don't match the reference list.** Turing is cited as [1] and Legg & Hutter as [2], but in the list [1] *is* Legg & Hutter and [2] is Li et al. Chollet is cited as [4], but [4] is Puccetti.
- **Turing (1950) and Chollet (2019) are cited but missing from the references.**
- **The first paragraph of Section 2 attributes Position B's claim to Position A** ("producing intelligent behavior is not, by itself, sufficient evidence…"). It looks like a sentence was lost when the drafts were merged.

[[How this happened (e.g. sections drafted separately or by Gen AI and not cross-checked) and what you'd do differently, e.g. "check every in-text number against the reference list as a last step".]]

## 4. What was new to me and how it connects to the course

- **Representation is the core issue, in the debate and in my code.** In [PA3](../pa3-search/README.md), the problem became solvable once I chose the right state representation (an infinite plane became 35 states). Li et al. ask the same question about a neural network: did it *build* a state representation by itself? Before this, I had only thought of representations as something the programmer designs.
- **Checking the process, not only the output.** Position B's demand to "look at how the answer was produced" is the same idea as the verification I did in my projects. In PA3, UCS and A\* had to agree on every scene. In [Domino AI](../domino-ai/README.md), our engine had to match OpenSpiel move by move.
- **Hidden state.** In the Domino agent, the program keeps beliefs about hands it can't see. That is a hand-built version of what the Othello model learned on its own.
- **My view didn't change.** I still hold Position A: being made of neurons isn't what makes something intelligent. [[Optional: one thing Position B made you more careful about, e.g. not treating performance alone as proof of understanding.]]

## 5. What I still want to learn
[[e.g. "Read the follow-up showing the Othello board representation is linear when encoded as mine/theirs (Nanda et al., 2023)", "Try a probe on a small model myself", "Look at Chollet's ARC benchmark as a way to test generalization."]]

## 6. Outcome connection

**CO3 → SO7 (Acquiring and applying new knowledge).** I read sources from philosophy, cognitive science and machine-learning research, classified each by the kind of evidence it provides, and identified where each claim stops being valid. I connected the one empirical result (Li et al.) to representation and verification work in my own projects. Re-checking the citations for this portfolio also found errors in the submitted version. **Limits:** most sources are from 1980–1990, the reading list was shared by the team, and only one source is empirical.

**CO4 → SO3 (Communication).** The arguments were presented live in a six-round [recorded debate](https://www.youtube.com/watch?v=sORd6XOfe7U) with rebuttals, then written up as an essay. I presented the Othello paper in Round 5. Position B answered that a game representation isn't understanding. We replied that in Round 2 they had asked us to examine the model's internal process, and this experiment does exactly that.

**Optional SO5 (Teamwork).** The team split into two subgroups that argued opposite positions: Ricardo and I for Position A, Jose and Leonardo for Position B. Afterward we wrote a joint synthesis. I wrote the descriptions of the debate and the Conclusion. Sections 2–4 were drafted with Gen AI from our transcript (see below).

## 7. Gen AI disclosure

The submitted essay states that the team used Claude (Anthropic) and ChatGPT (OpenAI) on November 12, 2026. We gave the tools our debate transcript (steelman rounds, six debate rounds, final syntheses) and our own draft of Section 1. The tools drafted Sections 2–4 and matched the document formatting. [[Confirm which tool did what; the submitted wording "Claude sonnet 5.5, OpenAI ChatGPT" mixes the two.]]

**What we changed or rejected:** [[edits you made to the drafted sections]]
**How it was checked:** [[e.g. compared the drafted summaries with the debate transcript]]. The citation errors in Section 3 above were **not** caught before submission. I found them while re-checking sources for this portfolio.
**My own contribution:** my Position A arguments and rebuttals in the debate, the Round 5 presentation of the Othello paper, the essay's descriptions of the debate and its Conclusion, and the source check on this page. **This page:** drafted with Claude (Anthropic) in November 2026 from the submitted essay and my answers about my role. I checked the citation errors against the essay's reference list myself. [[What you rewrote in your own words.]]

## References
1. S. Legg and M. Hutter, "Universal intelligence: A definition of machine intelligence," *Minds and Machines*, vol. 17, no. 4, pp. 391–444, 2007.
2. K. Li, A. K. Hopkins, D. Bau, F. Viégas, H. Pfister, and M. Wattenberg, "Emergent world representations: Exploring a sequence model trained on a synthetic task," in *Proc. ICLR*, 2023.
3. J. R. Searle, "Minds, brains, and programs," *Behavioral and Brain Sciences*, vol. 3, no. 3, pp. 417–424, 1980.
4. R. Puccetti, "The chess room: Further demythologizing of strong AI," *Behavioral and Brain Sciences*, vol. 3, no. 3, pp. 441–442, 1980.
5. S. Harnad, "The symbol grounding problem," *Physica D*, vol. 42, no. 1–3, pp. 335–346, 1990.
6. E. M. Bender and A. Koller, "Climbing towards NLU: On meaning, form, and understanding in the age of data," in *Proc. 58th Annual Meeting of the ACL*, 2020, pp. 5185–5198.
7. A. M. Turing, "Computing machinery and intelligence," *Mind*, vol. 59, no. 236, pp. 433–460, 1950. *(cited in the essay but missing from its reference list)*
8. F. Chollet, "On the measure of intelligence," arXiv:1911.01547, 2019. *(cited in the essay but missing from its reference list)*
