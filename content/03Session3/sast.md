---
title: "Static Application Security Testing"
linkTitle: "Static Application Security Testing"
weight: 3
#archetype: "chapter"
---

## Session 3

### SAST

We will look at some popular tools for identifying and understanding common flaws in source code. Static Application Security Testing focuses on YOUR proprietary code, and testing your code without actually running the application. The benefit of SAST is that you don't need to provision infrastructure or concern yourself with docker containers just to produce a running application for security analysis. SAST tools are designed to scan the code for common flaws that attackers are experts at finding and exploiting - 

```
Cross-Site Scripting (XSS) 
Cross-Site Request Forgery (CSRF)
Server-Side Request Forgery (SSRF)
Command Injection
Broken Authentication
Remote Code Execution
Buffer Overflow
```