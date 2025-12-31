# GitHub Actions – Complete Guide

This repository provides a **complete, beginner‑friendly yet detailed guide to GitHub Actions**, covering both **basic and advanced concepts** used in real‑world DevOps and CI/CD pipelines.

---

## Table of Contents

1. What is GitHub Actions?
2. Why GitHub Actions is Important (DevOps View)
3. How GitHub Actions Works
4. Core Components of GitHub Actions

   * Workflow
   * Events (Triggers)
   * Jobs
   * Runners
   * Steps
   * Actions
5. Basic CI Pipeline Example
6. Environment Variables
7. Secrets Management
8. CI vs CD using GitHub Actions
9. GitHub Actions with Docker
10. Advanced GitHub Actions Concepts
11. GitHub Actions vs Jenkins
12. Real‑World Use Cases
13. Interview‑Ready Summary

---

## 1. What is GitHub Actions?

**GitHub Actions** is a CI/CD (Continuous Integration and Continuous Deployment) tool provided by GitHub. It allows you to automate tasks such as:

* Building code
* Running tests
* Performing static code analysis
* Building Docker images
* Deploying applications

Automation is triggered when events like code push, pull request, or manual execution occur.

---

## 2. Why GitHub Actions is Important (DevOps View)

GitHub Actions helps teams to:

* Automate repetitive tasks
* Detect issues early in development
* Maintain code quality
* Speed up delivery
* Follow DevOps best practices

---

## 3. How GitHub Actions Works (High‑Level Flow)

1. Developer pushes code to GitHub
2. A workflow is triggered
3. Jobs are executed on runners
4. Steps perform tasks like build, test, deploy
5. Results are displayed in GitHub UI

---

## 4. Core Components of GitHub Actions

### 4.1 Workflow

A **workflow** is an automated process defined using a YAML file.

Location:

```
.github/workflows/
```

Example:

```yaml
name: CI Pipeline
```

---

### 4.2 Events (Triggers)

Events define **when** the workflow should run.

Common events:

* push
* pull_request
* schedule
* workflow_dispatch

Example:

```yaml
on:
  push:
    branches:
      - main
```

---

### 4.3 Jobs

A **job** is a collection of steps executed on the same runner.

Example:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
```

Jobs run in parallel by default.

---

### 4.4 Runners

Runners are machines where jobs run.

Types:

* GitHub‑hosted runners
* Self‑hosted runners

Common runners:

* ubuntu-latest
* windows-latest
* macos-latest

---

### 4.5 Steps

Steps are individual tasks inside a job.

Example:

```yaml
steps:
  - name: Checkout code
    uses: actions/checkout@v4

  - name: Run tests
    run: npm test
```

---

### 4.6 Actions

Actions are reusable automation units.

Types:

* Official GitHub actions
* Community actions
* Custom actions

Example:

```yaml
uses: actions/checkout@v4
```

---

## 5. Basic CI Pipeline Example

```yaml
name: Node.js CI

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: 18

      - run: npm install
      - run: npm test
```

---

## 6. Environment Variables

Environment variables allow reuse of values.

Example:

```yaml
env:
  APP_ENV: production
```

Usage:

```yaml
run: echo $APP_ENV
```

---

## 7. Secrets Management

Secrets store sensitive data securely.

* Stored in GitHub repository settings
* Never hard‑code secrets

Example:

```yaml
env:
  DB_PASSWORD: ${{ secrets.DB_PASSWORD }}
```

---

## 8. CI vs CD using GitHub Actions

### Continuous Integration (CI)

* Build application
* Run unit tests
* Perform static code analysis

### Continuous Deployment (CD)

* Build Docker images
* Push images to registry
* Deploy to servers or Kubernetes

---

## 9. GitHub Actions with Docker

```yaml
- name: Build Docker image
  run: docker build -t myapp:latest .

- name: Push Docker image
  run: docker push myapp:latest
```

---

## 10. Advanced GitHub Actions Concepts

### 10.1 Job Dependencies (`needs`)

```yaml
needs: build
```

---

### 10.2 Conditional Execution (`if`)

```yaml
if: github.ref == 'refs/heads/main'
```

---

### 10.3 Matrix Strategy

```yaml
strategy:
  matrix:
    node-version: [16, 18, 20]
```

---

### 10.4 Caching

```yaml
- uses: actions/cache@v4
  with:
    path: ~/.npm
    key: npm-cache
```

---

### 10.5 Artifacts

```yaml
- uses: actions/upload-artifact@v4
  with:
    name: build-files
    path: dist/
```

---

### 10.6 Manual Trigger (`workflow_dispatch`)

```yaml
on:
  workflow_dispatch:
```

---

### 10.7 Scheduled Workflows (Cron)

```yaml
on:
  schedule:
    - cron: "0 2 * * *"
```

---

### 10.8 Permissions & Security

```yaml
permissions:
  contents: read
```

---

### 10.9 Reusable Workflows

```yaml
uses: org/repo/.github/workflows/ci.yml@main
```

---

### 10.10 Composite Actions

Used to combine multiple steps into one reusable action.

---

### 10.11 Self‑Hosted Runners

Used for custom tools, compliance, or cost optimization.

---

### 10.12 Concurrency Control

```yaml
concurrency:
  group: prod-deploy
  cancel-in-progress: true
```

---

### 10.13 Workflow Status Badges

```md
![CI](https://github.com/user/repo/actions/workflows/ci.yml/badge.svg)
```

---

### 10.14 Logging & Debugging

```yaml
ACTIONS_STEP_DEBUG: true
```

---

### 10.15 GitHub Contexts

Examples:

* github.actor
* github.repository
* github.ref

Used to make workflows dynamic.

---

## 11. GitHub Actions vs Jenkins

| Feature     | GitHub Actions | Jenkins      |
| ----------- | -------------- | ------------ |
| Setup       | Easy           | Complex      |
| Maintenance | GitHub managed | Self‑managed |
| UI          | GitHub UI      | Separate UI  |
| Plugins     | Limited        | Very large   |

---

## 12. Real‑World Use Cases

* Automated testing
* Security scans
* Code linting
* Docker image builds
* Cloud & Kubernetes deployments
* Infrastructure automation

---

## 13. Interview‑Ready Summary

GitHub Actions supports:

* CI/CD automation
* Job dependencies and conditions
* Matrix builds
* Caching and artifacts
* Manual and scheduled workflows
* Secure secrets and permissions
* Reusable workflows
* Self‑hosted runners
* Concurrency control

**One‑Line Summary:**

> GitHub Actions is a GitHub‑native automation platform that enables CI/CD using YAML‑based workflows with enterprise‑level flexibility and security.

---

## Conclusion

This README provides a complete understanding of GitHub Actions from basics to advanced concepts, making it suitable for:

* Beginners learning CI/CD
* DevOps engineers
* Interview preparation
* Real‑world project implementation

---

Happy Learning 🚀
