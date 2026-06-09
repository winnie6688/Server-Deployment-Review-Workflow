# Deployment Plan Template

Use this template to summarize Phase 5 findings.

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

```text
PM2 process name: my-new-project
```

Reason:

## 5. Recommended environment variable strategy

```text
/var/www/my-new-project/.env
```

Rules:

- Keep project-specific configuration in the project environment file.
- Do not reuse unrelated project secrets.
- Redact sensitive values when documenting.

## 6. Recommended Nginx strategy

```text
/etc/nginx/sites-available/my-new-project.conf
```

or:

```text
/etc/nginx/conf.d/my-new-project.conf
```

Reason:

## 7. Recommended domain strategy

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

```text
/var/log/my-new-project
```

Reason:

## 10. Deployment change preview

| Item | Proposed value | Reason | Conflict risk |
|---|---|---|---|

## 11. User decisions required

| Decision | Recommended choice | Reason |
|---|---|---|
