# Skill: omc_plan

## Purpose
Plan creates comprehensive, actionable work plans. It supports interview mode (gathering requirements), direct mode (generating plans from specific requests), and consensus mode (iterative review by Planner, Architect, and Critic).

## Use When
- Planning is needed before implementation.
- Triggers: "plan this", "plan the", "ralplan", "consensus plan".

## Workflow

### 1. Interview Mode (Broad Requests)
- **Goal**: Clarify requirements.
- **Action**: Ask one question at a time using `omc_analyst`. Explore the codebase with `omc_explore` before asking the user about facts.

### 2. Direct Mode (Specific Requests)
- **Goal**: Generate a plan immediately.
- **Action**: Use `omc_planner` to produce a 3-6 step plan with acceptance criteria.

### 3. Consensus Mode (High Stakes)
- **Goal**: Ensure architectural soundness and quality.
- **Action**:
    1. **Planner**: Creates initial plan.
    2. **Architect**: Reviews for feasibility and tradeoffs.
    3. **Critic**: Validates against quality standards.
    4. **Loop**: If Critic/Architect reject, Planner revises. Repeat until consensus.

## Output
- Save plans to `.gemini/plans/plan-*.md`.
- Include: Requirements, Acceptance Criteria, Implementation Steps, Risks, and Verification.
