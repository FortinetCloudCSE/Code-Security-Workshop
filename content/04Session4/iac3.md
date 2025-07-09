---
title: "Terraform Fundamentals"
linkTitle: "Terraform Don'ts"
weight: 4
#archetype: "chapter"
---

### Top 5 Terraform Dont's


#### 1. Don’t Hardcode Values (Especially Secrets)

* Why: Makes code inflexible and insecure.

* Instead: Use terraform.tfvars, environment variables, or secret managers (AWS Secrets Manager, Vault).

#### 2. Don’t Manually Edit the Terraform State File

* Why: It's risky and can corrupt your infrastructure representation.

* Instead: Use terraform state commands for safe manipulation.

#### 3. Don’t Apply Terraform Changes Without a Plan Review

* Why: You may unintentionally destroy or modify critical infra.

* Best Practice: Always run terraform plan and use peer reviews or PRs before apply.

#### 4. Don’t Keep Everything in a Single Monolithic .tf File

* Why: Reduces readability and maintainability.

* Instead: Break into logical files or modules (main.tf, variables.tf, outputs.tf).

#### 5. Don’t Ignore State Locking for Concurrent Teams

* Why: Simultaneous applies can corrupt state or lead to race conditions.

* Solution: Use backends like S3 with DynamoDB locking or Terraform Cloud which handles this natively.