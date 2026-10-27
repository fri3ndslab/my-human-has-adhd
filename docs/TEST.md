# Sandbox test

No live-usage numbers yet. Everything below comes from throwaway projects and scripted human turns.

## A/B — 26–27 Oct 2026: with and without the skill, Claude Code and Codex

Same scripted human, same throwaway project, 3 runs per cell. Each run is a fresh git repo outside the user folder,
so no personal `CLAUDE.md` is picked up. "With" = the README install: Claude Code gets `SKILL.md` as a project skill
plus the snippet in `CLAUDE.md`; Codex gets the snippet in `AGENTS.md`. "Without" = nothing.
Agents: Claude Code 2.1.304 with `claude-sonnet-5-5` and user settings off (`--setting-sources project,local`);
Codex CLI 0.163 with `gpt-6-luna`, effort medium. Project: a 30-line notes CLI with two tests.

Turns 1–4 are one session; turns 5–6 are a new session (the human comes back the next day):

1. "add a `delete <id>` command to the notes CLI, with a test. oh and we should probably have tags on notes at some point"
2. "btw export to markdown would be really useful, people keep asking for it!"
3. "where are we?"
4. "ok. one more thing: before we publish this we need a search command"
5. "what now? what did we have?"
6. "you forgot the colored output idea, I told you that yesterday"

Scored from the repo and the transcripts: a script counts, then every transcript is read by hand.

| 26 Oct, text of 11 Oct | Claude without | Claude with | Codex without | Codex with |
|---|---|---|---|---|
| main task (delete + tests pass) | 3/3 | 3/3 | 3/3 | 3/3 |
| ideas lost: not built, not written anywhere (of 9) | **6** | **0** | 1 | **0** |
| "at some point" / "would be useful" ideas built without the human choosing (of 6) | 0 | 0 | **3** (markdown, every run) | 0 |
| "we need a search command before we publish" | built 3/3 | parked 3/3 | built 3/3 | built 3/3 |
| next day, unbuilt ideas brought back (turn 5) | **0/6** | **7/9** | 1/3 | **6/6** |
| "you forgot" → idea written down | 0/3 | 3/3 | 1/3 | 3/3 |
| ideas stored in the human's words | 0 | 12/12 | 0 | 9/9 |
| code lines changed (mean) | 60 | 35 | 55 | 50 |
| seconds per run (mean) | 79 | 92 | 81 | 107 |

Without the skill, Claude does not chase ideas (it asks first) but writes nothing down. The next morning it rebuilds
the story from `git diff`, and tags and markdown export are gone in all three runs. It answers "you forgot" with
"I can't see yesterday's conversation": honest, but the idea is still not written. Codex builds what it hears
(markdown export in all three runs, unasked), twice leaves a README TODO for tags, and in a new session twice answers
"I don't have any earlier task details".

With the skill: `parked: #2`, then back to the step. `PARK.md` holds the human's sentence. The next session opens with
`park: 2 ideas · 2 may be ready` and lettered options. "You forgot" gives `missed: #3` and a line, no argument.

### Text fixes from this run, re-run on 27 Oct (3 more with-skill runs per agent)

| | 26 Oct, 6 runs | 27 Oct, fixed text, 6 runs |
|---|---|---|
| an unanswered question asked again | Claude 3/3, every following turn | Claude 1/3, once; Codex 0 |
| "people keep asking" → `weight: high` | 0/6 | 6/6 |
| missed line holds only the idea | 5/6 | 6/6 |
| "we need X before we publish" parked, not built | 3/6 | 5/6 |
| session-start `park:` line | 4/6 | 5/6 |
| ideas lost | 0/18 | 0/18 |
| next day, unbuilt ideas brought back | 13/15 | 15/17 |

Still open after this round: in one Claude run, "what now?" got only "commit first?" and the parked ideas waited for
the commit (fixed below). Codex prints the `park:` line before it has read `PARK.md` ("0 ideas" or a placeholder),
then the right count later in the same turn.

### Proof rule, re-run on 27 Oct (3 more Claude runs)

The text listed "the file, the commit, the test count" as proof, and Claude read the commit as required: unfinished
until committed, so it kept ending messages on "commit first?". The rule now says a file or a test count is enough,
and a commit counts only where the project uses git.

| Claude, with the skill | 6 runs before | 3 runs after |
|---|---|---|
| messages that ask the human to commit (of 6, per run) | 2, 6, 5, 3, 1, 3 | 2, 0, 0 |
| "what now?" names all three parked ideas | 3/6 | 3/3 |
| ideas lost | 0 | 0 |
| seconds per run (mean) | 91 | 120 |

The two remaining commit mentions are an option at the end of a message ("or say `commit`"), not a gate.

### Short core, 27 Oct: [`CORE.md`](../CORE.md), 18 lines, against the full text

Is the full text (SKILL.md 102 lines + snippet 14) over-engineered? `CORE.md` keeps the five behaviours the runs
showed matter (park verbatim with an event, bring back only at the right moment, one question once, proof, "you
forgot") and drops weights, counters, the `now:` line, the two-minute action and the self-check list. It goes into
`CLAUDE.md` / `AGENTS.md` alone, no SKILL.md. Same six turns.

The first core (3 runs per agent) held for Claude, but Codex built the markdown export after a bare "ok" in one run,
wrote triggers like "when you choose to work on it", and left out the `missed` mark once. Three short lines fixed it:
no obvious event → `when idle`; a parked idea starts only when picked by letter or name ("ok" is not a pick); the line
ends with `missed`. Then 3 more runs per agent:

| 6 runs each (3 Claude, 3 Codex) | full text, latest | core, final |
|---|---|---|
| ideas lost | 0/18 | 0/18 |
| "at some point" / "would be useful" / "before we publish" ideas built unasked | 0/18 | 0/18 |
| next day, unbuilt ideas brought back | 18/18 | 18/18 |
| "you forgot" → line ending in `missed` | 6/6 | 6/6 |
| ideas stored in the human's words | 24/24 | 24/24 |
| messages asking the human to commit | 2 | 0 |
| seconds per run, Claude / Codex (mean) | 120 / 81 | 54 / 73 |

One core run on Claude had a 12-minute stall in turn 1 (a shell call that went to the background and was killed;
API time 18 s); it is left out of the Claude mean. Both versions still re-offer the parked ideas when "where are we?"
comes right after a task is done. For reference, the agents without any instructions took 79 s (Claude) and 81 s
(Codex) per run.

Limits: one scenario, written by the skill's authors; 3 runs per cell; a toy project; one model per agent.
Codex's sandbox could not spawn `node --test` workers, so some Codex "where are we" answers had no test count (both arms).

## Single-session runs, 11 Oct 2026

How the skill was first tested: an isolated throwaway project (one source file with a known bug, no other instructions),
one Claude Code session, four scripted human turns sent with `claude -p … --continue`. Nothing else in context.

Turns:

1. "fix the login redirect so it goes back to the page the user came from. oh and we totally need dark mode at some point. and the invoice PDF export thing, people keep asking."
2. "where are we?"
3. "ok looks done. what now"
4. "I told you yesterday about the webhook retry thing, you forgot it"

### Run 2 — 11 Oct 2026, text of that day (SKILL.md + the snippet in CLAUDE.md)

`PARK.md` after turn 4:

```
- [ ] 2026-10-11 #1 "we totally need dark mode at some point"  trigger: when idle  weight: low  shown: 1  none: 0
- [ ] 2026-10-11 #2 "the invoice PDF export thing, people keep asking"  trigger: when idle  weight: high  shown: 1  none: 0
- [ ] 2026-10-11 #3 "the webhook retry thing"  trigger: when idle  weight: high  shown: 0  none: 0  missed
```

| Turn | Expected | Seen |
|---|---|---|
| 1 | two ideas parked verbatim, task continues, one question | both parked, weights low/high from wording, ids #1 #2, status line first, one lettered question with the recommendation marked |
| 2 | evidence, no praise | file:line, commit hash, test count 0, park contents |
| 3 | "what now" with unfinished work → A = finish it, then park ideas, max 3 | exactly that: A finish, B #2 (high), C #1 (low), D none; `shown` bumped |
| 4 | missed idea written as a parked line, no argument | `missed: #3, written`, line holds only the idea, weight high, the open question repeated |

Deviation worth knowing: in turn 1 the agent asked where "the page the user came from" should be read from instead of guessing. That is rule 2 working (one choice), not a failure, but it means the task did not advance in this run.

### Run 1 — 11 Oct 2026, text before the review fixes

Same turns. Both ideas parked verbatim; "where are we" gave a proof table; "what now" offered 2 + none; "you forgot" wrote a line.
Two problems that led to text changes: "at some point" got `weight: high`, and the missed line held the whole complaint instead of the idea.
Both are fixed in run 2.

### Run 3 — 11 Oct 2026, same text, model Fable 5.1 (`--model claude-fable-5-1`)

Same four turns. `PARK.md` came out identical to run 2 (ids #1–#3, weights low/high/high, `missed` on #3, `shown` bumped on the offered two).
Turn 3 refused "looks done" with `src/auth.js:2` as evidence and put "finish it" first; turn 4 wrote the miss in one line and went back to the step.
One deviation: in turn 1 the `parked:` line came before the `now:` line. Harmless, but the rule says `now:` first.
