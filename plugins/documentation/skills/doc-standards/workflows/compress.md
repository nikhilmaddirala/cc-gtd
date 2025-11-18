---
description: Create condensed versions of documentation for quick reference and lookup
---

## Compress Documentation Workflow

Create condensed summaries of lengthy documentation for quick reference and lookup.

## Overview

This workflow guides you through systematically compressing a document. The goal is to reduce length while preserving critical information that matters for your use case and audience.

## Context

Before starting:

- You have a lengthy document to compress
- You want a quick-reference version for your team
- You understand what information is critical vs. supplementary
- You know your target audience and their lookup needs

## Your Task

- Goal: Create a condensed version of documentation
- Target: Preserve critical information your audience needs
- Role: Technical editor removing noise while preserving substance

### Step 1: Identify the Document and Target Compression

```bash
# Locate the file to compress
ls -la /path/to/file

# Check file size
wc -l /path/to/file
wc -w /path/to/file

# Review current length against guidelines in SKILL.md
```

Decide on target compression:

- **Light compression** (2-3×) - Remove examples and explanations, keep structure and details
- **Medium compression** (5-8×) - Remove verbose explanations, keep decisions and critical details
- **Heavy compression** (10×+) - Keep only essential details, API contracts, thresholds, decisions

Choose based on:

- Document type (API reference compresses more than tutorials)
- Audience (expert teams can compress more heavily)
- Use case (quick lookup vs. learning reference)
- Detail preservation needs

### Step 2: Understand What's Critical

Identify what your audience *must* have for their use case:

```bash
# For API reference: function signatures, parameters, error codes
# For guides: key decisions, critical steps, caveats
# For architecture: components, data flow, deployment topology
# For configuration: all options, defaults, constraints
```

Ask:

- What would break if removed?
- What prevents errors or misunderstanding?
- What numbers/thresholds are non-obvious?
- What gotchas does my audience need to know?

### Step 3: Extract Critical Elements

Systematically identify what to keep:

```bash
# Scan for key terms and concepts
grep -E "^##? |^###? " /path/to/file

# Find defined terms
grep -E "\*\*.*\*\*|__.*__" /path/to/file

# Find numbers and constraints
grep -E "[0-9]+" /path/to/file

# Find decisions and recommendations
grep -E "should|must|always|never|use when|avoid" /path/to/file

# Find warnings and caveats
grep -E "important|note|caveat|gotcha|careful|watch out|exception" /path/to/file
```

Preserve:

- Definitions of concepts
- Key decisions and their rationale
- Numbers, thresholds, constraints, SLAs
- Caveats, gotchas, limitations
- API contracts and function signatures
- Configuration options and defaults

Remove:

- Verbose explanations (condense to essentials)
- Repeated information (keep once, link elsewhere)
- Examples (unless essential for understanding)
- Marketing language and motivation
- Detailed walkthroughs (replace with quick reference)

### Step 4: Choose Your Format

The SKILL.md defines acceptable document types and their length guidelines. Choose a format that:

- Matches your document type
- Meets length targets
- Preserves critical information
- Is scannable for your audience

Options:

- Dense bullet points
- Structured sections (definitions, decisions, details, caveats)
- Quick reference tables
- Glossary/term definitions
- API contracts only
- Checklist format
- Other formats your team prefers

### Step 5: Build the Condensed Version

Write your condensed version using your chosen format:

```bash
# Create new file
touch /path/to/file-compressed.md
# or
touch /path/to/file-quick-ref.md
```

Include only:

- What your audience needs for their use case
- Critical details, numbers, constraints
- Key decisions and gotchas
- Skip: verbose explanations, repeated content, examples (unless essential)

Guidelines:

- Use short, direct sentences
- Preserve all terminology and variable names exactly
- Keep all numbers, thresholds, and constraints
- Make it scannable
- Use formatting (bold, tables, bullets) to aid scanning

### Step 6: Measure Compression

Calculate how much you've compressed:

```bash
# Original stats
original_lines=$(wc -l < /path/to/file)
original_words=$(wc -w < /path/to/file)

# Compressed stats
compressed_lines=$(wc -l < /path/to/file-compressed.md)
compressed_words=$(wc -w < /path/to/file-compressed.md)

# Calculate ratio
ratio=$((original_lines / compressed_lines))
echo "Compression: $original_lines → $compressed_lines lines (~1:${ratio}×)"
```

Compare to your target compression level.

### Step 7: Verify Against Original

```bash
# Accuracy check:
# 1. Do all numbers match the original exactly?
# 2. Have you changed any terminology or simplified it incorrectly?
# 3. Are all critical decisions captured?
# 4. Are important caveats included?

# If format requires specific sections:
# - Verify each section per SKILL.md guidelines
# - Confirm all cross-references work
# - Check that format matches your documentation standards
```

### Step 8: Document What Was Removed

Note what was removed and why:

- Removed verbose explanations → kept essential details
- Removed examples → users can find in original document
- Removed background context → decisions included
- Removed repeated information → consolidated to single source

This helps readers understand what's in the compressed version vs. where to go for full details.

### Step 9: Save with Clear Naming

Use naming that indicates this is a compressed/quick-reference version:

```bash
# Original: README.md
# Compressed: README-quick-ref.md
# Or: README-compressed.md

# Original: docs/api-reference.md
# Compressed: docs/api-reference-quick-ref.md

# Original: docs/architecture.md
# Compressed: docs/architecture-summary.md
```

### Step 10: Commit and Link

Link compressed version from original if appropriate:

```bash
# In original document, add section:
# ## Quick Reference
# For a condensed quick-reference version, see [README-quick-ref.md](README-quick-ref.md)

git add /path/to/file-compressed.md
git commit -m "docs: add compressed reference for [document]

- Created [filename] from [original document]
- Original: X lines/words
- Compressed: Y lines/words (~1:[ratio]× compression)
- Compression level: [light/medium/heavy]
- Includes: [what's included]
- Removed: [what was removed and why]"
```

## Examples

### Example 1: API Reference (Medium Compression)

**Original:** 800 lines
**Target:** 100-150 lines (5-8× compression)
**Format:** Function signatures + critical details in tables

### Example 2: Architecture Document (Light Compression)

**Original:** 600 lines
**Target:** 200-300 lines (2-3× compression)
**Format:** Components + data flow + deployment, with essential details preserved

### Example 3: Configuration Reference (Heavy Compression)

**Original:** 400 lines
**Target:** 40-50 lines (8-10× compression)
**Format:** Table of options, defaults, constraints only

## Guidelines

- **Choose compression level consciously** - Match to your audience's needs
- **Preserve critical information** - Never compress away gotchas, constraints, or decisions
- **Keep exact terminology** - No simplification or substitution
- **Keep all numbers** - Don't round or approximate
- **Make it scannable** - Use formatting to aid quick lookup
- **Document removals** - Note what was condensed and why
- **Verify accuracy** - Cross-check every detail against source
- **Follow SKILL.md guidelines** - Respect length targets for your document type

## Success Criteria

- ✅ Target compression level achieved
- ✅ All critical information preserved for your audience
- ✅ All numbers, constraints, and decisions included exactly
- ✅ Format appropriate for document type
- ✅ Document is scannable and well-organized
- ✅ Terminology preserved exactly as in original
- ✅ Verified against original for accuracy
- ✅ Removals documented (what was removed and why)
- ✅ Linked from original document if appropriate
