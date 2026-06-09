# Phase 5: Isolated Deployment Plan

## Goal

Design a safe deployment plan for the new project based on previous review phases.

The deployment plan must avoid conflicts with existing services.

## Input required

Use the reports from:

- Phase 1: Server Discovery
- Phase 2: Architecture Analysis
- Phase 3: Risk Analysis
- Phase 4: Change Impact Analysis

Also use the new project requirements provided by the user.

## Scope

This is a planning-only phase. Do not make system changes.

## Planning areas

Design recommendations for:

- Project directory
- Runtime method
- Port
- Process manager name
- Environment variable file
- Nginx config file
- Domain or subdomain
- Log directory
- Database strategy
- Cache strategy
- File upload/storage strategy
- Monitoring or health check idea

## Required output format

```markdown
# Phase 5: Isolated Deployment Plan

## 1. Deployment strategy summary

## 2. Recommended project directory

```text
/var/www/my-new-project
```

Reason:

## 3. Recommended port

```text
3010
```

Reason:

## 4. Recommended process manager

Example:

```text
PM2 process name: my-new-project
```

Reason:

## 5. Recommended environment variable strategy

Example:

```text
/var/www/my-new-project/.env
```

Rules:

- Do not use global environment variables unless necessary.
- Do not reuse unrelated project secrets.
- Keep project-specific secrets inside the project environment file.

## 6. Recommended Nginx strategy

Example:

```text
/etc/nginx/sites-available/my-new-project.conf
```

or:

```text
/etc/nginx/conf.d/my-new-project.conf
```

Reason:

## 7. Recommended domain strategy

Example:

```text
project.example.com
```

Reason:

## 8. Recommended database strategy

Choose one:

- Independent database
- Shared database with independent schema
- Shared database with table prefix
- External managed database
- No database required

Reason:

## 9. Recommended logging strategy

Example:

```text
/var/log/my-new-project
```

Reason:

## 10. Deployment change preview

| Item | Proposed value | Reason | Conflict risk |
|---|---|---|---|

## 11. User decisions required before rollback planning

Phase 5 completed. Waiting for user confirmation before moving to the next phase.
```

## Stop condition

After completing this plan, stop.

Do not proceed to rollback planning until the user says:

```text
Continue to next phase
```
