# Skill: omc_ralph

## Purpose
Ralph is a persistence loop that ensures a task is 100% complete and verified. It prevents "polite-stop" anti-patterns where an agent stops after a partial implementation.

## Use When
- Task requires guaranteed completion with evidence.
- Triggers: "ralph", "don't stop", "must complete", "finish this", "keep going until done".

## Workflow (The Persistence Loop)

### Phase 1: Requirement Breakdowns (Strategy)
- **Goal**: Break the task into discrete, verifiable "User Stories".
- **Action**: Create a `.gemini/ralph/prd.json` file with a list of stories. Each story must have:
    - `id`: unique identifier.
    - `description`: what needs to be done.
    - `acceptanceCriteria`: specific, testable criteria (e.g., "Function X returns Y").
    - `status`: "pending", "in_progress", or "completed".
- **Output**: `.gemini/ralph/prd.json`.

### Phase 2: Iterative Execution (Act)
- **Goal**: Implement stories one-by-one.
- **Action**:
    1. Pick the highest priority "pending" story.
    2. Delegate implementation to `omc_executor`.
    3. **Verification**: For the current story, run tests/builds. Do NOT proceed until all acceptance criteria for THIS story are met.
    4. Update `status` to "completed" in `prd.json`.
- **Constraint**: Loop until ALL stories in `prd.json` are "completed".

### Phase 3: Final Verification (Validate)
- **Goal**: Cross-verify the entire implementation.
- **Action**:
    1. Invoke `omc_architect` to review the entire diff against the `prd.json`.
    2. Run the full project test suite.
- **Exit Condition**: `omc_architect` gives an "APPROVED" verdict and all tests pass.
- **Rejection**: If `omc_architect` rejects, return to Phase 2 to fix issues.

## Critical Instructions
- **The Boulder Never Stops**: Do not ask the user "Should I continue?" or "I have finished step 1, what next?". Automatically proceed to the next story.
- **Evidence-First**: Every `status: "completed"` update must be preceded by a tool output showing success (test pass, build success).
- **Smallest Viable Diff**: Match the codebase style and avoid unnecessary abstractions.
- **No Premature Exit**: Only exit the skill when the Final Verification (Phase 3) is 100% successful.
