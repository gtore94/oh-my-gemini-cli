# Gemini CLI with oh-my-claudecode (OMC) Integration

Welcome to the enhanced Gemini CLI, now supercharged with the multi-agent orchestration patterns from `oh-my-claudecode` (OMC). This integration transforms the Gemini CLI into a sophisticated engineering environment with specialized agents and advanced autonomous workflows.

## 🚀 Key Features

### 🤖 Specialized Sub-Agents
Leverage a team of expert personas via `invoke_agent`:
- **Architect**: Strategic code analysis and complex debugging.
- **Planner**: Structured requirements gathering and work planning.
- **Analyst**: Gap detection and edge-case analysis.
- **Executor**: Precision implementation following codebase patterns.

### 🛠 Advanced Autonomous Skills
Powered by the R-S-E lifecycle:
- **Autopilot**: End-to-end execution from a brief idea to working code.
- **Ralph**: A relentless persistence loop that ensures 100% completion.
- **CCG**: Multi-model consultation (Claude-Codex-Gemini).
- **Deep Interview**: Socratic requirements gathering with ambiguity gating.

## ⌨️ Slash Commands

Use these first-class commands directly in the CLI (ensure you run `/commands reload` first):

| Command | Description |
| :--- | :--- |
| `/autopilot <idea>` | Start full autonomous lifecycle |
| `/ralph <task>` | Start persistence loop with verification |
| `/deep-interview <idea>` | Start Socratic requirements gathering |
| `/plan <task>` | Strategic planning with expert consensus |
| `/trace <issue>` | Evidence-driven causal root-cause analysis |
| `/debug <problem>` | Diagnose session or workflow breakages |
| `/team <task>` | Orchestrate parallel agents for large tasks |
| `/ccg <request>` | Consult Gemini, Claude, and Codex |
| `/verify <change>` | Strictly verify implementation with evidence |
| `/ask <model> <q>` | Consult a specific external model |

## 📖 Getting Started

### 1. Initial Setup (First-time clone)
After cloning this repository, you must install dependencies for the OMC orchestration engine:
```bash
cd oh-my-claudecode && npm install && npm run build && cd ..
```

### 2. Reload Commands
In your Gemini CLI session, run to register the new slash commands:
```bash
/commands reload
```

### 3. Start a Task
Try starting a new feature with autopilot:
```bash
/autopilot "Build a simple task manager with local storage"
```

### 4. Refine Requirements
If you have a vague idea, use the interview:
```bash
/deep-interview "I want to improve the performance of our database layer"
```

## 📂 Project Structure

- `subagents/`: Ported agent persona definitions.
- `skills/`: OMC-inspired workflow logic.
- `.gemini/commands/`: Native slash command registrations.
- `GEMINI.md`: Integrated project instructions for autonomous behavior.

---
*Inspired by [oh-my-claudecode](https://github.com/oh-my-claudecode)*
