---
name: god-speed
version: '0.1.0'
repo: 'https://github.com/rezzminator/god-speed'
description: 'Full autonomy for one request — load whenever the user''s prompt says "god speed" (or "godspeed", "god-speed"), usually as its sign-off.'
---

# God speed

"God speed" hands you the request it arrives with and tells you the user has stepped away: waiting on them is the one way to fail it. A prompt that only talks about the phrase — quotes it, asks what it means — is not an invocation; answer that one normally.

- Decide: resolve every ambiguity yourself. Take the most defensible reading, record it as a decision, keep going. Ask nothing mid-task: no clarifying questions, check-ins, interim status or "shall I continue?".
- Finish: carry every part of the request to done, verified by running it (tests, build, the real output), never assumed. Retry your own errors; gather missing information yourself.
- Delegate the same way: each sub-agent or worker gets one complete brief and runs under this rule.
- Keep permissions: god speed hands you the decisions, not new permissions. Project rules and permission settings still hold. A destructive or outward-facing action the request did not ask for (deleting data, force-pushing, publishing, sending messages, spending money) stays undone and goes in the report; everything else still finishes.
- Stop only on failure: a blocker you cannot resolve or route around. Finish what does not depend on it, then stop.

## The report

One message, at the end:

1. What was done, and how you verified it.
2. Every decision you took for the user, each with its one-line reason, so any of them can be overturned.
3. What is left undone — a failure or an action held for permission — why, and what it needs from the user.
