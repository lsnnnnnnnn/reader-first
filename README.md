# Reader First · 顺着读懂

A writing skill for Chinese and English. Spend words where they help the reader follow the idea.

Sometimes I understand every word in an AI-generated answer and still need a second pass to work out what happened. A stack of nouns hides the action. A condition appears after the claim it limits. A "this" could refer to three different things.

Reader First asks the agent to make those relationships explicit. Keep the facts, technical terms, conditions, and uncertainty. Give the reader the connections needed to understand them.

[The story behind it](https://lsnnnnnnnn.github.io/blog/2026-11-14-reader-first.html) · [Read the skill](SKILL.md) · [More editing examples](references/examples.md)

## A sentence I would rather read once

Here is a hypothetical progress report from the examples that motivated the skill.

**Before**

> I added three concurrent-write cache-invalidation regression tests, all passing locally; production reliability under high load remains unverified.

**After**

> I added three regression tests to check whether the cache is invalidated as expected during concurrent writes. All three tests passed locally. Reliability under high production load has not been verified.

The revision introduces the tests, explains what they check, then states the result and its scope. "Cache invalidation" keeps its technical meaning. The same three tests passed in the same local setting.

The Chinese version uses the same editing decision:

> **原句：** 我新增了三个并发写入场景下的缓存失效回归测试，本地全部通过；线上高负载情况下的可靠性尚未验证。
>
> **改写：** 我新增了三个回归测试，检查并发写入时缓存能否按预期失效。三个测试在本地都通过了；线上高负载下是否可靠，还没有验证。

The revised version takes more words. Those words tell the reader how the facts fit together.

## Install in Codex

Clone the repository into your user skills directory:

```sh
mkdir -p ~/.agents/skills
git clone https://github.com/lsnnnnnnnn/reader-first.git ~/.agents/skills/reader-first
```

The repository root contains `SKILL.md`, so no build or package installation is needed. Codex detects local skills automatically. If Reader First does not appear, restart Codex. See the [official skill documentation](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills) for other installation locations.

## Use it on a real paragraph

Mention `$reader-first` in your prompt, followed by the text or task:

```text
Use $reader-first to revise this explanation for engineers who know Python
but have not worked with this service. Preserve the conditions and test results.
Return the revised text.

[Paste the explanation here.]
```

```text
请用 $reader-first 修改下面这段说明。读者了解机器学习，但没有看过这项工作。
保留术语、数字和结论范围，把需要读者自己猜的关系写清楚。只返回改写后的正文。

[粘贴原文]
```

You can also ask for a new explanation, a code review, or a progress report using the skill. State who will read it and what they need to understand. If you prefer suggestions before a rewrite, ask for those explicitly.

## What the skill pays attention to

- Introduce the object before explaining what it does. Let each sentence build on information the reader already has.
- Expand noun strings when their relationships are unclear. Keep established technical terms when the intended reader knows them.
- Keep a condition beside the claim it qualifies. Preserve quantities, negation, uncertainty, and the state of the work.
- Replace an ambiguous pronoun with the relevant noun. A little repetition can save a reread.
- Leave clear sentences alone. Preserve deliberate literary language, exact quotations, code, and identifiers when the task calls for them.

There is no target sentence length or vocabulary score. Sometimes an edit adds a clause. Sometimes it removes a paragraph. The useful question is whether the reader can follow the intended meaning with less reconstruction.

## Where the idea came from

Thomas Hikaru Clark, Matias B. Martin, and Kyle Mahowald's [*Why is AI-generated language so hard to understand?*](https://arxiv.org/abs/2610.29162v1) helped me think about long dependencies, stacked nouns, and the cost of compressing a sentence.

The paper studies English language features and model preferences. Reader First's editing workflow and Chinese guidance are practical extensions of that motivation. The [research notes](references/research-basis.md) explain the evidence and the limits of those extensions.

## Inside the repository

```text
SKILL.md                       Skill instructions, written in Chinese
agents/openai.yaml             Name, icon, and invocation settings
assets/icon.svg                Skill icon
references/examples.md         Chinese and English editing decisions
references/research-basis.md   Paper summary and evidence boundaries
```

The instructions support both Chinese and English. The examples and research notes are primarily in Chinese.
