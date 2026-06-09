# Server Deployment Review Workflow

A staged review workflow for deploying new projects on existing servers with AI Coding tools.

This repository provides a structured process for AI agents and AI Coding tools to inspect, analyze, plan, and prepare a human-readable deployment guide before a new project is added to an existing server.

It is designed to reduce deployment risks such as:

- Port conflicts
- Nginx configuration conflicts
- PM2 process conflicts
- Docker container conflicts
- Environment variable pollution
- Database conflicts
- Missing rollback plans
- Accidental impact on existing services
- Accidental exposure of sensitive configuration, logs, tokens, or environment variables

## Why this project exists

AI Coding tools are becoming increasingly capable of writing applications and generating deployment steps. However, deploying a new project to an existing server is not only a coding task. It is a system change.

Before deployment, an AI agent should help the user understand:

- What is already running on the server
- Which ports are occupied
- How Nginx routes traffic
- Whether PM2, Docker, or systemd is managing existing services
- Which databases and caches are in use
- What resources may be affected by the new project
- How to roll back if deployment fails
- Which discovery outputs may contain sensitive information and require human redaction
- What deployment steps the human user should perform manually

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
Phase 7: Human Deployment Guide
```

## Phase 1 discovery model

Phase 1 uses a two-part discovery model:

```text
Phase 1 = AI-executable low-risk discovery + human-executed sensitive discovery
```

The AI may run low-risk read-only commands directly, such as:

- System information checks
- Resource usage checks
- Port usage checks
- Process overview checks
- Common deployment tool detection
- Shallow project directory scanning

However, some read-only commands may expose sensitive information. These should be executed by the human manually, redacted, and then pasted back as summaries.

Sensitive discovery areas include:

- Full Nginx configuration
- Environment variables and `.env` files
- `docker inspect`
- Application logs and system logs
- `docker-compose.yml`
- `ecosystem.config.js`

Core rule:

```text
Read-only does not always mean safe.
```

A command may be read-only but still unsafe to expose directly if it prints secrets, tokens, environment variables, private routing rules, logs, or business data.

## Core principle

Do not deploy first.

Review first.

Guide the human user clearly.

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

The AI is allowed to inspect, analyze, plan, and prepare guidance.

Safety in this workflow includes both system safety and information safety.

The AI must not directly:

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
- Request or print full secrets, tokens, private keys, passwords, cookies, or database connection strings
- Request or print full production logs without redaction
- Operate the server as an autonomous deployment agent

Phase 7 does not mean the AI starts deployment.

Phase 7 means the AI generates a human-readable deployment guide based on the reviewed information from Phase 1 to Phase 6.

The human user performs backend deployment manually.

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
│   ├── architecture-summary-template.md
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
4. In Phase 1, let the AI run only Class A low-risk discovery commands.
5. For Class B sensitive discovery, run the command manually, redact sensitive values, and paste back only the necessary summary.
6. Review the output manually.
7. Continue to the next phase only after confirmation.
8. In Phase 7, ask the AI to generate the human deployment guide.
9. Review the guide and perform backend deployment manually.

## Design philosophy

This workflow treats AI-assisted deployment as a controlled system change, not a casual command execution task.

It also treats server discovery as both an engineering task and an information-safety task.

The goal is to help users move from:

```text
Let AI write and deploy code
```

to:

```text
Let AI help review, plan, and generate safe human deployment guidance
```
