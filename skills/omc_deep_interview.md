# Skill: omc_deep_interview

## Purpose
Deep Interview is a Socratic requirements gathering process. It prevents "building the wrong thing" by asking targeted questions that expose hidden assumptions and measuring clarity across weighted dimensions.

## Use When
- User has a vague idea (e.g., "Build a task app", "Add something cool").
- Triggers: "deep interview", "interview me", "ask me everything", "vague idea", "not sure what I want".

## Workflow (The Socratic Loop)

### Phase 1: Initialize
- **Goal**: Identify the starting point.
- **Action**: Use `omc_analyst` to parse the initial idea and identify the most obvious gaps.
- **Ambiguity Score**: Initialize Ambiguity at 100%.

### Phase 2: Socratic Interview Loop
Repeat until **Ambiguity ≤ 20%** (or user exits):

#### Step 2a: Generate Question
- **Goal**: Target the weakest clarity dimension (Goal, Constraint, or Success Criteria).
- **Action**: Ask **ONE** targeted question.
    - *Goal Clarity*: "What exactly happens when...?"
    - *Constraint Clarity*: "What are the boundaries?"
    - *Success Criteria*: "How do we know it works?"
- **Brownfield Check**: If this is an existing project, use `omc_architect` to find relevant code patterns BEFORE asking the user about them.

#### Step 2b: Score Ambiguity
- **Goal**: Calculate progress.
- **Action**: Invoke `omc_analyst` to score 0.0-1.0 on:
    1. **Goal Clarity** (40%)
    2. **Constraint Clarity** (30%)
    3. **Success Criteria** (30%)
- **Report**: Show the current Ambiguity score (1 - weighted average) to the user.

### Phase 3: Crystallize Spec
- **Goal**: Document the final understanding.
- **Action**: Use `omc_architect` and `omc_analyst` to write a comprehensive spec.
- **Output**: Save to `.gemini/specs/deep-interview-{slug}.md`.

### Phase 4: Execution Bridge
- **Goal**: Hand off to execution.
- **Action**: Present options:
    1. **Execute with autopilot**: Hand off the spec to `omc_autopilot`.
    2. **Execute with ralph**: Hand off to `omc_ralph`.
    3. **Plan only**: Stop with the saved spec.

## Critical Instructions
- **One Question at a Time**: Never batch multiple questions.
- **Expose Assumptions**: Focus on "What are you assuming?" rather than "What do you want?".
- **Mathematical Gate**: Do not proceed to execution until Ambiguity ≤ 20% or the user explicitly overrides.
- **No Direct Mutation**: This is a requirements gathering skill. Do not edit source code during the interview.
