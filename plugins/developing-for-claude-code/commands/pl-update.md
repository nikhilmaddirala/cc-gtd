---
name: pl-update
description: Add new components or update existing plugin structure
---

# Update existing plugin

## Overview

This command guides you through adding new components or updating existing structure in an established Claude Code plugin. CRITICAL: You MUST use the plugin-development-gtd skill for this task.

## Context

User will provide plugin name, component type (command, agent, workflow, or skill), and component details. The command validates the plugin exists and has proper structure before processing.

## Process

Load plugin-development-gtd skill first. Interactively guide the user through this skill and update-existing-plugin workflow step by step, collecting inputs and executing each step with confirmation.
