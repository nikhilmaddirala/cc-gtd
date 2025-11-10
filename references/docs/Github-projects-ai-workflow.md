---
type: resource
tags:
  - workflow
  - ai-agents
  - github
  - development
created: 2025-10-29
---

## Overview

This workflow uses GitHub Issues as the primary unit of work, with AI agents handling execution and humans providing strategic oversight. This is a general workflow applicable across github repos.

**Architecture:**
- Issues progress through 7 distinct stages with clear inputs, outputs, and status labels
- AI agents execute work autonomously between human approval gates
- Git worktrees provide isolated development environments
- Conventional commits maintain clear change history
- Continuous maintenance monitoring ensures repository health

**Key Stages:**
1. Issue creation → 2. Planning → 3. Plan approval → 4. Implementation → 5. AI review → 6. Human review → 7. Merge & cleanup

**Human Approval Gates:**
- After planning (approve implementation approach)
- After AI review (approve code changes before merge)

## GitHub Issues as State Machines

Issues serve as the central coordination point, with labels tracking workflow stage and driving agent automation.

**Issue states:**
- Open: Issue is active and being worked on
- Closed: Issue is complete and merged, or abandoned

**Status labels (track workflow stage):**
- "needs planning" - Issue created, awaiting planning agent
- "needs plan approval" - Plan exists, awaiting human review
- "needs implementation" - Plan approved, ready for implementation agent
- "in progress" - Implementation active, PR in draft or changes being made
- "needs review" - PR ready, awaiting AI preliminary review
- "ready for approval" - AI preliminary review passed, awaiting human review
- "approved for merge" - Human approved, ready for merge
- "blocked" - Work stopped due to blocker (specifics in comments: tests failing, needs clarification, etc.)
- "needs cleanup" - Issue closed but branches/worktrees remain

**Type labels:**
- "feature" - New functionality
- "bug" - Defect or unexpected behavior
- "docs" - Documentation changes
- "refactor" - Code improvements without behavior change

**Workflow integration:**
- Labels drive automation: agents query for issues with specific labels
- Maintenance agent ensures labels stay synchronized with actual state
- Project board columns mirror label states for visualization
- Transitions between labels follow strict workflow stages (see diagram and table below)

## State Transition Diagram

> This diagram shows how issues flow through the workflow stages via status label changes.

```
[New task]
    ↓
[Issue Created] ─────────→ needs planning
    ↓
[Planning Agent] ────────→ needs plan approval
    ↓
[Human Review] ──┬───────→ needs implementation (approved)
                 │
                 └───────→ needs planning (changes requested)
    ↓
[Implementation] ────────→ in progress
    ↓
[PR Created] ────────────→ needs review
    ↓
[AI Review] ──┬──────────→ ready for approval (passed)
              │
              └──────────→ needs implementation (changes needed)
    ↓
[Human Review] ──┬───────→ approved for merge
                 │
                 ├───────→ needs implementation (changes requested)
                 │
                 └───────→ needs planning (major changes)
    ↓
[Merge] ─────────────────→ Closed
    ↓
[Cleanup] ───────────────→ Complete

[Maintenance Agent] - monitors all stages continuously
```

## Workflow Stages (Detailed)

| Stage                  | **Implementation**                                                    | Inputs                                                                                              | Outputs                                                                                                                                                        | Process                                                                                                                                                                                                                |
| ---------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Issue creation**  | ✅  `commands/gh-issue`<br><br>Slash command: Human + AI (interactive) | User has a task in mind / in task list                                                              | Issue following issue template with "needs planning" label                                                                                                     | - Understand user request and clarify details interactively<br>- Create GH issue following template                                                                                                                    |
| **2. Planning**        | AI agent (non-interactive)                                            | Issue has "needs planning" label                                                                    | Implementation plan with options analysis (if applicable); label "needs plan approval"                                                                         | - Do internal and external research to develop detailed plan<br>- Add options and tradeoffs if needed                                                                                                                  |
| **3. Plan feedback**   | Human only                                                            | Issue has plan with "needs plan approval" label                                                     | Label changed to "needs implementation" or "needs planning"<br><br>If it goes back to "needs planning" - feedback in comments                                  | - Human adds comment and updates label                                                                                                                                                                                 |
| **4. Implementation**  | AI agent (non-interactive)                                            | Issue has detailed plan with "needs implementation"                                                 | Branch + worktree with commits; draft PR linked to issue; PR description with implementation details; passing test results                                     | - Create branch and worktree <br>- rebase on main <br>- implement changes with conventional commits <br>- creates draft PR with description and label "needs review"                                                   |
| **5. AI review**       | AI agent (non-interactive)                                            | Issue has "needs review" label and associated PR; all CI checks completed; no merge conflicts       | Label changes to "needs implementation" or "ready for approval"<br><br>Detailed PR review comment                                                              | - Review code (style, tests, docs, security, commits) <br>- Post review comment with label change                                                                                                                      |
| **6. Human review**    | Slash command: Human + AI (interactive)                               | Issue has "ready for approval" label; AI preliminary review complete                                | Label changes to "approved for merge" or "needs implementation" or "needs planning"<br><br>If "needs implementation" or "needs planning", detailed comment<br> | - Human reviews PR and AI comments; may test locally <br>- AI will help with testing                                                                                                                                   |
| **7. Merge & cleanup** | AI agent                                                              | Issue labeled "approved for merge"; PR approved by human; all CI checks passing; no merge conflicts | Changes merged to main branch; closed issue; clean repository state (no orphaned branches/worktrees)                                                           | - Squash-merge performed → GitHub auto-deletes feature branch → issue auto-closed via PR ("Closes #123") → local worktree removed → maintenance agent verifies cleanup → moved to "Done" column → clean state achieved |

## Continuous Monitoring: Maintenance Agent

Running in parallel with all stages, the maintenance agent continuously monitors repository health:

**Monitoring activities:**
- Check all open issues for current status and next action
- Ensure issues have required branches/worktrees if in implementation
- Verify closed issues have cleaned up branches/worktrees
- Identify stale work (issues idle >7 days)
- Flag PRs waiting for review
- Detect orphaned branches or worktrees

**Responsibilities:**
- Keep issue labels synchronized with actual workflow state (see status labels above)
- Detect and flag issues in "needs cleanup" state (closed but branches/worktrees remain)
- Update project board to mirror current issue labels
- Generate daily reports on items needing attention

**Outputs:**
- Updated issue/PR labels reflecting current state
- Project board with accurate status
- Daily report summarizing: items needing attention, blocked items, stale items
- Automated cleanup of stale branches/worktrees where safe

## Appendix

### Design Decision: Plan Approval Gate

**Decision:** Always wait for explicit human approval before implementation (see "needs plan approval" stage above).

**Rationale:**
- Ensures human oversight before significant work begins
- Prevents wasted effort from misaligned approaches
- Allows humans to provide strategic input on trade-offs
- Slight delays are acceptable given the benefits of alignment

**Alternatives considered:**
- Auto-proceed and get feedback on PR (faster but risks wasted effort)
- Hybrid approach based on complexity (adds decision complexity)

### Branch Naming Conventions

**Standard patterns:**
- `issue-<number>-<slug>` - For GitHub issues (primary pattern)
- `hotfix-<slug>` - For urgent fixes outside normal workflow
- `docs-<slug>` - For documentation-only updates

**Examples:**
- `issue-12-workflow-standardization`
- `issue-45-add-user-authentication`
- `hotfix-container-restart-loop`
- `docs-update-installation-guide`

**Slug guidelines:**
- Use lowercase with hyphens
- Keep concise (3-5 words maximum)
- Describe the change, not the problem
- Avoid redundant words like "fix" or "add" if type is clear from context

### Worktree Setup

**Creating worktrees:**
```bash
# Create worktree for issue
git worktree add worktrees/issue-12-workflow-standardization

# Switch to worktree
cd worktrees/issue-12-workflow-standardization

# Start working...
```

**Managing worktrees:**
```bash
# List all worktrees
git worktree list

# Remove worktree (after branch is merged/deleted)
git worktree remove worktrees/issue-12-workflow-standardization

# Prune stale worktree references
git worktree prune
```

**Worktree best practices:**
- One worktree per active issue
- Keep worktrees in dedicated `worktrees/` directory
- Remove worktrees promptly after merging
- Never commit from main repo directory when worktrees are active

### Conventional Commit Format

**Structure:**
```
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

**Types:**
- `feat` - New feature
- `fix` - Bug fix
- `docs` - Documentation changes
- `refactor` - Code refactoring without behavior change
- `test` - Adding or modifying tests
- `chore` - Maintenance tasks, dependency updates
- `ci` - CI/CD configuration changes
- `perf` - Performance improvements
- `style` - Code style/formatting changes

**Scope (optional):**
- Component or area affected (e.g., `auth`, `api`, `ui`)

**Description:**
- Use imperative mood ("add" not "added" or "adds")
- Don't capitalize first letter
- No period at the end
- Keep under 72 characters

**Examples:**
```
feat(auth): add OAuth2 authentication flow
fix(api): resolve race condition in request handler
docs: update installation instructions for macOS
refactor(parser): simplify token processing logic
test(auth): add integration tests for login flow
```

### Common Commands Quick Reference

> These commands support the workflow stages described above.

```bash
# Create worktree
git worktree add worktrees/issue-<num>-<slug>

# Fetch and rebase
git fetch origin && git rebase origin/main

# Remove worktree when done
git worktree remove worktrees/issue-<num>-<slug>

# View issue details
gh issue view <number>

# Create draft PR
gh pr create --draft --title "Title" --body "Description"

# View PR details
gh pr view <number>

# Quickfix workflow
git checkout main && git pull origin main
# make changes, test, then:
git add . && git commit -m "quickfix: description"
git push origin main
```

### Key Resources

- Issue templates: Create new issue and select appropriate template
- Project board: Track issue status and workflow stages
- CI status: Monitor automated checks and test results
- Repository settings: Branch protection, required reviews, auto-merge settings
