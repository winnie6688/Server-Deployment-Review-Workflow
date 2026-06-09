# Terminology

This document explains common terms used in the workflow.

## Server

A machine that runs applications and services. In this workflow, the server already has existing projects, so new deployment must be planned carefully.

## Port

A port is like a numbered door on the server. Different applications usually listen on different ports.

Common examples:

- `80`: HTTP
- `443`: HTTPS
- `3000`: Common development or Node.js app port
- `5432`: PostgreSQL
- `3306`: MySQL
- `6379`: Redis

A new project should not use a port that is already occupied.

## Reverse proxy

A reverse proxy receives external requests and forwards them to internal application services.

Nginx is commonly used as a reverse proxy.

## Nginx

Nginx is a web server and reverse proxy. It often handles:

- Domain routing
- HTTPS certificates
- Static files
- Forwarding traffic to application ports

## PM2

PM2 is a process manager often used for Node.js applications.

It can:

- Start applications
- Keep applications running
- Restart applications after crashes
- Save process lists

## Docker

Docker packages applications into containers.

A Docker deployment may involve:

- Images
- Containers
- Port mappings
- Networks
- Volumes

## systemd

systemd is a Linux service manager. Many system services are managed by systemd, including Nginx, databases, and custom application services.

## Environment variables

Environment variables store configuration such as:

- API keys
- Database URLs
- Secret tokens
- Runtime mode
- Service ports

Project-specific environment variables should usually be stored in a project-level `.env` file rather than a global system file.

## Database schema

A schema is a logical namespace inside a database.

Using a separate schema can reduce conflicts when multiple projects share the same database.

## Table prefix

A table prefix is a naming convention that separates tables from different projects.

Example:

```text
project_a_users
project_b_users
```

This is weaker than a separate database or schema, but may be useful for small projects.

## Rollback

Rollback means returning the system to a previous stable state after a failed deployment or unsafe change.

A deployment plan should always have a rollback plan.

## Change impact analysis

Change impact analysis answers:

```text
What existing resources may be affected by this new project?
```

It helps avoid accidental damage to existing services.

## Deployment gate

A deployment gate is a final checkpoint before actual changes begin.

In this workflow, deployment must not start until the user explicitly confirms:

```text
Start deployment
```
