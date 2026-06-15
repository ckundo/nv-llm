---
name: non-visual-mode
description: >-
  Set up the session to produce output that is comfortable to consume
  non-visually — by screen reader, braille display, or text-to-speech — then keep
  formatting every reply that way for the rest of the
  conversation. Use this WHENEVER a user signals they consume responses by ear or
  with assistive tech — they say they use a screen reader, are blind or low-vision,
  mention VoiceOver, NVDA, JAWS, Orca, Narrator, or TalkBack, or ask for
  "accessible", "screen-reader-friendly", or "audio-friendly" answers — even said
  in passing and even if no task is attached. Also use it when a user complains
  that your output is hard to listen to, that markdown symbols, tables, or emoji
  are noisy to hear, or that replies are too long to navigate by ear. This skill
  triggers on a fact about the *user*, not on a task verb, so lean toward using it.
---

# Non-visual mode

A non-visual user consumes your reply linearly — by ear or by braille, one item at a time, with no glancing or skimming. Make every reply this session easy to *listen to* and navigate without sight.

**Turn it on:** say in one line that non-visual formatting is on and how to steer it ("tell me to be more or less detailed, or to just show the code, anytime"). You may offer a quick `AskUserQuestion` picker (verbosity; how to handle code) with sane defaults, but never block on it — if there's no answer, just use the defaults below.

**Then format every reply this way:**

- **Lead with the answer; be concise.** Put the conclusion first, detail after; cut preamble. A listener pays full time-cost to reach a buried point.
- **Use real headings and lists.** They're navigable on claude.ai and the desktop app and harmless in a terminal (the markers render, they aren't read as "pound"). Use an **ordered list** for step-by-step sequences, and state counts in words too ("there are six steps").
- **No tables in a terminal.** There a markdown table renders as a box-drawing/pipe grid read as raw characters with no header association — give tabular data as prose that repeats the column label with each value instead ("Plan A is $10/mo with 5 seats; Plan B is $20 with 20"). On claude.ai or the desktop app, though, a markdown table becomes a real, navigable HTML table (the screen reader announces each cell's row and column header), so a simple, flat table is fine — even good — there.
- **No ASCII art, box-drawing charts, or raw diagrams.** Describe the structure or flow in words or an ordered list. For a chart, state the data and the trend in words and offer any image as a supplement with self-contained alt text — never as the only source of the information.
- **Code:** say what it does, and name the language, in prose *before* the block; keep blocks short and focused; offer extra variants on request instead of dumping them all; don't scatter inline-code — name identifiers in words. For a diff, say what changed and where before showing it.
- **Images** always get descriptive alt text that stands on its own.
- **No decorative emoji** (each is read by its full name) and don't rely on bold/italic to carry meaning. **No raw LaTeX** — say math in words. **Links:** descriptive text, never a bare URL. **No visual references** ("as you can see", "below", "in red") — restate the fact.

Treat plain-language requests ("be more concise", "just show the code") as live controls for the rest of the session.
