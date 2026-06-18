# Feature Branching Strategy with DevSecOps CI/CD Pipeline

## Overview

This workflow demonstrates a Feature Branching Strategy integrated with a DevSecOps CI/CD pipeline. Every code change passes through automated quality checks, security validations, testing stages, and approval workflows before reaching production.

---

## Workflow

### 1. Create Feature/Hotfix Branch

Development starts by creating a feature or hotfix branch from the main branch.

```text
main (v1.0.0)
   |
   └── feature/hotfix branch
```

Developers work independently without impacting the stable production code.

---

### 2. Development Pipeline (DEV)

Every commit triggers the DEV pipeline.

#### Build
Builds the application source code.

#### Compile
Compiles and validates the application.

#### Unit Tests
Executes automated unit tests.

#### Sonar Scan
Performs code quality analysis to identify bugs, vulnerabilities, and code smells.

#### SAST
Performs Static Application Security Testing on source code.

#### DAST
Performs Dynamic Application Security Testing on the running application.

#### Docker Image Build
Creates a container image after successful validation.

#### Image Scan
Scans the container image for vulnerabilities and CVEs.

#### DEV Deployment
Deploys the application to the Development environment.

#### Functional Testing
Validates application functionality through automated tests.

---

### 3. Pull Request Process

After successful DEV validation:

1. Create Pull Request
2. Perform Code Review
3. Collect Approvals
4. Merge into Main Branch

```text
Feature Branch
      |
      ▼
Pull Request
      |
      ▼
Main Branch
```

---

### 4. QA/UAT Pipeline

Once merged into the main branch, the QA/UAT pipeline starts.

#### Download Image
Uses the validated image generated in the DEV pipeline.

#### Set Environment Configuration
Applies QA/UAT-specific configurations and secrets.

#### Deploy to QA/UAT
Deploys the application to the QA/UAT environment.

#### Integration Testing
Validates service communication, APIs, databases, and external integrations.

#### Raise CR and JIRA
Creates Change Requests and updates release tracking tickets.

---

### 5. Production Deployment

After approvals are completed:

#### CR Approval Process
Release approvals are obtained from stakeholders.

#### Download Approved Image
Uses the same tested artifact from QA/UAT.

#### Set Production Configuration
Applies production-specific settings and secrets.

#### Deploy to Production
Deploys the approved release to the Production environment.

#### Done
Application is successfully released to end users.

---

## Release Flow

```text
Feature Branch
       │
       ▼
DEV Pipeline
(Build → Unit Tests → Sonar → SAST → DAST → Image Scan)
       │
       ▼
Pull Request & Review
       │
       ▼
Merge to Main
       │
       ▼
QA/UAT Pipeline
(Deploy → Integration Tests)
       │
       ▼
CR & Approval Process
       │
       ▼
Production Deployment
       │
       ▼
Live Application
```

---

## Benefits

- Isolated feature development
- Automated code quality validation
- Integrated security testing (SAST, DAST, Image Scanning)
- Consistent artifact promotion across environments
- Controlled production releases through approval workflows
- Improved traceability using Pull Requests, JIRA, and Change Requests
- Reduced deployment risk and increased release reliability