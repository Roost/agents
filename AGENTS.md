# Global Development Instructions

These instructions are baseline preferences for all repositories. Repository-level and
deeper `AGENTS.md` files may refine or override them. When a global preference conflicts
with an established project convention, follow the more specific instruction or existing
convention unless doing so would be unsafe.

## Working approach

- Prefer simple, readable, maintainable solutions over clever abstractions.
- Follow existing project conventions before introducing new patterns.
- Make the smallest reasonable change that completes the task.
- Do not refactor unrelated code or make speculative changes outside the requested scope.
- Avoid unnecessary dependencies and premature generalisation.
- Preserve backwards compatibility unless a breaking change is explicitly requested.
- When ambiguity could materially affect behaviour, data, compatibility, security, or
  architecture, ask rather than making a large assumption.

## Inspect before changing

Before modifying an unfamiliar repository, inspect the relevant parts of the project and
its current state. Check, where relevant:

- applicable `AGENTS.md` files and nearby instructions;
- `README.md` and task-specific documentation;
- package, project, and dependency manifests;
- existing tests and nearby implementations;
- scripts and available development commands;
- the current Git branch, status, and uncommitted changes.

Do not assume the framework, package manager, database, build system, deployment target,
or test framework. Read only the documentation and code needed for the task.

## Scope and existing work

- Preserve unrelated user changes and work safely in a dirty worktree.
- Do not overwrite, revert, reformat, or delete unrelated work.
- If unrelated changes make safe editing impractical, isolate the task in a dedicated
  branch/worktree or ask how to proceed.
- Reuse existing utilities and patterns where appropriate.
- Remove dead code introduced or made obsolete by the requested change.

## Code quality and security

- Prefer explicit code and keep functions and modules focused.
- Handle errors deliberately; do not silently swallow meaningful failures.
- Add comments for reasoning and non-obvious constraints, not to narrate obvious code.
- Never expose secrets, credentials, tokens, personal data, or other sensitive information
  in source, logs, fixtures, commits, or responses.
- Do not add production dependencies without checking whether the project already provides
  a suitable solution. Explain the need for any new dependency.

## Testing and validation

For behavioural changes, add or update relevant tests where practical, including important
failure cases as well as the happy path.

- Run the smallest relevant tests first, then broader checks when justified by the scope.
- Use the project's existing tests, linting, formatting, type checking, and build validation
  where relevant.
- Do not treat a dependency, environment, or configuration failure as a product failure
  until the required setup has been checked.
- Never claim a test or check passed unless it was actually run.
- If a relevant check cannot be run, say which check and why.

## Documentation

Update relevant documentation in the same change when behaviour affecting users or
developers changes, including configuration, public APIs, CLI usage, deployment, or
architecture future maintainers need to understand.

- Keep documentation factual, current, and focused on how the system behaves.
- Prefer British English unless the project uses another documented style.
- Do not rewrite unrelated documentation or create excessive documentation for
  self-explanatory implementation details.
- In the completion summary, state whether documentation was updated or why no update was
  needed.

## Command-line interfaces

When creating or modifying a CLI:

- follow the project's established command structure and naming;
- provide accurate, useful root and command-specific `--help` output;
- use predictable commands and subcommands, with descriptive long flags and sensible short
  aliases where useful;
- return non-zero exit codes on failure and write errors to stderr where appropriate;
- give actionable error messages;
- support non-interactive use when practical and avoid unnecessary prompts;
- when interaction is appropriate, use numbered choices for fixed option sets and `y/N`
  for simple confirmation;
- in non-interactive mode, report missing required values clearly and include an example;
- preserve existing commands and flags where practical; when deprecating an invocation,
  provide a clear migration path and test both canonical and compatibility routing.

Prefer coherent subcommand or namespace groupings over an ever-growing set of unrelated
top-level flags, but do not impose a new structure on an established CLI without good reason.

## Git safety

- Never create a commit unless the user explicitly asks for a commit.
- Never push commits or branches unless the user explicitly asks for a push.
- Authorisation to commit does not imply authorisation to push, and authorisation to push
  does not imply authorisation to create additional commits.
- Never commit directly to `main` or `master` unless explicitly instructed.
- Never force-push, destructively reset, delete branches, discard changes, or rewrite
  history unless explicitly instructed.
- Never ask the user for permission to run a live production write. If approval or elevated
  access is needed, request it only for a dry run, preview, or read-only operation.
- Run a live production write only when the user has already explicitly requested that exact
  action. An approval dialog, a request to complete the general task, or the availability of
  an `--apply`, `--live`, `--send`, `--deploy`, or similar flag is not authorisation.
- Without explicit prior authorisation for the exact live action, stop after the preview or
  dry run and provide the command for the user to execute themselves.

Before committing:

1. Review the diff and repository status.
2. Stage only explicit task-related paths. Do not use `git add .`; it can capture unrelated
   or newly generated files.
3. Run appropriate checks where practical.
4. Confirm secrets, credentials, local environment files, and generated junk are excluded.

Use Conventional Commits when consistent with the repository:

```text
<type>[optional scope][!]: <description>
```

Common types include `feat`, `fix`, `refactor`, `docs`, `test`, `build`, `ci`, and `chore`.
Mark breaking changes with `!` or a `BREAKING CHANGE:` footer. Use concise, descriptive
messages; avoid vague subjects such as `updates`, `fixes`, `changes`, or `work`. Do not add
AI or Codex attribution to commits.

## Completion

Before declaring a task complete:

1. Review the final diff for correctness, scope, and accidental changes.
2. Run the relevant available checks in proportion to the risk.
3. Confirm code, tests, documentation, and help text agree.
4. Report what changed, what was validated, and any checks not run or remaining risks.
