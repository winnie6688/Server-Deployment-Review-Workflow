# Workflow Overview

Server Deployment Review Workflow is a staged review process for AI-assisted deployment planning.

It is designed for situations where a user wants to add a new project to a server that already runs existing services.

The AI does not autonomously operate the server in this workflow.

Instead, the AI helps the user inspect, analyze, plan, and finally produce a human-readable deployment guide.

## Why staged review matters

AI Coding tools can generate deployment steps quickly, but speed is not always safe.

On an existing server, the AI must first help the user understand the current environment:

- Which services are already running
- Which ports are already occupied
- How traffic is routed
- Which process manager is used
- Which data services exist
- Which files and configurations must be protected
- Which sensitive discovery outputs require redaction

A deployment is not only a code task. It is a system change.

## Seven phases

### Phase 1: Server Discovery

Collect safe discovery information about the server.

Phase 1 uses two discovery modes:

- AI-executable low-risk discovery
- Human-executed sensitive discovery with redaction

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

### Phase 7: Human Deployment Guide

Generate a human-readable guide that the user can review and use when performing backend deployment manually.

Phase 7 does not mean the AI operates the server.

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

At Phase 7, ask the AI to generate the human deployment guide.

The user should review the guide and perform backend deployment manually.

## Human-in-the-loop principle

The user should review each phase before the AI proceeds.

This prevents early misunderstandings from becoming later deployment mistakes.

The final output of the workflow is not an autonomous deployment action.

The final output is a clear guide for human-controlled backend deployment.