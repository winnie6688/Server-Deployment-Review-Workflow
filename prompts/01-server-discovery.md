# Phase 1: Server Discovery

## Goal

Safely inspect the current server state before any deployment planning.

Phase 1 is not a deployment phase. It is a discovery phase.

The goal is to understand:

1. Which projects are already running on the server
2. Which ports are already in use
3. Whether Nginx, Docker, PM2, systemd, or other deployment methods are present
4. Whether server resources are sufficient for a new project
5. Whether a new project may cause port, directory, reverse proxy, process, or resource conflicts

## Core design

Phase 1 uses a two-part discovery model:

```text
Phase 1 = AI-executable low-risk discovery + human-executed sensitive discovery
```

The AI should automatically run low-risk read-only commands.

For commands that may expose secrets, tokens, environment variable values, private configuration, request logs, or business data, the AI must not directly collect the full output. Instead, the human should run the command manually, redact sensitive values, and paste back only the necessary summary.

## Safety principle

Read-only does not always mean safe.

Some commands do not modify the server, but their output may expose sensitive information.

Before running or requesting any command output, classify it as one of the following:

| Class | Executor | Meaning |
|---|---|---|
| A | AI | Low-risk read-only command. The AI may run it directly. |
| B | Human | Sensitive read-only command. The human should run it manually, redact the output, and paste back only necessary information. |

## Global restrictions

During Phase 1, neither the AI nor the human should use this workflow to perform deployment changes.

Do not:

- Create files or directories
- Modify files
- Delete files
- Install software
- Restart services
- Stop services
- Modify configuration
- Upload code
- Change Nginx
- Change PM2
- Change Docker
- Change databases
- Change environment variables

## Sensitive information handling rule

Never print or request full sensitive values.

Redact values such as:

- API keys
- access_token
- refresh_token
- AppSecret
- Authorization headers
- Cookies
- Database connection strings
- Private keys
- Passwords
- OpenID or user identifiers
- Full request bodies
- Full production logs

Use `***` when redacting.

Example:

```text
WECHAT_APP_SECRET=***
Authorization: Bearer ***
proxy_pass http://127.0.0.1:***
```

---

# A. AI-executable low-risk read-only commands

The AI may run the following commands directly because they are read-only and usually do not expose secrets.

## A1. System information

```bash
uname -a
cat /etc/os-release
uptime
whoami
pwd
```

Use this to identify:

- Operating system
- Linux distribution
- System uptime
- Current user
- Current working directory

## A2. Resource usage

```bash
free -h
df -h
lsblk
```

Use this to identify:

- Memory availability
- Disk usage
- Mounted disks
- Whether disk capacity may become a deployment risk

## A3. Port usage

```bash
ss -tulpn
```

If `ss` is unavailable, use:

```bash
netstat -tulpn
```

Use this to identify:

- Occupied ports
- Listening services
- Ports the new project should avoid

Output:

| Port | Protocol | Service/process | PID if visible | Notes |
|---|---|---|---|---|

## A4. Process overview

```bash
ps aux --sort=-%mem | head -30
ps aux --sort=-%cpu | head -30
```

Use this to identify:

- High-memory processes
- High-CPU processes
- Possible Node.js, Python, Java, Nginx, Docker, or database processes
- Whether the server is already under pressure

Do not inspect process-specific environment variables in this phase.

## A5. Common deployment tools

```bash
which nginx || true
which docker || true
which docker-compose || true
which pm2 || true
which node || true
which npm || true
which python3 || true
```

If the corresponding tool exists, the AI may run:

```bash
pm2 list || true
docker ps || true
docker compose ls || true
systemctl is-active nginx || true
```

Use this to identify:

- Whether PM2 is used
- Whether Docker is used
- Whether Docker Compose is used
- Whether Nginx is active
- Whether Node.js or Python is available

Do not run `docker inspect` in Class A.

Do not run `pm2 logs` in Class A.

## A6. Common project directories

The AI may scan common deployment directories at low depth.

```bash
ls -la /var/www 2>/dev/null
ls -la /opt 2>/dev/null
ls -la /srv 2>/dev/null
ls -la /home 2>/dev/null
find /var/www -maxdepth 2 -type d 2>/dev/null
find /opt -maxdepth 2 -type d 2>/dev/null
```

Use this to identify:

- Where existing projects may be deployed
- Whether a new project may conflict with an existing directory name
- Whether a separate project directory is needed

Do not recursively read configuration files during this phase.

---

# B. Human-executed sensitive discovery commands

The following commands may still be read-only, but their output may contain sensitive information.

The AI must not directly collect full raw output from these commands.

The human should run them manually, redact sensitive values, and paste back only the necessary summary.

## B1. Nginx full configuration

Sensitive command:

```bash
sudo nginx -T
```

Reason:

The full Nginx configuration may contain:

- Internal upstream addresses
- proxy_pass internal ports
- Authorization headers
- Certificate paths
- Internal domains
- Basic authentication configuration paths
- Other private routing details

Preferred human-redacted command:

```bash
sudo nginx -T | grep -E "server_name|listen|proxy_pass|root|location" -n
```

The human may also paste a redacted server block:

```nginx
server {
    listen 443 ssl;
    server_name example.com;

    location / {
        proxy_pass http://127.0.0.1:***;
        proxy_set_header Authorization ***;
    }
}
```

Required summary:

| Domain | Listen port | Proxy target | Root path | Config file if known | Notes |
|---|---|---|---|---|---|

## B2. Environment variables and `.env` files

Sensitive commands:

```bash
env
printenv
cat .env
cat .env.production
cat /etc/environment
```

Do not paste full output.

Preferred method: only list variable names, not values.

Example:

```bash
awk -F= '{print $1}' .env
```

Human-redacted summary example:

```text
Confirmed variable names:
- NODE_ENV
- PORT
- FEISHU_APP_ID
- FEISHU_APP_SECRET
- WECHAT_APP_ID
- WECHAT_APP_SECRET
- ACTION_API_KEY

Values are not shared.
```

Required summary:

| Project/path | Env file exists? | Variable names only | Notes |
|---|---|---|---|

## B3. Docker inspect

Sensitive command:

```bash
docker inspect <container-name>
```

Reason:

`docker inspect` may contain:

- Env values
- Database URLs
- API keys
- Registry information
- Mount paths
- Network configuration

Human-redacted summary example:

```text
Container: xxx
Image: xxx
Ports: 3000->3000
Mounts: /opt/project:/app
Networks: bridge
Env: exists, values redacted
```

Required summary:

| Container | Image | Ports | Mounts | Networks | Env values shared? |
|---|---|---|---|---|---|

## B4. Application logs and system logs

Sensitive commands:

```bash
journalctl -u <service-name>
pm2 logs
docker logs <container-name>
tail -n 200 app.log
```

Reason:

Logs may contain:

- access_token
- refresh_token
- openid
- Request body
- Third-party API response
- User data
- Callback URL

Do not paste full logs.

Human-redacted example:

```text
Error: request failed
status: 401
Authorization: Bearer ***
WECHAT_APP_SECRET: ***
openid: ***
```

Required summary:

| Service/project | Error type | Redacted context | Impact |
|---|---|---|---|

## B5. docker-compose.yml and ecosystem.config.js

Sensitive files:

```bash
cat docker-compose.yml
cat ecosystem.config.js
```

Reason:

These files may contain:

- Environment variables
- Ports
- Commands
- Volumes
- Database URLs
- Secrets

Human-redacted example:

```yaml
services:
  app:
    image: xxx
    ports:
      - "3000:3000"
    env_file:
      - .env
    environment:
      NODE_ENV: production
      API_KEY: ***
```

Required summary:

| File | Project | Ports | Volumes | Env source | Secrets redacted? |
|---|---|---|---|---|---|

---

# Required output format

```markdown
# Phase 1: Server Discovery Report

## 1. Discovery mode

Explain that Phase 1 used:

- Class A: AI-executable low-risk read-only commands
- Class B: human-executed sensitive discovery with redaction

## 2. System information

## 3. Resource usage

## 4. Port usage

| Port | Protocol | Service/process | PID if visible | Notes |
|---|---|---|---|---|

## 5. Process overview

## 6. Common deployment tools

| Tool | Installed? | Status | Notes |
|---|---|---|---|

## 7. Common project directory findings

| Directory | Possible project | Notes |
|---|---|---|

## 8. Human-sensitive discovery checklist

| Sensitive area | Human input provided? | Redacted? | Notes |
|---|---|---|---|
| Nginx full config |  |  |  |
| Environment variables |  |  |  |
| Docker inspect |  |  |  |
| Logs |  |  |  |
| docker-compose / ecosystem config |  |  |  |

## 9. Initial observations

Summarize:

- Existing projects likely running
- Occupied ports
- Deployment tools detected
- Resource capacity
- Potential conflict areas

## 10. Open questions for the user

List missing information that may be needed before Phase 2.

Phase 1 completed. Waiting for user confirmation before moving to the next phase.
```

# Stop condition

After completing this report, stop.

Do not proceed to architecture analysis until the user says:

```text
Continue to next phase
```
