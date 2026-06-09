# Phase 4: Change Impact Analysis

## Goal

Analyze which existing resources may be affected by deploying the new project.

This phase answers one core question:

```text
If this new project is added, who or what may be affected?
```

## Input required

Use the reports from:

- Phase 1: Server Discovery
- Phase 2: Architecture Analysis
- Phase 3: Risk Analysis

If the user has provided new project information, also use:

- Project name
- Expected runtime
- Expected port
- Expected domain
- Expected database usage
- Expected deployment method

## Scope

This is an analysis-only phase. Do not make system changes.

## Impact areas

Analyze possible impact on:

- Domains
- Nginx configuration
- Ports
- PM2 processes
- Docker containers
- Docker networks and volumes
- Databases
- Redis or cache services
- File storage
- Upload directories
- Log directories
- SSL certificates
- Environment variables
- Existing projects

## Required output format

```markdown
# Phase 4: Change Impact Analysis Report

## 1. Change summary

Describe the intended new project deployment in plain language.

## 2. Impact matrix

| Resource | Current user | Proposed new usage | Affected? | Risk level | Notes |
|---|---|---|---|---|---|

## 3. Existing services that must not be touched

| Service/project | Reason | Protection rule |
|---|---|---|

## 4. Shared resources

| Shared resource | Existing usage | New project usage | Isolation recommendation |
|---|---|---|---|

## 5. Isolation classification

Choose one:

- Fully isolated
- Partially shared resources
- Highly dependent on existing system

Explain the reason.

## 6. User decisions required

Phase 4 completed. Waiting for user confirmation before moving to the next phase.
```

## Stop condition

After completing this report, stop.

Do not proceed to isolated deployment planning until the user says:

```text
Continue to next phase
```
