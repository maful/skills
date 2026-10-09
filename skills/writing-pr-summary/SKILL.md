---
name: writing-pr-summary
description: Draft a PR summary — a 2–3 sentence paragraph saying what the PR delivers and why, outcome first, for the top of a PR description or a team update.
disable-model-invocation: true
---

A PR summary is the pitch: the paragraph a teammate reads first to know what the PR delivers and why it exists. "What changed" lists the changes; the summary tells the story they add up to.

## Steps

1. **Find the outcome.** Read the PR title, branch name, linked tickets or issues, and commit messages.

   Done when you can say in one sentence what someone can do, or stops suffering from, once this merges.

2. **Read the full diff**: `git diff <base>...HEAD` or `gh pr diff <n>`, every file.

   Done when the diff sorts into the outcome's main parts (usually two or three) plus one bucket of hardening and edge-case fixes.

3. **Write the paragraph.**
   - Sentence 1: the outcome, naming the feature area and the result a user or merchant sees.
   - Sentence 2: the parts that make it work, ticket IDs in parentheses.
   - Sentence 3, when there is hardening: what can no longer go wrong, as one list of clauses.

   Done when it is 2–3 sentences, roughly 80 words or fewer, and a reader outside the team understands the result without opening the diff.

## Openings

Pick the opening that puts this PR's outcome up front; vary it from PR to PR.

- Subject first: "This PR adds magic-link sign-in…"
- Outcome first: "Exports of more than 10,000 rows now finish in the background…"
- Problem, then fix: "Webhook retries could deliver the same event twice; this…"
- Capability: "Admins can now invite teammates with a role already set…"
- Before and after: "Search used to return only exact matches; now it…"

## Examples

> This PR adds magic-link sign-in, so users can log in from an emailed link instead of a password (AUTH-112). It issues single-use links that expire after 15 minutes, and adds a rate limit per email address (AUTH-118). Existing password logins are unchanged, and an expired or reused link shows a clear error rather than a blank page.

> Exports of more than 10,000 rows now run in the background and arrive as an emailed download link, instead of timing out in the browser (DATA-43). A queued job builds the CSV in chunks and stores it for 7 days. Small exports still download right away.

> Webhook retries could deliver the same event twice when a receiver answered slowly. This PR gives every delivery an idempotency key and drops repeats on our side (HOOK-9), so receivers see each event once. It also stops retrying after 24 hours and marks the endpoint unhealthy, so failures are visible in the dashboard.

## Voice

- Outcome language: what works, for whom. Name the feature area and the surface a reader knows (an endpoint, a screen, a status code); class and method names belong to "What changed".
- Concrete over general: "drops duplicate webhook deliveries" beats "improves reliability".
- One plain paragraph, ticket IDs in parentheses.

## Output

The paragraph alone, with nothing before or after it.
