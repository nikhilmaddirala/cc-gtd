---
description: Initialize documentation structure for new or existing projects
---

## Initialization Workflow

Set up proper documentation structure for a project, choosing the right documentation layer based on project maturity.

## Overview

This workflow guides you through choosing and implementing the appropriate documentation layer for your project. It helps prevent documentation that's either too minimal or unnecessarily complex.

## Context

Before starting:

- Understand your project size (solo dev, small team, large team)
- Know what exists currently (no docs, just README, scattered docs)
- Identify primary users (developers, end users, both)
- Consider maintenance capacity

## Your Task

- Goal: Establish proper documentation structure
- Target: Create README.md or folder structure based on project phase
- Role: Ensure documentation grows with project, not all at once

### Process

1. **Assess Current State**

```bash
# Check what documentation currently exists
ls -la | grep -i readme
find . -name "README.md" -o -name "CONTRIBUTING.md" | head -20
ls -la docs/ 2>/dev/null || echo "No /docs folder"
```

2. **Determine Project Phase**

Answer these questions to choose your phase:

- How many people work on this? (Solo = Phase 1, 2-5 = Phase 2, 5+ = Phase 3)
- How many distinct modules/components? (1 = Phase 1, 2-3 = Phase 2, 4+ = Phase 3)
- Do contributors need to understand local structure? (No = Phase 1, Yes = Phase 2-3)
- Is architecture complex? (No = Phase 1-2, Yes = Phase 3)
- Multiple tutorials needed? (No = Phase 1-2, Yes = Phase 3)

**Phase 1: Small Project**
- Use if: Solo developer, simple scripts/MVP, <1000 lines of code
- Create: README.md only

**Phase 2: Medium Project**
- Use if: 2-3 modules, 2+ developers, established project
- Create: README.md + directory READMEs in key folders

**Phase 3: Growing Project**
- Use if: Complex architecture, multiple teams, 4+ major components
- Create: README.md + directory READMEs + /docs folder with deep content

3. **Create Root README.md (All Phases)**

```bash
# Check if README exists
test -f README.md && echo "README exists" || echo "Creating README"
```

If no README, create with this template:

```markdown
# Project Title

One-line description of what this does.

## About

[2-3 paragraphs explaining the problem, solution, and why it matters]

## Built With

- Technology 1
- Technology 2
- Framework 3

## Getting Started

### Prerequisites

```
node >= 16
npm >= 8
```

### Installation

```bash
git clone <repo>
cd <project>
npm install
```

### Quick Start

```bash
npm run dev
```

## Usage

[Show minimal examples of common tasks]

## Contributing

See [CONTRIBUTING.md](./docs/contributing.md) for guidelines.

## License

[License type - e.g., MIT]

## Contact

[Your name, email, or links]
```

4. **Phase 2: Add Directory READMEs**

If choosing Phase 2, identify 2-3 key directories that need explanation:

```bash
# Find main directories to document
ls -d src/* 2>/dev/null | head -5
ls -d packages/* 2>/dev/null | head -5
```

For each directory, create README.md:

```markdown
# [Directory Name]

## Overview

[1-2 sentences explaining what this directory contains]

## Structure

- FileA.js — description
- FileB.js — description
- subfolder/ — description

## Key Patterns

[How to extend this component, naming conventions, common gotchas]

## Related Docs

- ../README.md
- ../../docs/architecture.md
```

5. **Phase 3: Create /docs Folder**

If choosing Phase 3, create structure:

```bash
mkdir -p docs/tutorials docs/diagrams
```

Create `/docs/index.md`:

```markdown
# Project Documentation

Welcome. Start here for detailed guides.

## Quick Links

- [Getting Started](tutorials/getting-started.md)
- [Architecture](architecture.md)
- [API Reference](api_reference.md)
- [Contributing](contributing.md)

## For Contributors

- [Architecture Overview](architecture.md)
- [Development Setup](tutorials/getting-started.md)
- [Code Guidelines](contributing.md)

## Reference

- [Configuration](configuration.md)
- [Troubleshooting](troubleshooting.md)
```

Create `docs/architecture.md`:

```markdown
# Architecture Overview

## System Design

[Explain the major components and how they interact]

## Component Descriptions

[Detail each major component's responsibility]

## Data Flow

[Show how data moves through the system]

## Deployment

[How the system is deployed and scaled]
```

6. **Update Root README to Link to Docs (Phase 3 only)**

Add section to README:

```markdown
## Documentation

For detailed guides and references, see [docs/](docs/index.md):

- [Getting Started](docs/tutorials/getting-started.md)
- [Architecture](docs/architecture.md)
- [API Reference](docs/api_reference.md)
```

7. **Create .gitignore Entries (If Needed)**

Add generated documentation if applicable:

```bash
# Example: if generating docs from code
echo "docs/generated/" >> .gitignore
echo "docs/api/" >> .gitignore
```

8. **Initial Commit**

```bash
git add README.md docs/ [directory READMEs]
git commit -m "docs: initialize documentation structure for [project]"
```

## Organizing Content Across Layers

When creating documentation, follow structure rules from SKILL.md:

### Basic Structure Rules

1. **One fact, one place** - Never duplicate. Link to authoritative source.
2. **Layer by audience** - README for everyone, directory READMEs for maintainers, /docs for deep dives
3. **README should be short** - Keep under 500 lines, move large sections to /docs
4. **Directory READMEs are local** - Explain module context, don't repeat README
5. **Link between layers** - Create clear navigation from README → /docs → directories

### What Goes Where

**README.md:**
- Project title and one-line description
- About/motivation section
- Tech stack
- Quick start (installation + hello world)
- Links to deeper documentation
- License and contact

**Directory READMEs (Phase 2+):**
- What's in this folder
- Folder structure explanation
- How to extend it
- Local conventions

**/docs (Phase 3):**
- Getting started tutorials
- Architecture and design decisions
- Configuration reference
- Complete API documentation
- Troubleshooting guides
- Contribution guidelines

### Directory README Template

Create README.md in key directories:

```markdown
# [Folder Name]

Brief description of what this folder contains.

## Structure

- FileA — description
- FileB — description
- subfolder/ — description

## How to Extend

Steps for adding new content to this folder.

## Related Documentation

- [Architecture](../../docs/architecture.md)
- [API Reference](../../docs/api-reference.md)
```

## Guidelines

- Start with README only if truly small project (solo dev, <1000 LOC)
- Add directory READMEs as soon as you find yourself explaining folder structure
- Move to /docs when README exceeds 500 lines or you have multiple tutorials
- Document as you code, not after the fact
- Avoid documenting what's obvious from code - explain *why* not *what*
- Follow structure rules from SKILL.md to avoid duplication

## Success Criteria

- ✅ README.md exists and explains project clearly
- ✅ Each directory README explains its purpose (if Phase 2+)
- ✅ /docs folder exists with index.md (if Phase 3)
- ✅ Table of contents works (all links valid)
- ✅ Quick start instructions work end-to-end
- ✅ Architecture is explained at appropriate level
- ✅ Contributors know where to find information
- ✅ No duplication across layers
- ✅ Clear navigation between layers
