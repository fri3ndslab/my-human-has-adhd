# Changelog

## 0.1.0 (unreleased)

- Initial release: `SKILL.md` (three rules, the park, event triggers, self-check), `CLAUDE.snippet.md`, `EXAMPLES.md`, `TEST.md`.
- Review changes: numbered ids, a `none` counter that drops an idea after three "none"s, a forgotten idea written back as a parked line marked `missed`, examples that follow the rules, install notes.
- Sandbox test changes: weight comes from the wording ("at some point" = low, "people keep asking" = high), and the `missed` line holds the idea, not the complaint.
- A/B test changes (Claude Code and Codex): a question is asked once and silence is not an answer; "add X" is a task, anything tied to later is an idea; any high signal wins the weight; the session-start line comes after reading `PARK.md`; proof is a file or a test count, a commit only where the project uses git.
- `CORE.md`: the 18-line version, now the main install; same results as the long version in the A/B runs, faster.
- README rebuilt around the problem (scope creep, ideas lost between sessions), the measured results and a FAQ; three diagrams in light and dark; the real example has its project details removed.
- Repo layout: `CORE.md` at the root; the long version in `skills/my-human-has-adhd/`; `TEST.md`, `EXAMPLES.md` and this file in `docs/`; launch videos and the demo GIF moved out.
- Mascot: a fluffy friend holding the `#3` note (`assets/mascot.svg`, dark variant, square `avatar.svg`); new 1280x640 social preview.
