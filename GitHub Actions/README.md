# 🚀 GitHub Actions – Enterprise DevOps Learning Repository

## 📌 Overview
This repository is a structured, hands-on learning path to master **GitHub Actions** from an **industry (enterprise DevOps) perspective**.

The goal is to move beyond basics and build the ability to:
- Design scalable CI/CD pipelines
- Implement secure deployments using OIDC
- Manage multi-environment workflows
- Troubleshoot real-world pipeline failures

---

## 🎯 Learning Objectives

By completing this repository, you will be able to:

- Build production-grade CI/CD pipelines using GitHub Actions
- Replace or integrate with tools like Jenkins / GitLab CI
- Implement secure authentication with AWS (OIDC)
- Optimize pipeline performance and cost
- Design reusable workflows across multiple repositories

---

## 📚 Syllabus

### 1️⃣ Introduction to GitHub
- Repository structure, branches, and permissions
- Branch protection rules & required checks
- GitHub CLI (`gh`) basics

---

### 2️⃣ Overview of GitHub Actions
- CI/CD concepts in GitHub ecosystem
- Event-driven workflows
- GitHub-hosted vs self-hosted runners

---

### 3️⃣ Components of GitHub Actions
- Workflows
- Jobs & Steps
- Actions (Marketplace & custom)
- Runners
- Contexts & Expressions

---

### 4️⃣ Understanding Workflows
- Workflow syntax deep dive
- Matrix builds (parallel execution)
- Conditional execution (`if`)
- Reusable workflows (`workflow_call`)
- Composite actions

---

### 5️⃣ Secret Management 🔐
- Repository vs Organization vs Environment secrets
- Secure authentication using OIDC (AWS)
- `GITHUB_TOKEN` permissions
- Secret masking & security best practices

---

### 6️⃣ Pipeline Management with Multiple Workflows
- Workflow chaining (`workflow_run`)
- CI vs CD separation
- Multi-environment deployments (Dev → Staging → Prod)
- Manual approvals using environments

---

### 7️⃣ Troubleshooting 🧯
- Debugging workflows (`ACTIONS_STEP_DEBUG`)
- Common issues:
  - Permission errors
  - Missing secrets
  - Runner failures
- Logs analysis & rerun strategies

---

### 8️⃣ Interview Preparation 🎯
- GitHub Actions vs Jenkins vs GitLab CI
- Pipeline design questions
- Security (OIDC, secrets handling)
- Real-world troubleshooting scenarios

---

## ➕ Additional Advanced Topics

- Performance optimization (caching, parallel jobs)
- Self-hosted runners (EC2 / Kubernetes)
- Organization-wide reusable workflows
- GitOps integration (optional)

---

## 🛠️ Hands-On Projects

### ✅ Project 1: Basic CI Pipeline
- Trigger on pull request
- Run lint + tests
- Upload artifacts

---

### ✅ Project 2: Multi-Language Pipeline
- Matrix build (Node + Python)
- Dependency caching
- Test reports

---

### ✅ Project 3: AWS Deployment with OIDC
- Configure IAM role for GitHub
- Deploy to S3 / ECS / Lambda
- Remove static credentials

---

### ✅ Project 4: Enterprise CI/CD Pipeline
- Build Docker image
- Push to ECR
- Deploy to ECS
- Manual approval for production

---

### 🏁 Capstone Project: Production-Ready CI/CD Platform

- CI: Lint + Test + Build
- CD:
  - Auto deploy to Dev
  - Approval-based deploy to Staging
  - Gated deploy to Production
- AWS OIDC authentication
- Docker + ECR + ECS
- Notifications (Slack/Teams)

---

## 📂 Repository Structure
Recommended layout; each top-level folder includes a README and runnable examples.

```text
.
├─ .github/
│  ├─ workflows/                # Production-quality workflow examples (.yml)
│  ├─ workflows/reusable/       # Reusable workflow templates (workflow_call)
│  ├─ actions/                  # Composite actions and action metadata
│  └─ CODEOWNERS
├─ projects/
│  ├─ microservice-ci/          # Project: CI pipeline for a microservice
│  ├─ oidc-cross-account/       # Project: OIDC + cross-account deploy
│  └─ secure-artifact-pipeline/ # Project: SBOM, signing, verification
├─ infra/
│  ├─ terraform/                # IaC used by examples (remote state config)
│  └─ cloudformation/           # Optional CloudFormation examples
├─ docs/
│  ├─ patterns.md               # Architectural patterns and templates
│  └─ security-guides.md
├─ examples/                    # Minimal sample apps used by workflows
├─ scripts/                     # Helper scripts for local testing and runner emulation
└─ README.md
```

## Security Best Practices 🔒

- Prefer OIDC federated authentication; avoid embedding long-lived secrets
- Apply least-privilege IAM roles and minimal trust policies for CI jobs
- Centralize secrets in organization-level secret vaults; use environment protection rules for production
- Pin action versions (semver) and require PR review for action updates
- Sign artifacts and verify signatures during deploys (Cosign/Sigstore)
- Enable secret scanning, dependency scanning, and attestation generation in CI
- Use ephemeral self-hosted runners with strict host hardening and network controls

## CI/CD Best Practices ⚙️

- Keep jobs concise and idempotent; prefer many small jobs over one monolith
- Use artifact handoffs to avoid duplicate heavy builds across workflows
- Cache deterministically and invalidate caches explicitly when dependencies change
- Limit matrix expansion and cap concurrency to control cost
- Implement retries, timeouts, and backoff for fragile external calls
- Emit structured deployment metadata and integrate with monitoring/alerting systems
- Enforce policy gates (SCA, tests, approvals) before production release

## Learning Approach — What to do vs avoid 🧭

Do:
- Break workflows into reusable, testable primitives
- Model enterprise constraints: multi-account AWS, separate infra repo, staged approvals
- Automate guardrails: linting, policy checks, and CI tests for workflows/actions
- Version workflows and maintain clear changelogs

Avoid:
- Storing secrets or credentials in plaintext anywhere in the repo
- Using unpinned action references (avoid `@master` or `@main`)
- Overly large workflows that slow iteration and are hard to debug
- Relying on a single runner topology for all workloads without scaling strategy

## Prerequisites
Expected baseline for contributors and learners:
- Comfortable with Git, GitHub organizations, and CODEOWNERS
- Strong AWS knowledge: IAM, STS, ECR, ECS/EKS, and OIDC concepts
- Docker build and container runtime experience
- Familiarity with at least one IaC tool (Terraform recommended)
- Basic scripting skills (Bash, PowerShell, or Python)

## Contribution Guidelines

- Use feature branches and descriptive PR titles: `feature/<scope>-<short-desc>`
- All changes must pass CI, be reviewed by CODEOWNERS, and have at least one approver
- Pin action versions; include migration notes when upgrading major versions
- Add tests for new workflow behavior and unit tests for composite actions where practical
- Follow semantic versioning for published actions and workflows
- Report security issues privately through the repository's SECURITY process

## Quick Usage

- Inspect `/.github/workflows` for runnable examples
- Follow `projects/` for guided, hands-on exercises
- Read `projects/oidc-cross-account/README.md` for OIDC setup and example trust policies
- Use `scripts/` to emulate or debug runner behavior locally

## Final Goal — Where this gets you 🚀

This repository equips experienced DevOps engineers to design and operate GitHub Actions pipelines that satisfy enterprise requirements for security, scale, and reliability. You'll be able to implement cross-account AWS deployments, build reusable workflow libraries, harden supply chains, and integrate CI/CD into enterprise governance and compliance processes.

---

Treat workflows and actions as production software — they are critical infrastructure.
