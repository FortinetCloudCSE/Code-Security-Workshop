---
title: "Terraform Fundamentals"
linkTitle: "Terraform Do's"
weight: 3
#archetype: "chapter"
---

### Top 5 Terraform Do’s


#### 1. Use Remote Backends for State Management

* Why: Keeps state consistent and shareable across teams.

* Best Options: AWS S3 + DynamoDB, Terraform Cloud, Azure Blob, etc.

#### 2. Leverage Modules for Reusability

* Why: Promotes DRY principles and simplifies infra as it grows.

* How: Use separate modules for things like VPCs, IAM, compute resources, etc.

#### 3. Use Version Pinning for Providers and Modules

* Why: Prevents unexpected behavior due to upstream changes.

* How: Lock with required_providers and version constraints like ~> 4.0.

#### 4. Use terraform fmt, validate, and plan Regularly

* Why: Ensures clean, syntactically correct, and predictable code.

* Tools: Integrate in CI/CD for automated checks.

#### 5. Protect Critical Resources

* Why: Avoid accidental deletions.

* How: Use lifecycle { prevent_destroy = true } for sensitive infra like RDS, VPCs, etc.