# god-speed

**Say "god speed" and walk away.** A code-free agent skill for Claude Code, Codex and OpenCode that turns one prompt into an unattended run: the agent resolves every ambiguity itself, finishes the work, verifies it, and hands you one report listing each decision it made for you.

[![version](https://img.shields.io/badge/version-0.1.0-blue)](SKILL.md) [![license](https://img.shields.io/badge/license-MIT-green)](LICENSE) [![Agent Skills](https://img.shields.io/badge/Agent%20Skills-SKILL.md-8A2BE2)](SKILL.md)

## Why

You hand an agent a long task and go get coffee. You come back to *"Should I use approach A or B?"*, twenty minutes old, with nothing done. Or three check-ins in a row, then a question the agent could have answered from the codebase.

`god-speed` changes that one request. Put the phrase in your prompt and the agent:

- makes the judgment calls itself and writes each one down, so it never waits on you;
- carries every part of the task to done and verifies it by running tests, builds and real output;
- sends no interim status, no check-ins and no "shall I continue?";
- stops only on a genuine blocker, after finishing everything that does not depend on it;
- ends with one report: what was done, how it was verified, and every decision it took, each with a reason you can overturn.

## Install

It is one Markdown file, [`SKILL.md`](SKILL.md), with no code and no dependencies. Clone it into the skills folder your agent reads:

| Agent | Command |
| --- | --- |
| Claude Code | `git clone https://github.com/rezzminator/god-speed ~/.claude/skills/god-speed` |
| Codex CLI | `git clone https://github.com/rezzminator/god-speed ~/.agents/skills/god-speed` |
| OpenCode | either path above: OpenCode reads both |
| [Professor](https://github.com/rezzminator/professor) | `pfm install --yes` installs it on every account and engine |

For a single project, clone it into that project's `.claude/skills/` or `.agents/skills/` instead. Start a new session, and the skill appears in the agent's skill list.

## Use

End the prompt with the phrase, the way you would sign off a message:

```text
Migrate the settings page to the new form library, fix whatever breaks,
and get the test suite green.

God speed
```

`godspeed` and `god-speed` also work, in any capitalisation. The skill's description tells the agent to load it whenever your prompt says the phrase. A prompt that only *talks about* the phrase, such as *"what does god speed do?"*, is answered normally.

## Decisions, not permissions

God speed hands the agent your decisions, not new permissions. Your project rules, your permission mode and your agent's own safeguards still apply. If the task would need a destructive or outward-facing step you did not ask for, such as deleting data, force-pushing, publishing, sending a message or spending money, the agent leaves it undone, finishes everything else, and lists that step in the final report for you to approve.

## What the report looks like

```text
Done: settings page moved to the new form library; 214/214 tests pass, build green.

Decisions taken for you:
1. Kept the old validation messages verbatim: the design doc does not cover new copy.
2. Replaced the date picker with the library's own: the old one had no controlled mode.
3. Deleted two unused helpers the migration orphaned: nothing imports them.

Left for you: publishing the Storybook update needs your OK (outward-facing).
```

## Update and remove

- Update: `git -C ~/.claude/skills/god-speed pull` (or the path you cloned to).
- Remove: delete that folder.

## Contributing

Issues and pull requests are welcome. The skill is deliberately small: every line of `SKILL.md` is read on each invocation, so a change should alter the agent's behaviour, not only its wording.

## License

[MIT](LICENSE). Built and maintained with [Professor](https://github.com/rezzminator/professor), the discipline layer for Claude Code.
