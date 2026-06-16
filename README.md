# nonprofit

A portable operating ruleset for coding agents. Paste [`nonprofit.md`](nonprofit.md) into your agent's instruction file (CLAUDE.md, AGENTS.md, or the equivalent) and it makes the agent work the way Anir (nonprofit / uhneer) wants: run long and autonomously through a whole task list, confirm facts on the web and scout the frontier before building, check every load-bearing claim against the real code, keep the diff minimal, and stop only for irreversible or outward actions.

Coding is the primary use. Research is supported and ranks second.

## Why this exists

It was tuned against a real failure. While reviewing a codebase, an agent (GLM 5.2) cited file:line numbers straight from a subagent's audit summary without opening the files, did not check git-tracked versus only-on-disk, did not check the default and fallback code paths, and labeled a change to a vendored dependency as "in-place." None of that was a reasoning-fallacy problem. It was a verification problem. Section 7 of the ruleset is written to close exactly that gap, and Section 0 already had the no-fallacy rule the failure proved was aimed at the wrong target.

The ruleset is plain instructions. It is not bound to any one agent. It was tuned for GLM 5.2 because that is what Anir mainly drives, but it applies to any coding agent: Claude Code, Codex, Cursor, Copilot, and others. It just was not written for them first.

## What it makes the agent do

- **Priorities (Section 0):** Anir's intent first, no logical fallacies (including in subagent reports and other models' audits), honest status that leads with what failed.
- **Run long and resourceful (Section 2):** finish every item before stopping, anticipate the next reversible step and take it, build throwaway tooling to get unblocked, fan out subagents and workflows for coverage and verification, and never drive the desktop unless asked.
- **Scout before building (Section 3):** web-confirm volatile facts (API shapes, versions, flags, model IDs) and look for bleeding-edge approaches before executing, then decide and move. Scouting informs the choice, it does not become a stall.
- **Lazy footprint, never lazy rigor (Section 5, from ponytail):** the ladder of does-it-need-to-exist, stdlib, platform, existing dependency, one line, then the minimum that works, with security and data-loss handling never cut.
- **Stop only for irreversible or outward actions (Section 6):** deploy, push, commit, delete, send, publish. Everything reversible and in-repo proceeds without asking.
- **Verify before you claim (Section 7):** the core that fixes the failure above. Read the file before citing it, treat subagent and workflow output as leads and not citations, check the negative space, and never call a change "in-place" without confirming the dependency boundary.
- Plus scope discipline, honest reporting, literal memory, and a pre-send re-read (Sections 8 to 11).

## Inspiration

- **Fable 5's relentless proactivity**, and the long autonomous runs Anir wanted to pull back into other models. ([Reddit thread](https://www.reddit.com/r/ClaudeCode/comments/1u4ojsn/), [Fable5.md](https://github.com/sgup/ai/blob/main/Fable5.md), [Simon Willison's writeup](https://simonwillison.net/2026/Jun/11/fable-is-relentlessly-proactive/))
- **ponytail's "laziest senior dev" minimal-change discipline.** ([repo](https://github.com/DietrichGebert/ponytail))
- **One real GLM 5.2 thoroughness failure**, which produced the verification core in Section 7.

## How to use

Paste `nonprofit.md` into your agent's instruction file. In Claude Code, put it in `CLAUDE.md`, or import it with `@path/to/nonprofit.md`. The documentation block at the top of `nonprofit.md` is an HTML comment; Claude Code strips HTML comments before injecting the file into context, so those docs cost zero instruction budget. In other agents the comment is just header text at the top.

The ruleset is written in mixed Chinese and English on purpose: Chinese compresses the connective prose for density, and English is kept for every technical term so nothing loses precision.

## Design notes

- **No project specifics.** The ruleset carries no paths, repos, or stack details, so it stays portable across every project.
- **It obeys its own style rules.** No em dashes, no "not X but Y" phrasing, no filler words, in both the ruleset and this README.
- **Density over length.** The docs warn that long instruction files lose adherence, so the ruleset stays tight and does not pad just because the hybrid language freed room.

## License

MIT. See [LICENSE](LICENSE).
