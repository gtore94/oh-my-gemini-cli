# oh-my-claudecode Integration for Gemini CLI

This project integrates high-performance orchestration patterns from `oh-my-claudecode` (OMC).

## Slash Command Mapping
If the user starts a message with `/`, treat it as a direct command to activate the corresponding skill:
- `/autopilot` -> `activate_skill(name="omc_autopilot")`
- `/ralph` -> `activate_skill(name="omc_ralph")`
- `/deep-interview` -> `activate_skill(name="omc_deep_interview")`
- `/ccg` -> `activate_skill(name="omc_ccg")`
- `/ultrawork` -> `activate_skill(name="omc_ultrawork")`
- `/team` -> `activate_skill(name="omc_team")`
- `/trace` -> `activate_skill(name="omc_trace")`
- `/verify` -> `activate_skill(name="omc_verify")`
- `/debug` -> `activate_skill(name="omc_debug")`
- `/plan` -> `activate_skill(name="omc_plan")`

## Core Orchestration Library
... (rest of the file)

### Specialized Sub-agents
Defined in `subagents/OMC_AGENTS.md`. Use these for high-difficulty tasks:
- `omc_architect`: Use for root-cause analysis, complex debugging, and architecture review. (READ-ONLY)
- `omc_planner`: Use for multi-step task planning and requirement gathering.
- `omc_analyst`: Use for gap analysis and edge-case identification. (READ-ONLY)
- `omc_executor`: Use for focused implementation tasks with match-codebase-style constraints.

### Advanced Skills
Activate these using `activate_skill(name="omc_<skill_name>")`:
- `omc_autopilot`: End-to-end autonomous execution (Idea -> Working Code).
- `omc_ralph`: Persistence loop. Do not stop until verified 100% complete.
- `omc_ccg`: Tri-model orchestration (Gemini + Claude + Codex).

## Workflow Guidelines

### 1. When to use Autopilot
If the user's request is a broad goal (e.g., "Build a feature", "Refactor the entire module"), activate `omc_autopilot`. Follow its 5-phase lifecycle strictly.

### 2. When to use Ralph
If the task is complex or prone to "polite-stop" (e.g., "Fix all lint errors", "Implement these 5 user stories"), activate `omc_ralph`. Maintain the `prd.json` state and verify every story before proceeding.

### 3. When to invoke the Architect
If you fail a fix 2+ times, or if the architecture is unfamiliar, invoke `omc_architect` via `invoke_agent`. Use its diagnosis to pivot your strategy.

### 4. Multi-Model Synthesis
For high-stakes decisions or complex code reviews, use `omc_ccg` to cross-validate recommendations with external perspectives.

## Technical Integrity
- **Evidence-First**: Never claim a task is complete without tool output evidence (tests, builds, lsp).
- **Smallest Viable Diff**: Match existing codebase patterns and avoid scope creep.
- **Relentless Persistence**: Follow the OMC "boulder never stops" principle. Automate handoffs between agents and phases without unnecessary user prompts.
