# High-Leverage Cursor Rules Recommendations

Based on extensive community research and analysis of your current .mdc files, here are targeted recommendations to enhance your Cursor Agent mode experience.

## 🚀 Immediate High-Impact Changes

### 1. Add YAML Frontmatter to All Rules
**Issue**: None of your .mdc files have frontmatter, limiting Cursor's ability to intelligently apply them.

**Fix for each file**:
```yaml
---
description: "Brief description for agent selection"
globs: "**/*.py,**/*.js"  # For auto-select rules
alwaysApply: true  # or false
---
```

**Specific recommendations**:
- `00-global.mdc`: Add `alwaysApply: true` (no description needed)
- `planner-executor.mdc`: Add `description: "Systematic planning and execution workflow"`
- `architecture.mdc`: Add `description: "Trust LLM intelligence with primitives"`
- `housekeeping.mdc`: Add `globs: "**/*.{js,ts,py,md}"` for auto-select
- `researcher.mdc`: Keep as manual with clear description
- `designer.mdc`: Add `globs: "**/*.{css,tsx,jsx,html}"`

### 2. Optimize Rule Length and Structure
**Community consensus**: 25 lines ideal, 50 lines max per rule.

**Your current lengths**:
- ✅ `00-global.mdc`: 6 lines (perfect)
- ✅ `lessons.mdc`: 11 lines (good)
- ⚠️ `architecture.mdc`: 41 lines (consider splitting)
- ⚠️ `planner-executor.mdc`: 31 lines (borderline)
- ⚠️ `housekeeping.mdc`: 32 lines (borderline)

**Recommendation**: Split `architecture.mdc` into:
- `trust-llm.mdc`: Core philosophy (15 lines)
- `llm-patterns.mdc`: Examples and patterns (20 lines)

### 3. Implement the Four Rule Types Strategy

Based on BMad's proven framework:

| Your File | Recommended Type | Rationale |
|-----------|-----------------|-----------|
| `00-global.mdc` | Always | Core constraints |
| `planner-executor.mdc` | Agent Selected | Context-dependent workflow |
| `scratchpad.mdc` | Auto Select | Apply to `.cursor/scratchpad.md` |
| `housekeeping.mdc` | Auto Select | Apply to code files |
| `lessons.mdc` | Always | Universal learnings |
| `researcher.mdc` | Manual | Specific deep-dives |
| `designer.mdc` | Auto Select | UI/UX files |
| `architecture.mdc` | Agent Selected | Design discussions |

### 4. Add XML-Style Examples (Community Favorite)

Replace your current emoji checkmarks with structured examples:

```xml
<!-- In housekeeping.mdc -->
<examples>
  <valid>
    <commit>feat(auth): add OAuth2 integration</commit>
    <branch>feature/oauth-integration-123</branch>
  </valid>
  <invalid>
    <commit>fixed stuff</commit>
    <branch>my-branch</branch>
  </invalid>
</examples>
```

### 5. Create a Memory Bank System

Add a new file `.cursor/rules/memory-bank.mdc`:
```yaml
---
description: "Project decisions and context"
alwaysApply: true
---
<decisions>
  <decision date="2025-01-06">
    <topic>Architecture Pattern</topic>
    <choice>Trust LLM Intelligence</choice>
    <rationale>Primitives over templates for flexibility</rationale>
  </decision>
</decisions>
```

## 📁 Recommended Directory Structure

```
.cursor/
├── rules/
│   ├── core/           # Always applied
│   │   ├── 00-global.mdc
│   │   ├── lessons.mdc
│   │   └── memory-bank.mdc
│   ├── workflow/       # Agent selected
│   │   ├── planner-executor.mdc
│   │   └── scratchpad.mdc
│   ├── auto/          # Auto-selected by file type
│   │   ├── housekeeping.mdc
│   │   └── designer.mdc
│   └── manual/        # Manual reference
│       ├── researcher.mdc
│       └── architecture.mdc
├── archive/           # As you have
└── .cursorindexingignore  # NEW: Prevent rule caching issues
```

## 🔧 Technical Optimizations

### 1. Add `.cursorindexingignore`
```
# Prevent rule caching issues
.cursor/rules/**/*.mdc
.cursor/archive/**
```

### 2. Update VS Code Settings
```json
{
  "workbench.editorAssociations": {
    "*.mdc": "default"
  }
}
```

### 3. Implement Rule Validation Script
Create `.cursor/validate-rules.py`:
```python
import yaml
import glob

for file in glob.glob('.cursor/rules/**/*.mdc', recursive=True):
    with open(file) as f:
        content = f.read()
        if not content.startswith('---'):
            print(f"⚠️  {file}: Missing frontmatter")
        # Additional validations...
```

## 🎯 Content-Specific Improvements

### For `planner-executor.mdc`:
- Add concrete task status format:
  ```
  - [ ] Task description | assigned: executor | status: blocked
  - [x] Completed task | completed: 2025-01-06
  ```

### For `architecture.mdc`:
- Include discriminated union example (community favorite):
  ```typescript
  type Event = 
    | { type: 'click'; x: number; y: number }
    | { type: 'keypress'; key: string }
  ```

### For `lessons.mdc`:
- Structure as:
  ```xml
  <lesson id="L001" date="2025-01-06">
    <issue>Force pushed without permission</issue>
    <solution>Always confirm with user first</solution>
    <prevention>Added to global rules</prevention>
  </lesson>
  ```

## 🚦 Implementation Priority

1. **Immediate** (Do now):
   - Add frontmatter to all files
   - Create `.cursorindexingignore`
   - Split long rules

2. **Short-term** (This week):
   - Reorganize into subdirectories
   - Add XML examples
   - Create memory bank

3. **Long-term** (As needed):
   - Build rule validation
   - Create rule templates
   - Share with community

## 💡 Pro Tips from Power Users

1. **"Vibe Coding" Pattern**: 
   - Let Agent generate tests first
   - Then implement to pass tests
   - Finally refactor with confidence

2. **Context Loading**:
   - Use `@File` references in prompts
   - Load multiple rules: "Apply researcher and designer rules"
   - Reference PRs: "Follow patterns from PR #123"

3. **Agent Mode Mastery**:
   - Start with broad request
   - Let Agent ask clarifying questions
   - Use "continue" for iterative refinement

4. **Debugging Workflow**:
   - Create `.cursor/debug-context.md`
   - Track: Input → Process → Output → Error
   - Reference in rules for pattern matching

## 🎬 Example Enhanced Rule

Here's how your `00-global.mdc` could look with all improvements:

```yaml
---
alwaysApply: true
---
# Global Constraints

<rules>
  <rule priority="critical">
    <constraint>No git push --force without explicit user confirmation</constraint>
    <example type="valid">User: "Yes, force push" → git push --force</example>
    <example type="invalid">git push --force (no confirmation)</example>
  </rule>
  
  <rule priority="high">
    <constraint>Read files before editing</constraint>
    <verification>Check file exists and review content</verification>
  </rule>
</rules>

<principles>
  - Trust LLM intelligence over rigid templates
  - Include debug context in all outputs
  - Run security audits on dependencies
</principles>
```

## 📊 Measuring Success

Track these metrics:
1. **Rule trigger rate**: Which rules activate most?
2. **Agent accuracy**: Fewer corrections needed?
3. **Development speed**: Tasks completed faster?
4. **Error reduction**: Fewer force-push incidents?

## 🔗 Community Resources

- [BMad's Rule Generator](https://github.com/bmadcode/cursor-custom-agents-rules-generator)
- [Awesome Cursor Rules](https://github.com/PatrickJS/awesome-cursorrules)
- [Cursor Forum](https://forum.cursor.com) - Search "rules" and "agent mode"

Remember: The best rules are discovered through iteration. Start with these improvements, then refine based on your specific workflow patterns.