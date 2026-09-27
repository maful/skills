# Examples and Specification

This is an agent-facing restatement of [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/). The examples use original change descriptions. Treat **MUST** as required and **MAY** as optional, following the specification's RFC 2119 terminology.

## Examples

Each block is one complete commit message.

### Description and breaking-change footer

```text
feat(config): support inherited settings

BREAKING CHANGE: configuration now uses `extends` instead of `inherits`.
```

### Breaking change marked with `!`

```text
feat!: require email confirmation before checkout
```

### Scope and breaking-change marker

```text
feat(auth)!: require tokens on previously public endpoints
```

### Both breaking-change forms

```text
fix(cache)!: remove the legacy cache key format

BREAKING CHANGE: clients must generate cache keys with the new prefix.
```

### Description without a body

```text
docs: correct the installation command
```

### Scoped, nonbreaking change

```text
feat(locale): add Indonesian translations
```

### Multiple body paragraphs and footers

```text
fix(requests): ignore stale responses

Track the newest request ID and discard responses from earlier requests.

Remove the timeout workaround because request ordering is now explicit.

Reviewed-by: Ana
Refs #204
```

## Specification

1. Every commit **MUST** start with a noun type, optionally followed by a scope and `!`, then a colon and a space.
2. Use `feat` when the commit adds a feature to the application or library.
3. Use `fix` when the commit fixes a bug in the application or library.
4. A scope **MAY** follow the type. If present, it **MUST** be a noun naming a codebase section inside parentheses, such as `fix(parser):`.
5. The short description **MUST** begin immediately after the colon and space and summarize the change.
6. A body **MAY** follow the description. If present, it **MUST** begin after one blank line.
7. The body is free-form and **MAY** contain multiple paragraphs.
8. One or more footers **MAY** follow the body, separated from it by one blank line. If there is no body, separate the footers from the description with a blank line.
9. Each footer **MUST** start with a word token, then either `: ` or ` #`, then a value.
10. Replace whitespace inside ordinary footer tokens with hyphens, as in `Reviewed-by`. `BREAKING CHANGE` is the exception.
11. A footer value **MAY** contain spaces or newlines. It ends when the next valid footer token and separator begin.
12. A breaking change **MUST** be marked in the header with `!` or in a footer.
13. A breaking-change footer **MUST** use uppercase `BREAKING CHANGE: ` followed by a description.
14. A header marking a breaking change **MUST** put `!` immediately before the colon. With this form, the footer **MAY** be omitted, and the short description explains the break.
15. Types besides `feat` and `fix` **MAY** be used; the specification does not assign them an automatic SemVer effect.
16. Implementations **MUST** treat structural elements without case sensitivity, except that the `BREAKING CHANGE` token **MUST** be uppercase. For Release Please, write lowercase `feat` and `fix` regardless.
17. A footer token spelled `BREAKING-CHANGE` **MUST** be treated as equivalent to `BREAKING CHANGE`. Prefer the space form when writing a new message.
