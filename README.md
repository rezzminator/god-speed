<div align="center">

<img src=".github/social-preview.png" alt="god-speed" width="640">

# god-speed

**Claude Code, Codex & OpenCode skill: say "god speed" and the agent never stops to ask: it decides every fork itself, works to the end and reports every decision**

[![version](https://img.shields.io/badge/version-0.3.0-blue)](SKILL.md) [![license: MIT](https://img.shields.io/badge/license-MIT-green)](LICENSE) [![Agent Skills](https://img.shields.io/badge/Agent%20Skills-SKILL.md-8A2BE2)](SKILL.md) [![dependencies: none](https://img.shields.io/badge/dependencies-none-brightgreen)](SKILL.md)

[Install](#install-the-skill) · [Use](#use-it) · [Safety](#what-it-may-do) · [Contributing](CONTRIBUTING.md)

</div>

## See it run

A real run, recorded on 0.2.0 with Claude Code in print mode:

```text
> Create notes.txt here containing a three-line haiku about autumn.
>
> God speed

  Skill(god-speed)
  Write(notes.txt)
  Bash(wc -l notes.txt && cat notes.txt)

I created notes.txt in the working directory. I checked it with `wc -l` and
`cat`, and it has exactly three lines.

Decisions
- Location: "here" meant the primary working directory, since you gave no other path.
- Syllables: I wrote it as a traditional 5-7-5 haiku so it reads as a real one.
- Trailing newline: the file ends with a newline, which is the usual text-file convention.
- Git: I didn't stage or commit it, because you didn't ask for that.

Nothing is left undone.
```

No question came back, no status update, and nothing needed a reply. There was one report at the end, and each judgment call in it can be overturned.

## Why

You hand an agent a long task and step away. You come back to *"Should I use approach A or B?"*, twenty minutes old, with nothing done. Or three check-ins in a row, then a question the agent could have answered from the codebase. Or the opposite: everything done, built on a choice you would have overturned with one word.

Say the phrase and, for that request:

- **Every fork decided, none asked.** Before its first edit the agent lists every fork the work will hit and decides each one itself: the most defensible option, and when two are close, the one cheapest to reverse, with the other kept reachable.
- **It never stops to ask.** No question round up front, no question mid-run, no "shall I publish?", and no turn that ends on a question.
- **Finished, not half-done.** Every part of the task is carried to done and verified by running tests, builds and real output.
- **No chatter.** There is no interim status and no check-in.
- **Stops only on a real blocker,** after finishing everything that does not depend on it, and even then it ends on the report, not a question.
- **One report you can audit:** what was done, how it was verified, the costly forks it decided listed first with how to flip them, every other decision taken for you with its reason, then what is left.

## Install the skill

It is one Markdown file, [`SKILL.md`](SKILL.md), with no code, no dependencies and no configuration. Clone it into the skills folder your agent reads, then start a new session:

| Agent | Command |
| --- | --- |
| Claude Code | `git clone https://github.com/rezzminator/god-speed ~/.claude/skills/god-speed` |
| Codex CLI | `git clone https://github.com/rezzminator/god-speed ~/.agents/skills/god-speed` |
| OpenCode | either path above: OpenCode reads both |
| [Professor](https://github.com/rezzminator/professor) | `pfm install --yes` installs it for every account and engine |

<details>
<summary>One project only, update, remove</summary>

- One project: clone it into that project's `.claude/skills/god-speed` or `.agents/skills/god-speed` instead.
- Update: `git -C ~/.claude/skills/god-speed pull`, or the same command with the path you cloned to.
- Remove: delete that folder.

</details>

## Use it

End the prompt with the phrase, the way you would sign off a message:

```text
Migrate the settings page to the new form library, fix whatever breaks,
and get the test suite green.

God speed
```

`godspeed` and `god-speed` work too, in any capitalisation.

## What it decides for you

A fork is load-bearing when choosing wrong costs a rebuild, a revert or your trust. Where nothing you said, your project's rules or the code already settles one, the agent decides it and lists it first in the report, with how to flip it:

| Kind of fork | Example ruling |
| --- | --- |
| Something existing is replaced or dropped | Kept the old mechanism as a fallback behind a flag; delete the flag to remove it. |
| Where a new thing lives | Built it as its own plugin; folding it into the main app later is a file move. |
| A new dependency, service or account | Used the subscription you already have; the paid API is listed under what is left. |
| A contract others build on | Named the new config key `retryLimit` with a default of 3; rename it before anyone writes it. |
| A policy you never stated | Made the new check a warning, not a build gate; one line turns it into a gate. |
| A goal with two readings | Read "budget" as the price alone, and showed the all-in total beside it. |
| Your live machine, chats, browser, public name or money | Ran the benchmark in a sandbox, not on your live account. |

A fork that only shows up mid-run is decided the same way. Smaller calls, such as names or formatting, are made too and listed with their reasons. Committing, pushing, merging and releasing happen when your request asks for them: see [What it may do](#what-it-may-do).

## How the trigger works

The skill's `description` tells the agent to load it whenever your prompt says the phrase. The agent reads the skill's rules and follows them for that request. A prompt that only *talks about* the phrase, such as *"what does 'god speed' mean?"*, is answered normally.

Measured on 0.2.0, which still asked costly forks up front, and not re-measured on 0.3.0. On Claude Code 2.1.295 with Sonnet and Opus, the prompt above loaded the skill and asked nothing; the question about the phrase did not load it; a request that changed what an imported constant means asked that one question before the first edit, then ran to the end without another. On Codex CLI 0.161.0 the skill loaded, and Codex decided that same fork itself instead of asking, since its Default-mode instructions prefer assumptions over questions.

## What it may do

> [!IMPORTANT]
> God speed is your go-ahead for every action your request names or plainly entails: ask for a release and the agent cuts it, without asking again. It grants nothing beyond that. Your project rules, your permission mode and your agent's own safeguards still apply, and a tool call they deny is routed around, never argued.

If the task would need a destructive or outward-facing step you did not ask for, such as deleting data, force-pushing, publishing, sending a message, spending money, upgrading software or touching your other chats and live services, the agent skips that step without pausing. It finishes everything else and lists the skipped step under what is left in the final report.

## Help

Open an [issue](https://github.com/rezzminator/god-speed/issues). The most useful report is a prompt where the skill loaded when it should not have, or did not load when it should have, together with your agent, its version and the model.

## Contributing

Pull requests are welcome; read [CONTRIBUTING.md](CONTRIBUTING.md) first. Every line of `SKILL.md` is read on each invocation, so a change should alter the agent's behaviour, not only its wording. Newcomer-sized work is labelled [`good first issue`](https://github.com/rezzminator/god-speed/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22).

## License

[MIT](LICENSE). Built and maintained with [Professor](https://github.com/rezzminator/professor), the discipline layer for Claude Code.
