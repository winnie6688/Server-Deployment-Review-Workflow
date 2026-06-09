# Rollback Plan Template

Use this template to summarize Phase 6 findings.

## 1. Rollback strategy summary

## 2. Pre-deployment backup checklist

| Item | Backup needed? | Method | Notes |
|---|---|---|---|
| Nginx config |  |  |  |
| Environment file |  |  |  |
| Database |  |  |  |
| PM2 process list |  |  |  |
| Docker compose file |  |  |  |
| Project files |  |  |  |

## 3. Rollback triggers

- New service cannot start
- Configuration validation fails
- Existing service becomes unreachable
- New domain returns error
- CPU, memory, or disk usage becomes abnormal
- Database migration fails

## 4. Rollback steps

### Step 1: Stop or isolate the new project process

### Step 2: Restore reverse proxy configuration

### Step 3: Restore environment variable state

### Step 4: Revert database changes if any

### Step 5: Verify existing services

### Step 6: Confirm server health

## 5. Verification checklist after rollback

| Check | Expected result | Pass/Fail |
|---|---|---|

## 6. Estimated rollback complexity

Choose one:

- Low
- Medium
- High

Reason:

## 7. User decisions required
