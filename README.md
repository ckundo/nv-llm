# non-visual-mode

A Claude [skill](https://docs.claude.com/en/docs/claude-code/skills) that makes the assistant's answers easy to use **without looking at the screen** — for people who read with a screen reader, a braille display, or text-to-speech.

When someone mentions they use a screen reader (or names VoiceOver, NVDA, JAWS, and so on), the skill switches Claude into a mode that keeps every reply easy to *listen to*: it puts the answer first, uses real headings and numbered lists you can move through, and avoids the things that are painful to hear — tables (a screen reader reads them as a stream of "vertical bar, vertical bar…"), charts drawn out of text characters, piles of emoji, raw web links, and big blocks of code with no explanation.

## What we tested

We asked Claude the same 5 everyday questions — compare some developer tools, explain how OAuth login works, write a small Python function, summarize an accessibility standard, and "chart" four quarters of revenue — and we asked each one three different ways:

1. **With the skill turned on.**
2. **With no skill, but telling Claude "I use a screen reader."**
3. **With nothing — just the plain question.**

Then we checked each answer for the things that matter when you're listening instead of looking. Does it lead with the answer? Does it skip tables and text-art charts? Does it use a real numbered list for steps? Does it describe a chart in words and offer an image with a written description? Five checks per question.

## What we found

| How Claude was asked | Checks passed |
|---|---|
| **With the `non-visual-mode` skill** | **25 of 25 — 100%** |
| Just saying "I use a screen reader" | 19 of 25 — 76% |
| Nothing special | 14 of 25 — 56% |

In plain terms:

- **Just saying "I use a screen reader" already helps a lot.** Claude adjusts on its own — it shortens things, adds headings, drops emoji.
- **But it's hit-or-miss.** On the revenue question it produced *both* a table *and* a chart drawn in text characters — two of the worst things to hear. On the OAuth question it wrote the steps as plain paragraphs instead of a real numbered list you can step through. Good on average, but unpredictable from one question to the next.
- **The skill makes it reliable.** It passed every check on every question and consistently avoided the painful patterns — for about a sentence's worth of extra instructions per turn.

So the point of the skill isn't to teach Claude something it can't do — it's to make Claude do it *every time*, so the person doesn't have to keep asking and hoping.

**[See every answer side by side →](https://ckundo.github.io/nv-llm/)**

## A fair word about the numbers

This was a small, quick test: one answer per question per method, one version of Claude, and the same five questions the skill was tuned on. That's enough to show a clear, believable difference — but it isn't a formal study, so read the percentages as a strong hint, not proof. A bigger test (more questions, several runs each) would firm them up.

## What's in this repo

- **`non-visual-mode/`** — the skill itself.
- **The [results page](https://ckundo.github.io/nv-llm/)** (published from the `gh-pages` branch) — every answer from all three methods, side by side, plus the scorecard.
- **`screen-reader-mode-workspace/`** — the raw runs behind the numbers.
