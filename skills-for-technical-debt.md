# Skills for Combating AI-Era Technical Debt

Companion to [agents-and-technical-debt-talk-notes.md](agents-and-technical-debt-talk-notes.md). Maps the six debt categories from the talk to popular agent skills (Claude Code / Codex / Cursor / Gemini CLI / Antigravity compatible — `SKILL.md` open standard, released Dec 2025).

> **Ecosystem context.** Anthropic introduced the SKILL.md format in Oct 2025 and made it an open standard in Dec 2025. As of May 2026 there are 1,000+ curated skills across registries. **Caution:** an April 2026 Snyk study found **36.8% of 3,984 scanned skills carry at least one security issue and 13.4% contain critical-level flaws** — vet skills before adoption (especially anything that ships its own MCP server).

---

## Skill Registries (start here)

| Registry | Scope | Stars / Notes |
|---|---|---|
| [anthropics/skills](https://github.com/anthropics/skills) | Official Anthropic reference skills (testing, MCP gen, document creation) | Authoritative baseline |
| [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills) | 1,000+ official-team skills (Anthropic, Vercel, Stripe, Cloudflare, Trail of Bits, Sentry, Figma…) | Curated, official-team focus |
| [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills) | 232+ skills/plugins, multi-agent | ~5.2k★ |
| [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) | 1,000+ production skills | Cross-agent |
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | Production-grade engineering skills | 20 core skills incl. /simplify, code-review |
| [trailofbits/skills](https://github.com/trailofbits/skills) | Security research / vuln detection / audit | High-trust source |
| [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills) | Curated list, Claude Code focus | Community |

GitHub CLI added native skill management in **April 2026** (`gh skill ...`) — useful for org-level rollout.

---

## 1. Technical Debt — *slow delivery, big-change risk*

**Goal:** keep the agent fast and the cost-per-task low; shrink blast radius.

| Skill | Source | What it does |
|---|---|---|
| **tech-debt-skill** | [ksimback/tech-debt-skill](https://github.com/ksimback/tech-debt-skill) | Produces file-cited `TECH_DEBT_AUDIT.md` with severity, effort estimates, ranked fix list |
| **/simplify** | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | Spawns 3 parallel sub-agents (reuse / quality / efficiency) to turn first-draft into second-draft code. Announced Feb 2026 |
| **refactoring-expert** | [VoltAgent/awesome-claude-code-subagents](https://github.com/VoltAgent/awesome-claude-code-subagents) | Smell-driven, test-guarded, named refactoring transformations |
| **levnikolaevich/claude-code-skills** | [repo](https://github.com/levnikolaevich/claude-code-skills) | Full-lifecycle plugin suite: codebase audits, perf optimization, hex-graph (code knowledge graph) MCP |
| **Codebase Audit (DRY/KISS/YAGNI, dead code, coupling cycles)** | bundled in addyosmani + levnikolaevich | Targets AI-induced bloat that ESLint/SonarQube miss |

**Pre-skill hygiene:** also run [fewer-permission-prompts](https://github.com/anthropics/skills) (this CLI's built-in skill) — fewer interruptions = fewer half-context retries.

---

## 2. Comprehension Debt — *no one understands the code or the change*

**Goal:** restore mental model on demand; preserve "why" alongside "what".

| Skill | Source | What it does |
|---|---|---|
| **Codebase Architecture Explainer** | [findskill.ai listing](https://findskill.ai/skills/claude-code/codebase-architecture-explainer/) | Architecture diagrams, dependency maps, pattern analysis, onboarding docs |
| **hex-graph (knowledge graph MCP)** | [levnikolaevich/claude-code-skills](https://github.com/levnikolaevich/claude-code-skills) | Code knowledge graph the agent queries instead of re-reading files |
| **Visual Explainer** | [battlecat.ai writeup](https://www.battlecat.ai/tutorials/visual-explainer-agent-skill-terminal-output-html) | Converts terminal/agent output to shareable HTML with diagrams, dark mode |
| **code-reviewer (subagent)** | [VoltAgent/awesome-claude-code-subagents](https://github.com/VoltAgent/awesome-claude-code-subagents/blob/main/categories/04-quality-security/code-reviewer.md) | Forces "explain this PR" pass before merge |
| **init / generate AGENTS.md skills** | [anthropics/skills](https://github.com/anthropics/skills), built-in `/init` | Bootstrap and maintain the agent-readable architecture brief |

> Pair with the talk's principle: *AI writes, humans sign* — explainer skills feed the human-review side.

---

## 3. Intent Debt — *shipping the wrong thing*

**Goal:** make the spec the executable artifact; close the loop with the business.

| Skill | Source | What it does |
|---|---|---|
| **cc-sdd** | [gotalab/cc-sdd](https://github.com/gotalab/cc-sdd) | Minimal SDD harness — turn approved specs into long-running autonomous implementation. Multi-agent (Claude/Codex/Cursor/Copilot/Windsurf/OpenCode/Gemini/Antigravity) |
| **sdd-skill** | [SpillwaveSolutions/sdd-skill](https://github.com/SpillwaveSolutions/sdd-skill) | Guided walkthrough of GitHub's Spec-Kit + spec-driven methodology |
| **CCPM (Claude Code PM)** | [skills.pawgrammer.com/skills/ccpm](https://skills.pawgrammer.com/skills/ccpm) | Idea → PRD → epic → GitHub issues → code, with full traceability |
| **prd-taskmaster** | [anombyte93/prd-taskmaster](https://github.com/anombyte93/prd-taskmaster) | AI-powered PRD generation with taskmaster integration |
| **Spec Writing / Technical PRD** | [mcpmarket listing](https://mcpmarket.com/tools/skills/technical-specification-writer-1) | Templated PRD authoring, research → clarification → sequencing → delivery |

**Gap to flag in the talk:** automatic spec-to-implementation verification is still weak across all platforms — humans remain in the loop here.

---

## 4. Verification Debt — *can't prove the work is correct*

**Goal:** invert the cost — verification cheaper than re-reading the diff. Talk's hierarchy: **E2E > Integration > Unit**.

| Skill | Source | What it does |
|---|---|---|
| **Playwright Agents (planner / generator / healer)** | [shipped with Playwright](https://shipyard.build/blog/playwright-agents-claude-code/), [TestDino guide](https://testdino.com/blog/claude-code-with-playwright) | 4-agent pipeline: explore app → write plan → generate tests → self-heal failures |
| **playwright-skill** | [lackeyjb/playwright-skill](https://github.com/lackeyjb/playwright-skill) | Model-invoked browser automation; agent autonomously writes & runs tests |
| **playwright-cli-agents** | [yusuftayman/playwright-cli-agents](https://github.com/yusuftayman/playwright-cli-agents) | E2E generation, debugging, planning using POM |
| **qa-skills** | [neonwatty/qa-skills](https://github.com/neonwatty/qa-skills) | 6 specialized QA agents — multi-user flows, mobile audits |
| **agentmantis/test-skills** | [repo](https://github.com/agentmantis/test-skills) | Cross-agent (Claude/Codex/Cursor/Antigravity) Playwright skills |
| **testing-specialist** | [VoltAgent subagents](https://github.com/VoltAgent/awesome-claude-code-subagents) | TDD/BDD strategy, coverage planning |
| **security-review** | built-in CLI skill, [trailofbits/skills](https://github.com/trailofbits/skills) | Vuln detection on the diff before merge |

> Talk's slide 6 framing: this is the "agent review" half (correctness, regression, perf, security) of the verification bottleneck.

---

## 5. Artifact Drift — *agent reading stale truth*

**Goal:** detect, flag, and refresh stale context (docs, AGENTS.md, schemas, examples).

| Skill / Pattern | Source | What it does |
|---|---|---|
| **Skill staleness checker** | pattern documented in [Anthropic enterprise skills docs](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/enterprise) | Skills declare `last_reviewed` + review cadence; checker flags overdue |
| **Living spec / CLAUDE.md sync** | [fazm.ai guide](https://fazm.ai/blog/keeping-claude-md-in-sync-multiple-agents) | Post-commit hook greps CLAUDE.md for paths that no longer exist; flags drift |
| **agent-skill-creator** | [FrancyJGLisboa/agent-skill-creator](https://github.com/FrancyJGLisboa/agent-skill-creator) | One SKILL.md → 14+ platforms; central source-of-truth for agent guidance |
| **consolidate-memory** | [anthropic-skills:consolidate-memory](https://github.com/anthropics/skills) (built-in) | Reflective pass over memory — merges duplicates, fixes stale facts, prunes index |
| **Documentation generation suite** | [levnikolaevich/claude-code-skills](https://github.com/levnikolaevich/claude-code-skills) | Auto-regenerate docs from code on cadence |
| **Termdock comparison: SKILL.md vs CLAUDE.md vs AGENTS.md** | [reference](https://www.termdock.com/blog/skill-md-vs-claude-md-vs-agents-md) | Use to decide what belongs always-on vs on-demand |

**Pattern to enforce:** keep CLAUDE.md + AGENTS.md under ~120 lines combined; push depth into on-demand skills with explicit review dates.

---

## 6. Duplication — *parallel implementations of the same thing*

**Goal:** converge to one source of truth; surface clones the moment they appear.

| Skill | Source | What it does |
|---|---|---|
| **DRY Violation Detector** | [mcpmarket listing](https://mcpmarket.com/tools/skills/dry-violation-detector) | Identifies & eliminates duplication, prevents tech-debt accrual |
| **QuickDup** | [mcpmarket listing](https://mcpmarket.com/tools/skills/quickdup-code-duplication-detector) | Structural clone detection across large codebases |
| **Duplicate Code Detector (jscpd-backed)** | [mcpmarket](https://mcpmarket.com/es/tools/skills/duplicate-code-detector) | Exact + near-match duplicates with %/clone counts |
| **Single Source of Truth Validator** | [mcpmarket](https://mcpmarket.com/tools/skills/single-source-of-truth-validator) | Governance: ensures automation logic lives only in designated skills |
| **Code Clone Assistant** | [mcpmarket](https://mcpmarket.com/tools/skills/code-clone-assistant) | Refactor-clones-to-shared-helper workflow |
| **AI-native quality analyzer (27 rules / 7 dims)** | bundled in addyosmani/levnikolaevich | Targets AI smells ESLint/SonarQube miss: over-generation leftovers, structural clones, god files, unused deps |
| **Open issue: native dedup** | [anthropics/claude-code#10170](https://github.com/anthropics/claude-code/issues/10170) | Track upstream support |

---

## Recommended Starter Bundle (one of each)

For a presentation demo / pilot, install these and map them on stage:

1. **Tech Debt** → [ksimback/tech-debt-skill](https://github.com/ksimback/tech-debt-skill) + `/simplify` from [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)
2. **Comprehension** → Codebase Architecture Explainer + `hex-graph` MCP from [levnikolaevich](https://github.com/levnikolaevich/claude-code-skills)
3. **Intent** → [gotalab/cc-sdd](https://github.com/gotalab/cc-sdd) (cross-agent SDD harness)
4. **Verification** → Playwright Agents + [trailofbits/skills](https://github.com/trailofbits/skills)
5. **Artifact Drift** → built-in `consolidate-memory` + CLAUDE.md staleness git hook
6. **Duplication** → DRY Violation Detector + QuickDup

> Total install time on a fresh repo with `gh skill install ...`: ~5 minutes. Mirrors the talk's 8-pillar agent-readiness investment in concrete tooling.

---

## Sources

- [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills)
- [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills)
- [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills)
- [anthropics/skills](https://github.com/anthropics/skills)
- [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills)
- [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)
- [trailofbits/skills](https://github.com/trailofbits/skills)
- [levnikolaevich/claude-code-skills](https://github.com/levnikolaevich/claude-code-skills)
- [ksimback/tech-debt-skill](https://github.com/ksimback/tech-debt-skill)
- [VoltAgent/awesome-claude-code-subagents — code-reviewer](https://github.com/VoltAgent/awesome-claude-code-subagents/blob/main/categories/04-quality-security/code-reviewer.md)
- [Codebase Architecture Explainer](https://findskill.ai/skills/claude-code/codebase-architecture-explainer/)
- [Visual Explainer skill writeup](https://www.battlecat.ai/tutorials/visual-explainer-agent-skill-terminal-output-html)
- [SpillwaveSolutions/sdd-skill](https://github.com/SpillwaveSolutions/sdd-skill)
- [gotalab/cc-sdd](https://github.com/gotalab/cc-sdd)
- [CCPM listing](https://skills.pawgrammer.com/skills/ccpm)
- [anombyte93/prd-taskmaster](https://github.com/anombyte93/prd-taskmaster)
- [Technical Specification Writer](https://mcpmarket.com/tools/skills/technical-specification-writer-1)
- [Playwright Agents on Claude Code (Shipyard)](https://shipyard.build/blog/playwright-agents-claude-code/)
- [Claude Code with Playwright (TestDino)](https://testdino.com/blog/claude-code-with-playwright)
- [lackeyjb/playwright-skill](https://github.com/lackeyjb/playwright-skill)
- [yusuftayman/playwright-cli-agents](https://github.com/yusuftayman/playwright-cli-agents)
- [neonwatty/qa-skills](https://github.com/neonwatty/qa-skills)
- [agentmantis/test-skills](https://github.com/agentmantis/test-skills)
- [Skills for enterprise — staleness](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/enterprise)
- [Keeping CLAUDE.md in sync (Fazm)](https://fazm.ai/blog/keeping-claude-md-in-sync-multiple-agents)
- [SKILL.md vs CLAUDE.md vs AGENTS.md (Termdock)](https://www.termdock.com/blog/skill-md-vs-claude-md-vs-agents-md)
- [FrancyJGLisboa/agent-skill-creator](https://github.com/FrancyJGLisboa/agent-skill-creator)
- [DRY Violation Detector](https://mcpmarket.com/tools/skills/dry-violation-detector)
- [QuickDup](https://mcpmarket.com/tools/skills/quickdup-code-duplication-detector)
- [Single Source of Truth Validator](https://mcpmarket.com/tools/skills/single-source-of-truth-validator)
- [Duplicate Code Detector](https://mcpmarket.com/es/tools/skills/duplicate-code-detector)
- [Code Clone Assistant](https://mcpmarket.com/tools/skills/code-clone-assistant)
- [anthropics/claude-code#10170 — native dedup feature request](https://github.com/anthropics/claude-code/issues/10170)
- [GitHub CLI agent skill management (Apr 2026)](https://github.blog/changelog/2026-04-16-manage-agent-skills-with-github-cli/)
- [Hack the AI agent — GitHub Secure Code Game](https://github.blog/security/hack-the-ai-agent-build-agentic-ai-security-skills-with-the-github-secure-code-game/)
- [10 Must-Have Skills for Claude in 2026 (Medium)](https://medium.com/@unicodeveloper/10-must-have-skills-for-claude-and-any-coding-agent-in-2026-b5451b013051)
