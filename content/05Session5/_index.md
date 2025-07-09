---
title: "Supply Chain Attacks"
linkTitle: "Session 5: Protecting Supply Chains"
weight: 1
#archetype: "chapter"
---

## Session 5

Here are three of the most recent and impactful supply chain attacks—spanning open-source components to global manufacturing—and practical measures organizations could’ve taken to prevent them:

#### 1. Trojanized Lottie-Player (Oct 2024)

What happened: Versions 2.0.5–2.0.7 of the popular Lottie-Player library were compromised, injecting a cryptominer that stole crypto from sites using the library—resulting in a confirmed loss of nearly 10 BTC (~$700k).

Prevention:

   * Strict vetting of third-party assets before updating.

   * Implement dependency integrity checks (e.g., checksums, signed releases).

   * Regular vulnerability scans targeting open-source libraries.

#### 2. tj-actions/changed-files GitHub Action (March 2025)

What happened: The widely used GitHub Action tj-actions/changed-files was hijacked to steal secrets—including AWS keys, GitHub tokens, npm credentials—via malicious code in public logs. It affected over 23,000 repositories. As one user warned:

    “A third‑party GitHub Action … suffering a supply chain compromise. … allows attackers to access sensitive information …”

Prevention:

   * Pin GitHub Actions to specific commit SHA rather than floating tags.

   * Rotate secrets immediately post-incident.

   * Audit logs regularly and enforce least privilege for CI permissions.

#### 3. Sarcoma Ransomware on Unimicron (January 2025)

What happened: Electronics supplier Unimicron suffered a ransomware-driven supply chain attack. On January 30, 2025, attackers used phishing and software exploits to steal 377 GB of sensitive data including SQL files.

Prevention:

   * Enhance employee training to recognize phishing.

   * Keep systems and dependencies fully patched.

   * Use network segmentation and multifactor authentication to limit lateral movement.

   * Maintain immutable, offline backups.

### 🧠 Cross-Cutting Lessons: How to Prevent Supply Chain Attacks

| ✅ Measure                             | 💡 Why It Matters |
|---------------------------------------|--------------------|
| **🛠️ Dependency Integrity Verification** | Ensures third-party code is authentic (e.g., checksums, GPG signatures, SBOMs). |
| **🔒 Principle of Least Privilege**     | Limits blast radius if a dependency or vendor tool is compromised. |
| **🔄 Secret Rotation & Token Custody** | Regularly rotating credentials reduces the lifespan of stolen secrets. |
| **📌 Pin CI/CD Tools to Fixed Versions** | Prevents auto-pulling malicious or altered code via floating tags. |
| **🧑‍💻 Phishing Resistance & Patch Management** | Stops the initial attack vector and closes known exploits quickly. |
| **🔍 Monitoring & EDR Implementation**  | Detects anomalous behavior and allows rapid response to compromise. |


These incidents highlight supply chain vulnerabilities at different layers: open‑source modules, CI/CD pipelines, and physical manufacturers. The consistent theme? Treat all external code and services as untrusted by default, enforce strict verifications, least privileges, and be ready to respond quickly with credential rotation and forensic monitoring.

