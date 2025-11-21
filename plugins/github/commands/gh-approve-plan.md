---
name: gh-approve-plan
description: Review AI's implementation plan and approve or request revisions
---

## Overview

This command guides you through reviewing AI-generated implementation plans. It provides a structured decision framework for approving plans, requesting revisions, or asking clarifying questions. This is a human-in-the-loop checkpoint in the workflow that ensures architectural decisions are sound before development begins.

## Required Information

- **GitHub Issue URL**: The issue with the plan to review
- **Plan Assessment**: Have you reviewed the architecture and approach?
- **Decision**: Approve, request revisions, or ask questions?
- **Feedback**: Specific feedback or concerns about the plan (if requesting changes)

## Prerequisites

- Issue exists with `needs plan approval` label
- Implementation plan has been posted as a GitHub comment
- You have read access to the issue and comments
- You understand the project architecture and requirements
- You have authority to approve implementation approaches

## Workflow Process

1. **Plan Retrieval**: Fetch and display the implementation plan from the issue
2. **Plan Review**: Present plan content for your evaluation
3. **Decision Prompts**: Ask if you approve, want changes, or need clarification
4. **Feedback Capture**: Collect specific feedback if requesting revisions
5. **Documentation**: Post your decision as a GitHub comment
6. **Status Update**: Update issue label based on decision (approved or back to planning)
7. **Confirmation**: Confirm next workflow step

## Expected Outputs

- GitHub comment with your approval decision or feedback
- Updated issue label (either `needs implementation` or back to `needs planning`)
- Clear guidance on next steps
- Documentation of decision rationale (if helpful)

## Common Issues & Solutions

- **"Can't find the plan"**: Ensure you're looking at the correct issue with the plan posted as a comment.
- **"Plan is unclear"**: Post a comment asking for clarification. Use `/gh-approve-plan` again after revisions.
- **"Multiple issues with the plan"**: List all concerns in your feedback. The planning process will address them.
- **"Not sure if approach is right"**: Ask questions as comments. The AI can provide more detail or options.
- **"Issue label missing"**: Verify the issue has `needs plan approval` label. Manually add it if needed.

## Typical Usage

Review and approve an implementation plan:

```bash
/gh-approve-plan
```

Then follow prompts to:
- Enter the GitHub issue URL
- Review the generated plan details
- Decide: Approve, revise, or ask questions
- Provide feedback if needed

## Approval Criteria

You should approve a plan when:
- Architecture is sound and consistent with project patterns
- Implementation approach is realistic and manageable
- Estimated effort is reasonable
- All acceptance criteria will be addressed
- No critical risks are unmitigated

Use the github-gtd skill and follow its approve-plan-workflow exactly as written.
