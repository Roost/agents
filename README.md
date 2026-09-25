# Global Codex instructions

This repository is the source of truth for personal, reusable Codex development
instructions. Its root [`AGENTS.md`](AGENTS.md) is intended to be installed at
`~/.codex/AGENTS.md`.

Project repositories should keep their own `AGENTS.md` files focused on information that is
specific to that project: its stack, verified commands, architecture, domain invariants,
deployment constraints, unusual conventions, and pointers to relevant documentation.

## Instruction hierarchy

Codex assembles instructions from broadest to most specific:

```text
~/.codex/AGENTS.md
  -> <repository>/AGENTS.md
    -> <repository>/<subsystem>/AGENTS.md
```

Files closer to the working directory appear later in the instruction chain and therefore
override broader guidance when they conflict. `AGENTS.override.md` can replace `AGENTS.md`
at the same level and should be reserved for intentional overrides.

Codex reads this chain when a run or TUI session starts. Restart Codex after changing an
instruction file.

## Install

From this repository, link the tracked file into the default Codex home:

```bash
mkdir -p ~/.codex
ln -sfn "$(pwd)/AGENTS.md" ~/.codex/AGENTS.md
```

Review differences before replacing an existing global file:

```bash
diff -u ~/.codex/AGENTS.md AGENTS.md
```

If `CODEX_HOME` is set, install `AGENTS.md` there instead of `~/.codex`.
The symbolic link keeps the global instructions in sync whenever the tracked repository
file changes.

## Verify

Start a new Codex session from a project repository and ask it to list or summarise its
active instruction sources. A repository with nested guidance should resolve in this order:

1. the global Codex home file;
2. the repository-root file;
3. any applicable files between the repository root and current working directory.

Keep the global file concise. Detailed project knowledge belongs in the relevant repository
or dedicated project documentation.
