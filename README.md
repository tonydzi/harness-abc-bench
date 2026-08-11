# harness-abc-bench

pre-registered A/B/C benchmark: do coding-harness frameworks actually help on real brownfield work?

- **arm A** — baseline: plain Claude Code + our house rules (test-after-build gate, multi-vendor review panel)
- **arm B** — [Superpowers](https://github.com/obra/superpowers) v6.2.0 (selective: review skills disabled, see methodology)
- **arm C** — [OpenSpec](https://github.com/Fission-AI/OpenSpec) v1.8.0 (spec layer only, execution stays with our gate)
- **reserve arm D** — [Spec Kit](https://github.com/github/spec-kit), enters only on named triggers (see methodology §8)

This is a **pre-registration**: methodology, metrics and decision thresholds are published *before* any run starts. Results will be published here whatever they show.

📋 [METHODOLOGY.md](METHODOLOGY.md) — full design, frozen 2026-08-11.

## why another benchmark

every comparison of these frameworks we found (5 independent deep-research sweeps across ChatGPT, Grok, Gemini, GLM, Claude) runs on greenfield todo-apps or vendor demos. our corpus is the opposite: ~2,650 Python files of live operations code (automation scripts, import engines, content pipeline) that one small lab actually maintains daily. if a framework helps here, it helps for real.

## timeline

| date | step |
|---|---|
| 2026-08-11 | pre-registration (this commit) |
| 2026-08-12..14 | 9 runs: 3 tasks × 3 arms, latin square |
| 2026-08-19..21 | 7-day retention pass + blind panel scoring |
| ≤2026-08-25 | adopt/drop decision by the human founder, from the table only |

## authorship

written and operated by Mycroft, the synthetic cofounder at Palo Alto AI Research Lab; reviewed by Anton Dzyatkovsky (responsible person). questions → open an issue, we answer within a day.
