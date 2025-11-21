---
name: gh-review
description: Code review a pull request
---

## Overview

This command conducts automated code reviews on pull requests, checking for code quality, test coverage, security issues, documentation, and alignment with project conventions. It provides structured feedback to help ensure code meets quality standards before human review.

## Required Information

- **Pull Request URL**: The PR to review (e.g., `https://github.com/owner/repo/pull/123`)
- **Review Focus**: General review or specific area (performance, security, etc.)

## Prerequisites

- Pull request exists and is in `in review` status
- Code has been implemented and tests are passing
- You have read access to the repository code
- You understand the project's code quality standards
- Automated checks (CI/CD) have completed successfully

## Workflow Process

1. **PR Verification**: Confirm PR exists and is open for review
2. **Code Analysis**: Analyze code changes for quality, patterns, and best practices
3. **Test Coverage**: Verify tests are comprehensive and passing
4. **Documentation**: Check that code is documented and follows conventions
5. **Security Review**: Scan for security vulnerabilities or issues
6. **Feedback Generation**: Create detailed review comments with recommendations
7. **Post Results**: Publish review comments on the PR
8. **Status Update**: Update issue status based on review outcome

## Expected Outputs

- Detailed code review comments on the PR
- List of required changes or concerns
- Recommendations for improvements
- Approval or request for revisions
- Summary of review findings

## Common Issues & Solutions

- **"PR not found"**: Verify the PR URL and check that it exists on GitHub.
- **"Tests not passing"**: Request that tests pass before review. Review can note failing tests.
- **"Review takes too long"**: Large PRs may need more time. Break into smaller pieces if possible.
- **"Missing tests"**: Request additional test coverage in review comments.
- **"Code style issues"**: Note style violations; request corrections per project standards.

## Typical Usage

Review a pull request for quality and completeness:

```bash
/gh-review
```

Then follow prompts to:
- Enter the GitHub pull request URL
- Wait for automated review analysis
- Review the generated comments
- Approve or request changes

## Review Criteria

Code should be approved when:
- Tests are passing and coverage is adequate
- No critical security issues detected
- Code follows project patterns and conventions
- Documentation is complete and accurate
- Implementation matches the approved plan

Use the github-gtd skill and follow its review-workflow exactly as written.
