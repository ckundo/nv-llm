# non-visual-mode

A Claude [skill](https://docs.claude.com/en/docs/claude-code/skills) that sets up a session to produce output comfortable to consume **non-visually** — by screen reader, braille display, or text-to-speech — and then keeps formatting every reply that way for the rest of the conversation.

It triggers on a fact about the *user* ("I use a screen reader", "I'm blind", VoiceOver / NVDA / JAWS, "make this accessible"), not on a task verb. Once on, it formats by ear: lead with the answer, real headings and ordered lists, **no tables** (prose with the label repeated per value), **no ASCII charts** (describe the data and trend in words, offer images with standalone alt text), describe code before showing it, no decorative emoji, descriptive link text, no visual deixis ("as you can see").

## Results

Three-way ablation on 5 prompts that deliberately bait the anti-patterns (a comparison that tempts a table, a chart request, a code dump, a wall of text). Same rubric (5 assertions per eval), one run per condition.

| Condition | Pass rate |
|---|---|
| **`non-visual-mode` skill (32 lines)** | **100%** (25/25) |
| Just saying *"I use a screen reader"* (no skill) | 76% (19/25) |
| No skill, no disclosure | 56% (14/25) |

The bare disclosure already gets Claude most of the way, but it's inconsistent case-to-case (3/5–5/5): it produced both a markdown table *and* an ASCII bar chart on the revenue prompt, and gave the OAuth steps as prose instead of a navigable ordered list. The skill closes that gap on exactly the high-impact cases and stays 5/5 every time, for ~1k extra tokens per turn.

The full interactive results (every output under each condition + the benchmark) are published on the [`gh-pages`](../../tree/gh-pages) branch / GitHub Pages site.

## Layout

- **`non-visual-mode/`** — the skill (`SKILL.md` + `evals/evals.json`).
- **`screen-reader-mode-workspace/`** — eval harness output: iterations 1–4, each with per-condition responses, gradings, and a benchmark. `skill-snapshot-full/` holds the earlier 186-line version before it was pared to 32 lines.

## Method & caveats

Each condition was run by an independent subagent producing the assistant reply for a fixed prompt; outputs were graded against per-eval assertions — objective checks (no tables / ASCII art / emoji; headings and ordered lists present) plus judgment calls (answer-first, code-described-before-block, counts stated in words, standalone alt text). **n = 1 per cell, a single model, and the same 5 prompts the skill was shaped against** — so treat the numbers as directional, not a significance test. Built and evaluated with the [skill-creator](https://github.com/anthropics/skills) harness.
