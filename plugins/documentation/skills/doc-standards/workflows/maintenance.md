---
description: Implement and maintain documentation health over time
---

## Maintenance Workflow

Keep documentation fresh and accurate through systematic PR-based updates and quarterly reviews.

## Overview

Documentation rot is prevented through continuous maintenance, not occasional overhauls. This workflow establishes habits and checklists to keep docs fresh as code evolves.

## Context

Before starting:

- Documentation exists and follows three-layer structure
- Team is familiar with documentation layout
- PRs are the primary place code changes happen
- You want to prevent docs becoming stale

## Your Task

- Goal: Establish sustainable documentation maintenance practices
- Target: Keep docs fresh on every change
- Role: Make documentation updates part of definition of done

### Process

1. **Establish PR Documentation Checklist**

Add to your pull request template:

```markdown
## Documentation

- [ ] Updated README.md if behavior changed
- [ ] Updated relevant /docs files if structure changed
- [ ] Removed outdated information (not just patched around it)
- [ ] Added cross-references instead of duplicating content
- [ ] Verified all links still work
- [ ] Tested Quick Start if commands changed
```

Example PR description template:

```markdown
## Changes

[Description of code changes]

## Documentation Updates

- [ ] README.md - updated installation steps
- [ ] docs/api-reference.md - added new function signatures
- [ ] src/components/README.md - updated component structure

## Verification

- [ ] Quick Start tested end-to-end
- [ ] All links verified
- [ ] No information duplicated across layers
```

2. **Create Release Checklist**

Before each release, verify:

```bash
# Check README matches current version/behavior
grep -i "version" README.md

# Verify Getting Started still works
# Run through every step manually

# Check configuration reference is current
ls docs/configuration.md 2>/dev/null && wc -l docs/configuration.md

# Look for TODOs or placeholders in docs
grep -r "TODO\|FIXME\|XXX" docs/ --include="*.md" 2>/dev/null || echo "No TODOs in docs"

# Check that major changes are documented
# (compare git log with recent doc changes)
git log --oneline docs/ | head -10
```

Release checklist items:

- [ ] README.md version matches code
- [ ] README.md "Getting Started" tested end-to-end
- [ ] Configuration documentation is current
- [ ] API reference has no TODOs
- [ ] Architecture docs match implementation
- [ ] Breaking changes clearly documented
- [ ] Upgrade guide written (if applicable)
- [ ] Examples in docs work with new code

3. **Implement Quarterly Documentation Review**

Schedule a quarterly review (every 3 months):

```bash
# Find documentation files and their modification dates
find . -name "*.md" -not -path "./node_modules/*" -not -path "./.git/*" \
  -exec ls -lh {} \; | awk '{print $6, $7, $8, $9}' | sort

# Find docs not modified in 3+ months
find . -name "*.md" -not -path "./node_modules/*" -not -path "./.git/*" \
  -mtime +90 -type f
```

Quarterly review checklist:

- [ ] Delete stale or obsolete pages
- [ ] Update diagrams to match current architecture
- [ ] Trim README back to essentials (remove details moved to /docs)
- [ ] Verify directory READMEs still match real structure
- [ ] Fix broken cross-references
- [ ] Update version numbers and dates
- [ ] Remove duplicate content
- [ ] Add missing documentation for recent features
- [ ] Check that getting started instructions work
- [ ] Verify all code examples are current

4. **Create a Documentation Maintenance Schedule**

Add to your project documentation:

```markdown
## Documentation Maintenance

We maintain documentation continuously through:

### Per PR
- Documentation changes required for behavior changes
- Links verified before merge
- Duplicated content identified and removed

### Per Release
- README version updated
- Getting Started verified end-to-end
- Configuration documentation reviewed
- Breaking changes documented

### Quarterly
- Stale documentation removed
- Architecture diagrams updated
- Link validity checked
- Version numbers updated
- Directory READMEs verified against real structure
```

5. **Handle Common Maintenance Tasks**

**When adding a feature:**

```bash
# 1. Update appropriate layer(s)
# - Quick feature? Update README
# - Complex? Add to docs/api-reference.md
# - Architectural change? Update docs/architecture.md

# 2. Update examples/tutorials if applicable
# docs/tutorials/getting-started.md

# 3. Update configuration reference if applicable
# docs/configuration.md

# 4. Add to README Roadmap (mark as done)

# 5. Verify no duplication across layers
grep -r "new-feature" . --include="*.md" | wc -l
```

**When removing a feature:**

```bash
# 1. Find all references to removed feature
grep -r "removed-feature" . --include="*.md"

# 2. Delete or update each reference (don't just comment it out)
# Remove the lines, don't leave "// removed" comments in docs

# 3. Update README if it's in Getting Started

# 4. Update API reference if applicable
```

**When reorganizing code structure:**

```bash
# 1. Find all directory READMEs
find . -path "./docs" -prune -o -name "README.md" -type f -print

# 2. Update each directory README to match new structure

# 3. Update diagrams in docs/ if structure shown there

# 4. Update architecture.md if relevant
```

6. **Set Up Documentation Quality Checks (Optional)**

Create a documentation linting script:

```bash
#!/bin/bash
# Checks for common documentation problems

echo "Checking documentation..."

# Check README exists
test -f README.md || echo "ERROR: No README.md found"

# Check for broken links (basic check)
grep -r "\[.*\](.*)" . --include="*.md" | \
  grep -oP '\]\(\K[^)]+' | \
  while read link; do
    if [[ $link != http* ]] && [[ $link != ./* ]] && [[ $link != ../* ]]; then
      echo "WARNING: Possible broken link: $link"
    fi
  done

# Check for TODO markers
if grep -r "TODO\|FIXME\|XXX" docs/ --include="*.md" 2>/dev/null; then
  echo "WARNING: Found TODOs in documentation"
fi

# Check README isn't too long
readme_lines=$(wc -l < README.md)
if [ "$readme_lines" -gt 500 ]; then
  echo "WARNING: README.md is $readme_lines lines (>500 suggested)"
fi

echo "Documentation check complete"
```

7. **Establish Clear Ownership**

Decide:

- Who reviews documentation in PRs?
- Who runs quarterly reviews?
- What's the process for fixing outdated docs?
- How are documentation issues reported?

Update CONTRIBUTING.md:

```markdown
## Documentation Guidelines

### On Every PR
- Documentation changes required for code changes
- See our [documentation standards](docs/) for structure
- Run doc linting check before submitting

### On Release
- Maintainer verifies documentation is current
- README version matches release version
- Getting Started still works

### Quarterly
- Team lead schedules documentation review
- Outdated content is removed
- Architecture diagrams updated
```

8. **Prevent Documentation Debt**

Create a policy:

```markdown
## Documentation Principles

1. **Document as you code** - Don't plan to document later
2. **One fact, one place** - Link instead of duplicate
3. **Remove, don't patch** - Delete outdated content, don't comment it out
4. **Layer by audience** - README for quick facts, /docs for details
5. **Quarterly cleanups** - Dedicate time to removing stale content
6. **Link verification** - All links must work at merge time
7. **Example verification** - Code examples must work as written
```

9. **Commit Your Maintenance Processes**

```bash
git add CONTRIBUTING.md .github/PULL_REQUEST_TEMPLATE.md
git commit -m "docs: establish documentation maintenance practices

- Add documentation checklist to PR template
- Document release documentation requirements
- Establish quarterly review schedule
- Create documentation maintenance policy"
```

## Audit Documentation Health

As part of quarterly reviews or before releases, conduct a comprehensive documentation audit.

### Phase 1: Documentation Inventory

Create comprehensive inventory:

```bash
# Find all documentation files
find . -name "*.md" -not -path "./node_modules/*" -not -path "./.git/*" | sort

# Check file structure
ls -la | grep -E "^d"

# Check README presence
find . -name "README.md" -type f

# Check /docs presence
test -d docs && find docs -type f -name "*.md" | head -20 || echo "No /docs folder"
```

### Phase 2: Structure Assessment

Evaluate if documentation follows three-layer model:

```bash
# Check README size
wc -l README.md

# Check for directory READMEs
find . -path "./docs" -prune -o -name "README.md" -type f -print

# Check /docs organization
ls -la docs/ 2>/dev/null || echo "No /docs"
```

Assessment questions:

- [ ] Is README the clear entry point?
- [ ] Is README <500 lines?
- [ ] Are directory READMEs in key folders?
- [ ] Is /docs organized logically?
- [ ] Are there cross-references between layers?

### Phase 3: Check for Broken Links

```bash
# Find all markdown links
grep -r "\[.*\](" . --include="*.md" | grep -oP '\]\(\K[^)]+' | sort | uniq

# Check if linked files exist
# Sample check for relative links
grep -r "\[.*\](\./" . --include="*.md" | \
  grep -oP '\]\(\K[^)]+' | \
  while read link; do
    if [ ! -f "$link" ]; then
      echo "✗ MISSING: $link"
    fi
  done
```

Record broken links to fix.

### Phase 4: Check for Duplication

Identify information repeated across layers:

```bash
# Search for common terms across files
for term in "Installation" "Getting Started" "Configuration"; do
  echo "$term appears in:"
  grep -l "$term" $(find . -name "*.md" -not -path "./node_modules/*") 2>/dev/null | wc -l
done
```

Create table of duplications and where to consolidate.

### Phase 5: Check for Stale Content

Look for signs of outdated documentation:

```bash
# Find TODO/FIXME markers
grep -r "TODO\|FIXME\|XXX\|DEPRECATED" . --include="*.md" -n

# Find version references
grep -r "version\|v[0-9]\." . --include="*.md" | head -20

# Check modification dates
find . -name "*.md" -not -path "./node_modules/*" -not -path "./.git/*" \
  -exec ls -lh {} \; | awk '{print $9, $6, $7, $8}' | sort
```

Look for:

- [ ] TODO/FIXME markers
- [ ] Version numbers that don't match code
- [ ] Outdated dates
- [ ] References to removed features
- [ ] Configuration options that no longer exist

### Phase 6: Verify Code Examples

Check that examples work:

```bash
# Find code blocks
grep -r "^\`\`\`" . --include="*.md" | head -20

# For critical examples, test them manually
# - Installation commands
# - Quick start examples
# - API usage examples
```

### Phase 7: Check Coverage

Identify missing documentation:

```bash
# Check README mentions major features
# Check /docs has tutorial for each feature
# Check API documentation exists
# Check configuration is documented
```

Ask:

- [ ] Is every public API documented?
- [ ] Does every major module have explanation?
- [ ] Are there tutorials for common use cases?
- [ ] Is deployment/operations documented?
- [ ] Are common gotchas documented?
- [ ] Is contribution process documented?

### Phase 8: Create Audit Report

Document findings:

```markdown
# Documentation Audit Report

**Date:** [date]
**Overall Health:** [score]/10

## Critical Issues (Fix Immediately)

- Broken links: [list with locations]
- Outdated configs: [examples]
- Missing critical docs: [what's missing]

## High Priority (This Month)

- Duplication to consolidate
- Outdated examples
- Missing feature docs

## Medium Priority (This Quarter)

- Navigation improvements
- Coverage expansion
- Consistency improvements

## Action Items

| Priority | Task | Effort |
|----------|------|--------|
| Critical | Fix broken links | 30 min |
| High | Remove duplication | 1 hr |
```

### Phase 9: Prioritize and Plan

Convert findings to actionable items:

```markdown
## Audit Follow-Up

### Immediate (This Week)
- [ ] Fix broken links
- [ ] Update outdated configs
- [ ] Add missing critical docs

### Next Month
- [ ] Remove duplication
- [ ] Move content between layers
- [ ] Create missing tutorials

### This Quarter
- [ ] Improve navigation
- [ ] Add advanced guides
- [ ] Enhance architecture docs
```

## Guidelines

- Treat documentation like code - it needs maintenance
- Update docs on the same PR that changes behavior
- Remove outdated information - don't patch around it
- Verify links and examples work before merging
- Schedule quarterly reviews - don't let docs drift
- Make documentation updates part of definition of done
- Remove documentation debt early, before it accumulates
- Use audit procedure quarterly to identify problems early

## Success Criteria

- ✅ Every behavior-changing PR updates documentation
- ✅ Links are verified before merge
- ✅ Outdated information is removed (not commented out)
- ✅ README/Getting Started works end-to-end
- ✅ Documentation updates tracked in git log
- ✅ Quarterly reviews scheduled and tracked
- ✅ No duplicate information across layers
- ✅ Team understands documentation expectations
