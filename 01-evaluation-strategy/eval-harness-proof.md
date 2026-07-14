# First LLM-as-a-Judge Eval — Module 1

> Module 1 · First Eval Lab · repo file `01-evaluation-strategy/eval-harness-proof.md`
>
> How I wired my first eval harness — an LLM-as-a-Judge running over a dataset — and beat the cold start by seeding a starter dataset. In Module 1 the harness is wired but not scored yet (the dataset is near-empty); the first scored run comes in Module 2.

## Version A — Concise (system prompt used)

```text
You are an executive briefing assistant.
Summarize in exactly 3 bullet points under 60 words. No preamble, no extra text.
```

## Version B — Narrative (system prompt used)

```text
You are a PR communications assistant.
Write a 100-word narrative summary highlighting wins first, then risks and next steps. Keep a positive tone. No bullets.
```

## Eval setup — dataset name + judge model/family

Dataset: `email_summary_quality_dataset` in LangSmith. Evaluator: `Conciseness (LLM-as-a-Judge)`.

Generator = GPT-5 mini (OpenAI). Judge = an OpenAI model as well, for this first wiring pass. **Known limitation:** the judge is from the same model family as the generator, which risks self-preference bias — I plan to swap the judge to a different family (e.g. Anthropic or Google) before the first scored run in Module 2.

## Cold-start — the prompt I used to seed a starter dataset

```text
Generate 20 example rows for evaluating email-summary quality.
Each row: an input email + a candidate summary + a first-pass label ("good" or "bad") + a one-line reason.
Make roughly half concise/faithful ("good") and half verbose or inaccurate ("bad").
Return it as a markdown table.
```

## My definition of good vs bad (golden-set criteria)

**Good** = faithful to the source email with no invented facts, keeps the key numbers (e.g. engagement +25%, open rate 42% to 35%), surfaces the decision-relevant items (video delay, Friday tracking-link deadline), and stays within the length limit (60 words or less for the concise format).

**Bad** = adds claims not in the source, drops or buries a key number, hides risks behind positive framing, or rambles past 100 words so the CEO has to dig for the point.

## Screenshots — links or repo paths (optional if you followed the live demo)

Followed the instructor's live demo — screenshots to be added under `01-evaluation-strategy/screenshots/` in a follow-up commit.

| What it shows | Screenshot / link |
|---|---|
| Eval setup (dataset + judge) | _to add_ |
| Starter dataset rows | _to add_ |
