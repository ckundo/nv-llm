---
name: non-visual-mode
description: >-
  Reformat the session's replies for non-visual consumption — screen reader,
  braille display, or text-to-speech — and keep them that way for the rest of the
  conversation. This is an explicit opt-in: use it when the user invokes it by name
  or directly asks you to make your output non-visual, screen-reader-friendly,
  accessible, or audio-friendly. Because it changes formatting for the whole rest
  of the session, do NOT switch it on just because a screen reader, braille,
  VoiceOver, NVDA, JAWS, Orca, Narrator, or TalkBack happens to be mentioned —
  passing, hypothetical, and third-party mentions ("my coworker uses a screen
  reader", "is this chart accessible?", general accessibility questions) are not
  requests to reformat. If the user says they themselves use assistive tech but
  hasn't clearly asked you to adapt, OFFER to turn non-visual formatting on and
  wait for confirmation rather than assuming.
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
