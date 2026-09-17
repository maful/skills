---
name: writing-what-changed
description: Draft the "What changed" section of a PR description — a terse, human bullet list of what was added, changed, or removed, grounded in the diff and its context.
disable-model-invocation: true
---

A "What changed" section is read by a teammate who will act on it in seconds — approve, ask a question, or jump to a file. It is not a summary of the diff's shape; it is the diff's meaning, one bullet per change.

## Steps

1. **Understand why the change exists** before reading a line of diff. Check the PR title, branch name, linked ticket, and prior commits on the branch for the motivation.

   Done when you can say in one sentence what problem this PR solves, not just what files it touches.

2. **Read the full diff**, file by file, every hunk — `git diff <base>...HEAD` or `gh pr diff <n>`, not just the first screen. A renamed variable and a new code path both show up as `+` lines; only one belongs in the output.

   Done when every changed file's behavior is accounted for: folded into a bullet, or deliberately left out as noise (formatting, renames, generated files, lockfiles).

3. **Group into distinct changes, not files.** One change often touches several files (a new option, the service behind it, its wiring) — that's one bullet, not three. Two unrelated fixes riding the same PR are two bullets, never merged into one "and."

   Done when each bullet answers one "why did we need this?", and no two bullets restate the same change from different files.

4. **Write each bullet**: verb first, present tense (`adds`, `removes`, `changes`, `renames`, `verifies`), naming the concrete thing — a class, flag, endpoint, option — never a vague area. Add a clause after a comma only when the reader needs the *why* or *when* to place the change; drop it when the verb and noun already say everything.

   Done when every bullet reads like a teammate describing their own work, not a system narrating a diff — see Voice.

## Voice

Written by the person who made the change, for the person reviewing or building on it.

- **Lead with the verb, end with the point.** "adds `RetryQueue`, which replays a failed job after its backoff window" — not "a new class was added to handle retries."
- **Name real things.** Classes, flags, endpoints, option names — exact, backtick-quoted. A bullet that could describe any PR ("improves reliability") says nothing.
- **One line, no sub-bullets.** A change that needs a sub-list to explain is two bullets, or it's over-explained — cut to the part a reviewer acts on.
- **No filler between verb and noun.** Delete "this PR", "in order to", "additionally", "it's worth noting."
- **Skip what isn't a behavior change** — formatting, renamed locals, comment tweaks — unless the PR is only that.

## Output

```
## What changed

- <verb> <thing>[, <why/when only if not obvious>]
- <verb> <thing>
```

Nothing before or after the list. One change, one bullet.
