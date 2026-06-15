# screen-reader-mode — skill vs bare disclosure vs nothing

| Condition | Pass rate |
|---|---|
| Pared skill (32 lines) | 100% |
| 'I use a screen reader' (no skill) | 76% |
| No skill, no disclosure | 56% |

## Per-eval (with_skill / disclosure_only / without_skill)

| Eval | Skill | Disclosure | Nothing |
|---|---|---|---|
| table-compare-terminal | 5/5 | 4/5 | 2/5 |
| code-retry-decorator-terminal | 5/5 | 4/5 | 2/5 |
| oauth-summary-terminal | 5/5 | 3/5 | 4/5 |
| wcag-pour-rendered | 5/5 | 5/5 | 4/5 |
| revenue-chart-terminal | 5/5 | 3/5 | 2/5 |

## Notes

- THREE-WAY ABLATION on the same 5 prompts + same rubric: pared SKILL 100%  >  bare 'I use a screen reader' 76%  >  no skill / no disclosure 56%.
- The bare disclosure does a LOT on its own (76% vs 56%) — modern Claude genuinely adapts to 'I use a screen reader': it front-loads, uses headings, and avoids emoji without being told.
- But the skill closes the last 24 points on exactly the high-impact cases the disclosure misses: on the revenue prompt the disclosure produced BOTH a markdown table AND an ASCII bar chart (the two worst aural anti-patterns); on oauth it reverted to 'Step 1:' prose instead of a navigable ordered list and never stated the count in words.
- The disclosure's other misses were softer: a formatting preamble before the answer (table eval) and naming the language only in the code fence, not in prose (code eval).
- Consistency is the real differentiator: the disclosure is good on average but unpredictable case-to-case (3/5 to 5/5); the skill is 5/5 every time. A user shouldn't have to re-say 'I use a screen reader' each turn and hope — the skill makes it durable for the whole session.
- Cost is negligible: pared skill ~26190 tok/run vs ~25115 for no-skill and ~24847 for the disclosure — the 32-line skill adds well under 1k tokens over saying nothing.