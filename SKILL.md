---
name: god-speed
version: '0.2.0'
repo: 'https://github.com/rezzminator/god-speed'
description: 'Autonomy, big forks asked first — load whenever the user''s prompt says "god speed" (or "godspeed", "god-speed"), usually as its sign-off.'
---

# God speed

"God speed" hands you the request it arrives with: the user answers one round of questions, then steps away, and waiting on them after that is the one way to fail it. A prompt that only talks about the phrase — quotes it, asks what it means — is not an invocation; answer that one normally.

## 1. Foresee every fork, before the first edit

Read the request, this conversation, and the code, docs and rules the work touches, until you can list every fork the work will hit: each point where two reasonable builds diverge. A fork is load-bearing when choosing wrong costs a rebuild, a revert or the user's trust, never when a one-line change undoes it. These classes are the ones that cost real runs:

1. Supersession: something existing gets replaced, merged, dropped or kept beside the new — which side of a conflicting design survives; whether the old mechanism or flag outlives the new one.
2. Placement: where a new thing lives or which layer owns it — its own repo or plugin vs inside the platform; per-app config vs the OS; copied into every generated file vs injected once; this machine's setting vs the shipped default.
3. Commitment: a new dependency, service, account, paid API, or a component someone must maintain — build vs adopt; a design resting on an outside assumption nobody has checked live.
4. Contract: a name, key, format, version scheme or default others write against, or one that spends money or changes behaviour on every later run — a config key, a threshold, a fan-out cap, an automatic paid or outbound step.
5. Invented policy: a rule the user never stated, about to be enforced in code — a build gate, a ban, a redaction of the user's own data, a filter that drops records.
6. Success criterion: two stated goals that can pull apart; a number or word with two readings ("budget", "best", "valuable", "default"); a self-contradicting spec; a done-test you cannot run yourself (how a game feels, a phone scanning a QR).
7. Reach: the work needs what the user lives in or pays for — their live machine and installed software, their running chats or services, their own browser session, their public identity, their quota.

Every load-bearing fork goes to the user unless the user's words, the project's rules or the code already chose its answer. An option that only looks safest — backward compatible, conservative, easy to flip later — settles nothing: ask it anyway.

Never ask about commit, push, merge, release or a version bump (§ 3 Keep permissions settles them), names, formatting or file layout, anything the request already authorised or the user already answered, an edge case of a feature the user does not use, or a menu re-offering an agreed plan.

- ✗ Asked: "Should I push when it's green?" · "Name it `cache-ttl` or `ttl`?"
- ✗ Decided alone, listed for review: "Shipped the new settings as `autoCompact*` keys, which users write into their own config files."
- ✓ Asked first: "The new self-compaction replaces the fixed 100k window. Remove the window, or keep it as a fallback?"

## 2. Ask once

Ask every such fork in one round before the first edit: the harness's question tool where it has one, otherwise one numbered message ending the turn. Four questions at most — past four, ask the four costliest to reverse and decide the rest. Each question carries its own context in plain words, 2–4 options, your recommendation first. No fork qualifies: ask nothing and start.

A load-bearing fork that only surfaces mid-run is decided, not asked: take the option cheapest to reverse and keep the other reachable (the old path behind a flag, the dropped side on a branch).

## 3. Run unattended

- Decide: the user's own words outrank project defaults, existing runbooks and your extrapolation — "by hand" means by hand, a step the user reserved stays theirs, "X like Y" covers X and Y only. Every other ambiguity: take the most defensible reading, record it, keep going. No clarifying questions, check-ins, interim status or "shall I continue?".
- Finish: carry every part of the request to done, verified by running it under the real caller's conditions (its timeouts, its device, real input), never assumed. A review loop ends when no blocking finding remains; the rest go in the report. Retry your own errors; gather missing information yourself.
- Delegate the same way: each sub-agent or worker gets one complete brief carrying the user's answers, never asks the user, and returns any load-bearing fork it decided.
- Keep permissions: god speed hands you the decisions, not new permissions; project rules and permission settings still hold. An action the request did not ask for that is destructive, outward-facing or outside its footprint (deleting data, force-pushing, publishing, sending messages, spending money, upgrading software, touching other chats or live services) stays undone and goes in the report; everything else still finishes.
- Stop only on failure: a blocker you cannot resolve or route around. Finish what does not depend on it, then stop.

## The report

One message, at the end:

1. What was done, and how you verified it.
2. Rulings to review first: every load-bearing fork you decided yourself — past the four asked, or surfaced mid-run — with how to flip it; forks the user answered are not repeated here.
3. Every other decision you took, each with its one-line reason, so any of them can be overturned.
4. What is left undone — a failure or an action held for permission — why, and what it needs from the user.
