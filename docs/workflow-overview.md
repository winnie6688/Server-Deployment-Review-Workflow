# Workflow Overview

Server Deployment Review Workflow is a staged review process for AI-assisted deployment.

It is designed for situations where a user wants to add a new project to a server that already runs existing services.

## Why staged review matters

AI Coding tools can write and run deployment commands quickly, but speed is not always safe.

On an existing server, the AI must first understand the current environment:

- Which services are already running
- Which ports are already occupied
- How traffic is routed
- Which process manager is used
- Which data services exist
- Which files and configurations must be protected

A deployment is not only a code task. It is a system change.

## Seven phases

### Phase 1: Server Discovery

Collect read-only information about the server.

### Phase 2: Architecture Analysis

Turn discovery results into a clear architecture view.

### Phase 3: Risk Analysis

Identify risks before planning the new deployment.

### Phase 4: Change Impact Analysis

Analyze which existing resources may be affected by the new project.

### Phase 5: Isolated Deployment Plan

Design a deployment plan that minimizes conflicts.

### Phase 6: Rollback Plan

Plan how to return to the previous stable state if deployment fails.

### Phase 7: Deployment Execution Gate

Require explicit user confirmation before deployment begins.

## Recommended operating mode

Do not ask the AI to run all phases at once.

Use one phase at a time:

```text
Run Phase 1 only.
Stop after the report.
Wait for my confirmation.
```

Then continue:

```text
Continue to next phase.
```

Only start deployment when the user says:

```text
Start deployment
```

## Human-in-the-loop principle

The user should review each phase before the AI proceeds.

This prevents early misunderstandings from becoming later deployment mistakes.
