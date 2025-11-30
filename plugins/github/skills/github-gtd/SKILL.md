---
name: github-gtd
description: GitHub workflow automation skill for issue-driven development with planning, implementation, review, and merge workflows.
---

# GitHub GTD Workflow Skill

This skill provides guidance for executing GitHub workflows used in issue-driven development. It serves as the authoritative source for all GitHub workflow operations.

## About This Skill

The GitHub GTD skill facilitates structured issue-driven development workflows, encompassing repository initialization, issue creation, planning, implementation, review, and merge operations. This skill consolidates procedural knowledge, best practices, and detailed workflow instructions used across interactive commands and autonomous agents.

### When to Use This Skill

This skill should be used when:
- Setting up a new repository for issue-driven development
- Creating well-structured GitHub issues
- Developing implementation plans with analysis
- Reviewing and approving implementation approaches
- Implementing approved plans in isolated development environments
- Performing code reviews on implementations
- Reviewing and approving implementations locally
- Merging approved PRs and cleaning up development artifacts
- Committing changes with conventional commit messages

## Available Workflows

This skill provides detailed guidance for the following workflows:

- **Repository Setup** - Configure labels, templates, and worktree structure (one-time setup)
- **Issue Creation** - Transform user request into well-structured issue
- **Planning** - Research codebase, analyze options, create implementation plan
- **Plan Approval** - Human reviews and approves (or revises) implementation approach (conditional)
- **Implementation** - Write code in isolated worktree, create PR with tests
- **Code Review** - Review code for quality, security, completeness
- **Human Approval** - Human tests locally, reviews code, approves for merge
- **Merge & Cleanup** - Merge PR, close issue, delete branch and worktree
- **Git Commits** - Create well-structured git commits with conventional commit format

### Workflow Labels

**Status labels** (track issue progress through planning and implementation):
- `status-planning-todo` - Requires implementation plan
- `status-planning-review` - Plan is under review (conditional stage)
- `status-planning-done` - Planning completed, ready for implementation
- `status-implementation-todo` - Ready for coding
- `status-implementation-review` - Implementation under review
- `status-implementation-done` - Implementation completed, ready to merge
- `blocked` - Work stopped, needs intervention

**Type labels** (categorize issue):
- `type-feature` - New functionality
- `type-bug` - Defect or unexpected behavior
- `type-docs` - Documentation changes
- `type-refactor` - Code improvements without behavior change

## Individual Workflow Guides

Each workflow provides detailed procedural instructions in its respective markdown file:

### Repository Setup
**File**: `workflows/repo-setup.md`

Sets up essential GitHub workflow infrastructure in the current repository, including workflow labels, issue templates, PR templates, branch protection rules, and worktree directory structure.

**Use this when**: Setting up a new repository for the first time

### Issue Creation
**File**: `workflows/issue-creation.md`

Transforms user requirements into well-documented GitHub issues with clear problem statements, acceptance criteria, context, and appropriate labels.

**Use this when**: Creating new issues to track work

### Planning
**File**: `workflows/plan.md`

Develops focused implementation plans through codebase research, options analysis, and technical approach definition. Includes self-assessment logic to determine if human approval is needed.

**Use this when**: Planning how to implement an issue

### Plan Approval (Conditional)
**File**: `workflows/approve-plan.md`

Guides humans through reviewing AI-generated implementation plans. Provides decision framework for approval, revision requests, or questions.

**Use this when**: Human needs to review an implementation plan (only triggered when AI requests approval)

### Implementation
**File**: `workflows/implementation.md`

Autonomously implements approved plans by creating worktrees, writing code, running tests, and creating draft PRs ready for review.

**Use this when**: Building code from an approved implementation plan

### Code Review
**File**: `workflows/review.md`

Performs code reviews focusing on compliance with requirements, README guidelines, significant bugs, and architectural alignment. Filters for real issues only.

**Use this when**: Reviewing a pull request for quality and correctness

### Human Approval
**File**: `workflows/human-approval.md`

Guides humans through local testing, code review, and approval decision-making for implementations ready for merge.

**Use this when**: Human needs to test and approve an implementation

### Merge & Cleanup
**File**: `workflows/merge.md`

Executes final merge operations: squash-merges PR to main, closes issue, deletes branch, and removes worktree.

**Use this when**: Merging an approved implementation to main

### Git Commits
**File**: `workflows/commit.md`

Creates well-structured git commits with conventional commit format, describing changes with clear intent.

**Use this when**: Committing changes to the repository

## How to Use This Skill

When this skill is referenced by a command or agent:

1. **Read the workflow file** for the appropriate workflow (see list above)
2. **Follow the process steps** as written in the workflow
3. **Reference guidelines and success criteria** to ensure quality
4. **Execute the operations** (usually bash/git/gh commands embedded in workflow)

## Key Principles

**Single Source of Truth**: This skill and its workflow files contain all procedural knowledge for GitHub operations. Commands reference this skill rather than containing inline instructions.

**Workflow Progression**: Each workflow has clear entry conditions (labels/requirements) and exit conditions (what gets updated).

**Conditional Workflows**: Plan Approval is conditional—it only occurs when AI explicitly requests human input.

**Autonomous Execution**: Implementation, Review, and Merge workflows are designed for autonomous agent execution with minimal human interaction, while other workflows may require human input.

**Quality Assurance**: Each workflow has success criteria and error handling guidelines to maintain workflow integrity.

## Workflow Dependencies

- **Repository Setup must run first**: Repository needs labels and worktree directory before subsequent workflows
- **Issue Creation and Planning are sequential**: Issues need clear definition before planning
- **Planning and Plan Approval are conditional**: Planning may skip to Implementation if no approval needed
- **Implementation workflows are sequential**: Implementation → Code Review → Human Approval → Merge & Cleanup

## Error Handling

If workflows encounter blocking issues:
- Document the problem clearly
- Update issue label to `blocked` with explanation in comments
- Suggest alternative approaches or ask for clarification
- Resume when blocker is resolved

## Reference Files

All workflow details are contained in individual `.md` files in the `workflows/` directory. Each file provides complete procedural guidance for its specific workflow.
