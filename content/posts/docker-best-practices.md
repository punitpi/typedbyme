---
title: "Docker Best Practices for Production"
date: 2025-10-12T10:00:00Z
draft: false
author: "Puneeth Prakash"
description: "Essential Docker best practices for building secure, efficient, and production-ready containers."

tags: ["Docker", "DevOps", "Containers", "Best Practices"]
categories: ["Documentation & Guides"]

# hero: images/posts/docker/hero.jpg

toc:
  enable: true

menu:
  sidebar:
    name: "Docker Best Practices"
    identifier: "docker-best-practices"
    weight: 503
---

## Introduction

Docker has revolutionized how we build and deploy applications. However, creating production-ready containers requires following best practices for security, performance, and maintainability.

## 1. Use Official Base Images

Always start with official images from Docker Hub:

```dockerfile
# Good
FROM node:18-alpine

# Bad
FROM random-user/node:latest
```

## 2. Minimize Layer Count

Combine RUN commands to reduce layers:

```dockerfile
# Good
RUN apt-get update && \
    apt-get install -y package1 package2 && \
    rm -rf /var/lib/apt/lists/*

# Bad
RUN apt-get update
RUN apt-get install -y package1
RUN apt-get install -y package2
```

## 3. Use Multi-Stage Builds

Reduce final image size significantly:

```dockerfile
# Build stage
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Runtime stage
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
CMD ["node", "dist/index.js"]
```

## 4. Don't Run as Root

Create a non-root user:

```dockerfile
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001

USER nodejs
```

## 5. Use .dockerignore

Exclude unnecessary files:

```
node_modules
npm-debug.log
.git
.env
*.md
```

## 6. Leverage Build Cache

Order Dockerfile commands from least to most frequently changing:

```dockerfile
# Dependencies change less frequently
COPY package*.json ./
RUN npm ci

# Source code changes frequently
COPY . .
```

## 7. Health Checks

Add health checks for container orchestration:

```dockerfile
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD node healthcheck.js || exit 1
```

## 8. Use Specific Tags

Never use `latest` in production:

```dockerfile
# Good
FROM node:18.17.0-alpine3.18

# Bad
FROM node:latest
```

## 9. Scan for Vulnerabilities

Regularly scan images:

```bash
docker scan myimage:tag
# or
trivy image myimage:tag
```

## 10. Keep Images Small

- Use alpine variants
- Remove build dependencies
- Clean package manager cache

## Conclusion

Following these practices will result in secure, efficient, and maintainable Docker containers suitable for production environments.

---

Questions? Reach out at contact@puneeth.io
