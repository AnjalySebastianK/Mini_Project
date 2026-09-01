# Threat Modeling

## 1. Introduction
Threat modeling is the process of identifying important assets in a system, understanding possible threats and attack paths, analyzing vulnerabilities and risks, and selecting appropriate security controls to reduce those risks.

In this project, threat modeling will cover:
- IAM
- Git/GitHub
- CI/CD
- Security tools
- AWS cloud infrastructure
- Network
- Logs
- Monitoring
- SOC

The main purpose is to understand:
- What can go wrong
- How an attacker could cause it
- What the impact could be
- How we can prevent or detect it

---

## 2. Asset Identification
An asset is anything that has value and needs to be protected.  

| ID   | Asset               | Description                          | Importance |
|------|---------------------|--------------------------------------|------------|
| A01  | GitHub Repository   | Source code and project configuration| High       |
| A02  | CI/CD Workflow      | Automation and deployment config     | High       |
| A03  | IAM Identities      | Users and service identities         | Critical   |
| A04  | IAM Policies        | Permissions assigned to identities   | Critical   |
| A05  | Deployment Role     | Identity used by CI/CD to access AWS | Critical   |
| A06  | AWS Resources       | Cloud resources used by the project  | High       |
| A07  | VPC & Network       | Cloud network environment            | High       |
| A08  | Docker Image        | Containerized project artifact       | High       |
| A09  | Dependencies        | Third-party software components      | High       |
| A10  | Cloud Logs          | Audit and security evidence          | High       |
| A11  | CI/CD Logs          | Pipeline execution evidence          | Medium     |
| A12  | SOC Platform        | Security monitoring environment      | High       |

Most important assets:
- IAM credentials and policies because they control access to cloud resources
- CI/CD deployment identity because it allows automated interaction with AWS  
- GitHub repository and workflow because unauthorized modification could affect the software delivery process.
- Cloud resources because they may contain or provide access to project infrastructure.
- Security logs because they provide evidence required for detection and investigation.

---

## 3. Threat Identification

A threat is a potential event or action that could negatively affect an asset. The project will consider several types of threats.

**Identity Threats**
- Credential theft  
- Account compromise  
- Excessive permissions  
- Privilege misuse  
- Unauthorized access  

**Source-Code Threats**
- Unauthorized repository access  
- Malicious code changes  
- Workflow modification  
- Secret exposure  
- Malicious commits  

**CI/CD Threats**
- Pipeline manipulation  
- Workflow changes  
- Credential exposure  
- Insecure deployment  
- Compromised build process  

**Cloud Threats**
- IAM misuse  
- Misconfiguration  
- Excessive permissions  
- Unauthorized API activity  
- Public exposure  
- Network attacks  

**Supply-Chain Threats**
- Vulnerable dependencies  
- Compromised packages  
- Vulnerable container images  
- Malicious third-party components  

**Monitoring Threats**
- Missing logs  
- Incomplete logging  
- Incorrect detection rules  
- Alert failures  
- Insufficient visibility  

---

## 4. Threat Actors
- **External Attacker**: Unauthorized person attempting access to the environment.
- **Compromised Account**: An attacker using a legitimate account that has been compromised.  
- **Malicious Insider**: An authorized user intentionally misusing their permissions. 
- **Accidental Insider**: A legitimate user unintentionally introducing a security problem, such as committing a secret. 
- **Supply-Chain Attacker**: An attacker who compromises or abuses a third-party dependency or software component. 

---

## 5. Attack Surface Analysis
**GitHub Attack Surface**
- Potential entry points: Repository authentication, permissions, Pull Requests, branches, Github Action workflows, secrets , configuratuion files 
- Security controls: strong authentication, MFA, repository permissions, branch protection, PR review, secret scanning  

**IAM Attack Surface**
- Entry points: user credentials, IAM roles, IAM policies, access keys, Service identitiles
- Controls: least privilege, MFA, role-based access, credential protection, logging and monitoring 

**CI/CD Attack Surface**
- Entry points: workflow files, build runners, pipeline credentials, third-party actions, deployment configurations
- Controls: restricted permissions, secure workflow configuration, branch protection, security scanning, IAM least privilege

**AWS Attack Surface**
- Entry points: AWS APIs, IAM, network interfaces, publicly exposed resources  , security groups, cloud resources
- Controls: IAM, VPC, Security Groups, restricted network access, CloudTrail, monitoring

**Dependency/Container Attack Surface**
- Entry points: Third-party dependencies, Docker base images, Container packages, Build artifacts  
- Controls: Trivy scanning, dependency updates, minimal images, security gates  

---

## 6. Main Threat Scenarios
**Threat 1 — Compromised IAM Credential**  
Controls: MFA, least privilege, credential protection, CloudTrail, monitoring, SOC detection  

**Threat 2 — Secret Exposed in Repository**  
Controls: Gitleaks, secret management, repo protection, credential rotation, security gate  

**Threat 3 — Vulnerable Dependency**  
Controls: Trivy, dependency updates, security gate, regular scanning  

**Threat 4 — CI/CD Workflow Manipulation**  
Controls: MFA, branch protection, PR review, restricted permissions, monitoring  

**Threat 5 — Cloud Misconfiguration**  
Controls: secure VPC design, restricted Security Groups, IAM, config review, monitoring  

---

## 7. Risk Assessment
Risk assessment helps us determine which threats require the most attention.
Risk = Likelihood × Impact  

**Likelihood Scale**  
1 Very Low → 5 Very High  

**Impact Scale**  
1 Very Low → 5 Very High  

**Risk Rating**  
- 1–4 Low  
- 5–9 Medium  
- 10–16 High  
- 17–25 Critical  

---

## 8. Initial Risk Register
| ID  | Risk                        | Likelihood | Impact | Score | Rating   |
|-----|-----------------------------|------------|--------|-------|----------|
| R01 | IAM credential compromise   | 4          | 5      | 20    | Critical |
| R02 | Excessive IAM permissions   | 4          | 5      | 20    | Critical |
| R03 | Secret exposure             | 4          | 5      | 20    | Critical |
| R04 | CI/CD workflow manipulation | 3          | 5      | 15    | High     |
| R05 | Vulnerable dependency       | 4          | 4      | 16    | High     |
| R06 | Cloud misconfiguration      | 3          | 5      | 15    | High     |
| R07 | Container vulnerability     | 3          | 4      | 12    | High     |
| R08 | Insufficient logging        | 3          | 4      | 12    | High     |
| R09 | Detection failure           | 3          | 4      | 12    | High     |
| R10 | Unauthorized repo access    | 3          | 4      | 12    | High     |

---

## 9. Mitigation Planning

Mitigation means reducing the likelihood or impact of a risk by applying appropriate security controls.

**IAM Compromise**
- Risk: Unauthorized access using compromised credentials.
- Mitigation:  MFA, least privilege, avoid long-lived credentials, secure credential handling, CloudTrail, SOC monitoring  

**Excessive Permissions**  
- Risk: A user or service receives more permissions than required.
- Mitigation: Assign specific roles with minimum permissions, regular reviews  

**Secret Exposure**  
- Risk: A credential or secret is accidentally committed to GitHub.
- Mitigation: Gitleaks detection, security gate, revoke/rotate secrets  

**Vulnerable Dependency**  
- Risk: A third-party dependency contains a known vulnerability.
- Mitigation: Trivy scanning, dependency updates, security gates, regular vulnerability checks  

**Workflow Manipulation**  
- Risk: An attacker modifies the pipeline workflow.
- Mitigation: MFA, branch protection, PR review, restricted repo permissions, least-privilege deployment identity, monitoring  

**Cloud Misconfiguration**  
- Risk: Incorrect network or cloud configuration increases exposure.
- Mitigation: Secure VPC design, restricted Security Groups, IAM, config review, cloud logging, monitoring  

**Insufficient Logging**  
- Risk: Important security activity is not recorded.
- Mitigation: Enable CloudTrail, configure monitoring, maintain CI/CD logs, send relevant security information to the SOC monitoring layer, regularly test visibility


---

## 10. Risk-Control Mapping
| Risk                  | Preventive Control | Detective Control | Response                  |
|-----------------------|--------------------|------------------|---------------------------|
| IAM compromise        | MFA, least privilege | CloudTrail, SOC | Revoke credentials        |
| Secret exposure       | Secure handling    | Gitleaks         | Remove/rotate secrets     |
| Vulnerable dependency | Security gate      | Trivy            | Update dependency         |
| Workflow manipulation | Branch protection  | Monitoring       | Revert/fix workflow       |
| Cloud misconfiguration| IAM, Sec Groups    | Monitoring       | Correct configuration     |
| Container vulnerability| Secure build      | Trivy            | Rebuild/update image      |
| Logging gap           | Logging config     | Monitoring tests | Fix logging               |
| Detection failure     | Detection design   | Alert testing    | Tune detection rules      |

---

## 11. Residual Risk
Security controls reduce risk, but they do not normally eliminate it completely.
Example: IAM compromise → MFA + least privilege + logging + monitoring → residual risk remains, reviewed during testing.  

---

## 12. Threat Modeling Summary
The threat model identifies the main assets, threats, attack surfaces, and risks within the project.  
Major concerns:  
- IAM → credential/permission risks  
- GitHub → repo/workflow/secret risks  
- CI/CD → pipeline/credential risks  
- AWS → cloud/network/config risks  
- Dependencies → supply-chain risks  
- Logging & SOC → visibility/detection risks  

---

## 13. Overall Threat Modeling Flow
- Asset Identification  
- Threat Identification  
- Attack Surface Analysis  
- Threat Scenarios  
- Risk Assessment  
- Risk Prioritization  
- Security Controls  
- Mitigation  
- Residual Risk  
- Continuous Review  

---
