# AI Agents Configuration

## Overview
Nikhil's configuration for AI agents (Claude Code, OpenCode, Gemini CLI, etc.) used across multiple projects. These configs are either symlinked to AI CLI config directories or referenced directly.

The core components are commands, agents, skills. These are packaged into plugins or stand-alone. I'm currently working on the following plugins:

- github-workflow: collection for working with github projects from issue creation to planning to execution
  - gh-issue: create new issue
  - gh-plan: develop detailed implementation plan for issue
  - gh-build: build the implementation plan
  - gh-review: 
- obsidian-workflow: collection for working with obsidian PARA and Zettelkasten workflows.


## Development Roadmap

| Component Type | Plugin              | Description                                                      | Status |
| :------------- | :------------------ | :--------------------------------------------------------------- | :----- |
| `command`      | `github-workflow`   | `/gh-issue`: Creates a new GitHub issue from a prompt.           | To Do  |
| `command`      | `github-workflow`   | `/gh-plan`: Develops a detailed implementation plan for an issue.  | To Do  |
| `agent`        | `github-workflow`   | `gh-build`: Autonomously builds the code from an implementation plan. | To Do  |
| `command`      | `github-workflow`   | `/gh-review`: Interactively reviews code or implementation details. | To Do  |
| `plugin`       | `obsidian-workflow` | Collection for working with Obsidian PARA/Zettelkasten workflows.  | To Do  |


## Directory Structure

```
.config/ai-agents/
├── README.md              # This file
├── agents/                # Agent system prompts and configurations
├── commands/              # Executable workflows and meta-tasks
└── skills/                # Reference libraries and domain expertise
```

## Architecture

This configuration system has two layers:

1. **Foundation Layer: Skills** - Where the heavy lifting happens
2. **Orchestration Layer: Commands & Agents** - How skills get invoked

```
┌─────────────────────────────────────────────┐
│         Orchestration Layer                 │
│  ┌──────────────┐      ┌──────────────┐    │
│  │  Commands    │      │   Agents     │    │
│  │  (Human-in-  │      │  (Autonomous │    │
│  │   the-loop)  │      │ orchestration)│   │
│  └──────┬───────┘      └──────┬───────┘    │
│         │                     │             │
│         └──────────┬──────────┘             │
└────────────────────┼──────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────┐
│          Foundation Layer                   │
│         ┌─────────────────┐                 │
│         │     Skills      │                 │
│         │ (Domain logic & │                 │
│         │   expertise)    │                 │
│         └─────────────────┘                 │
└─────────────────────────────────────────────┘
```

---

## Component Types

### Skills (Foundation)
**Purpose**: Domain expertise and detailed workflows - this is where the heavy lifting happens

**What they are**: Self-contained knowledge bases with comprehensive documentation, detailed workflows, scripts, and reference material. Skills contain the actual logic and domain expertise.

**Directory structure**:
```
skill-name/
├── SKILL.md           # Main documentation with detailed workflows
├── LICENSE.txt        # Optional license
├── scripts/           # Executable code
├── references/        # Detailed reference material
└── assets/            # Templates and resources (not loaded into context)
```

**SKILL.md format**:
```yaml
---
name: skill-name
description: What this skill does and when to use it
license: [License info]
---

[Comprehensive instructions, detailed workflows, step-by-step guides, examples]
```

**Progressive loading**: Skills use progressive disclosure to manage context:
- Skill metadata (name + description) → always available
- Full SKILL.md content → loaded when skill is invoked
- Bundled resources → accessed as needed

**When to create**: Create a skill for any specialized domain knowledge, complex workflow, or reusable capability. Skills are the foundation - most logic should live here.

---

### Commands (Interactive Orchestrators)
**Purpose**: Human-in-the-loop orchestration of skills

**What they are**: Interactive workflow templates invoked by users (e.g., `/gh-issue`, `/gh-commit`). Commands orchestrate one or more skills while involving the user in decision-making steps.

**How they work**: Commands inject runtime context, guide the user through decisions, and invoke skills as needed. They're for workflows where human input, clarification, or approval is required at various stages.

**File format**:
```yaml
---
description: Brief description
allowed-tools: [Optional tool restrictions]
---

## Context
```bash
# Runtime context gathering
command-to-get-context
```

## Your task
[Step-by-step instructions that may invoke skills and interact with user]
```

**Key characteristics**:
- **Interactive**: Asks user for input, clarification, decisions
- **Context injection**: Gathers runtime environment info
- **Skill orchestration**: Can reference/invoke skills for heavy lifting
- **Step-by-step**: Guides user through a workflow

**When to create**: Create a command for workflows that need user input, approval, or decision-making at various steps.

---

### Agents (Autonomous Orchestrators)
**Purpose**: Autonomous orchestration of skills without user involvement

**What they are**: System prompts that orchestrate one or more skills to accomplish defined goals completely autonomously. Agents execute entire workflows from start to finish without stopping for user input.

**How they work**: Agent files define the goal/workflow and orchestrate skills to achieve it. They make decisions, handle edge cases, and complete tasks without human intervention.

**File format**:
```yaml
---
name: agent-name
description: What goal/workflow this agent accomplishes
model: sonnet  # Optional: specify model
---

[Instructions for autonomous workflow, which skills to use, decision logic, error handling]
```

**Key characteristics**:
- **Autonomous**: No user interaction during execution
- **Goal-oriented**: Focused on accomplishing a specific outcome
- **Skill orchestration**: Combines multiple skills to achieve goal
- **Decision-making**: Handles branching logic and edge cases independently

**When to create**: Create an agent for workflows that should run autonomously without user involvement - e.g., batch processing, scheduled tasks, or well-defined workflows where decisions can be automated.

---

## How Components Work Together

### Architecture Principle
**Skills** = Foundation (where logic lives)
**Commands** = Interactive orchestrators (human-in-the-loop)
**Agents** = Autonomous orchestrators (no human involvement)

### Example: Content Extraction

**As a Command** (human-in-the-loop):
```
User: /extract-content https://youtube.com/...
  ↓
Command asks: Where should I save this? What format?
  ↓
User responds: 03-zettel/sources/, use default template
  ↓
Command invokes: content-extraction skill
  ↓
Result: User has control over decisions
```

**As an Agent** (autonomous):
```
User activates: content-extraction-agent
User provides: https://youtube.com/...
  ↓
Agent invokes: content-extraction skill autonomously
  ↓
Agent decides: Save location, template choice, all details
  ↓
Result: Completed extraction without user interaction
```

### Loading Behavior
- **Skills**: Metadata always available; full content loaded on-demand
- **Commands**: Loaded when user invokes them (e.g., `/gh-issue`)
- **Agents**: Loaded when specified by user or as default for a session

### Decision: Command vs Agent?

Use a **Command** when:
- User needs to make decisions during workflow
- Clarifications or approvals are needed
- Workflow has multiple valid paths user should choose
- Interactive refinement improves quality

Use an **Agent** when:
- Workflow is well-defined with clear decision rules
- No user input needed during execution
- Batch processing or scheduled execution
- Speed and automation are priorities

---

## Key Design Principles

### 1. Skills as Foundation
Most logic, workflows, and domain expertise lives in skills, not in commands or agents.

**Why**: Skills are reusable across both interactive (command) and autonomous (agent) contexts. By putting heavy lifting in skills, we avoid duplicating logic and make it easier to maintain.

**Example**: The `options-analysis-skill` contains detailed research methodology. Both a command (interactive research) and an agent (autonomous research) can invoke this same skill.

### 2. Orchestration, Not Implementation
Commands and agents orchestrate skills; they don't contain detailed implementation logic.

**Why**: Keeps orchestrators lightweight and focused on coordination. When implementation details change, you only update the skill, not every command/agent that uses it.

**Anti-pattern**: Don't put detailed workflows in commands/agents. Extract them to skills.

### 3. Progressive Disclosure
Load only what's needed when it's needed:
- Skill metadata (name + description) → always available
- Full SKILL.md content → loaded when skill is invoked
- Bundled resources → accessed as needed

**Why**: Manages context window efficiently, especially important for large skill catalogs.

### 4. Context Injection
Commands inject runtime context via bash commands in backticks:
```bash
`gh label list`
`git status`
`git log --oneline -5`
```

**Why**: Gives AI current, accurate information about the environment rather than guessing or using stale data.

### 5. Clear Separation of Concerns
- **Skills** = Domain logic, detailed workflows, expertise (foundation)
- **Commands** = Interactive orchestration (human-in-the-loop)
- **Agents** = Autonomous orchestration (no human involvement)

**Why**: Each layer has a distinct responsibility. Skills can be reused by multiple orchestrators without modification.

### 6. Repository Awareness
Commands and agents adapt to existing conventions rather than imposing rigid structure.

**Example**: The `gh-issue` command checks for existing templates, labels, and recent issue styles, then matches that pattern.

**Why**: Works with any project without requiring project-specific configuration.

### 7. Composability
Skills should be composable - agents and commands can invoke multiple skills to accomplish complex goals.

**Why**: Enables building complex workflows from simple, well-tested building blocks.

**Example**: An agent might use `crawl4ai` skill to fetch content + `options-analysis-skill` to analyze it + document skill to format output.

### 8. Convention Over Configuration
Use consistent naming and structure patterns:
- Agent files: `agent-name.md`
- Command files: `command-name.md`
- Skill directories: `skill-name/SKILL.md`

**Why**: Predictable structure makes the system self-documenting and easier to extend.

---

## Usage

### Using Commands
Invoke commands with `/command-name`:
```bash
/gh-issue Add user authentication
/gh-commit
```

### Using Skills
Skills are invoked automatically when needed or can be referenced explicitly in prompts.

### Using Agents
Specify agent in AI CLI configuration or switch agents as needed per conversation/project.

---

## Contributing

### Adding a Skill (Start Here)
Skills are the foundation - always start by creating/identifying the skill first.

1. Use the `skill-creator` skill to generate proper structure
2. Write SKILL.md with comprehensive workflows and detailed logic
3. Add executable code to `scripts/`, detailed docs to `references/`
4. Test skill invocation and progressive loading
5. Document what the skill does in YAML frontmatter

**Remember**: Put the heavy lifting here. Skills should contain detailed workflows, not orchestrators.

### Adding a Command (Interactive Orchestrator)
Create a command when you need human-in-the-loop orchestration of skills.

1. Identify which skill(s) this command will orchestrate
2. Create `commands/new-command.md`
3. Add YAML frontmatter with `description`
4. Add context injection section (bash commands in backticks)
5. Write orchestration logic: when to invoke skills, when to ask user for input
6. Keep it lightweight - delegate heavy lifting to skills
7. Test in multiple repositories/contexts

### Adding an Agent (Autonomous Orchestrator)
Create an agent when you need autonomous orchestration of skills.

1. Identify which skill(s) this agent will orchestrate
2. Create `agents/new-agent.md`
3. Add YAML frontmatter with `name`, `description`, optional `model`
4. Define autonomous workflow: decision logic, error handling, which skills to invoke
5. Keep it lightweight - delegate heavy lifting to skills
6. Specify when this agent should be used
7. Test with relevant tasks

**Key principle**: Both commands and agents should be thin orchestration layers. If you find yourself writing detailed implementation logic, extract it to a skill instead.

---

## Philosophy

This configuration system is designed to:
- **Skills as building blocks**: Heavy lifting lives in reusable skills; orchestrators stay lightweight
- **Flexible orchestration**: Same skill can be used interactively (commands) or autonomously (agents)
- **Enhance, not constrain**: Provide helpful structure without rigid requirements
- **Adapt, not impose**: Work with existing conventions rather than forcing new ones
- **Scale gracefully**: Handle simple tasks easily while supporting complex workflows
- **Stay maintainable**: Keep components focused and loosely coupled

The goal is to make AI assistants more capable and consistent across projects while remaining flexible and unopinionated. By separating domain logic (skills) from orchestration (commands/agents), we maximize reusability and minimize duplication.
