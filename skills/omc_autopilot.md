# Skill: omc_autopilot

## Purpose
Autopilot takes a product idea or task description and autonomously handles the full lifecycle: requirements analysis, technical design, planning, implementation, and validation.

## Use When
- End-to-end autonomous execution is desired.
- Triggers: "autopilot", "auto pilot", "autonomous", "build me", "handle it all".

## Workflow (The 5-Phase Loop)

### Phase 1: Expansion (Research)
- **Goal**: Turn the idea into a detailed technical specification.
- **Action**: Invoke `omc_analyst` to extract requirements and `omc_architect` to create a technical spec.
- **Output**: Save spec to `.gemini/autopilot/spec.md`.

### Phase 2: Planning (Strategy)
- **Goal**: Create an implementation plan from the spec.
- **Action**: Invoke `omc_planner` to create a 3-6 step actionable plan.
- **Verification**: Use `omc_architect` to review the plan for feasibility.
- **Output**: Save plan to `.gemini/plans/autopilot-impl.md`.

### Phase 3: Execution (Act)
- **Goal**: Implement the plan.
- **Action**: Use the Gemini CLI `Execution` cycle. Delegate tasks to `omc_executor`.
- **Constraint**: Run independent tasks in parallel using parallel tool calls.

### Phase 4: QA & Validation (Validate)
- **Goal**: Ensure work is correct and complete.
- **Action**: 
    1. Run builds, linting, and tests. Fix failures using `omc_executor`.
    2. Invoke `omc_architect` for a final functional review.
- **Exit Condition**: All tests pass and `omc_architect` approves.

### Phase 5: Cleanup
- **Action**: Final summary of what was built and cleanup of temporary state files in `.gemini/autopilot/`.

## Critical Instructions
- **Relentless Execution**: Do not stop until all phases are complete.
- **Evidence-Driven**: Every phase must provide evidence (spec file, plan file, test results).
- **Handoffs**: Strictly use the designated sub-agents (`omc_analyst`, `omc_planner`, `omc_architect`, `omc_executor`).
- **Feedback Loop**: If Phase 4 fails, return to Phase 3 (or Phase 2 if the plan was flawed).
