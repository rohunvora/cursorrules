# Quick-Start Implementation Guide

## 🏃 5-Minute Quick Wins

### Step 1: Add Frontmatter to Your Rules (2 minutes)

Here are the exact frontmatter blocks to add to each of your files:

**`.cursor/rules/00-global.mdc`**
```yaml
---
alwaysApply: true
---
* **MUST:** No `git push --force` without explicit user OK ✅
[rest of your content...]
```

**`.cursor/rules/planner-executor.mdc`**
```yaml
---
description: "Systematic planning and execution workflow for complex tasks"
alwaysApply: false
---
| **Planner** | User request → create plan → get approval 🔧 |
[rest of your content...]
```

**`.cursor/rules/housekeeping.mdc`**
```yaml
---
description: "Code quality and repository hygiene standards"
globs: "**/*.{js,ts,py,jsx,tsx,java,go,rb,php,cs}"
alwaysApply: false
---

# Logging
[rest of your content...]
```

**`.cursor/rules/designer.mdc`**
```yaml
---
description: "UI/UX design principles and accessibility standards"
globs: "**/*.{css,scss,sass,less,html,jsx,tsx,vue}"
alwaysApply: false
---
- Content strategy and copywriting ✅
[rest of your content...]
```

**`.cursor/rules/researcher.mdc`**
```yaml
---
description: "Deep technical investigation and solution analysis"
alwaysApply: false
---
- Multiple solution exploration 🔧
[rest of your content...]
```

**`.cursor/rules/architecture.mdc`**
```yaml
---
description: "Trust LLM intelligence - use primitives over templates"
alwaysApply: false
---

### Trust LLM Intelligence
[rest of your content...]
```

**`.cursor/rules/lessons.mdc`**
```yaml
---
alwaysApply: true
---
* Run `npm audit` for vulnerabilities ✅
[rest of your content...]
```

**`.cursor/rules/scratchpad.mdc`**
```yaml
---
description: "Scratchpad structure and archival rules"
globs: ".cursor/scratchpad.md"
alwaysApply: false
---
- **Background & Motivation** - Initial context and goals ✅
[rest of your content...]
```

### Step 2: Create `.cursorindexingignore` (30 seconds)

Create `.cursor/.cursorindexingignore`:
```
# Prevent rule caching issues
rules/**/*.mdc
archive/**
scratchpad.md
```

### Step 3: Test Your Setup (2 minutes)

1. Open a new Cursor session
2. Type: "What rules are currently active?"
3. Verify that `00-global.mdc` and `lessons.mdc` are loaded
4. Open a Python file and verify `housekeeping.mdc` auto-loads
5. Type: "Apply the researcher rule" and verify it loads

## 🎯 Most Impactful Changes (Based on Community Feedback)

### 1. The "Dual-Use" Pattern (BMad's Discovery)
Rules with BOTH `description` AND `globs` work perfectly:
- Agent can select them based on description
- They auto-apply to matching files
- Example: Your `housekeeping.mdc` and `designer.mdc`

### 2. The "Memory Bank" Pattern
Create `.cursor/rules/memory-bank.mdc`:
```yaml
---
description: "Project-specific decisions and context"
alwaysApply: true
---
# Project Memory Bank

## Key Decisions
- **2025-01-06**: Using Trust LLM pattern - primitives over templates
- **[DATE]**: [DECISION] - [RATIONALE]

## Common Patterns
- Always use TypeScript discriminated unions for event handling
- Prefer composition over inheritance
- Use feature flags for gradual rollouts

## Team Conventions
- PR titles: `type(scope): description`
- Branch protection on main
- Minimum 1 reviewer for PRs
```

### 3. Enhanced Planner-Executor Workflow

Add this to your `planner-executor.mdc`:
```markdown
## Task Status Board Format
```markdown
### 🎯 Current Sprint
- [ ] TASK-001: Setup authentication | @executor | ⏳ in-progress
- [ ] TASK-002: Create user model | @planner | 🔍 planning
- [x] TASK-003: Initialize project | @executor | ✅ 2025-01-06

### Status Icons
- 🔍 planning
- ⏳ in-progress  
- 🚧 blocked
- 👀 review
- ✅ complete
```

## 🔥 Power User Workflow

### The "Context Cascade" Technique
```
1. Start broad: "Build a user authentication system"
2. Let Agent ask: "What type of auth? Any existing code?"
3. Reference: "@designer.mdc for UI, @architecture.mdc for patterns"
4. Iterate: "Make it more secure" → Agent applies OWASP standards
```

### The "Test-First Agent" Pattern
```
User: "Create a payment processing module"
Agent: "I'll start by creating comprehensive tests..."
[Agent generates test suite]
Agent: "Now implementing to pass these tests..."
[Agent implements code]
Agent: "All tests passing. Shall I add edge cases?"
```

### The "PR-Driven Development"
```
User: "Implement features from PR #456"
[Agent fetches PR, analyzes changes]
Agent: "I see this PR adds OAuth2. I'll implement similarly..."
```

## 📈 Measuring Impact

Track these in your `lessons.mdc`:
```xml
<metrics week="2025-W02">
  <metric name="force-push-incidents">0</metric>
  <metric name="linter-errors-introduced">3</metric>
  <metric name="tasks-completed">12</metric>
  <metric name="agent-accuracy">85%</metric>
</metrics>
```

## 🚨 Common Pitfalls to Avoid

1. **Don't Mix Rule Types**
   - ❌ `alwaysApply: true` with `globs: "*.js"`
   - ✅ Either `alwaysApply: true` OR `globs` pattern

2. **Don't Over-Constrain**
   - ❌ 20 different rules with specific instructions
   - ✅ 5-7 focused rules with clear principles

3. **Don't Forget Context**
   - ❌ "Fix the bug"
   - ✅ "Fix the auth bug in @login.js using @architecture.mdc patterns"

## 🎬 Your First Enhanced Session

Try this workflow:
1. "Load planner-executor workflow"
2. "As Planner, create a plan for adding user profiles to the app"
3. "Now switch to Executor and implement TASK-001"
4. "Update scratchpad with progress"
5. "What lessons should we add from this session?"

This approach leverages all the community's best practices while working with your existing structure!