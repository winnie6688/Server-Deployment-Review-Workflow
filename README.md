# Server Deployment Review Workflow

A staged review workflow for deploying new projects on existing servers with AI Coding tools.

This repository provides a structured process for AI agents and AI Coding tools to inspect, analyze, and plan before deploying a new project to an existing server.

It is designed to reduce deployment risks such as:

- Port conflicts
- Nginx configuration conflicts
- PM2 process conflicts
- Docker container conflicts
- Environment variable pollution
- Database conflicts
- Missing rollback plans
- Accidental impact on existing services

## Why this project exists

AI Coding tools are becoming increasingly capable of writing and deploying applications. However, deploying a new project to an existing server is not only a coding task. It is a system change.

Before deployment, an AI agent should understand:

- What is already running on the server
- Which ports are occupied
- How Nginx routes traffic
- Whether PM2, Docker, or systemd is managing existing services
- Which databases and caches are in use
- What resources may be affected by the new project
- How to roll back if deployment fails

## Workflow

```text
Phase 1: Server Discovery
↓
Phase 2: Architecture Analysis
↓
Phase 3: Risk Analysis
↓
Phase 4: Change Impact Analysis
↓
Phase 5: Isolated Deployment Plan
↓
Phase 6: Rollback Plan
↓
Phase 7: Deployment Execution Gate
```

## Core principle

Do not deploy first.

Review first.

## Recommended usage

Use this workflow with:

- ChatGPT Codex
- Claude Code
- Cursor
- TRAE
- OpenHands
- Coze Agent
- Other AI Coding tools

## Safety rule

Before the final deployment phase, the AI is only allowed to inspect, analyze, and plan.

It must not:

- Create project directories
- Upload code
- Delete files
- Modify configuration
- Restart services
- Stop services
- Change Nginx
- Change PM2
- Change Docker
- Change databases

Deployment can only begin after the user explicitly says:

```text
Start deployment
```

## Repository structure

```text
Server-Deployment-Review-Workflow/
├── README.md
├── prompts/
│   ├── 00-master-workflow.md
│   ├── 01-server-discovery.md
│   ├── 02-architecture-analysis.md
│   ├── 03-risk-analysis.md
│   ├── 04-change-impact-analysis.md
│   ├── 05-isolated-deployment-plan.md
│   ├── 06-rollback-plan.md
│   └── 07-deployment-execution-gate.md
├── templates/
│   ├── server-inventory-template.md
│   ├── architecture-report-template.md
│   ├── risk-report-template.md
│   ├── change-impact-report-template.md
│   ├── deployment-plan-template.md
│   └── rollback-plan-template.md
├── examples/
│   └── sample-review-report.md
└── docs/
    ├── workflow-overview.md
    └── terminology.md
```

## How to use

1. Copy `prompts/00-master-workflow.md` into your AI Coding tool.
2. Set the current phase, starting from Phase 1.
3. Let the AI complete only the current phase.
4. Review the output manually.
5. Continue to the next phase only after confirmation.
6. Do not allow deployment until Phase 7.

## Design philosophy

This workflow treats AI-assisted deployment as a controlled system change, not a casual command execution task.

The goal is to help users move from:

```text
Let AI write and deploy code
```

to:

```text
Let AI follow engineering review discipline before system changes
```
