# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

gtd-cc is a plugin marketplace for Claude Code that provides specialized tools for Getting Things Done (GTD) workflows. It consists of four main plugins:

- **github**: Complete GitHub workflow automation with 7-stage issue-driven development
- **obsidian**: Knowledge management with PARA and Zettelkasten workflows
- **web-research**: Content crawling, analysis, and extraction tools
- **documentation**: Three-layer documentation system for GitHub projects

## Plugin Architecture

This marketplace follows a layered architecture:

- **Skills** - Foundation layer containing domain expertise and reusable knowledge
- **Commands** - Interactive slash commands (`/command-name`) that guide users through workflows
- **Agents** - Autonomous workers that execute complex workflows without human interaction

All components are organized under `plugins/<plugin-name>/` with respective `commands/`, `agents/`, and `skills/` subdirectories.

## Common Development Tasks

### Plugin Installation and Management

Install the marketplace:
```bash
/plugin marketplace add nikhilmaddirala/gtd-cc
```

Install individual plugins:
```bash
/plugin install github@gtd-cc
/plugin install obsidian@gtd-cc
/plugin install web-research@gtd-cc
/plugin install documentation@gtd-cc
```

### Validation and Testing

Validate JSON manifests:
```bash
jq . .claude-plugin/marketplace.json
jq . plugins/<plugin>/.claude-plugin/plugin.json
```

### Creating New Components

**New Command:**
1. Create `plugins/<plugin>/commands/<name>.md` with YAML frontmatter
2. Add to plugin's `.claude-plugin/plugin.json`
3. Test locally with `/command-name`

**New Agent:**
1. Create `plugins/<plugin>/agents/<name>.md` with YAML frontmatter
2. Add to plugin's `.claude-plugin/plugin.json`
3. Document autonomy requirements and error handling

**New Skill:**
1. Create directory `plugins/<plugin>/skills/<skill-name>/`
2. Create comprehensive `SKILL.md` with domain expertise
3. Add to plugin manifest if needed

## Key Workflows

### GitHub 7-Stage Workflow

The github plugin implements a structured workflow:
1. Repository Setup (labels, templates, worktree)
2. Issue Creation (well-structured issues)
3. Planning (research and implementation plans)
4. Plan Approval (human review - conditional)
5. Implementation (isolated development)
6. Code Review (automated and human)
7. Merge & Cleanup (PR merge, branch cleanup)

**Key Commands:**
- `/gh-repo` - Initialize repository
- `/gh-issue` - Create structured issue
- `/gh-plan` - Develop implementation plan
- `/gh-build` - Autonomous code implementation
- `/gh-review` - Code review coordination
- `/gh-all-in-one` - Complete workflow from issue to merge

### Documentation Three-Layer Model

The documentation plugin uses a three-layer approach:
1. **Project README** - High-level overview and quick start
2. **Developer Guide** - Detailed architecture and patterns
3. **Component Documentation** - API docs and code comments

**Key Commands:**
- `/doc-init` - Initialize documentation structure
- `/doc-update` - Update docs for code changes
- `/doc-audit` - Audit documentation health

## File Structure Conventions

### Naming Conventions
- **Commands:** kebab-case, prefixed by plugin (e.g., `gh-issue`, `ob-capture`)
- **Agents:** kebab-case (e.g., `gh-build`, `content-extraction-agent`)
- **Skills:** kebab-case directories with uppercase `SKILL.md`
- **Plugins:** kebab-case directories

### Required Files
- `README.md` in every plugin directory
- `SKILL.md` in every skill directory with YAML frontmatter
- `.claude-plugin/plugin.json` in every plugin directory
- YAML frontmatter in all commands and agents

### JSON Manifest Structure
Each plugin must have a `.claude-plugin/plugin.json` with:
- `name`, `version`, `description`, `author`
- Arrays of `commands`, `agents`, `skills` with relative paths

## Plugin-Specific Notes

### GitHub Plugin
- Implements issue-driven development with strict state management
- Uses worktrees for isolated development environments
- Follows conventional commit message format
- Requires proper label management for workflow states

### Obsidian Plugin
- Integrates with PARA (Projects, Areas, Resources, Archives) methodology
- Supports Zettelkasten note creation and linking
- Includes content extraction from web sources

### Web-Research Plugin
- Uses Crawl4AI for JavaScript-heavy page crawling
- Integrates with Gemini CLI for content analysis
- Supports structured data extraction with schema generation

### Documentation Plugin
- Follows Best README Template patterns
- Provides template generation for CONTRIBUTING and API docs
- Includes compression workflows for quick reference guides

## Development Environment Setup

No special build tools required - this is a documentation and workflow definition project. All components are markdown files with JSON manifests for plugin registration.

## Error Handling Guidelines

- Commands should provide clear error messages and next steps
- Agents should implement graceful degradation and recovery patterns
- Skills should document edge cases and troubleshooting
- All components should maintain context across workflow stages