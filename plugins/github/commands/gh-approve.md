---
name: gh-approve
description: Review implementation, test locally, and approve for merge
---

## Overview

This command guides human reviewers through testing code locally, reviewing the implementation against requirements, and approving the pull request for merging. It's the final human checkpoint that ensures the implementation is production-ready before being merged to the main branch.

## Required Information

- **Pull Request URL**: The PR to approve (e.g., `https://github.com/owner/repo/pull/123`)
- **Testing Status**: Have you tested the changes locally?
- **Approval Decision**: Approve for merge or request revisions?
- **Feedback**: Any concerns or feedback about the implementation (if needed)

## Prerequisites

- Pull request exists with `ready for approval` label
- Automated code review has been completed
- You have write access to approve PRs
- You have local development environment set up
- You understand the issue requirements and context

## Workflow Process

1. **PR Details Retrieval**: Fetch and display the pull request information
2. **Requirements Review**: Display the original issue requirements
3. **Implementation Check**: Ask if you've tested the changes locally
4. **Test Instructions**: Provide guidance on running tests locally
5. **Decision Prompts**: Ask if you approve or want revisions
6. **Feedback Capture**: Collect any feedback if requesting changes
7. **Label Update**: Update PR to `approved for merge` or back to `in review`
8. **Confirmation**: Confirm next steps (merge or revision cycle)

## Expected Outputs

- GitHub comment with your approval decision
- Updated issue label (either `approved for merge` or back to `in review`)
- Local test verification results
- Clear guidance on next steps
- Documentation of approval decision

## Common Issues & Solutions

- **"PR not found"**: Verify the PR URL and that it's open on GitHub.
- **"Tests fail locally"**: Note the failures in your feedback. Ask for fixes before approval.
- **"Changes don't match plan"**: Compare PR changes to the approved implementation plan. Note discrepancies.
- **"Not sure about implementation"**: Ask questions as comments. Request clarification before approving.
- **"Performance concerns"**: Test and benchmark locally. Include performance feedback if needed.

## Typical Usage

Test and approve a pull request for merging:

```bash
/gh-approve
```

Then follow prompts to:
- Enter the GitHub pull request URL
- Review the requirements and implementation
- Test the changes locally
- Approve or request revisions

## Local Testing Checklist

Before approving, verify:
- All tests pass locally with `npm test` or `pytest` (as applicable)
- No TypeScript/linting errors
- New features work as described in the PR
- No performance regressions
- Documentation is accurate and complete

## Approval Criteria

Approve the PR when:
- All tests pass locally and in CI/CD
- Code matches the approved implementation plan
- Requirements are fully addressed
- No critical issues or blockers remain
- You have confidence in the solution quality

Use the github-gtd skill and follow its human-approval-workflow exactly as written.
