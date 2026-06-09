# Phase 7: Deployment Execution Gate

## Goal

This phase is the final gate before deployment.

No deployment action is allowed unless the user explicitly confirms.

## Required confirmation

The user must explicitly say:

```text
Start deployment
```

Without this exact confirmation, do not deploy.

## Required inputs before deployment

Before any deployment action, confirm that the following reports exist:

- Phase 1: Server Discovery Report
- Phase 2: Architecture Analysis Report
- Phase 3: Risk Analysis Report
- Phase 4: Change Impact Analysis Report
- Phase 5: Isolated Deployment Plan
- Phase 6: Rollback Plan

## Pre-deployment confirmation checklist

```markdown
# Phase 7: Deployment Execution Gate

## 1. Reports completed

| Report | Completed? | Notes |
|---|---|---|
| Phase 1 Server Discovery |  |  |
| Phase 2 Architecture Analysis |  |  |
| Phase 3 Risk Analysis |  |  |
| Phase 4 Change Impact Analysis |  |  |
| Phase 5 Isolated Deployment Plan |  |  |
| Phase 6 Rollback Plan |  |  |

## 2. Planned changes

| Change item | Planned value | Risk | Rollback method |
|---|---|---|---|

## 3. Resources that must not be touched

| Resource | Protection rule |
|---|---|

## 4. Final user confirmation required

Deployment has not started.

Please confirm with:

Start deployment
```

## Execution discipline after confirmation

If the user confirms deployment, execute step by step.

For each step:

1. State what will be changed.
2. Run the minimal necessary command.
3. Show the result.
4. Verify whether the step succeeded.
5. Stop immediately if a critical error occurs.

## Post-deployment verification

After deployment, verify:

- New project process is running
- New port is listening
- Nginx configuration is valid
- Domain or route works if applicable
- Existing services are still reachable
- Logs do not show critical errors
- Resource usage is normal

## Stop condition

If the user has not said `Start deployment`, stop at the gate.
