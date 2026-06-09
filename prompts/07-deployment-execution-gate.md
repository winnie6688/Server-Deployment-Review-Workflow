# Phase 7: Human Deployment Guide

## Goal

Create a human-readable deployment guide based on the completed Phase 1 to Phase 6 reports.

Phase 7 is not for autonomous operation.

The AI does not operate the server. The AI only prepares a clear guide for the user to review and use in their own backend environment.

## Core principle

```text
AI prepares the guide.
Human performs the backend work.
```

## Required inputs

Before creating the guide, confirm that these reports exist:

- Phase 1: Server Discovery Report
- Phase 2: Architecture Analysis Report
- Phase 3: Risk Analysis Report
- Phase 4: Change Impact Analysis Report
- Phase 5: Isolated Deployment Plan
- Phase 6: Rollback Plan

If any report is missing, do not create the final guide. Ask the user to complete the missing phase first.

## What Phase 7 should produce

Phase 7 should produce a final guide for the user, including:

1. Deployment readiness summary
2. Final deployment plan summary
3. Resources that must not be touched
4. Human execution checklist
5. Verification checklist
6. Rollback summary
7. Final reminders

## Important boundary

The AI must not claim that it will operate the server.

The AI should write the guide in a way that makes clear:

- The user will review each step.
- The user will perform backend work manually.
- Sensitive values should stay on the server and should not be pasted into public chat.
- If the actual result differs from the expected result, the user should stop and ask for review.

## Required output format

```markdown
# Phase 7: Human Deployment Guide

## 1. Deployment readiness summary

| Phase | Completed? | Key conclusion | Notes |
|---|---|---|---|
| Phase 1 Server Discovery |  |  |  |
| Phase 2 Architecture Analysis |  |  |  |
| Phase 3 Risk Analysis |  |  |  |
| Phase 4 Change Impact Analysis |  |  |  |
| Phase 5 Isolated Deployment Plan |  |  |  |
| Phase 6 Rollback Plan |  |  |  |

## 2. Final deployment plan summary

Summarize the final plan in plain language.

Include:

- Project name
- Project directory
- Runtime method
- Internal port
- Domain
- Reverse proxy strategy
- HTTPS strategy
- Environment file strategy
- Process manager strategy
- Database strategy if applicable

## 3. Resources that must not be touched

| Resource | Protection rule | Reason |
|---|---|---|

## 4. Human execution checklist

For each step, include:

- Purpose
- Suggested action
- Expected result
- Check before continuing
- Stop condition

Suggested sections:

### Step 1: Prepare project location

### Step 2: Place project code

### Step 3: Prepare runtime dependencies

### Step 4: Prepare environment configuration

### Step 5: Start project runtime

### Step 6: Prepare reverse proxy routing

### Step 7: Prepare HTTPS if needed

### Step 8: Verify the new project

### Step 9: Verify existing services

## 5. Verification checklist

| Check | Suggested method | Expected result | Status |
|---|---|---|---|
| New project runtime |  |  |  |
| Internal port |  |  |  |
| Reverse proxy routing |  |  |  |
| New domain |  |  |  |
| Existing API |  |  |  |
| Existing web service |  |  |  |
| Resource usage |  |  |  |

## 6. Rollback summary

Summarize the rollback plan from Phase 6.

## 7. Final reminder

The AI has not performed backend work.

The user should review and use this guide manually.

If any actual result differs from the expected result, stop and ask for review before continuing.
```

## Stop condition

After producing the human deployment guide, stop.

Do not operate the server.
