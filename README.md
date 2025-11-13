# gtd-cc - Getting Things Done with Claude Code

## Overview

A comprehensive GTD (Getting Things Done) implementation for Claude Code, providing specialized tools and workflows for GitHub project management, Obsidian knowledge management, and more. This suite offers curated collections of commands, agents, and skills that enhance your productivity through AI-powered workflow automation.

## Plugins

| Plugin name | Description | Development status |
|---|---|---|
| GitHub Workflow Plugin | Streamline your entire GitHub project lifecycle from issue creation to merge. See [plugins/github/README.md](plugins/github/README.md) for detailed workflow stages, state transitions, and implementation specifications. | Scaffolding |
| Obsidian Workflow Plugin | Enhance your knowledge management with PARA and Zettelkasten workflows. | Scaffolding |


## Quick start

### Add marketplace 

Add this marketplace to Claude Code:

```bash
/plugin marketplace add nikhilmaddirala/gtd-cc
```

### Install Individual Plugins

After adding the marketplace, install specific plugins:

```bash
# GitHub workflow tools
/plugin install github@gtd-cc

# Obsidian workflow tools
/plugin install obsidian@gtd-cc
```

### Browse Available Plugins

```bash
# Interactive plugin browser
/plugin

# List all available plugins from this marketplace
/plugin marketplace list gtd-cc
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

## Project Structure

The project is organized as a marketplace with multiple focused plugins:

- `plugins/github/` - GitHub workflow automation with commands
- `plugins/obsidian/` - Obsidian integration for knowledge management (scaffolding)
- `.claude-plugin/` - Marketplace configuration
- `references/docs/` - Reference documentation

For detailed information about the directory structure and how to extend it, see [CONTRIBUTING.md](CONTRIBUTING.md).

## Contributing

This GTD suite follows established patterns from reference implementations. Contributions welcome for:

- New workflow plugins
- Additional commands and agents
- Enhanced skill libraries
- Documentation improvements

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on project structure, component creation, and development workflow.

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
**Repository:** https://github.com/nikhilmaddirala/gtd-cc

