# Skill: omc_team

## Purpose
Coordinates multiple parallel agents (workers) to handle large tasks.

## Workflow
- **Lead**: Orchestrates the team, assigns tasks, and synthesizes results.
- **Workers**: Specialized agents (`omc_executor`, `omc_architect`, etc.) handling independent sub-tasks.
- **Phases**: Staged pipeline (`plan` -> `exec` -> `verify` -> `fix`).
