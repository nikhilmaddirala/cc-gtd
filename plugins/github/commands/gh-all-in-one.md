---
name: gh-all-in-one
description: All in one end to end github workflow from new issue to implementation and merging PR
---

## Overview

This command executes the complete 7-stage GitHub workflow from issue creation through implementation, review, and merge. It's the most comprehensive workflow for teams that want to automate the entire issue-driven development lifecycle without manual stage transitions.

## Required Information

- **Issue Description**: Clear problem statement or feature request
- **Repository URL**: GitHub repository where work will be tracked
- **Implementation Timeline**: Expected duration or deadlines
- **Review Requirements**: Any specific quality or testing standards

## Prerequisites

- GitHub repository is initialized with gtd-cc labels (`/gh-repo` completed)
- You have write access to create issues and pull requests
- You have administrator access or branch protection knowledge
- Local development environment is ready
- GitHub CLI is authenticated and configured

## Workflow Process

1. **Repository Setup**: Initialize labels and worktree (if not already done)
2. **Issue Creation**: Create well-structured GitHub issue with requirements
3. **Planning**: Develop comprehensive implementation plan with options analysis
4. **Plan Approval**: Review and approve the plan (if complex)
5. **Implementation**: Autonomously build code from approved plan
6. **Code Review**: Automated review of implementation quality
7. **Human Approval**: Manual review and testing of changes
8. **Merge & Cleanup**: Merge to main and clean up branches and worktrees

## Expected Outputs

- New GitHub issue fully documented with acceptance criteria
- Implementation plan with architecture recommendations
- Feature branch with all code changes and tests
- Pull request with comprehensive description
- Merged changes on main branch
- Closed issue with deployment status
- Cleaned up branches and development artifacts

## Common Issues & Solutions

- **"Process too slow"**: Complex issues may take time. Use intermediate stages `/gh-plan` and `/gh-review` for better control.
- **"Plan not approved"**: Review feedback and request revisions using `/gh-approve-plan` before building.
- **"Tests failing"**: Return to implementation stage. Fix issues and create new PR.
- **"Merge conflicts"**: Rebase feature branch on latest main before merging.
- **"Worktree locked"**: Close any editors/IDEs using the worktree directory.

## Typical Usage

Execute the complete workflow from issue to merge:

```bash
/gh-all-in-one
```

Then follow the interactive prompts through all 7 stages:
- Create issue
- Plan implementation
- Approve plan (if needed)
- Build implementation
- Review code
- Approve for merge
- Merge and cleanup

## Workflow Timeline

Typical end-to-end execution:
- Simple features: 1-2 hours
- Medium features: 4-8 hours
- Complex features: 8+ hours (may require multiple review cycles)

## When to Use This Command

Use `/gh-all-in-one` when:
- You want fully automated issue-to-merge workflow
- All team members trust the process
- No major architectural decisions needed
- You prefer hands-off implementation

For more control, use individual stage commands:
- `/gh-issue` then `/gh-plan` then `/gh-build`, etc.

Use the github-gtd skill and follow it exactly as written. Go through the end to end workflow including all stages with the user. 
