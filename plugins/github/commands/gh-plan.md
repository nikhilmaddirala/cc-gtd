---
name: gh-plan
description: Develop detailed implementation plans with options analysis for GitHub issues
---

## Overview

This command creates comprehensive implementation plans for GitHub issues by analyzing the codebase, researching implementation approaches, evaluating options, and providing detailed recommendations with pros/cons for each approach. It bridges the gap between issue requirements and actual code implementation.

## Required Information

- **GitHub Issue URL**: The issue you want to plan (e.g., `https://github.com/owner/repo/issues/123`)
- **Complexity Assessment**: Simple, Medium, or Complex (based on scope)
- **Research Requirements**: Whether external research is needed (yes/no)
- **Implementation Timeline**: Expected duration if known

## Prerequisites

- Repository has been initialized with gtd-cc labels (`/gh-repo` completed)
- Issue exists and has `needs planning` label
- You have read access to the repository code
- You understand the issue requirements
- Internet connectivity for codebase analysis

## Workflow Process

1. **Issue Analysis**: Extract and understand requirements from the GitHub issue
2. **Codebase Research**: Analyze existing patterns, similar implementations, and relevant code
3. **Options Analysis**: Research and evaluate 2-3 implementation approaches
4. **Architecture Design**: Document recommended architecture and design patterns
5. **Plan Generation**: Create detailed implementation plan with breakdown
6. **Risk Assessment**: Identify potential issues and mitigation strategies
7. **Documentation**: Post plan as GitHub issue comment with formatting
8. **Approval Decision**: Determine if human approval is needed based on complexity

## Expected Outputs

- Detailed implementation plan posted as GitHub comment
- Architecture recommendations with pros/cons
- Step-by-step breakdown of required changes
- Effort estimates and timeline
- Risk assessment and mitigation strategies
- Clear list of deliverables and acceptance criteria

## Common Issues & Solutions

- **"Issue not found"**: Verify the issue URL and repository access. Check that the issue exists.
- **"Complexity unclear"**: Default to Medium complexity for unknown scope. You can adjust after analysis.
- **"Codebase too large"**: Focus on the most relevant files. AI will prioritize based on the issue scope.
- **"Analysis timeout"**: Proceed with available information and note any research gaps in the plan.
- **"Issue not in needs planning"**: Verify the issue has the `needs planning` label. Run `/gh-repo` to set up labels.

## Typical Usage

Plan an issue to understand implementation approach:

```bash
/gh-plan
```

Then follow prompts to:
- Enter the GitHub issue URL
- Assess the complexity level
- Specify if research is needed
- Review the generated plan

## Next Steps

After planning:
- If plan is simple: Apply `needs implementation` label and move to building
- If plan is complex: It may request human approval with `needs plan approval` label
- You can review the plan and request revisions if needed

Use the github-gtd skill and follow its plan-workflow exactly as written.
