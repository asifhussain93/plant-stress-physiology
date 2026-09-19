# taskbot Benchmark Pipeline

> A repository scaffold for authoring original, repository-scale software-engineering benchmark tasks.

## Purpose

This repository organizes a taskbot-style workflow for turning **new, unmerged feature ideas** from curated open-source repositories into self-contained benchmark tasks. Each task should use natural developer-facing instructions and a functional verifier that accepts correct alternative implementations.

This is a **scaffold and documentation repository**. It does not implement the taskbot CLI, GitHub integration, agent judges, or verifier gates yet. It provides the project structure needed to build those components safely and consistently.

## Core principles

- Original tasks: never-merged feature work, not harvested historical fixes.
- Natural instructions: describe desired observable behavior without revealing the reference implementation.
- Functional verification: test public behavior rather than internal implementation details.
- Difficulty evidence: reject tasks that a frontier agent solves in one turn; retain a minimal, recorded hint ladder for accepted tasks.
- Verifier robustness: verify the baseline, reference solution, regression behavior, stub rejection, alternative correct patches, and repeatability.

## Repository layout

```text
.
├── .taskbot/                 # Repository-level configuration
├── .github/                  # Issue templates and CI workflow stubs
├── backend/                  # Future API/service implementation
├── frontend/                 # Future TypeScript dashboard implementation
├── docs/                     # Workflow and authoring guidance
├── lib/                      # Shared taskbot domain logic
├── release-notes/            # Versioned release notes
├── templates/task/           # Canonical task-directory scaffold
├── tasks/                    # One directory per benchmark task
├── tests/e2e/                # End-to-end workflow tests
├── scripts/                  # Local helper scripts
├── CONTRIBUTING.md
└── README.md
```

## Task lifecycle

```text
NEW → REPO_READY → DRAFT → SCOPED → SPEC_ALIGNED → TESTS_DRAFTED → REVIEWED → PUBLISHED
```

The intended commands are `/bootstrap`, `/init`, `/scope`, `/verify-spec`, `/gen-tests`, `/review`, `/analyse`, and `/submit`. See [the workflow guide](docs/workflow.md) for what each stage must accomplish.

## Create your first task

1. Choose an active open-source repository and identify a genuine unmerged feature.
2. Copy `templates/task/` to `tasks/<task-id>/`.
3. Fill in `task.toml` and write the solver-visible `instruction.md`.
4. Run the scope review before developing the hidden solution and verifier.
5. Record the least-to-most-specific hints in `hint.md` after genuine agent attempts.
6. Add a reproducible environment, verifier, reference patch, and alternative correct patches.
7. Run the full gate battery and benchmark/failure analysis before publishing.

## Important author rule

During task authoring, the solver should receive **only** the task instruction. Do not pass hidden solutions, patches, tests, or unrelated task artifacts to the solver.

## Status

The repository includes a small working Python task-state model and a TypeScript frontend starter. The next engineering work is to implement the command runner, blind test-generation isolation, nine verifier gates, and benchmark-result storage.

## License

MIT. See [LICENSE](LICENSE).
