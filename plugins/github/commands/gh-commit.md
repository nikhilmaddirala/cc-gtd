---
name: gh-commit
description: Create a git commit
---

## Overview

This command helps you create well-formatted Git commits that follow conventional commit standards. It ensures your commit messages are clear, structured, and provide context for future maintainers reviewing your changes.

## Required Information

- **Commit Type**: feat, fix, docs, style, refactor, test, or chore
- **Scope**: The area or component being changed (optional but recommended)
- **Subject**: Brief description of the change (50 characters or less)
- **Body**: Detailed explanation of what and why (optional but recommended for non-trivial changes)
- **Issue Reference**: GitHub issue number if applicable (optional)

## Prerequisites

- You have changes staged or ready to commit
- You're in the correct Git branch (feature branch, not main)
- Your Git user is configured with `git config user.name` and `git config user.email`
- You're committing from the worktree or isolated development environment

## Workflow Process

1. **Change Verification**: Confirm you have changes staged for commit
2. **Commit Type Selection**: Choose the appropriate commit type
3. **Scope Definition**: Specify the component or file area being changed
4. **Message Crafting**: Write clear subject line and detailed body
5. **Issue Linking**: Reference the GitHub issue number if applicable
6. **Commit Creation**: Create the commit with formatted message
7. **Verification**: Display commit hash and confirmation

## Expected Outputs

- Git commit with conventional commit format message
- Commit hash for reference in PR and discussions
- Confirmation of committed changes
- Link to the related GitHub issue in commit message

## Common Issues & Solutions

- **"Nothing staged to commit"**: Run `git add <files>` first to stage changes
- **"Subject too long"**: Keep subject to 50 characters maximum. Put details in body.
- **"Scope unclear"**: Use the component or file name as scope (e.g., `github: gh-plan.md`)
- **"Issue number missing"**: Add `Closes #123` in the commit body to auto-link
- **"Wrong branch"**: Check `git branch` to verify you're on the feature branch, not main

## Typical Usage

Create a commit for your changes:

```bash
/gh-commit
```

Then follow prompts to:
- Select commit type (feat/fix/docs/etc.)
- Enter the scope or component
- Write the subject line
- Add detailed body (optional)
- Reference the issue number

## Commit Message Format

The command follows conventional commit format:

```
<type>(<scope>): <subject>

<body>

Closes #<issue-number>
```

Example:
```
feat(gh-plan): enhance plan command with user guidance

Add comprehensive documentation to the gh-plan command including
required information, prerequisites, workflow process, and common
issues with solutions.

Closes #9
```

Use the github-gtd skill and follow its commit-workflow exactly as written.
