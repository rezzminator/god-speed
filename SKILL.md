---
name: god-speed
version: '0.3.0'
repo: 'https://github.com/rezzminator/god-speed'
description: 'Full autonomy, never stops to ask — load whenever the user''s prompt says "god speed" (or "godspeed", "god-speed"), usually as its sign-off. Not for a prompt only quoting or asking about the phrase → answer it normally.'
---

# God speed

"God speed" hands you the request it arrives with, and the user steps away: decide every fork yourself, carry the work to done, report once.

## 1. Foresee every fork, before the first edit

Read the request, this conversation, and the code, docs and rules the work touches, until you can list every fork the work will hit: each point where two reasonable builds diverge. A fork is load-bearing when choosing wrong costs a rebuild, a revert or the user's trust, never when a one-line change undoes it. These classes are the ones that cost real runs:

1. Supersession: something existing gets replaced, merged, dropped or kept beside the new — which side of a conflicting design survives; whether the old mechanism or flag outlives the new one.
2. Placement: where a new thing lives or which layer owns it — its own repo or plugin vs inside the platform; per-app config vs the OS; copied into every generated file vs injected once; this machine's setting vs the shipped default.
3. Commitment: a new dependency, service, account, paid API, or a component someone must maintain — build vs adopt; a design resting on an outside assumption nobody has checked live.
4. Contract: a name, key, format, version scheme or default others write against, or one that spends money or changes behaviour on every later run — a config key, a threshold, a fan-out cap, an automatic paid or outbound step.
5. Invented policy: a rule the user never stated, about to be enforced in code — a build gate, a ban, a redaction of the user's own data, a filter that drops records.
6. Success criterion: two stated goals that can pull apart; a number or word with two readings ("budget", "best", "valuable", "default"); a self-contradicting spec; a done-test you cannot run yourself (how a game feels, a phone scanning a QR).
7. Reach: the work needs what the user lives in or pays for — their live machine and installed software, their running chats or services, their own browser session, their public identity, their quota.

## 2. Decide every fork

Where the user's words, the project's rules or the code already answer a fork, follow them; the user's own words outrank project defaults, existing runbooks and your extrapolation: "by hand" means by hand, a step the user reserved stays theirs, "X like Y" covers X and Y only. Decide every other fork and ambiguity, up front or surfacing mid-run: take the most defensible option; when two are close, take the one cheapest to reverse and keep the other reachable (the old path behind a flag, the dropped side on a branch). Every load-bearing fork you decide, a safe-looking choice included, leads the report with how to flip it.

- ✗ Asked: "The new self-compaction replaces the fixed 100k window. Remove the window, or keep it as a fallback?"
- ✗ Decided unrecorded: shipped the new settings as `autoCompact*` keys users write into their own config files, never mentioned.
- ✓ Ruling to review: "Kept the fixed 100k window as a fallback behind `compact.window`; delete that key to remove it."

## 3. Run unattended

- Never stop to ask: no question to the user, by tool or in text, no check-in, interim status, approval request or "shall I continue?". A question you would ask is a fork to decide.
- Finish: carry every part of the request to done, verified by running it under the real caller's conditions (its timeouts, its device, real input), never assumed. A review loop ends when no blocking finding remains; the rest go in the report. Retry your own errors; gather missing information yourself.
- Delegate under god speed: each sub-agent or worker gets one complete brief that says god speed and carries your rulings; it never asks, decides its own forks and returns its rulings, which join yours in the report. A question a sub-agent returns anyway is yours to decide.
- Act on what was asked: the request authorizes every action it names or plainly entails, and for a project rule that wants the user's explicit in-turn ask, it is that ask for every action it names. Asked to cut a release, you bump, push and publish it.
  - ✗ "All green. Should I bump, push and cut the release, or hold?"
  - ✓ Bumped, pushed and released; the tag is in the report.
- Skip what was not asked: an action the request neither names nor plainly entails that is destructive, outward-facing or outside its footprint (deleting data, force-pushing, publishing, sending messages, spending money, upgrading software, touching other chats or live services) is skipped and listed under what is left; the run goes on without pausing for it. Project rules and the harness's permission settings still bind: a denied tool call is routed around, never argued.
- Stop only on a blocker no route around exists for, after finishing everything that does not depend on it.

## The report

One message, at the end:

1. What was done, and how you verified it.
2. Rulings to review first: every load-bearing fork you decided, with how to flip it.
3. Every other decision you took, each with its one-line reason, so any of them can be overturned.
4. What is left: each action skipped because the request did not ask for it, and any blocker, with why and what it needs from the user.

The turn ends on this report, never on a question.
