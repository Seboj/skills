# Lessons Learned — Living Document

**ALL AGENTS MUST READ THIS FILE before acting.** This document captures past mistakes, patterns to avoid, and hard-won knowledge. When a bug is found and fixed, the pattern gets added here so no agent repeats it.

---

## How to Use This File

- **Before implementing**: Check if your planned change matches a known pitfall below
- **After a bug fix**: Add the pattern here — what went wrong, why, and how to avoid it
- **Format**: Each lesson has a category, the mistake, the root cause, and the rule to follow

---

## Example Lessons

> **Replace these with your project's actual lessons as they're discovered.**
> **Delete the examples once you have real entries.**

### TS-001: Optional chaining on API response arrays
**Mistake**: Using `data?.items.map()` — crashes when `items` is undefined
**Root Cause**: API returns the object but nested arrays may be undefined during loading
**Rule**: ALWAYS use `data?.items?.map()` — double optional chain on nested properties

### API-001: Notification/audit services never throw
**Mistake**: Letting notification or audit errors propagate and crash callers
**Root Cause**: Observability is a side effect, not part of the critical path
**Rule**: ALWAYS wrap notification and audit calls in try/catch. Log errors, never rethrow.

### DB-001: Decimal for money, always
**Mistake**: Using Float or Number for monetary values
**Root Cause**: Floating-point precision loss
**Rule**: ALL monetary columns use `Decimal(19,4)`. Serialize as strings for JSON transport.

### TOOL-001: Jira MCP OAuth expires intermittently
**Mistake**: Assuming mcp__atlassian__* tools always work
**Root Cause**: OAuth token expiration
**Rule**: Always try MCP tools first. On 401, fall back to curl with Basic Auth.

### TOOL-002: Automated audit agents produce false positives
**Mistake**: Implementing "fixes" for gaps that were already resolved
**Root Cause**: Audit agents check for patterns but can't always verify functionality
**Rule**: ALWAYS manually verify alleged gaps by reading the actual source code before implementing fixes.

---

## Adding New Lessons

When a bug is found and fixed, add it here using this template:

```markdown
### [CATEGORY]-XXX: Short title
**Mistake**: What went wrong
**Root Cause**: Why it happened
**Rule**: What to do instead — the rule that prevents recurrence
**Files affected**: [optional] specific files
**Ticket**: [optional] PROJECT-XXX
```

Categories: TS (TypeScript/Build), API (Backend), FE (Frontend), DB (Database), PIPE (Pipeline), OBS (Observability), TOOL (Tooling), SEC (Security)

---
*Last updated: — initialized with example lessons*
