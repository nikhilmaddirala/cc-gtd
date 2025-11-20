---
name: gh-repo
description: Sets up workflow labels and worktree directory for issue-driven development
---

## Overview

This command initializes a GitHub repository for the GTD (Getting Things Done) 7-stage workflow. It sets up essential infrastructure including workflow labels, issue templates, PR templates, branch protection rules, and creates a worktree directory structure for isolated development.

## Required Information

- **Repository URL**: The GitHub repository to set up (e.g., `https://github.com/owner/repo`)
- **Repository Owner**: GitHub username or organization that owns the repo
- **Write Access**: You must have write/admin permissions on the repository

## Prerequisites

- You have a GitHub CLI (gh) configured with authentication
- The repository exists on GitHub
- You have write access to the repository settings
- You have local Git installed and configured
- Internet connection to access GitHub API

## Workflow Process

1. **Repository Verification**: Confirm repository exists and you have write access
2. **Label Creation**: Create all GTD workflow labels (needs planning, needs implementation, in review, etc.)
3. **Issue Template Setup**: Configure issue templates for structured issue creation
4. **PR Template Setup**: Create pull request template for standardized reviews
5. **Branch Protection**: Set up main branch protection rules (if applicable)
6. **Worktree Directory**: Create local directory structure for isolated development environments
7. **Completion**: Confirm successful setup and display next steps

## Expected Outputs

- Confirmation of all labels created in repository
- URLs to issue and PR templates in repository
- Local worktree directory structure created at `./worktree/`
- Setup summary with repository configuration details

## Common Issues & Solutions

- **"No write access"**: Ensure you have admin/write permissions on the repository. Contact the repository owner if needed.
- **"GitHub CLI not authenticated"**: Run `gh auth login` to authenticate GitHub CLI before running this command.
- **"Repository not found"**: Verify the repository URL is correct and the repository exists on GitHub.
- **"Worktree directory exists"**: Remove the existing `./worktree/` directory or use a different path. Run `rm -rf ./worktree/` to clear.
- **"Label creation failed"**: Some labels may already exist. This is normal - the workflow will use existing labels.

## Typical Usage

Run this command once when setting up a new repository:

```bash
/gh-repo
```

Then follow the prompts to specify your repository URL.

Use the github-gtd skill and follow its repo-setup-workflow exactly as written.
