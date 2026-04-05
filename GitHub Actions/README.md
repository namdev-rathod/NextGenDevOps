# GitHub Actions for Enterprise DevOps

A practical, industry-focused curriculum and reference implementation for designing, operating, and scaling GitHub Actions in enterprise environments. This repository prioritizes reusable workflows, secure AWS integrations, infrastructure-as-code, and production-grade release patterns.

## Project Overview

This repo provides real CI/CD patterns and runnable workflows for platform and application teams. It is aimed at experienced DevOps engineers who need pragmatic, secure, and scalable solutions for enterprise pipelines.

Key outcomes:
- Reusable, versioned workflow primitives
- Secure AWS integrations using OIDC and least-privilege IAM
- Production deployment patterns (canary, blue/green, progressive delivery)
- Observability, policy enforcement, and supply-chain hygiene

## Learning Objectives
After working through the projects and examples you'll be able to:
- Design modular workflows and composite actions for cross-team reuse
- Authenticate to AWS securely via OIDC and implement cross-account deployments
- Build hardened CI pipelines: build, test, scan, sign, and publish artifacts
- Implement progressive delivery strategies with automated rollback
- Enforce policy-as-code, generate audit evidence, and harden supply chains
- Operate self-hosted runners safely and cost-effectively

## Detailed Syllabus
This syllabus is compact but focused on enterprise needs. Each topic maps to examples and hands-on projects in the repository.

1) GitHub Governance & Foundations
   - Organizations, teams, repository permissions, branch protection, CODEOWNERS, environment protection rules

2) Actions & Runner Topology
   - Hosted vs self-hosted, autoscaling runners, isolation strategies, runner hardening, network constraints

3) Workflow Design & Composition
   - Jobs, steps, matrices, artifacts, caches, inputs/outputs, concurrency controls, failure policies

4) Secrets, Credentials & OIDC
   - Secrets sprawl, rotating secrets, OIDC trust relationships, short-lived credentials, cross-account role assumptions

5) AWS Integration Patterns
   - ECR/EKS/ECS deployments, STS assume-role patterns, least-privilege IAM policies, cross-account CI workflows

6) Reusability & Versioning
   - Reusable workflows (workflow_call), composite actions, semantic version pinning, changelogs, internal action registries

7) Multi-workflow Pipelines
   - Workflow chains, artifact handoffs, eventing (repository_dispatch), promoting artifacts between stages

8) Security & Supply Chain
   - SCA (dependency scanning), SBOMs, image scanning, signing (Cosign/Sigstore), attestations, policy gates

9) Observability & Telemetry
   - Emitting structured logs/events, workflow metrics, integrating with CloudWatch/Datadog/Prometheus, alerting on deploys

10) Release & Deployment Patterns
   - Canary, blue/green, progressive rollout, feature-flag integrations, automated rollback strategies, manual approval gates

11) Performance, Cost & Scale
   - Caching strategies, job parallelism limits, runner scheduling and cost optimization, deduplication strategies

12) Troubleshooting & Postmortems
   - Debugging workflows, reproducing runs locally, traceability, audit logs, postmortem templates

13) Interview & Architecture Prep
   - Real scenarios: tradeoffs, SLAs, sizing, governance, disaster recovery for CI/CD platforms

## Advanced Topics
Enterprise extensions and hardened patterns:

- OIDC + cross-account delegation with short-lived credentials and minimal trust surfaces
- Policy-as-code enforcement early in CI (OPA/Gatekeeper/Conftest)
- GitOps workflows for multi-cluster deployments (ArgoCD/Flux)
- Ephemeral, isolated self-hosted runners with autoscaling and secure bootstrapping
- External secret stores (AWS Secrets Manager, HashiCorp Vault, External Secrets Operator)
- Artifact signing, provenance, and attestation with Sigstore/Cosign and Rekor
- Compliance and evidence automation for audits
- Platform engineering patterns: central workflow libraries, onboarding playbooks, internal registries

## Hands-on Projects
Each project includes a README, test harness, and deployment scripts. Projects are practical and oriented to enterprise scenarios.

1) Polyglot Microservice CI
   - Build/test matrix, container image build, SBOM, SCA, push to ECR. Includes Makefile and test harness.

2) Reusable Workflow Library
   - Publishable, versioned reusable workflows and composite actions. Includes CHANGELOG and migration notes.

3) OIDC Cross-Account Deploy
   - Demonstrates OIDC trust, IAM role configuration, and ECS/EKS deployment workflow without long-lived credentials.

4) Progressive Delivery with Feature Flags
   - Canary promotion, rollout gates integrated with a feature-flag service, automated promotion/rollback.

5) Secure Artifact Pipeline
   - Build → Test → SBOM → Sign (Cosign) → Store provenance and enforce verification in deploy jobs.

## Capstone Project — End-to-End CI/CD System
Build a production-grade CI/CD system that demonstrates the following:

- Multi-repo and monorepo patterns with centralized reusable workflows
- OIDC-based cross-account deployments (ECR, ECS/Fargate, or EKS)
- IaC (Terraform) with remote state, drift detection, and CI-driven infra changes
- Artifact scanning, SBOM generation, signing and attestations
- Progressive delivery (canary + automated rollback) driven by observable signals and feature flags
- Observability and structured eventing into monitoring/alerting platforms
- Automated evidence collection for compliance and audits

Success criteria:
- Full automated pipeline: PR → build → integration tests → policy checks → canary → promote
- Deterministic rollback within the workflow on defined failure signals
- Minimal manual approvals limited to high-risk production stages

## Repository Structure
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
