# Phase 3: Risk Analysis

## Goal

Review the possible risks of adding a new project to an existing server.

This phase uses the Phase 1 and Phase 2 reports as input.

## Scope

This is an analysis-only phase. Do not make system changes.

## Risk categories

Analyze the following categories.

### 1. Port risk

Check whether the new project may conflict with existing ports.

Risk level:

- High
- Medium
- Low

### 2. Nginx risk

Check whether adding a new site or reverse proxy may conflict with existing Nginx configuration.

Consider:

- Existing server_name rules
- Existing proxy_pass targets
- HTTP and HTTPS handling
- SSL certificate configuration
- Default server behavior

### 3. PM2 risk

Check whether PM2 process names, startup scripts, or runtime behavior may conflict.

### 4. Docker risk

Check whether Docker containers, networks, volumes, images, or port mappings may conflict.

### 5. Database risk

Check whether the new project may affect existing databases.

Consider:

- Shared database usage
- Table name collisions
- Schema separation
- Migration risk
- Backup requirements

### 6. Environment variable risk

Check whether the new project may depend on shared or global environment variables.

### 7. File system risk

Check whether the new project may overlap with existing directories, logs, uploads, or configuration files.

### 8. Resource risk

Check whether CPU, memory, disk, or process limits may become a bottleneck.

### 9. Access and permission risk

Check whether the current access level is sufficient and whether elevated privileges are needed for later deployment.

## Required output format

```markdown
# Phase 3: Risk Analysis Report

## 1. Risk summary

| Risk category | Level | Reason | Evidence | Mitigation |
|---|---|---|---|---|

## 2. Detailed risk analysis

### Port risk

### Nginx risk

### PM2 risk

### Docker risk

### Database risk

### Environment variable risk

### File system risk

### Resource risk

### Access and permission risk

## 3. High-priority risks

## 4. Medium-priority risks

## 5. Low-priority risks

## 6. Required user decisions before deployment planning

Phase 3 completed. Waiting for user confirmation before moving to the next phase.
```

## Stop condition

After completing this report, stop.

Do not proceed to change impact analysis until the user says:

```text
Continue to next phase
```
