---
title: "Basics of Source Code Management"
linkTitle: "SCM Fundamentals"
weight: 2
---

### Overview

During this discussion, we'll talk about basic source code management practices. Some you may be familiar with, some may be newer concepts. The goal is to re-inforce and re-introduce those concepts. Many of the topics we will discuss in this workshop are standards defined by the Open Source Security foundation (https://best.openssf.org/)

#### **CI/CD**
##### Don't allow workflows to approve pull requests

While automation is critical to handling repetitive tasks and tasks that don't require human input or approval - it also frees up developers to focus on more critical areas, rather than building infrastructure or updating configuration files manually - automation workflows should be used only in specific build scenarios. 


##### Restrict workflows to specific repos

This is a security recommendation. Automation workflows are particularly dangerous in that if scoped too broadly, they could be run arbitrarily against any repository in the organization. Workflows should always be built with a specific purpose in mind, and then applied to only the workflows that require that action. 

If every user can run arbitrary workflows, this could enable malicious activity such as accessing organization secrets, crypto-mining, etc. This misconfiguration could lead to the following attack:

Prerequisite: the attacker is part of your GitHub organization
Attacker creates new repository in the organization
Attacker creates a workflow file that reads all organization secrets and exfiltrate them
Attacker triggers the workflow
Attacker receives all organization secrets and uses them maliciously

Solution:
Change “All repositories” to “Selected repositories” and select repositories that should be able to run actions

##### Set Workflow Token Permissions to Read Only (tj-actions)




##### Promote builds effectively

CI is designed with frequent, small iterations in mind and automating the testing. 

<img src="img/CI-CD-1.png" alt="CI/CD Diagram" style="width:50%;">

It's a cornerstone of Continuous Delivery, where the goal is to streamline the software release process. 

<img src="img/CI-CD-2.png" alt="CI/CD Diagram" style="width:50%;">

As more organizations move to the cloud, they adopt more complex workflows given the efficiency and robustness that cloud providers offer. Microservices, containerization, and automation & orchestration add more complexity than traditional CI/CD tools. Each microservice may be managed differently or independently of others, may have their own software life cycle and dependency chains, which can lead to difficulty managing. 

This creates branches in development, splits teams off into separate projects, and de-prioritizes collaboration as each of those teams are only focused on their own project. As a result, consistency across environments - such as dev, QA, staging - becomes more challenging. 

<img src="img/CI-CD-3.png" alt="CI/CD Diagram" style="width:75%;">

For those reasons, CI/CD has given rise to a newer concept referred to as Continuous Promotion (CP). The goal of continous promotion is to centralize the decision-making process for elevating builds into different environments. 

<img src="img/CI-CP.png" alt="CI/CD Diagram" style="width:75%;">

Tools like Kargo and Devtron are popular CI/CP tools for helping dev teams coordinate the release of new code in each stage or environment.  

#### **Access Control**

##### Enable two-factor authentication

Two-factor authentication is the bare minimum in terms of security standards these days. Organization SSO with biometric verification - such as Okta fastpass - is highly preferred. 

##### Enable fewer than 3 organization admins

This is all about least privilege. The more admins you have, the more cooks there are in the kitchen. Generally, at least 1 org admin should be available for granting access to collaborators, creating new repositories, setting up integrations, and updating repo permissions as needed. The more admins you have walking around with this level of permission, the greater the potential blast radius of a compromise becomes. 

##### Ensure org admins are active

If a user has org admin privileges and doesn't login, that means they don't need org admin because they're not being asked to perform administrative functions, or someone else is handling that responsibility. 

#### **Repository Configuration**
* Don't allow committer aprovals
* Require at least 2 reviewers
* Don't merge pull requests unless all checks pass
* Never rewrite Git history

#### **Operations Management**
* Configure Security Alerts and Vulnerability Scanning at the Organization or Repository Level 
* Use single-sign-on
* Webhooks Should Be Configured To Use SSL
* Limit public repositories