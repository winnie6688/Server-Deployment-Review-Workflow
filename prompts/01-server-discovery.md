# Phase 1: Server Discovery

## Goal

Inspect the current server state before any deployment planning.

This phase is read-only.

## Restrictions

You must not:

- Create files or directories
- Modify files
- Delete files
- Install software
- Restart services
- Stop services
- Modify configuration
- Upload code

## Commands to run

### 1. System environment

```bash
uname -a
cat /etc/os-release
hostname
whoami
pwd
```

Output:

- Operating system
- Linux distribution
- Current user
- Current working directory
- Hostname
- Permission observations

### 2. Server resources

```bash
df -h
free -h
uptime
```

Analyze:

- CPU load
- Memory usage
- Disk usage
- System uptime
- Whether the server appears suitable for another project

### 3. Project directories

```bash
ls -la /
ls -la /var/www || true
ls -la /opt || true
ls -la /home || true
find / -maxdepth 3 -type f -name "package.json" 2>/dev/null
find / -maxdepth 3 -type f -name "docker-compose.yml" 2>/dev/null
```

Output:

| Project directory | Possible stack | Notes |
|---|---|---|

### 4. Port usage

```bash
ss -tulpn
```

Output:

| Port | Service | PID/process | Status |
|---|---|---|---|

Also list:

- Occupied ports
- Possible available port ranges

### 5. Node.js and PM2

```bash
which node || true
node -v || true
which npm || true
npm -v || true
which pm2 || true
pm2 list || true
```

Output:

| PM2 name | Status | Port if known | Project if known |
|---|---|---|---|

### 6. Docker

```bash
which docker || true
docker ps || true
docker images || true
```

Output:

| Container | Image | Port mapping |
|---|---|---|

### 7. systemd services

```bash
systemctl list-units --type=service --state=running --no-pager
```

Classify services into:

- Web services
- Database services
- Cache services
- AI services
- Custom business services
- Other system services

### 8. Nginx

```bash
which nginx || true
nginx -v || true
nginx -T
```

Output:

| Domain | Proxy target / port | Config file |
|---|---|---|

Analyze:

- Existing domains
- Existing reverse proxies
- Whether the server appears ready for an additional site

### 9. Databases and cache

```bash
systemctl status mysql --no-pager || true
systemctl status mariadb --no-pager || true
systemctl status postgresql --no-pager || true
systemctl status redis --no-pager || true
```

Analyze:

- Database type
- Redis usage
- Whether reuse may be possible
- Whether a separate database is recommended later

## Required output format

```markdown
# Phase 1: Server Discovery Report

## 1. System environment

## 2. Server resources

## 3. Project directory findings

## 4. Port usage

## 5. Node.js / PM2 findings

## 6. Docker findings

## 7. systemd service findings

## 8. Nginx findings

## 9. Database and cache findings

## 10. Initial observations

## 11. Open questions for the user

Phase 1 completed. Waiting for user confirmation before moving to the next phase.
```

## Stop condition

After completing this report, stop.

Do not proceed to architecture analysis until the user says:

```text
Continue to next phase
```
