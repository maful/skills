---
name: conventional-commits
description: Write or check commit messages and squash-merge titles against Conventional Commits 1.0.0, with release-please versioning in mind. Use when preparing a commit, proposing a commit message, or reviewing a release-relevant merge message.
---

# Conventional Commits 1.0.0

Use the [Conventional Commits 1.0.0 specification](https://www.conventionalcommits.org/en/v1.0.0/) as the authority for message syntax. Release Please reads the final Git commit history, so check the message that will land on the release branch, including a squash merge message when applicable. This skill does not authorize creating, amending, or merging a commit.

Read [Examples and Specification](references/conventional-commits-1.0.0.md) before writing or validating a message. Check the result against every applicable numbered rule there.

## Choose the message from the change

Inspect the actual change before selecting a type. Use `feat` for a new feature and `fix` for a bug fix. Other noun types are valid for other changes, such as `docs`, `test`, `refactor`, or `chore`; do not call a change `feat` or `fix` solely to force a release. Use lowercase `feat` and `fix` for reliable Release Please recognition, even though the specification does not require lowercase types. Add an optional scope only when it names a section of the codebase; put the scope in parentheses immediately after the type.

Mark a breaking change regardless of type. Put `!` immediately before the colon, or add a `BREAKING CHANGE: <description>` footer. Prefer the footer when the migration or impact needs explanation; both forms may be used together. A change is breaking when consumers must change how they use an existing interface, not merely because the implementation is large.

If the work contains independently meaningful changes of different types, prefer separate commits when that is within the user's requested workflow. When asked for one message, describe its primary change accurately and call out any breaking change; do not pretend one prefix fully represents several unrelated changes.

## Check the syntax

```text
<type>[optional scope][!]: <short description>

[optional body]

[optional footer(s)]
```

The reference spells out the required separators, body and footer placement, case handling, and all supported breaking-change forms. Preserve that syntax exactly when composing a message for Release Please.

## Check release impact

Under Release Please's default versioning strategy, `fix` indicates a patch, `feat` a minor release, and a breaking change a major release. Repository configuration, release type, and pre-1.0 settings can change the actual bump; inspect those before promising a version number. Other types have no *implicit* SemVer effect in the Conventional Commits specification, but Release Please may handle them according to its configuration. When checking a PR, verify the final squash or merge commit message rather than assuming the PR title is what Release Please will parse.

When proposing or reviewing a message, return the exact message and briefly identify any syntax or classification issue that needs correction. If the change or release configuration is unavailable, state the uncertainty instead of inventing a type or exact version bump.
