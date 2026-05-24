# oh-my-claudecode to Gemini CLI Refactoring & Integration Plan

This document outlines the strategy for porting the multi-agent orchestration and advanced workflows of `oh-my-claudecode` (OMC) to `gemini-cli`.

## 1. Architecture Comparison

| Concept | oh-my-claudecode (OMC) | Gemini CLI |
| :--- | :--- | :--- |
| **Orchestrator** | Claude Code + OMC Plugin | Gemini CLI (Interactive Agent) |
| **Sub-agents** | Specialized personas via `Task` tool | Sub-agents via `invoke_agent` |
| **Skills** | Prompt-triggered behavior injections | Markdown-based skill instructions |
| **Hooks** | Lifecycle event listeners (Node.js) | Integrated workflow (R-S-E lifecycle) |
| **Memory** | `.omc/` (Project Memory, Notepad) | `GEMINI.md`, `MEMORY.md`, Private Memory |
| **Tools** | MCP, Bash, LSP, AST | Native tools (grep, glob, replace, etc.) + MCP |
| **Verification** | Evidence-driven protocol | Validation phase in Execution cycle |

## 2. Mapping & Porting Strategy

### A. Porting Agents (Personas)
OMC has 19 specialized agents. These should be ported as `gemini-cli` sub-agent definitions.
- **Action**: Create a repository of sub-agent prompts based on `oh-my-claudecode/agents/*.md`.
- **Integration**: Register these sub-agents in the system prompt or via a dynamic loader.

### B. Porting Skills (Workflows)
OMC's key skills like `autopilot`, `ralph`, and `ultrawork` represent complex workflows.
- **Action**: Convert these into `gemini-cli` Skills (markdown files).
- **Mapping**:
    - `autopilot`: A high-level skill that automates the Research -> Strategy -> Execution lifecycle.
    - `ralph`: A persistence skill that ensures the "Validate" phase of the execution cycle never exits until success.
    - `ultrawork`: Leverages `gemini-cli`'s parallel tool execution capability.
    - `ccg`: A specialized skill to orchestrate multiple models (Gemini + others via MCP or sub-agents).

### C. Hook Simulation
Since `gemini-cli` doesn't have an open hook system, we can use:
1. **Keyword Detection**: Add a step in the Research phase to detect "magic keywords" and activate relevant skills.
2. **Implicit Skills**: System-level instructions that automatically trigger certain behaviors (like `git-master` logic after successful `replace`).

### D. Memory & State Integration
- **OMC Project Memory** -> `GEMINI.md` (shared) or `MEMORY.md` (private).
- **OMC Notepad** -> A dedicated section in `MEMORY.md` or a separate `NOTEPAD.md` tracked by the agent.
- **Verification Logs** -> Use the `update_topic` summary to maintain an evidence ledger.

## 3. Implementation Roadmap

### Phase 1: Foundation (Skills & Agents)
1. **Skill Conversion**: Port the most critical OMC skills (`autopilot`, `ralph`, `team`) to `gemini-cli` format.
2. **Sub-agent Definitions**: Create a `subagents/` directory containing the ported persona prompts.
3. **Instruction Update**: Update `GEMINI.md` to guide the agent on how to use these new capabilities.

### Phase 2: Workflow Enhancement
1. **Enhanced Research**: Implement a "deep-interview" style research phase to clarify requirements before planning.
2. **Persistence Loop**: Formalize the `ralph` workflow within the standard execution cycle.
3. **Parallel Execution**: Optimize the use of parallel tool calls for `ultrawork`-style speed.

### Phase 3: Multi-Model (ccg) Integration
1. **MCP Connectors**: Ensure MCP servers for other models (Claude, OpenAI) are available.
2. **Advisor Skill**: Create a skill that prompts multiple models for advice and synthesizes the output.

### Phase 4: Advanced Verification
1. **Evidence Protocol**: Standardize the "Validation" phase to require specific evidence (logs, test results, diffs).
2. **Automated Fix-up**: Implement a "debugger" sub-agent specialized in resolving build/test failures.

## 4. Immediate Next Steps

1. **Create `SKILLS_OMC.md`**: A collection of ported OMC skills ready for `activate_skill`.
2. **Define Agent Library**: Convert `agents/*.md` to a format suitable for `invoke_agent`.
3. **Update Workspace Instructions**: Add a section to `./GEMINI.md` describing how to invoke these OMC-inspired workflows.

---
*Note: This plan focuses on porting the "intelligence" and "workflows" of OMC, which are its most valuable assets, to the Gemini CLI environment.*
