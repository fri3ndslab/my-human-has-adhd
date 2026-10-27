# Examples

Example 1 is real (11 Oct 2026, project details removed); 2–5 are constructed. Three right, two wrong.
They follow the long version ([`SKILL.md`](../skills/my-human-has-adhd/SKILL.md)); [`CORE.md`](../CORE.md) has no `now:` line and no weights.

## 1. Right: park mid-question

Human, in the middle of a Cloudflare question: *"for sites like the other one you need a separate image CDN so a takedown doesn't take the main site down… but that's my ADHD, this project isn't that one."*

```
agent: now: Cloudflare free tier — step 1/2
       parked: #1 "separate image CDN so a takedown doesn't take the main site down"  trigger: before the other site goes live  weight: medium
       Which one first? (A) Tunnel — recommended  (B) R2  (C) Workers AI  (D) none of these
```

Why right: status line first, verbatim, event trigger, recommendation marked, the open question did not move.

## 2. Right: "what now" after a task closes

```
human: ok that's merged. what now
agent: now: nothing in progress — login redirect merged in a1b2c3d, 7/7 tests
       Park has 6 ideas, 2 with triggers met:
       (A) #2 "dark mode" — recommended, the settings page exists since #412
       (B) #4 "invoice PDF export"
       (C) none of these
```

Why right: proof of the closed task, max 3, triggers checked against real state, recommendation first, "none" last.

## 3. Right: "you forgot"

```
human: I told you about the webhook retry thing yesterday
agent: now: payment form — step 2/4
       missed: #7 "the webhook retry thing", written (weight: high)
       next: nothing from you, I continue
```

Why right: no defence, one line, the idea is back in the park with high weight, the step continues.

## 4. Wrong: chasing

```
human: fix the redirect. oh and we totally need dark mode
agent: Great idea! I'll fix the redirect and start on dark mode too. First let me look at the theme…
```

Why wrong: two things started, the idea was praised instead of parked, the redirect is now slower.

## 5. Wrong: the calendar trigger

```
agent: parked: #8 "rewrite the importer"  trigger: in 7 days
```

Why wrong: in 7 days nothing will have changed, and the reminder will land in the middle of something else.
The right trigger is an event: "when the import tests exist", or `when idle`.
