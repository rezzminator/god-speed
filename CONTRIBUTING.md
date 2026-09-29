# Contributing

Thanks for helping. This repository is one skill, [`SKILL.md`](SKILL.md): a Markdown file that an agent reads each time it loads the skill. Every line costs tokens on every invocation, so the bar for a change is that it alters what the agent *does*.

## Reporting a problem

Open an issue with the **Trigger or behaviour report** template. Include:

- the exact prompt;
- the agent and its version (`claude --version`, `codex --version`, `opencode --version`) and the model;
- whether the skill loaded (in Claude Code, a `Skill(god-speed)` line appears in the transcript);
- what the agent did, and what you expected.

## Changing `SKILL.md`

1. Open an issue first for anything beyond a typo, so the behaviour change can be agreed before the wording.
2. Keep the `description` short: it is the trigger, and the agent routes on it alone.
3. State rules positively and once; no rule should appear twice.
4. Test the change on at least one agent. Run a prompt that ends with "God speed" and check that the skill loads and that the final report lists the decisions. Then run a prompt that only asks about the phrase and check that the skill does not load. Put both results in the pull request.
5. Bump `version:` in the `SKILL.md` frontmatter and the version badge in `README.md` together: a patch for a wording fix, a minor for a behaviour change.

## Code of conduct

This project follows the [Contributor Covenant](CODE_OF_CONDUCT.md).
