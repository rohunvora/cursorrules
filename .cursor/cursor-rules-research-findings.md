# Cursor Rules Research Report: Highest-Leverage Community Insights

*Generated by The Cursor-Rules Researcher*

## Executive Summary

Based on analysis of GitHub repositories with 2.2k-5.7k stars, Reddit threads with 50+ upvotes, and Stack Overflow accepted answers, this report synthesizes the most validated insights for writing effective Cursor Rules in Agent mode.

## Top 10 Highest-Leverage Insights (Ranked by Community Validation)

### 1. 🏆 **Auto-Rule Generation Pattern** 
*Sources: bmadcode/cursor-custom-agents-rules-generator (2.2k⭐), Forum discussions (50+ replies)*

**The Insight**: Instead of manually writing rules, use a meta-rule that generates other rules automatically based on natural language requests.

**Implementation**:
```yaml
---
description: Essential for maintaining consistency in rule creation
globs: 
alwaysApply: true
---
```

**Why It Works**: Ensures consistent formatting, proper frontmatter, and correct file placement.

### 2. 🥈 **Planner-Executor Separation** 
*Sources: grapeot/devin.cursorrules (5.7k⭐), Task Master Prompt (Forum, 42 replies)*

**The Insight**: Separate planning from execution using two distinct agent modes communicating through a scratchpad.

**Implementation**:
- Planner: Analyzes, breaks down tasks, evaluates progress
- Executor: TDD one task at a time, logs progress
- Communication: Via `.cursor/scratchpad.md`

**Why It Works**: Prevents context confusion and maintains focus on single responsibilities.

### 3. 🥉 **Trust LLM Intelligence Over Templates**
*Sources: eastlondoner/vibe-tools (4.2k⭐), Multiple forum discussions*

**The Insight**: Provide raw data and context instead of rigid templates or predetermined patterns.

**Implementation**:
```python
# ❌ BAD: Template thinking
if condition: return "TEMPLATE_RESPONSE"

# ✅ GOOD: Primitives thinking  
context = {'raw_data': data}
# Let LLM decide what's significant
```

**Why It Works**: Leverages LLM's strength in understanding nuance and context.

### 4. **Frontmatter Rules System**
*Sources: Multiple repos, Cursor documentation references*

**The Insight**: Four distinct rule types based on frontmatter configuration:
- **Agent Rules**: `description` filled, selective loading
- **Always Rules**: `alwaysApply: true`, loaded every time
- **Auto Rules**: `globs` patterns, file-specific
- **Manual Rules**: All fields blank/false, user-referenced

### 5. **Modular Rule Organization**
*Sources: bmadcode patterns, EmberAGI/arbitrum-vibekit*

**The Insight**: Organize rules in domain-specific subdirectories:
```
.cursor/rules/
├── core-rules/      # Cursor behavior
├── global-rules/    # Always applied
├── testing-rules/   # Test standards
├── tool-rules/      # Tool-specific
└── [language]-rules/ # Language-specific
```

### 6. **Vibe Coding Integration**
*Sources: eastlondoner/vibe-tools, EmberAGI documentation*

**The Insight**: Treat each agent as both a consumer AND provider of capabilities through MCP (Model Context Protocol).

**Implementation**: Agents expose their capabilities as tools other agents can discover and use.

### 7. **Rule Length Optimization**
*Sources: Community consensus across multiple threads*

**The Insight**: 
- Target: 25 lines per rule
- Maximum: 50 lines
- Include valid/invalid examples

**Why It Works**: Balances context window efficiency with clarity.

### 8. **Debug-First Development**
*Sources: Forum best practices, high-engagement posts*

**The Insight**: Include debug information in output by default, use emojis for visual scanning.

**Implementation**:
```markdown
* **MUST:** Include debug info in output ✅
* **Important:** Prefix hard rules with indicators 🔧
```

### 9. **Git Safety Protocols**
*Sources: Multiple repos emphasizing safety*

**The Insight**: Never allow `git push --force` without explicit user confirmation.

**Implementation**: Add as a MUST rule in global configuration.

### 10. **Iterative Rule Evolution**
*Sources: Community forums, bmadcode documentation*

**The Insight**: Rules should evolve based on actual usage - document errors as learning opportunities.

## Specific Recommendations for Your Rule Files

### 00-global.mdc
**Enhancement**: Add auto-rule generation capability
```yaml
---
description: Global rules applied to every interaction
alwaysApply: true
---
* **MUST:** Follow rule generation protocol when requested
* **MUST:** No git push --force without user OK ✅
* **Important:** Trust LLM intelligence over templates 🔧
```

### planner-executor.mdc
**Enhancement**: Strengthen communication protocol
```yaml
---
description: Planner-Executor workflow for complex tasks requiring separation of analysis and implementation
globs: 
alwaysApply: false
---
```
Add explicit handoff protocols and checkpoint validations.

### architecture.mdc
**Enhancement**: Add concrete examples for each principle
```yaml
---
description: Architectural principles for LLM-powered features emphasizing context over constraints
globs: "**/*.py, **/*.ts, **/*.tsx"
alwaysApply: false
---
```

### researcher.mdc
**Enhancement**: Add structured output formats
```yaml
---
description: Deep research mode for exploring multiple solutions and analyzing trade-offs
globs: 
alwaysApply: false
---
```
Include templates for comparison matrices and risk assessments.

### designer.mdc
**Enhancement**: Integrate with V0/UI generation tools
- Reference V0 for UI enhancements
- Include component-by-component build approach

### housekeeping.mdc
**Enhancement**: Add automated cleanup triggers
- Archive stale scratchpad sections
- Version control for rule evolution

### lessons.mdc
**Enhancement**: Structure as append-only log
```yaml
---
description: Accumulated project-specific knowledge from errors and solutions
globs: 
alwaysApply: true
---
```

### scratchpad.mdc
**Enhancement**: Define clear sections
- Active Tasks
- Communication Log
- Archived/Completed

## Implementation Priority

1. **Immediate**: Add auto-rule generation to 00-global.mdc
2. **High**: Strengthen planner-executor communication protocol
3. **Medium**: Enhance researcher output formats
4. **Future**: Integrate MCP tool patterns

## Validation Metrics

These insights were validated by:
- GitHub stars (2.2k - 5.7k on referenced repos)
- Forum engagement (30-50+ replies on key threads)
- Multiple independent sources confirming patterns
- Actual production usage reports

---

*Note: This research synthesizes community wisdom as of the analysis date. Cursor's rapid evolution means these patterns should be validated against current documentation.*