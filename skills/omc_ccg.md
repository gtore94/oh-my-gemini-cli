# Skill: omc_ccg

## Purpose
CCG (Claude-Codex-Gemini) performs tri-model orchestration. It consults external models (Claude and Codex) for their specialized perspectives and synthesizes the results within Gemini.

## Use When
- Multi-perspective review is needed (e.g., architecture + UX).
- Cross-validation of complex logic.
- Triggers: "ccg", "tri-model", "consult others", "claude-codex-gemini".

## Workflow

### Phase 1: Decomposition (Strategy)
- **Goal**: Split the request into specialized prompts for different models.
- **Action**: 
    - **Codex/ChatGPT Prompt**: Focus on backend, architecture, performance, and risk.
    - **Claude Prompt**: Focus on implementation details, refactoring, and logic correctness.
    - **Gemini (Self) Focus**: Focus on UI/UX, documentation, and overall integration.

### Phase 2: Multi-Model Consultation (Act)
- **Goal**: Collect advice from external models.
- **Action**: Attempt to run the following commands via `run_shell_command`:
    - **Claude**: `claude -p "<claude prompt>"` or `omc ask claude "<claude prompt>"`
    - **Codex**: `omc ask codex "<codex prompt>"` or `codex "<codex prompt>"`
- **Artifacts**: Capture the output from these commands. If a command fails or a CLI is missing, continue with the remaining models and note the limitation.

### Phase 3: Synthesis (Validate)
- **Goal**: Combine all perspectives into a final recommendation.
- **Action**:
    1. List points of agreement.
    2. Identify conflicts and provide a reasoned tie-breaker.
    3. Produce a unified "Consensus Recommendation".

## Critical Instructions
- **Tool Check**: Before running, briefly check if `claude`, `codex`, or `omc` are in the PATH.
- **Synthesize, Don't Just Paste**: Do not just list the outputs. Provide a single, coherent response that integrates all advice.
- **Actionable Output**: End with a concrete checklist of actions based on the tri-model consensus.
