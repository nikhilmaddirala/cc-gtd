---
description: Set up repo specific claude code workflows 
---

## Overview

Analyze a specific repository to understand its domain, technologies, and common development operations. Based on this analysis, propose custom skills, commands, and agents to be added to that repository's local .claude/ directory. These components are repository-specific, complementing the generic github-gtd workflows with domain expertise unique to each project. For example, a package manager repository might propose a "publish-package-skill" or "/version-bump" command, while a documentation site might propose a "content-generation-skill" or "/add-doc-page" command.

## Context

You are analyzing the repository in the current working directory. Check the existing state of the .claude/ directory infrastructure:

```bash
# Check current repository
echo "Repository: $(pwd)"
echo "Current branch: $(git branch --show-current 2>/dev/null || echo 'No branch')"

# Check existing .claude/ structure
echo -e "\n=== Existing .claude/ Structure ==="
if [ -d ".claude" ]; then
  find .claude -type f -name "*.md" | sort
else
  echo "No .claude/ directory found - first time setup"
fi

# Check key repository files
echo -e "\n=== Repository Files ==="
ls -la README.md CONTRIBUTING.md package.json Cargo.toml requirements.txt 2>/dev/null | awk '{print $NF}' || echo "Some key files not found"

# Check CI/CD workflows
echo -e "\n=== CI/CD Workflows ==="
if [ -d ".github/workflows" ]; then
  ls -la .github/workflows/ | grep -E "\.yml|\.yaml" | wc -l
else
  echo "No .github/workflows/ found"
fi
```

## Your Task

Goal: Analyze the current repository's domain, technologies, and workflows to generate a comprehensive set of recommendations for custom .claude/ directory components (skills, commands, and agents) tailored to this project's specific needs.

Target: The repository in the current working directory (cwd).

Supports both scenarios:
- **First-time setup**: Create .claude/ directory structure and initialize with recommendations
- **Updating existing setup**: Add to or modify existing .claude/ structure with new recommendations

Role: This is a standalone workflow that establishes or evolves repository-specific automation infrastructure. Run once during initial setup or periodically (e.g., quarterly) to identify new automation opportunities as the project evolves.

### Process

1. **Understand Repository Domain and Technologies**
   - Verify this is a git repository (check .git directory exists)
   - Determine the repository type (library, application, tool, framework, monorepo, etc.)
   - Identify primary technologies, languages, and frameworks
   - Review README.md and CONTRIBUTING.md to understand project goals and development model
   - Examine package.json, Cargo.toml, requirements.txt, or equivalent dependency files
   - Understand the build, test, and deployment architecture

2. **Analyze Common Operations and Workflows**
   - Review recent commit history to identify patterns in common tasks developers perform
   - Examine CI/CD pipeline configuration (.github/workflows/, .gitlab-ci.yml, etc.) to understand automated processes
   - Look for operations mentioned in README or CONTRIBUTING that are manual or repetitive
   - Identify domain-specific concepts unique to this project (e.g., package versioning, schema migrations, content publishing)
   - Check for existing .claude/ directory content to understand current automation

3. **Identify Workflow Gaps and Opportunities**
   - Compare against operations that are typically automated in similar projects
   - Find repetitive developer tasks that could benefit from automation
   - Identify operations that are documented but require multiple manual steps
   - Recognize domain-specific workflows that would benefit from Claude Code support
   - Assess which gaps would provide the most value for development velocity

4. **Design Custom Components**
   - **Skills**: Domain expertise components that provide specialized knowledge (e.g., "api-versioning-skill", "database-migration-skill")
   - **Commands**: Interactive workflows for complex operations (e.g., "/create-release", "/add-migration")
   - **Agents**: Autonomous components for background tasks (e.g., "dependency-updater-agent")
   - Ensure proposed components complement github-gtd workflows without duplication
   - Prioritize components by development impact and implementation effort

5. **Create Implementation Recommendations and Setup .claude/ Structure**
   - Document each proposed component with: name, description, purpose, location in .claude/ directory
   - Provide markdown structure templates for how each component should be organized
   - Explain how each component integrates with existing github-gtd workflows
   - Estimate implementation effort for each component
   - Prioritize recommendations into High/Medium/Low impact categories

   **For first-time setup:**
   - Create .claude/ directory structure if it doesn't exist
   - Initialize standard subdirectories: .claude/skills/, .claude/commands/, .claude/agents/
   - Add .claude/ to .gitignore if not already present

   **For updating existing setup:**
   - Review existing .claude/ structure to understand current customizations
   - Propose additions or modifications that complement existing components
   - Avoid overwriting existing customizations without user approval

   - Create a structured recommendations document for user review and implementation

### Guidelines

- Focus on repository-specific operations, not generic GitHub workflows already covered by github-gtd (issues, PRs, merges, releases)
- Look for operations mentioned in README, CONTRIBUTING, or documentation that are manual or multi-step
- Consider the repository's domain and development patterns when proposing components
- Ensure proposed components complement github-gtd, not duplicate it
- Prioritize high-impact, low-effort automation opportunities
- Balance automation with maintainability - don't over-engineer simple tasks
- Document assumptions about the repository's structure and workflows
- If no unique patterns are found, document that github-gtd workflows alone may be sufficient
- **Non-destructive approach**: Never overwrite existing .claude/ customizations without user approval
- **Support both scenarios**: Handle first-time setup (create structure) and updates (enhance existing) gracefully
- **Idempotent workflow**: This workflow should be safe to run multiple times without causing problems

## Success Criteria

Your work is complete when:
- ✅ Verified this is a git repository in the current working directory
- ✅ Checked existing .claude/ structure (first-time or update scenario identified)
- ✅ Repository type, domain, and primary technologies are clearly identified
- ✅ Common development operations and workflows are catalogued
- ✅ Repository-specific automation gaps are identified and documented
- ✅ Custom skills, commands, and agents are proposed with clear rationale
- ✅ Proposed components show how they integrate with github-gtd workflows
- ✅ Implementation effort and impact prioritization is provided

- ✅ **For first-time setup**: .claude/ directory structure created with subdirectories (skills, commands, agents)
- ✅ **For update scenario**: Existing customizations respected, no overwrites without approval
- ✅ A structured recommendations document is generated with markdown structure templates
- ✅ The recommendations document is provided to the user for review and implementation

## Error Handling

If you encounter the following issues, address them as indicated:

**Issue: Not in a git repository**
- Solution: Cannot proceed - stop and inform user they must run this workflow from within a git repository root
- Guide user to navigate to the repository directory (cd /path/to/repo) and run the workflow again
- Verify the current directory has a .git folder

**Issue: Insufficient information to analyze repository**
- Solution: Document what files/information were accessible and what was not
- Make recommendations based on available information
- Note assumptions in the generated recommendations document
- Suggest the user review for accuracy

**Issue: No unique patterns or specialized workflows identified**
- Solution: Document that the repository appears to follow standard development practices
- Recommend that generic github-gtd workflows are sufficient for this project
- Suggest revisiting periodically as the project evolves
- Note specific areas where repo-specific automation could be added in the future

**Issue: Repository is too simple or follows standard conventions exactly**
- Solution: This is valid - document that existing plugins and generic workflows provide sufficient automation
- Recommend standard development practices from github-gtd

**Issue: Overwriting existing .claude/ customizations**
- Solution: Never overwrite existing .claude/ files without explicit user approval
- Review existing components and propose additions/modifications that respect current setup
- If updating, clearly mark what's new vs. what's being modified
- Suggest user review changes before implementation

## Output Structure Templates

The recommendations document you generate should follow this markdown structure. You provide these templates to help the user understand and implement your recommendations:

```markdown
# Custom Workflow Recommendations for [Repository Name]

## Repository Analysis

- Type: [Library/Application/Framework/Tool/Monorepo/Other]
- Primary Technology: [Language/Framework]
- Key Dependencies: [Major frameworks/tools]
- Identified Operations: [Bulleted list of common workflows]

## Proposed Skills

### [skill-name-description]
- **File location**: `.claude/skills/[skill-name]/SKILL.md`
- **Purpose**: [What domain knowledge this skill provides]
- **Rationale**: [Why this skill is needed based on repository analysis]
- **Integration**: [How it works with github-gtd workflows]
- **Effort estimate**: [Low/Medium/High]

## Proposed Commands

### [/command-name]
- **File location**: `.claude/commands/[command-name].md`
- **Purpose**: [What interactive workflow it provides]
- **Rationale**: [Why this command would improve developer workflows]
- **Integration**: [How it works with github-gtd workflows]
- **Effort estimate**: [Low/Medium/High]

## Proposed Agents

### [agent-name]
- **File location**: `.claude/agents/[agent-name].md`
- **Purpose**: [What autonomous task it performs]
- **Rationale**: [Why this agent would improve development automation]
- **Trigger conditions**: [When/how it runs]
- **Effort estimate**: [Low/Medium/High]

## Implementation Priority

### High Impact
[Components that provide immediate value and should be implemented first]

### Medium Impact
[Nice-to-have components that add value but are less critical]

### Low Impact
[Future considerations or components for specific scenarios]

## Next Steps

[Guidance for implementing the proposed components using the templates above]
```
