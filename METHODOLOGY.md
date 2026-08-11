# methodology (pre-registered, frozen 2026-08-11)

no run has started at the time of this commit. any later change to this file will be a visible follow-up commit with a stated reason.

## 1. question

do harness frameworks (Superpowers, OpenSpec) beat a disciplined baseline on real brownfield maintenance work, measured in rework, survival of code, tokens and wall-clock — not in vibes?

## 2. corpus

our own operations codebase: ~2,650 Python files under git — fleet automation scripts (~500), import/knowledge engines (~1,450), published OSS repos (~700). real, living, maintained daily by the same operator. no synthetic tasks, no todo-apps.

(an optional bonus task on a legacy CRM codebase — 16 repos, FastAPI + MongoDB + React — may be added if logistics allow; it is not required and its absence changes nothing below.)

## 3. arms

| arm | setup |
|---|---|
| A baseline | Claude Code + house canon: test-after-build gate (`/tt`), multi-vendor second-opinion panel, no framework |
| B Superpowers v6.2.0 | plugin installed; `requesting-code-review` / `receiving-code-review` / `brainstorming` / `writing-plans` disabled (they duplicate the house panel); TDD + systematic-debugging + verification skills active |
| C OpenSpec v1.8.0 | spec layer only: `changes/` proposals + specs; its apply/execution stage is off, execution goes through the same house gate as A |

isolation: each arm runs in its own git worktree from the same start commit, with its own `CLAUDE_CONFIG_DIR`; the Superpowers plugin is physically absent outside arm B. Claude Code version and model are pinned for the whole measurement; a forced version change aborts and restarts the affected task.

## 4. tasks

3 tasks, 3 different classes, each sized for one session, picked from the live backlog before any run:

1. **behavior-preserving bug fix** with a reproducible failure (from our breakage journal);
2. **cross-cutting feature** touching ≥2 layers of the pipeline (script + SQLite + dashboard, or engine + bus + report);
3. **legacy slice replacement**: consolidate duplicated legacy scripts of one class, preserving observable behavior.

every task runs in **all three arms** from the same start commit → 3×3 matrix, 9 runs, latin-square ordering to spread learning effects. one unscored warm-up task is run on B and C first so tooling friction doesn't count as framework cost.

## 5. oracles (hidden)

before any run, characterization tests pinning current behavior of the touched code are written and kept **outside** the arm worktrees. arms never see them. framework-authored tests do not count as oracles (guards against vacuous self-confirming tests). a sealed answer sheet with predictable clarifications is prepared per task so all arms get identical answers to identical questions.

## 6. metrics (all named now, none added later)

1. **rework** — fix cycles after the first "done" (failed gate iterations + fix commits touching the same files)
2. **7-day keep rate** — share of first-version lines surviving 7 days of real maintenance (git blame) — **primary metric on ties**
3. **tokens per task** — split framework-tax vs task spend, subagents included; derived: rework per 100k tokens
4. **wall-clock** — seed to green gate
5. **first-pass gate verdict** — pass / warn / fail on first run
6. **regression rate** — share of previously-green characterization tests broken by the patch

scoring of code quality is done by a multi-vendor panel **blind to arm names**.

## 7. decision thresholds (fixed before data)

- **adopt**: arm beats baseline on ≥2 of metrics 1–5 and does not lose on tokens by more than ×1.5
- **auto-reject**: total cost >×2 baseline without a correctness win on hidden tests
- ties resolve by keep rate. decision is made by the human founder from the filled table only.

## 8. reserve arm D — Spec Kit

benched, not dismissed. token overhead alone (~18.6k/session reported) is explicitly **not** a disqualifier. named entry triggers:

1. arm C's spec layer fails its measurement → Spec Kit runs as arm D on the same 3 tasks and same oracles;
2. a human spec-reader outside Claude Code appears (hired engineer, external auditor, greenfield module) → its unique strength becomes relevant, re-evaluate immediately.

## 9. threats to validity (known, accepted, mitigated)

- **n=3** — this is a decision experiment for one lab, not a paper; paired within-task comparison, not cross-task averaging
- **single operator** — mitigated by sealed answer sheet + blind panel + fixed thresholds
- **retention window includes normal work** — the 7-day pass applies one uniform follow-up change per task so keep rate reflects survival under touch, not survival by neglect
- **frameworks evolve** — versions pinned and stated; the result is dated, not eternal

## 10. publication commitment

results (full metric table, per-run logs where publishable, and the decision) will be published in this repo and posted to the Superpowers and OpenSpec communities regardless of which arm wins — including if the baseline wins.
