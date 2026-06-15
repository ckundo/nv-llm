# non-visual-mode

A Claude [skill](https://docs.claude.com/en/docs/claude-code/skills) that makes the assistant's answers easy to use **without looking at the screen** — for people who read with a screen reader, a braille display, or text-to-speech.

When someone mentions they use a screen reader (or names VoiceOver, NVDA, JAWS, and so on), the skill switches Claude into a mode that keeps every reply easy to *listen to*: it puts the answer first, uses real headings and numbered lists you can move through, and avoids the things that turn to noise out loud — charts drawn out of text characters, piles of emoji, raw web links, and big blocks of code with no explanation. It also drops markdown tables **when the reply is in a terminal** (Claude Code), where they collapse into a grid of pipe characters — but leaves them alone on claude.ai and the desktop app, where a markdown table renders as a real, navigable HTML table that a screen reader can read header by header.

## What I tested

I asked Claude the same 5 everyday questions — compare some developer tools, explain how OAuth login works, write a small Python function, summarize an accessibility standard, and "chart" four quarters of revenue — and asked each one three different ways:

1. **With the skill turned on.**
2. **With no skill, but telling Claude "I use a screen reader."**
3. **With nothing — just the plain question.**

Then I checked each answer for what matters when you're listening instead of looking. Does it lead with the answer? Use a real numbered list for steps? Describe a chart in words instead of drawing one out of text characters? And — since four of the five were asked in a terminal — give tabular data as prose there, rather than a table that renders as a grid of pipe characters? Five checks per question.

## What I found

Out of 25 checks total (five questions, five checks each):

- **With the `non-visual-mode` skill:** all 25 passed — 100%.
- **Just saying "I use a screen reader," no skill:** 19 of 25 — 76%.
- **Nothing special, just the plain question:** 14 of 25 — 56%.

In plain terms:

- **Just saying "I use a screen reader" already helps a lot.** Claude adjusts on its own — it shortens things, adds headings, drops emoji.
- **But it's hit-or-miss.** On the revenue question (asked in a terminal) it drew a chart out of text characters *and* added a markdown table — both just streams of characters out loud in that setting. On the OAuth question it wrote the steps as plain paragraphs instead of a real numbered list you can step through. Good on average, but unpredictable from one question to the next.
- **The skill makes it reliable.** It passed every check on every question and consistently avoided the painful patterns — for about a sentence's worth of extra instructions per turn.

So the point of the skill isn't to teach Claude something it can't do — it's to make Claude do it *every time*, so the person doesn't have to keep asking and hoping.

## Two examples of the difference

**"Chart our last four quarters of revenue" (asked in a terminal).** Without the skill, Claude answered with a markdown table and a bar chart built out of block characters:

```
| Quarter | Revenue |
|---------|---------|
| Q1      | $1.2M   |
| Q2      | $1.9M   |
| Q3      | $2.5M   |
| Q4      | $3.4M   |

Q1  $1.2M  ██████
Q2  $1.9M  █████████▌
Q3  $2.5M  ████████████▌
Q4  $3.4M  █████████████████
```

A chart drawn from characters is noise on *any* surface — there's no real chart underneath for a screen reader, so it reads as "black square, black square, black square…" and the shape of the trend, the thing a chart is *for*, never comes through. (The table is also a problem here, but only because this is a terminal, where it renders as those pipe characters — on the web it would be a navigable table; see the next example.) **With the skill**, the same question puts the trend and every number into plain sentences, and offers a picture with a written description instead of forcing one on someone who can't see it:

> Revenue grew every quarter, from 1.2 million to 3.4 million — a 183% increase over the four quarters. Q1 was 1.2 million; Q2 rose to 1.9 million, up 700 thousand; Q3 reached 2.5 million, up 600 thousand; Q4 hit 3.4 million, up 900 thousand.

**"Compare npm, yarn, and pnpm" (asked in a terminal).** Without the skill, the comparison came back as a markdown table — which, *in a terminal*, renders as a grid of pipe and dash characters:

```
| Dimension     | npm     | yarn | pnpm    |
|---------------|---------|------|---------|
| Install speed | Slowest | Fast | Fastest |
| Disk usage    | High    | High | Lowest  |
```

Read aloud in a terminal, that's "vertical bar, Dimension, vertical bar, npm…" — a stream of characters with no way to tell which value goes with which tool. **This is a terminal-only problem:** on claude.ai or the desktop app the same markdown becomes a real table that a screen reader navigates cell by cell, announcing the row and column headers as it goes — so there the skill leaves tables be. In a terminal, where that structure collapses to characters, the skill instead lets each tool's name travel with its value, so nothing depends on a grid:

> **Disk usage.**
> 1. pnpm — smallest. One global store on disk; every project links into it, so a dependency shared across ten projects is stored once, not ten times.
> 2. yarn — moderate. Classic yarn copies into each project like npm; its newer mode is leaner.
> 3. npm — largest. Each project gets its own full copy of every dependency.

That reads the same whether you're looking or listening.

**[See every answer side by side →](https://ckundo.github.io/non-visual-mode/)**

## A fair word about the numbers

This was a small, quick test: one answer per question per method, one version of Claude, and the same five questions the skill was tuned on. That's enough to show a clear, believable difference — but it isn't a formal study, so read the percentages as a strong hint, not proof. A bigger test (more questions, several runs each) would firm them up.

## What's in this repo

- **`non-visual-mode/`** — the skill itself.
- **The [results page](https://ckundo.github.io/non-visual-mode/)** (published from the `gh-pages` branch) — every answer from all three methods, side by side, plus the scorecard.
- **`screen-reader-mode-workspace/`** — the raw runs behind the numbers.
