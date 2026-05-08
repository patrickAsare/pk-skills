# Agents and Technical Debt

- Process and automation in AI-assisted software engineering
- Adoption is solved; maturity is the question
- The system around agents needs to preserve quality, accountability, and maintainability

Agents can increase short-term velocity while also increasing technical debt. More code, more pull requests, and faster iteration are not automatically productivity gains if quality, intent, verification, and governance do not keep pace.

Reference: <https://monitornerds.com/reviews/peter-steinberger-setup-tour-2026>

## Types of Debt Accelerated by Agents

### Technical Debt

Classic slow, inefficient delivery.

Examples:

- Every task becomes slower.
- More context, more edits, more cost.
- Big changes create big risk.

### Comprehension Debt

The team no longer understands what changed or why.

Examples:

- Hard-to-understand code.
- Too much complexity.
- No accountability.

### Intent Debt

The system ships something different from the business or product intent.

Examples:

Shipping the wrong thing.
No continuous learning for skills, docs, and automation.
Missing feedback loops from the business.

### Verification Debt

The team cannot prove the generated work is correct.

Examples:

Incorrect or insufficient testing.
End-to-end tests matter more than integration tests, which matter more than unit tests.
Test provenance must be tracked.
Tests need to be realistic, not just numerous.
Coverage alone is less important than logs and proof of behavior.

### Artifact Drift

The agent works from stale or inconsistent knowledge.

Examples:

Stale or inconsistent data.
Conflicting data or documentation.
Agent follows out-of-date guidance.
Documentation becomes unreliable.

### Duplication

The agent creates parallel implementations instead of converging on one source of truth.

Examples:

No single source of truth.
Multiple code paths or types do the same thing.
Same bugs show up many times.

## Reducing Technical Debt

### Failure Modes

Eight pillars; each "without it" describes the agent failure mode.

| Pillar | What | Without it |
| --- | --- | --- |
| **Style and Validation** | Linters, type checkers, formatters | Agent submits code with formatting issues, waits for CI, fixes blindly, repeats |
| **Build System** | Clean, documented build commands | Agent tries the wrong command, gets cryptic errors, cannot proceed |
| **Testing and Verification** | Integration and end-to-end tests; clarify where unit tests still add value | Agent cannot verify changes, submits untested code, breaks main |
| **Documentation** | `AGENTS.md`, READMEs, skills | Agent lacks context, makes incorrect assumptions, produces unusable code |
| **Dev Environment** | Reproducible setups | Agent hits environment-specific failures humans never see |
| **Code Quality** | Modular code, reasonable file sizes | Agent cannot fit relevant code in context, loses track of dependencies |
| **Observability** | Structured logging, tracing, metrics | Agent sees "error" with no context, cannot diagnose or fix |
| **Security and Governance** | Branch protection, secret scanning, `CODEOWNERS` | Agent commits secrets, bypasses review, introduces vulnerabilities |

## Code Quality

Six complementary practices:

- **Spec-Driven Development**: Clear specs reduce unstated assumptions and catch quality issues early.
- **Enforce Consistency**: One way to write code, one way to organize files, and a single source of truth.
- **Code Health Metrics**: Measure complexity, warnings, churn, duplication, and test coverage. There is no perfect single metric.
- **Frequent Refactoring**: Use automations to proactively address the biggest quality issues. Include compliance and internal tooling.
- **Lint and Static Analysis**: Deterministic analysis complements probabilistic review.
- **Preserve Comprehension**: Every action emits metrics, traces, and logs. Route them to SIEM, Splunk, or Datadog.

> No silver bullet. Code quality is a multi-dimensional, continuous investment.

## Skill Breakdown

- **idea-refine**: Turns vague ideas into focused problem statements, assumptions, MVP scope, and explicit non-goals.
- **spec-driven-development**: Converts unclear work into a reviewed spec, plan, task list, and success criteria before coding.
- **context-engineering**: Curates the right project rules, docs, files, and errors so agents work from relevant context.
- **issues**: Tracks bugs and debt as local Markdown issues with status, evidence, attachments, and resolution history.
- **architecture-map**: Builds a concise map of modules, dependencies, flows, ownership, and known risks.
- **documentation-and-adrs**: Captures decisions, project knowledge, and agent-facing guidance so the "why" is preserved.
- **artifact-drift-control**: Finds stale docs, specs, generated files, agent instructions, and competing sources of truth.
- **staleness-checker**: Reviews docs and skills for old commands, broken paths, missing owners, and overdue review dates.
- **api-and-interface-design**: Designs stable contracts and module boundaries that reduce misuse, drift, and duplicate integrations.
- **incremental-implementation**: Breaks large changes into small, testable, rollback-friendly slices.
- **deprecation-and-migration**: Moves APIs, schemas, dependencies, and legacy paths safely with compatibility and rollback plans.
- **code-review-and-quality**: Reviews diffs for correctness, maintainability, regressions, duplication, and agent-specific failure modes.
- **code-simplification-and-deduplication**: Removes unnecessary complexity and converges parallel implementations into one source of truth.
- **duplication-detector**: Detects exact, structural, and conceptual duplication before it becomes persistent debt.
- **test-driven-verification**: Defines realistic tests and proof targets so generated work can be trusted.
- **browser-e2e-verification**: Proves browser workflows with end-to-end, visual, accessibility, and interaction checks.
- **debugging-and-error-recovery**: Uses systematic triage to reproduce, localize, fix, and guard against recurring failures.
- **ci-cd-and-automation**: Turns build, test, lint, security, and generated-artifact checks into repeatable merge gates.
- **performance-optimization**: Measures bottlenecks before optimizing and guards against performance regressions.
- **security-and-hardening**: Applies security constraints for untrusted input, auth, data handling, and external integrations.

## Questions

- Where would agents currently fail in our codebase: build, tests, docs, environment, observability, or governance?
- Are we measuring generated volume or verified outcomes?
- Which forms of debt are invisible in our current dashboards?
- Do our tests prove realistic behavior or just increase coverage numbers?
- Who is accountable when AI-generated code introduces a defect?
- What policies do we need for AI-generated code provenance and disclosure?
