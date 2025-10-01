# 🛡️ Securing system and network infrastructures: the DevSecOps

## 📝 Purpose
This Technology Watch was carried out during my **5-month bootcamp: Technicien Supérieur Système et Réseau**. 
During this formation, I prepared a **Canva** presentation for my class (file available in [Ressources](/W38-DevSecOps/Ressources/LeMondeDuDevSecOps.pdf)).

Today, I wanted to :
- **enrich it** with more detailed explanations, diagrams, and definitions,
- **add it** to my GitHub repository *Exploration de la Tech IT**, in order to keep a written and evolving record of my learnings.

> ℹ️ **Note**: This document is a Technology Watch carried out as part of my training. It is not intended to be official documentation, but rather an accessible synthesis to introduce **DevSecOps**.

## 🇫🇷 French version  
The French version is available [here](/W38-DevSecOps/index.fr.md).

## ⚙️🛡️ DevOps vs DevSecOps
### ⚙️ DevOps
The missions of **DevOps** are mainly related to automation, reliability and infrastructure management.
- **Automation and deployment**
  - Setting up and optimizing CI/CD pipelines to accelerate development and deployment.
  - Continuous Integration (CI) and Continuous Delivery (CD)
- **Infrastructure management**
  - Deployment and administration of Cloud infrastructures (AWS, Azure, GCP...)
  - Monitoring scalability and service availability
- **Reliability and optimization**
  - Ensuring resilience and high availability of applications
  - Optimizing costs and performance through automation (IaC, monitoring)

### 🛡️ DevSecOps
**DevSecOps** is a **natural evolution of DevOps**, integrating security from the very beginning of the software lifecycle.
- **Securing deployments**
  - Automation vulnerability scan in CI/CD pipelines
  - Proactively detecting security flaws before putting into production
- **Monitoring and compliance**
  - Real-time monitoring to prevent threats
  - Compliance with standards such as ISO 27001, RGPD, NIST, PCI-DSS…
- **Collaboration between Dev, Ops and Sec**
  - *Shift Left* approach: security test are integrated from the development stage
  - Shared culture: security is no longer the sole responsibility of **Security team**, but of everyone

## 🛠️ Tools of DevSecOps
🔹 **_Key Definitions_**
- **SAST (Static Application Security Testing)**  
  - Static analysis of source code to detect flaws before execution
  - Examples: SonarQube, Snyk Code, Checkmarx
- **DAST (Dynamic Application Security Testing)**  
  - Testing applications at runtime to simulate attacks
  - Examples: OWASP ZAP, Burp Suite, AppScan
- **Container Security**  
  - Securing Docker images, containers, and Kubernetes clusters
  - Examples: Trivy, Falco, Aqua Security 
- **IaC Security (Infrastructure as Code)** 
  - Analysis of infrastructure scripts (Terraform, Ansible) to avoid vulnerable configurations
  - Examples: Checkov, Terraform Sentinel  
- **Monitoring & SIEM (Security Information and Event Management)**
  - Centralizing and analyzing logs to detect threats
  - Examples: ELK, Splunk, Wazuh

🔹 **_Chosen tools_**
- **SonarQube (SAST)**
  - Static code analysis to detect bugs, vulnerabilities, and *code smells*
  - Multi-language support (Java, Python, JavaScript, etc.)
  - Native integration with GitLab CI/CD, Jenkins, GitHub Actions
- **OWASP ZAP (DAST)**
  - Automated penetration testing tool for web applications
  - Simulate common attacks (SQLi, XSS, CSRF…)
  - Can be integrated into CI/CD pipelines to scan every build

## 🔄🚀 CI/CD Pipeline
### 📦 Stages of a CI/CD pipeline
1. **Build (Compilation & Packaging)**
  - Transforming source code into an executable artifact (binary, Docker image, jar, etc...)
  - Example: a developer pushes a code ➡️ Jenkins/GitHub Actions triggers a build
2. **Automated tests (Quality & Security)**
  - Unit tests ➡️ check that each function works correctly
  - Integration tests ➡️ ensure compatibility between modules
  - Security tests (DevSecOps) ➡️ SAST, DAST, dependency scans at this stage
  - Example: SonarQube analyzes the code, OWASP ZAP tests the application deployed in a temporary environment
3. **Deployment (Release & Delivery)**
  - Automated production release with rollback in case of failure
  - Example: GitLab CI automatically deploys a new version of the application

### ⚓ Delivery with Kubernetes & Helm
In modern environments, applications are often containerized with Docker and orchestrated by **Kubernetes (K8s)**.
- Kubernetes (K8s)
  - Container orchestrator that manages deployment, scalability and service resilience
  - Advantages: fault tolerance, automatic scaling, updates without downtime (rolling updates).
- Helm
  - Package manager for Kubernetes, used to deploy application via charts (YAML templates)
  - Advantages: simplification and standardization of complex deployments

👉 **Concrete example of a final pipeline step**
1. CI builds a Docker image and pushes it to a registry (DockerHub, GitLab, Container Registry).
2. CD triggers Helm, which automatically deploys the new version on a Kubernetes cluster.
3. Kubernetes ensures progressive rollout of the new version (rolling update) and rollback in case of failure.

### 🛡️ DevSecOps in CI/CD
👉 **Security is integrated in every stage**:
- Static analysis (Static Application Security Testing) from the build phase
- Dynamic tests (Dynamic Application Security Testing) before deployment
- Scanning Docker images before pushing to the registry
- Monitoring & alerts once in production (logs, SIEM, Kubernetes security)

### ⚙️ Pipeline DevSecOps Examples
```text
                ┌─────────────┐
                │   Code &    │
                │  Commit     │
                └──────┬──────┘
                       │
                       ▼
              ┌──────────────────┐
              │ Static analysis  │  ← (SAST : SonarQube, Snyk…)
              │   of code        │
              └──────┬───────────┘
                     │
                     ▼
            ┌──────────────────┐
            │  Build & Test    │
            │ (Unit tests)     │
            └──────┬───────────┘
                   │
                   ▼
          ┌─────────────────────┐
          │  Dynamic analysis   │  ← (DAST : OWASP ZAP, Burp…)
          │   App Security      │
          └────────┬────────────┘
                   │
                   ▼
        ┌───────────────────────┐
        │  Dependency &         │ ← (Librairies, packages)
        │  Container scanning   │ ← (Trivy, Clair, AquaSec)
        └──────────┬────────────┘
                   │
                   ▼
          ┌───────────────────┐
          │   Deployment      │ ← (CI/CD to Cloud / K8s)
          │   secured         │
          └────────┬──────────┘
                   │
                   ▼
        ┌────────────────────────┐
        │   Monitoring & Logs    │ ← (SIEM : Wazuh, Splunk, ELK)
        │   Security alerts      │
        └────────────────────────┘
```

## ☁️ Infrastructure Cloud
The use of the **Cloud** (AWS, Azure, GCP, OVH…) is now the standard in **DevOps**.
It offers **elasticity, speed and scalability**, but also introduces new security risks.

🔹 **_Security challenges in the Cloud_**
1. **Identity and Access Management (IAM)**
  - Stric control of users, roles, and permissions
  - *Least privilege* principle ➡️ give only the necessary rights
  - Example: an application account should not have the same privileges as an administrator
2. **Data Security**
  - In transit ➡️ TLS/HTTPS mandatory
  - At rest ➡️ disks, databases and backups must be encrypted
  - Example: enable native AWS S3 encryption to protect stored data
3. **Regulatory compliance**
  - ISO 27001: information security management
  - GDPR: personal data protection in Europe
  - NIST: cybersecurity best practices
  - Example: an application processing medical data must comply with GDPR and sometimes HIPAA (US).
4. **Monitoring and incident response**
  - Collection and analysis of logs with SIEM solutions (Splunk, Wazuh, ELK)
  - Real-time anomaly detection (compromised IAM, suspicious activities)
  - Example: trigger an alert if multiple failed login attempts come from a foreign IP address

👉 In summary, the **Cloud** is not *less secure*, but it requires strict practice to avoid misconfiguration and attack.

## ⬅️ Shift Left
The principle is to move security earlier in the development cycle.

```
         ┌──────────────┐
         │   Plan       │
         │ (requirements│
         │   & design)  │
         └───────┬──────┘
                 │
                 ▼
        ┌──────────────────┐
        │   Develop        │ ← Static analysis (SAST),
        │   (coding)       │    code reviews, secrets scanning
        └───────┬──────────┘
                │
                ▼
       ┌─────────────────────┐
       │    Test early       │ ← Integrated security tests:
       │   (build, CI/CD)    │    DAST, dependency scans
       └────────┬────────────┘
                │
                ▼
     ┌────────────────────────┐
     │ Deploy & Monitor       │ ← Anomaly detection,
     │   (prod monitoring)    │    logs, SIEM
     └────────────────────────┘
```

👉 The idea: identify vulnerabilities **before** going into production.

🔹 **_Advantages_**
- Fewer bugs in production, lower remediation costs
- Faster feedback for developers (fixes are applied while changes are still fresh)
- Security culture spread across the team

🔹 **_Limits / consideration_**
- Shift left **does not eliminate** the need for production monitoring: some vulnerabilities (runtime configuration, targeted attacks) only appear in production
- Require automation and training: adding tools without proper process = false sense of security

## 📈 Current Trends
- **Growing adoption of Shift Left** ➡️ security integrated from the development phase
- **Zero Trust architecture** ➡️ “Never trust, always verify”
- **Container & Kubernetes security** ➡️ clusters are frequent targets of attacks
- **Automation & AI** ➡️ automatic detection and remediation of simple vulnerabilities

## 🔍 Critical Analysis
- ✅ **Growing adoption**: DevSecOps is becoming a standard in large enterprises
- ❌ **Low maturity**: many teams integrate tools but lack a truly shared security culture
- ⚠️ **Main challenge**: people → training developers and involving management
- 🎯 **Future trend**: automation (AI, self-healing bots, intelligent pipelines) and Cloud-native security

## 📚 Sources
- **Standards**
  - [ISO 27001](https://www.iso.org/fr/standard/27001)
  - [NIST](https://tsapps.nist.gov/publication/get_pdf.cfm?pub_id=958795)
  - [GDPR](https://www.economie.gouv.fr/entreprises/reglement-general-protection-donnees-rgpd#:~:text=conformer%20au%20RGPD-,Le%20RGPD%2C%20qu%27est-ce%20que%20c%27est,application%20le%2025%20mai%202018)
- **Tools**
  - [SonarQube](https://www.sonarsource.com/products/sonarqube/)
  - [OWASP ZAP](https://www.zaproxy.org/)
  - [Top DevSecOps Tools – Gologic](https://www.gologic.ca/top-10-outils-devsecops/)
  - [Integrating OWASP ZAP – BlueGoatCyber](https://bluegoatcyber.com/blog/integrating-owasp-zap-in-devsecops/)
- **Trends**
  - [DevSecOps Trends – YourSky](https://yoursky.blue/fr/articles/tendances-devsecops)
  - [Shift Left vs Shift Right – Red Hat](https://www.redhat.com/fr/topics/devops/shift-left-vs-shift-right)
  - [Zero Trust – Microsoft](https://learn.microsoft.com/en-us/security/zero-trust/develop/secure-devops-environments-zero-trust)
  - [Cloud Security & Shift Left – Palo Alto](https://www.paloaltonetworks.com/resources/ebooks/cloud-security-spotlight-how-organizations-adopt-devsecops-and-shift-left-security)

## 📖 Glossary for IT Beginners
- **CI/CD pipeline**: an automated “assembly line” that builds, tests, and deploys software
- **Artifact**: the final file generated by a build (e.g., executable, Docker image)
- **Registry**: a repository where Docker images are stored (e.g., DockerHub, GitLab Registry)
- **Rollback**: reverting to a previous version of an app after a failed update
- **Orchestrator (Kubernetes)**: a “conductor” that automatically manages multiple containers (start, stop, restart, update)
- **Helm**: a “recipe manager” for Kubernetes, simplifying the deployment of complex applications
- **Logs**: files that record everything happening (errors, access, alerts)
- **SIEM**: a system that collects and analyzes logs to detect attacks

## 📝 Personal Conclusion
This Technology Watch allowed me to discover the fundamentals of DevSecOps and understand how security can be integrated at every stage of the software development lifecycle.
I came across this subject somewhat by chance: I really enjoy Bash scripting, my professor introduced me to DevOps, and my research led me to DevSecOps.
It is this discovery that I chose to share during my presentation, and that I am documenting here today.

> ⚠️ Note: I have not yet practiced the tools and concepts mentioned (SAST, DAST, Kubernetes, Helm, SIEM) directly, but this Technology Watch gave me a theoretical understanding and helped me make them accessible to other IT beginners.