# Phase 6: Rollback Plan

## Goal

Design a rollback plan before the human user performs backend deployment work.

This phase answers:

```text
If deployment fails, how can the system return to the previous stable state?
```

## Input required

Use the reports from:

- Phase 1: Server Discovery
- Phase 2: Architecture Analysis
- Phase 3: Risk Analysis
- Phase 4: Change Impact Analysis
- Phase 5: Isolated Deployment Plan

## Scope

This is a planning-only phase. Do not make system changes.

The AI must not operate the server in this phase.

The rollback plan will later be summarized into the human deployment guide in Phase 7.

## Rollback areas

Create rollback guidance for:

- Project directory
- Application process
- Nginx configuration
- Domain / DNS assumptions
- SSL certificate changes
- Environment variables
- Database changes
- Docker changes if applicable
- PM2 changes if applicable
- Log files
- Health check verification

## Required output format

```markdown
# Phase 6: Rollback Plan

## 1. Rollback strategy summary

## 2. Pre-deployment backup checklist

| Item | Backup needed? | Method | Notes |
|---|---|---|---|

## 3. Rollback triggers

List conditions that should trigger rollback, for example:

- New service cannot start
- Nginx configuration validation fails
- Existing service becomes unreachable
- New domain returns error
- CPU, memory, or disk usage becomes abnormal
- Database migration fails

## 4. Rollback steps

### Step 1: Stop or remove only the new project process

### Step 2: Restore or remove the new Nginx configuration

### Step 3: Restore environment variable state

### Step 4: Revert database changes if any

### Step 5: Verify existing services

### Step 6: Confirm server health

## 5. Verification checklist after rollback

| Check | Expected result | Pass/Fail |
|---|---|---|

## 6. Estimated rollback complexity

Choose one:

- Low
- Medium
- High

Reason:

## 7. User decisions required before Phase 7 Human Deployment Guide

Phase 6 completed. Waiting for user confirmation before moving to the next phase.
```

## Stop condition

After completing this plan, stop.

Do not proceed to Phase 7 Human Deployment Guide until the user says:

```text
Continue to next phase
```
