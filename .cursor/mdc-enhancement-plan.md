# MDC Files Enhancement Plan

## Priority 1: Immediate High-Impact Changes

### 1. 00-global.mdc - Add Auto-Rule Generation
**Impact**: 🔥 Highest - Enables consistent rule creation across the project
**Current State**: Basic global rules
**Enhancement**: Add meta-rule for automatic rule generation

```yaml
---
description: Global rules applied to every interaction, including auto-rule generation
alwaysApply: true
---
* **MUST:** When user requests a rule, follow the rule generation protocol
* **MUST:** Place new rules in appropriate .cursor/rules/ subdirectory
* **MUST:** Include proper frontmatter (description, globs, alwaysApply)
* **MUST:** No `git push --force` without explicit user OK ✅
* **Important:** Prefix hard rules with **"MUST:"** or **"Important:"** 🔧
* **Important:** Target 25 lines per rule (max 50) for efficiency
* **MUST:** Trust LLM intelligence - prefer primitives over templates 🔧
* **MUST:** Read files before editing ✅
* **Important:** Include debug info in output ✅
* **Important:** Run `npm audit` for vulnerabilities ✅
```

### 2. planner-executor.mdc - Strengthen Communication Protocol
**Impact**: 🔥 High - Core workflow pattern used frequently
**Current State**: Good separation but needs clearer handoffs
**Enhancement**: Add explicit protocols and validation checkpoints

```yaml
---
description: Planner-Executor workflow for complex tasks requiring separation of analysis and implementation
globs: 
alwaysApply: false
---
## Workflow States
| Role | Status | Actions |
|------|--------|---------|
| **Planner** | Analyzing | Define journey → break tasks → create Status Board 🔧 |
| **Executor** | Plan approved | TDD one task at a time → log → archive stale notes 🔧 |

### Communication Protocol
* **Handoff Format**: Planner writes task with acceptance criteria
* **Progress Updates**: Executor logs after each test passes
* **Validation Checkpoints**: Every 3 tasks or at blockers
* **Scratchpad Sections**:
  - 📋 Status Board (active tasks)
  - 🔄 In Progress (current executor work)
  - ✅ Completed (archived tasks)
  - 💬 Communication Log

### Task Format Template
```markdown
## Task: [ID] - [Name]
**Assigned to**: Executor
**Status**: Not Started | In Progress | Blocked | Complete
**Acceptance Criteria**:
- [ ] Criterion 1
- [ ] Criterion 2
**Test Plan**: [TDD approach]
```
```

## Priority 2: High-Value Enhancements

### 3. lessons.mdc - Structure as Append-Only Log
**Impact**: 🟧 High - Prevents repeated errors
**Current State**: Empty file
**Enhancement**: Create structured learning log

```yaml
---
description: Accumulated project-specific knowledge from errors and solutions - append only, never delete
globs: 
alwaysApply: true
---
# Project Lessons Log

## Format for New Entries
```
### [DATE] - [CATEGORY]: Brief Description
**Context**: What we were trying to do
**Error/Issue**: What went wrong
**Solution**: How we fixed it
**Prevention**: Rule or practice to avoid repeat
---
```

## Categories
- 🐛 BUG: Code errors and fixes
- 🏗️ ARCH: Architecture decisions
- 🔧 TOOL: Tool-specific learnings
- 📦 DEP: Dependency issues
- 🚀 PERF: Performance optimizations
```

### 4. researcher.mdc - Add Structured Output Formats
**Impact**: 🟧 High - Makes research actionable
**Current State**: Good principles, needs structure
**Enhancement**: Add concrete deliverable templates

```yaml
---
description: Deep research mode for exploring multiple solutions, analyzing trade-offs, and documenting findings
globs: 
alwaysApply: false
---
## Research Deliverables

### 1. Solution Comparison Matrix
```markdown
| Solution | Pros | Cons | Effort | Risk | Recommendation |
|----------|------|------|--------|------|----------------|
| Option A | • Pro1<br>• Pro2 | • Con1<br>• Con2 | Low/Med/High | Low/Med/High | ✅/❌ |
```

### 2. Technical Analysis Document
1. **Problem Statement**: Clear definition
2. **Constraints**: Technical, time, resource
3. **Options Explored**: Min 3 alternatives
4. **Deep Dive**: Selected approach details
5. **Implementation Plan**: Step-by-step
6. **Risk Mitigation**: Identified risks + solutions

### 3. Dependency Analysis
- Direct dependencies + versions
- Transitive dependencies of concern
- Security audit results
- Alternative packages considered
```

## Priority 3: Medium-Impact Improvements

### 5. architecture.mdc - Add More Concrete Examples
**Impact**: 🟨 Medium - Clarifies principles
**Current State**: Good philosophy, needs examples
**Enhancement**: Add real-world scenarios

Add after existing content:
```markdown
### Real-World Applications

#### Example 1: User Notifications
❌ **Template Approach**:
```python
NOTIFICATION_TEMPLATES = {
    'payment_success': "Payment of ${amount} successful",
    'payment_failed': "Payment failed: {reason}"
}
```

✅ **Context Approach**:
```python
notification_context = {
    'event_type': 'payment',
    'status': 'success',
    'amount': 150.00,
    'user_history': user.recent_transactions,
    'time_of_day': datetime.now(),
    'user_preferences': user.notification_settings
}
# Let LLM craft appropriate message with full context
```

#### Example 2: Error Handling
❌ **Fixed Categories**:
```python
ERROR_TYPES = ['network', 'validation', 'permission', 'unknown']
```

✅ **Rich Context**:
```python
error_context = {
    'error': str(e),
    'stack_trace': traceback.format_exc(),
    'user_action': current_action,
    'system_state': get_system_state(),
    'recent_events': event_log[-10:]
}
```
```

### 6. scratchpad.mdc - Define Clear Structure
**Impact**: 🟨 Medium - Improves agent communication
**Current State**: No structure defined
**Enhancement**: Create sections and rules

```yaml
---
description: Communication hub between Planner and Executor roles - structured sections for active work
globs: 
alwaysApply: false
---
# Scratchpad Structure

## 📋 STATUS BOARD
<!-- Planner updates this section -->

## 🔄 IN PROGRESS
<!-- Executor works here -->

## ✅ COMPLETED ARCHIVE
<!-- Move completed tasks here -->

## 💬 COMMUNICATION LOG
<!-- Async messages between roles -->

## 🗑️ ARCHIVE RULES
- Archive completed sections weekly
- Keep only last 5 completed tasks visible
- Move archives to `.cursor/archives/[date].md`
```

## Priority 4: Nice-to-Have Enhancements

### 7. designer.mdc - Add V0 Integration
**Impact**: 🟩 Low - Specialized use case
**Current State**: No content
**Enhancement**: Add UI enhancement workflow

```yaml
---
description: Design-focused workflow integrating with V0 and UI generation tools
globs: "**/*.tsx, **/*.jsx, **/*.css"
alwaysApply: false
---
## Design Workflow

### V0 Integration Process
1. Build functional component first
2. Copy component to V0.dev
3. Enhance with prompt: "Make this [style guide] with [requirements]"
4. Integrate improvements back

### Component Structure
- Separate logic from presentation
- Use composition over inheritance
- Implement responsive design first
- Accessibility as default

### Design Tokens
Reference design system variables for:
- Colors: Use CSS variables
- Spacing: 4px base unit system
- Typography: Defined scale
- Breakpoints: Mobile-first
```

### 8. housekeeping.mdc - Add Automation Triggers
**Impact**: 🟩 Low - Quality of life improvement
**Current State**: No content
**Enhancement**: Define cleanup rules

```yaml
---
description: Automated cleanup and maintenance rules for project organization
globs: 
alwaysApply: false
---
## Cleanup Triggers

### Daily
- [ ] Archive completed scratchpad sections
- [ ] Clear terminal outputs over 1000 lines
- [ ] Update task progress in Status Board

### Weekly  
- [ ] Archive old scratchpad to `.cursor/archives/`
- [ ] Review and consolidate lessons.mdc
- [ ] Clean up unused imports
- [ ] Remove commented code blocks

### On PR/Merge
- [ ] Run linters and formatters
- [ ] Update documentation
- [ ] Clean up feature branches
- [ ] Archive feature-specific notes
```

## Implementation Order

1. **Day 1**: 
   - Update 00-global.mdc (auto-rule generation)
   - Enhance planner-executor.mdc (communication protocol)

2. **Day 2**:
   - Create lessons.mdc structure
   - Enhance researcher.mdc templates

3. **Day 3**:
   - Add examples to architecture.mdc
   - Structure scratchpad.mdc

4. **When Needed**:
   - designer.mdc (when doing UI work)
   - housekeeping.mdc (when project grows)

## Success Metrics
- ✅ All rules under 50 lines
- ✅ Clear frontmatter on every file
- ✅ Concrete examples where applicable
- ✅ Structured templates for outputs
- ✅ Append-only logs for learning