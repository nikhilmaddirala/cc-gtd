---
name: gh-build
description: Autonomous agent that builds code from approved implementation plans or addresses review feedback
---

## Overview

This command autonomously implements approved plans by creating isolated development environments, writing code, running tests, creating documentation, and submitting pull requests ready for review. It bridges the gap between planning and code review by fully implementing the planned changes.

## Required Information

- **GitHub Issue URL**: The issue with approved implementation plan (must have `needs implementation` label)
- **Branch Strategy**: Feature branch or worktree isolation (auto-configured)

## Prerequisites

- Issue has `needs implementation` label (not `needs plan approval`)
- Implementation plan has been created and reviewed
- You have write access to create branches and PRs
- Local Git and development environment are configured
- All required development tools are installed

## Workflow Process

1. **Approval Verification**: Confirm issue has `needs implementation` label
2. **Plan Retrieval**: Fetch the implementation plan from issue comments
3. **Worktree Creation**: Create isolated development environment for changes
4. **Code Implementation**: Write all required code changes per the plan
5. **Test Suite**: Create and run unit tests for new functionality
6. **Documentation**: Update relevant documentation and comments
7. **PR Creation**: Create pull request with implementation details
8. **Label Update**: Update issue to `in review` status
9. **Confirmation**: Display PR URL and next steps

## Expected Outputs

- New feature branch with all code changes
- Isolated worktree directory with implementation
- Pull request with description and link to issue
- Test results and coverage reports
- Updated documentation and code comments
- Issue automatically moved to `in review` status

## Common Issues & Solutions

- **"Issue not approved"**: Ensure issue has `needs implementation` label, not `needs plan approval`.
- **"Plan not found"**: Verify the implementation plan is posted as a comment on the issue.
- **"Tests failing"**: Review test failures and fix code issues. Re-run tests to verify.
- **"Merge conflicts"**: Rebase branch on latest main and resolve conflicts.
- **"Worktree creation failed"**: Ensure no other worktree exists for this branch. Clean up with `git worktree prune`.
- **"PR not created"**: Check GitHub CLI authentication with `gh auth status`.

## Typical Usage

Implement an approved issue:

```bash
/gh-build
```

Then follow prompts to:
- Enter the GitHub issue URL
- Wait for implementation (autonomous process)
- Review the created pull request

## What Gets Built

Based on the implementation plan, the build process will:
- Create or modify source files
- Add tests and test data
- Update configuration files if needed
- Update documentation and README
- Create a well-formatted pull request

Use the github-gtd skill and follow its implementation-workflow exactly as written.
