# PK Skills

A local skill library for using coding agents to reduce AI-era technical debt.

The skills are organized around the main debt modes from `TECH-DEBT.md`:

- **Technical debt**: slow delivery, risky changes, and inefficient implementation loops.
- **Comprehension debt**: code and decisions that are hard for humans or agents to understand.
- **Intent debt**: work that ships something different from the product or business goal.
- **Verification debt**: changes that cannot be proven correct.
- **Artifact drift**: stale docs, generated files, specs, examples, or agent instructions.
- **Duplication**: parallel implementations that should converge on one source of truth.

## Skills

Each skill lives in its own directory with a `SKILL.md` file.

- `api-and-interface-design`: Stable APIs, contracts, and module boundaries.
- `architecture-map`: Concise codebase maps for modules, flows, ownership, and risk.
- `artifact-drift-control`: Detection and repair of stale or conflicting project artifacts.
- `browser-e2e-verification`: Browser workflow checks with E2E, accessibility, and visual proof.
- `ci-cd-and-automation`: Repeatable quality gates for build, test, lint, security, and releases.
- `code-review-and-quality`: Review workflow for correctness, maintainability, regressions, and agent failure modes.
- `code-simplification-and-deduplication`: Complexity reduction and convergence on shared implementations.
- `context-engineering`: Curated project context for higher-quality agent output.
- `debugging-and-error-recovery`: Structured root-cause debugging and recurrence prevention.
- `deprecation-and-migration`: Safe migrations for APIs, schemas, dependencies, and legacy paths.
- `documentation-and-adrs`: Decision records and project knowledge that preserve the "why".
- `duplication-detector`: Exact, structural, and conceptual duplicate detection.
- `idea-refine`: Structured ideation from vague ideas to scoped direction.
- `incremental-implementation`: Small, testable, rollback-friendly delivery slices.
- `issues`: Markdown-based local issue tracking for bugs and debt.
- `performance-optimization`: Measurement-first performance diagnosis and regression prevention.
- `security-and-hardening`: Security constraints for untrusted input, auth, data, and integrations.
- `spec-driven-development`: Specs, plans, tasks, and success criteria before implementation.
- `staleness-checker`: Review of docs and skills for broken paths, stale commands, and ownership gaps.
- `test-driven-verification`: Realistic tests and proof targets for generated or high-risk changes.

## Supporting Notes

- `TECH-DEBT.md`: presentation notes and technical-debt breakdown.
- `skills-for-technical-debt.md`: external skill research and mapping.
- `local-skill-coverage-review.md`: coverage review for the local skill set.
