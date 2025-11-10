# cc-gtd - Getting Things Done with Claude Code

## Overview

A comprehensive GTD (Getting Things Done) implementation for Claude Code, providing specialized tools and workflows for GitHub project management, Obsidian knowledge management, and more. This suite offers curated collections of commands, agents, and skills that enhance your productivity through AI-powered workflow automation.

## Available Plugins

### GitHub Workflow Plugin
Streamline your entire GitHub project lifecycle from issue creation to merge:

- **`/gh-issue`** - Create structured GitHub issues with proper templates and labels
- **`/gh-plan`** - Develop detailed implementation plans with options analysis
- **`gh-build`** - Autonomous agent that builds code from implementation plans
- **`/gh-review`** - Interactive code review and implementation guidance

**Key Features:**
- 7-stage workflow with clear approval gates
- AI-driven planning and implementation
- Conventional commit enforcement
- Automated PR creation and review
- Git worktree isolation for safe development

### Obsidian Workflow Plugin
Enhance your knowledge management with PARA and Zettelkasten workflows:

- Automated content extraction and organization
- Zettelkasten note creation and linking
- Project resource management
- Cross-reference and knowledge graph building

**Coming Soon:** Full Obsidian integration suite

## Development Roadmap

| Component | Plugin | Description | Status |
|-----------|---------|-------------|--------|
| `command` | `github-workflow` | `/gh-issue`: Create structured GitHub issues | In Development |
| `command` | `github-workflow` | `/gh-plan`: Develop implementation plans | In Development |
| `agent` | `github-workflow` | `gh-build`: Autonomous code building | In Development |
| `command` | `github-workflow` | `/gh-review`: Interactive code review | In Development |
| `plugin` | `obsidian-workflow` | PARA/Zettelkasten workflow tools | Planned |

## Installation

### Quick Start

Add this marketplace to Claude Code:

```bash
/plugin marketplace add nikhilmaddirala/cc-gtd
```

### Install Individual Plugins

After adding the marketplace, install specific plugins:

```bash
# GitHub workflow tools
/plugin install github-workflow@cc-gtd

# Obsidian workflow tools  
/plugin install obsidian-workflow@cc-gtd
```

### Browse Available Plugins

```bash
# Interactive plugin browser
/plugin

# List all available plugins from this marketplace
/plugin marketplace list cc-gtd
```

## Usage Examples

### GitHub Project Management

```bash
# Create a new issue
/gh-issue Add user authentication to the API

# Plan the implementation
/gh-plan 123

# Let AI build it autonomously
# (gh-build agent activates automatically for approved plans)

# Review the changes
/gh-review
```



## Plugin Architecture

### Components

- **Skills** - Domain expertise and detailed workflows (foundation layer)
- **Commands** - Interactive workflows with human input (`/command-name`)
- **Agents** - Autonomous execution without human interaction

### Design Principles

- **Skills as Foundation** - Heavy logic lives in reusable skills
- **Orchestration Layers** - Commands (interactive) and agents (autonomous) coordinate skills
- **Progressive Loading** - Load only what's needed when needed
- **Repository Awareness** - Adapt to existing project conventions

## Contributing

This GTD suite follows established patterns from reference implementations. Contributions welcome for:

- New workflow plugins
- Additional commands and agents
- Enhanced skill libraries
- Documentation improvements

## Support

- **Issues**: Report bugs via GitHub Issues
- **Documentation**: See `/references/docs/` for detailed guides
- **Community**: Join discussions for feature requests

## References

- [Plugin Marketplaces Documentation](references/docs/plugin-marketplaces.md) - Comprehensive guide to marketplace structure and best practices
- [GitHub Projects AI Workflow](references/docs/Github-projects-ai-workflow.md) - Detailed workflow architecture
- [AI Agents Configuration](references/docs/ai-agents-README.md) - Component architecture and design principles

---

**License:** MIT  
**Maintainer:** Nikhil Maddirala  
**Repository:** https://github.com/nikhilmaddirala/cc-gtd


