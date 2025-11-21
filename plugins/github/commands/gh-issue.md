---
name: gh-issue
description: Create well-structured GitHub issues with clear requirements and acceptance criteria
---

## Overview

This command transforms user requests or feature ideas into well-documented GitHub issues that follow GTD principles. It helps structure issues with clear problem statements, acceptance criteria, context, and appropriate workflow labels for the 7-stage implementation workflow.

## Required Information

- **Issue Title**: Clear, descriptive title for the issue (5-10 words)
- **Issue Description**: Detailed problem statement or feature request
- **Issue Type**: Choose from feature, bug, refactor, or docs
- **Acceptance Criteria**: Success conditions for completing the issue
- **Context**: Background information and related issues (if applicable)

## Prerequisites

- Repository has been initialized with gtd-cc labels (`/gh-repo` completed)
- You have write access to create issues in the repository
- GitHub repository is set up with workflow labels
- You can describe the issue clearly

## Workflow Process

1. **Title & Description Capture**: Gather issue title and detailed description
2. **Type Classification**: Classify issue as feature, bug, refactor, or docs
3. **Acceptance Criteria Definition**: Help define clear success conditions
4. **Context Gathering**: Collect related context and background information
5. **Issue Creation**: Create GitHub issue with structured format
6. **Label Application**: Apply appropriate type and workflow labels
7. **Confirmation**: Display issue URL and next steps

## Expected Outputs

- New GitHub issue with clear structure and formatting
- Automatic `needs planning` label for workflow tracking
- Issue URL for reference in discussions and commits
- Recommendations for the next workflow step (planning)

## Common Issues & Solutions

- **"Title too vague"**: Make it more specific. Instead of "Fix bug", use "Fix authentication failure on login with 2FA enabled"
- **"Acceptance criteria missing"**: Define what success looks like. What will be true when this issue is complete?
- **"Repository not found"**: Verify you're in the correct repository directory and it has GitHub remote configured.
- **"Authentication failed"**: Run `gh auth login` to authenticate GitHub CLI with your account.
- **"No permission to create issues"**: Ensure you have write access to the repository.

## Typical Usage

Create a new issue with clear requirements:

```bash
/gh-issue
```

Then answer prompts about:
- What is this issue about?
- What type of work is it (feature/bug/refactor/docs)?
- What are the acceptance criteria?

Use the github-gtd skill and follow its issue-creation-workflow exactly as written.
