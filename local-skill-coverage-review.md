# Local Skill Coverage Review

Date: 2026-05-08

This review maps the local skills in this workspace to the six technical-debt categories from `presentation.md`.

## Current Local Skills

| Skill | Primary coverage |
| --- | --- |
| `idea-refine` | Intent debt, early product clarity |
| `spec-driven-development` | Intent debt, verification setup |
| `context-engineering` | Comprehension debt, artifact drift |
| `api-and-interface-design` | Intent debt, duplication, technical debt |
| `incremental-implementation` | Technical debt, big-change risk |
| `debugging-and-error-recovery` | Verification debt, incident learning |
| `performance-optimization` | Technical debt, quality regression control |
| `security-and-hardening` | Verification debt, governance |
| `code-review-and-quality` | Comprehension debt, verification debt, duplication |
| `test-driven-verification` | Verification debt |
| `documentation-and-adrs` | Comprehension debt, artifact drift |
| `artifact-drift-control` | Artifact drift |
| `code-simplification-and-deduplication` | Duplication, technical debt, comprehension debt |
| `ci-cd-and-automation` | Verification debt, artifact drift, governance |
| `browser-e2e-verification` | Verification debt, UI confidence |
| `deprecation-and-migration` | Technical debt, artifact drift, big-change risk |
| `architecture-map` | Comprehension debt |
| `staleness-checker` | Artifact drift |
| `duplication-detector` | Duplication |

## Debt Coverage

### Technical Debt

Covered by:

- `incremental-implementation`
- `performance-optimization`
- `code-simplification-and-deduplication`
- `ci-cd-and-automation`
- `deprecation-and-migration`

Remaining risk:

- Tool-specific automation is intentionally lightweight. Add repo-specific scripts when a pilot codebase is selected.

### Comprehension Debt

Covered by:

- `context-engineering`
- `documentation-and-adrs`
- `code-review-and-quality`
- `code-simplification-and-deduplication`
- `architecture-map`

Remaining risk:

- Diagram generation is procedural, not tool-backed. Add Mermaid or dependency-graph scripts if needed.

### Intent Debt

Covered by:

- `idea-refine`
- `spec-driven-development`
- `api-and-interface-design`

Remaining risk:

- No dedicated product-feedback or issue-triage skill. Add one if work frequently ships without business validation.

### Verification Debt

Covered by:

- `test-driven-verification`
- `debugging-and-error-recovery`
- `code-review-and-quality`
- `security-and-hardening`
- `ci-cd-and-automation`
- `browser-e2e-verification`

Remaining risk:

- Browser verification is framework-neutral. Add Playwright project templates per stack when needed.

### Artifact Drift

Covered by:

- `artifact-drift-control`
- `documentation-and-adrs`
- `context-engineering`
- `ci-cd-and-automation`
- `staleness-checker`
- `deprecation-and-migration`

Remaining risk:

- Staleness checks are skill-guided. Add automation once the desired metadata format is adopted.

### Duplication

Covered by:

- `code-simplification-and-deduplication`
- `api-and-interface-design`
- `code-review-and-quality`
- `duplication-detector`

Remaining risk:

- Clone detection is skill-guided. Add `jscpd` or language-specific tooling if duplication should block CI.

## Recommended Next Additions

The local set is now broad enough for a presentation demo and practical use. The next useful work is not more generic skills; it is repo-specific automation:

1. Add stack-specific Playwright templates once a pilot app is chosen.
2. Add a `jscpd` or language-specific clone-detection command if duplication should block CI.
3. Add a staleness-check script after adopting `Last reviewed`, `Owner`, and `Source of truth` metadata.
4. Add architecture-map templates for the real repositories used in the talk.
