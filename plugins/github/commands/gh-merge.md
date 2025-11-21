---
name: gh-merge
description: Merge approved PR, close issue, and clean up branch and worktree
---

## Overview

This command completes the workflow by merging approved pull requests to the main branch, closing the associated issue, and cleaning up development artifacts (feature branches and worktrees). It's the final stage that makes the implementation live and ensures repository hygiene.

## Required Information

- **Pull Request URL**: The approved PR to merge (e.g., `https://github.com/owner/repo/pull/123`)
- **Merge Strategy**: Squash, rebase, or merge commit (auto-selected based on conventions)

## Prerequisites

- Pull request has `approved for merge` label
- Pull request has been reviewed and approved
- All CI/CD checks are passing
- No merge conflicts
- You have write access to merge PRs to main branch
- You have Git configured locally

## Workflow Process

1. **Approval Verification**: Confirm PR has `approved for merge` label
2. **PR Details**: Fetch and display PR and issue information
3. **Merge Preparation**: Verify no conflicts and all checks pass
4. **PR Merge**: Merge pull request to main branch
5. **Issue Closure**: Close the associated GitHub issue
6. **Branch Cleanup**: Delete the feature branch
7. **Worktree Cleanup**: Remove the local worktree directory
8. **Confirmation**: Display confirmation and summary

## Expected Outputs

- PR merged to main branch with merge commit
- Associated GitHub issue closed
- Feature branch deleted from remote and local
- Worktree directory removed
- Merge summary with commit information

## Common Issues & Solutions

- **"PR not approved"**: Ensure PR has `approved for merge` label. Complete approval process first.
- **"Merge conflicts"**: Resolve conflicts before merging. Rebase feature branch on latest main.
- **"CI checks failing"**: Fix failing checks before merging. Run tests and linting locally.
- **"Worktree locked"**: Ensure no active development in the worktree. Close any editors/IDEs first.
- **"No permission to merge"**: Verify you have write access to the repository.

## Typical Usage

Merge an approved pull request and close the issue:

```bash
/gh-merge
```

Then follow prompts to:
- Enter the GitHub pull request URL
- Confirm merge strategy
- Approve final merge
- Watch cleanup process complete

## Post-Merge Verification

After merging, verify:
- PR is marked as merged on GitHub
- Issue is closed and shows merged status
- Changes appear in main branch
- Feature branch is deleted
- Worktree is cleaned up

## Cleanup Details

The merge process will:
- Delete feature branch from GitHub (if applicable)
- Prune local Git worktrees
- Remove working directory files
- Update local main branch reference
- Remove any temporary files created during development

Use the github-gtd skill and follow its merge-workflow exactly as written.
