# History Decision Simulator

> A structured AI skill for reasoning about life decisions through historically analogous cases from **《史记》 (Shiji)** and **《资治通鉴》 (Zizhi Tongjian)**.

**历史不是答案库，而是复杂决策的案例库。**

`history-decision-simulator` 用于把现实人生抉择映射到结构相似的历史决策场景。它不做“古人名言式建议”，而是先抽取决策结构，再检索原始史料，还原当事人在当时信息条件下的选项、判断、结果，以及显性与隐性代价。

## What it does

Given a decision such as:

- Should I accept an opportunity that requires me to publicly choose sides?
- Should I stay in a powerful organization or leave while I still have an exit?
- Should I trust a partner whose incentives are only partially aligned with mine?
- Should I trade short-term resources for long-term independence?

The skill will:

1. Extract the **decision-structure kernel**: goals, power, incentives, information asymmetry, exit cost, time pressure, reversibility, reputation, alliances, and tail risk.
2. Retrieve **2–4 structurally similar historical cases** from designated primary-text libraries.
3. Reconstruct each case from the information available **at the time of the decision**, not from hindsight.
4. Separate actual options from inferred counterfactual options.
5. Analyze short-term and long-term outcomes, plus explicit and hidden costs.
6. Quote the original text and cite the exact chapter / volume.
7. State both the **similarity** and the **mismatch** between the historical case and the modern situation.
8. Extract only mechanisms that recur across cases, with explicit warnings against overgeneralization.

## Core principle

> **类比决策结构，不类比人物表面；复原当时信息，不用结局作弊；历史给机制和警报，不替现代人做决定。**
>
> Compare decision structures, not superficial personalities. Reconstruct information available at the time, do not cheat with hindsight. History provides mechanisms and warnings, not decisions for modern people.

## Why this is different from “historical wisdom”

The skill explicitly guards against:

- **Outcome bias**: later success does not prove a decision was optimal ex ante.
- **Survivorship bias**: historical records disproportionately preserve rulers, elites, major winners, and spectacular failures.
- **Narrative bias**: historians select and organize facts; a chronicle is not a camera recording.
- **Institutional mismatch**: ancient political, legal, military, and kinship systems do not map directly onto modern life.
- **Personality simplification**: outcomes should not be reduced to labels such as “Liu Bang was better with people.”
- **Single-case mythmaking**: one famous story is not a general law.

## Primary text sources

Default source policy in `SKILL.md`:

- **《史记》**: Chinese Text Project primary text, cross-checked with Chinese Wikisource.
- **《资治通鉴》**: Chinese Wikisource primary readable text, cross-checked with Chinese Text Project.
- OCR-derived text must be cross-checked when a quotation, name, date, or wording looks suspicious.
- Authorial commentary such as **“太史公曰”** and **“臣光曰”**, and later annotations such as **胡三省注 / 三家注**, must be separated from the event narrative.

Secondary sources may help locate a passage, but they are not accepted as the final source for a primary-text quotation.

## Similarity scoring

Candidate cases are scored on six dimensions, each from 0–2:

| Dimension | Question |
| --- | --- |
| Decision structure | Is the core choice actually similar? |
| Power & incentives | Are the parties' leverage and interests structurally similar? |
| Information uncertainty | Are the unknowns comparable? |
| Reversibility & time pressure | Is the cost of being wrong comparable? |
| Reputation & alliances | Does the choice similarly signal loyalty, trust, or alignment? |
| Cost structure | Are the visible costs and tail risks of the same type? |

- **9–12**: high similarity, preferred
- **6–8**: medium similarity, supplemental only
- **0–5**: weak analogy, normally excluded

## Default output

A normal run should contain:

```text
一句话判断

你的场景内核
- ...

最像的历史案例
1. 案例 / 决策节点
   - 当时局面
   - 当时可知信息
   - 可选项
   - 实际选择与判断逻辑
   - 短期 / 长期结果
   - 显性 / 隐性代价
   - 原文与出处
   - 相似点 / 失配点

跨案例规律
- 强启发 / 中启发 / 弱启发

放回今天的问题
- 哪个选择最不可逆？
- 哪个选择暴露你的立场？
- 谁会因此改变对你的信任？
- 最乐观结果没发生时还剩什么退路？
- 能否用低成本先换更多信息？

风险提醒
```

## Files

- [`SKILL.md`](./SKILL.md): complete operating rules for the AI skill.
- [`examples/career-opportunity.md`](./examples/career-opportunity.md): career opportunity / public alignment example.
- [`examples/startup-partnership.md`](./examples/startup-partnership.md): startup partnership and incentive alignment example.
- [`examples/stay-or-exit.md`](./examples/stay-or-exit.md): stay-versus-exit and dependency example.

## How to use

The simplest way is to provide `SKILL.md` to an AI agent as a persistent skill / system instruction, then ask a real decision question.

Example:

```text
Use history-decision-simulator.

I have an opportunity to join a much stronger team, but accepting it would require me to publicly distance myself from the people who originally helped me. The new opportunity is valuable, but the long-term stability of the new team is uncertain. Help me reason through the decision.
```

The agent should search the designated primary-text libraries before quoting history. It should **not** invent passages, motives, volume numbers, or counterfactual outcomes from memory.

## What this skill is not

This is not a substitute for current law, medicine, financial regulation, tax rules, safety guidance, or modern empirical evidence. When a present-day question can be answered directly by high-quality modern evidence, that evidence takes priority. Historical cases are used to illuminate mechanisms, second-order effects, and decision structure.

## License

MIT. See [`LICENSE`](./LICENSE).
