# Cursor Rules Overview

This document provides a quick reference to all modular rules in the `.cursor/rules/` directory.

## Rule System Structure

| Rule File | Type | Purpose | Last Modified |
|-----------|------|---------|---------------|
| `00-global.mdc` | alwaysApply | Global guardrails and defaults | 2025-01-06 |
| `planner-executor.mdc` | alwaysApply | Planner ↔ Executor role cycle and workflow | 2025-01-06 |
| `scratchpad.mdc` | alwaysApply | Scratchpad schema and archival rules | 2025-01-06 |
| `housekeeping.mdc` | alwaysApply | Repository hygiene (naming, logging, git) | 2025-01-06 |
| `lessons.mdc` | alwaysApply | Running list of mistakes and fixes | 2025-01-06 |
| `researcher.mdc` | manual | Deep-dive exploration charter | 2025-01-06 |
| `designer.mdc` | manual | UX/content design charter | 2025-01-06 |
| `architecture.mdc` | manual | Project architecture and design philosophy | 2025-01-06 |

## How Rules Work

### Always Applied Rules
Files marked with `alwaysApply: true` in their frontmatter are automatically loaded in every Cursor session. These include:
- Core guardrails and constraints
- The Planner/Executor workflow system
- Documentation standards
- Repository hygiene practices
- Accumulated lessons

### Manual Rules
Files marked with `manual: true` must be explicitly loaded when needed:
- Use `researcher.mdc` for deep technical investigations
- Use `designer.mdc` for UI/UX decisions
- Use `architecture.mdc` for system design discussions

## Quick Reference

### To load a manual rule:
Ask Cursor to "load the researcher rule" or "apply designer guidelines"

### To add a new rule:
1. Create a new `.mdc` file in `.cursor/rules/`
2. Add YAML frontmatter with `description` and either `alwaysApply: true` or `manual: true`
3. Update this overview document

### To archive old content:
Follow the archival rules in `scratchpad.mdc` - move to `.cursor/archive/` when content becomes irrelevant due to pivots or changes in direction.