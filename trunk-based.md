# Trunk-Based Development (TBD) with DevSecOps CI/CD Pipeline

## Overview

This repository demonstrates a Trunk-Based Development (TBD) workflow integrated with a DevSecOps CI/CD pipeline. Developers work on short-lived feature branches and frequently merge changes into the main (trunk) branch. Automated quality checks, security scans, testing, and deployments ensure that the trunk remains production-ready at all times.

<p align="center">
  <img src="images/trunk-based.svg" alt="Trunk Based Development Workflow" width="1000">
</p>

---

## What is Trunk-Based Development?

Trunk-Based Development is a source control branching model where developers collaborate on a single branch called the **trunk** (usually `main`).

Instead of maintaining long-running branches, developers create short-lived feature branches, perform their work, and merge back into the trunk frequently.

### Core Principles

- Single main branch (trunk)
- Short-lived feature branches
- Frequent commits and merges
- Continuous Integration
- Continuous Delivery
- Automated testing and security validation
- Main branch is always deployable

---

## Workflow

### 1. Create a Short-Lived Feature Branch

Developers create a feature branch from the trunk.

```text
main / trunk
      |
      └── feature branch
```

Branches are small, focused, and exist only for a short period.

---

### 2. Development Activities

Developers perform:

- Feature Development
- Bug Fixes
- Unit Testing
- Code Review Preparation
- Local Validation

Changes are committed frequently to minimize integration issues.

---

### 3. Pull Request Process

After development is completed:

1. Create Pull Request
2. Review Code
3. Run Automated Checks
4. Approve Changes
5. Merge into Main/Trunk

```text
Feature Branch
      |
      ▼
Pull Request
      |
      ▼
Main / Trunk
```

---

### 4. CI/CD Pipeline

Every commit and Pull Request automatically triggers the pipeline.

#### Checkout Code

Retrieves the latest source code.

#### Build

Compiles the application.

#### Unit Tests

Executes automated unit tests.

#### SonarQube Analysis

Validates code quality by detecting:

- Bugs
- Vulnerabilities
- Code Smells
- Technical Debt

#### SAST

Performs Static Application Security Testing.

#### DAST

Performs Dynamic Application Security Testing.

#### Dependency Scan

Identifies vulnerable third-party libraries.

#### Security Scan

Validates security policies and configurations.

#### Docker Image Build

Creates deployment-ready container images.

#### Image Scan

Scans Docker images for CVEs and vulnerabilities.

#### Deploy to Development/Staging

Deploys validated builds for testing.

#### Automated Testing

Executes:

- Functional Tests
- Integration Tests
- Regression Tests
- API Tests

---

### 5. Merge to Trunk

If all quality gates pass:

- Pull Request is approved
- Code is merged into trunk
- Trunk remains production-ready

```text
All Checks Passed
        |
        ▼
Merge to Main / Trunk
```

---

### 6. Release Process

Since the trunk is always deployable, releases can happen frequently.

Example:

```text
v1.0.0
v1.0.1
v1.0.2
v1.0.3
v1.0.4
v1.0.5
```

Release steps:

1. Tag stable commit
2. Deploy to Production
3. Monitor Application Health
4. Rollback if required

---

## Pipeline Flow

```text
Feature Branch
       │
       ▼
Development
       │
       ▼
Pull Request
       │
       ▼
CI/CD Pipeline
(Build → Unit Tests → Sonar → SAST → DAST → Dependency Scan → Image Scan)
       │
       ▼
Merge to Main / Trunk
       │
       ▼
Deploy to Dev / Staging
       │
       ▼
Automated Validation
       │
       ▼
Production Release
```

---

## Benefits

- Faster release cycles
- Reduced merge conflicts
- Continuous integration of code changes
- Faster developer feedback
- Better code quality
- Automated security validation
- Improved deployment reliability
- Higher deployment frequency
- Simpler branch management
- Production-ready trunk at all times

---

## Best Practices

- Keep feature branches short-lived.
- Commit small and frequent changes.
- Use Pull Requests for all merges.
- Automate testing and security checks.
- Protect the main branch with approval policies.
- Enable Continuous Integration for every commit.
- Use feature flags for incomplete functionality.
- Ensure trunk is always deployable.

---

## Technologies Commonly Used

- Git
- GitHub Actions
- Jenkins
- GitLab CI/CD
- ArgoCD
- Docker
- Kubernetes
- Terraform
- SonarQube
- Trivy
- Veracode
- Prometheus
- Grafana
- ELK Stack