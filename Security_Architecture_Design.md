# 4. Security Architecture Design

## 4.1 Introduction
Security architecture design defines how security controls, infrastructure, identities, logging, monitoring, and SOC capabilities are arranged and connected within the project.  

The architecture follows a **defense-in-depth** approach, meaning multiple layers of security are applied across development, CI/CD, cloud, and monitoring.  

The flow: developers push code to GitHub, GitHub Actions runs the CI/CD pipeline, security scanning tools (Semgrep, Gitleaks, Trivy) validate the code, and a security gate decides whether deployment can proceed. If approved, IAM enforces permissions for AWS cloud resources. Logging and monitoring (CloudTrail, CloudWatch) capture activity, while Wazuh provides SOC visibility, detection, and incident response.

---

## 4.2 Secure Network Architecture
The project uses an AWS VPC for isolation.  
- **Public Subnet**: Hosts only required resources that need limited internet exposure.  
- **Private Subnet**: Hosts internal/protected resources.  
- **Security Groups**: Control inbound/outbound traffic.  
- **Routing**: Ensures controlled communication paths.  

Main controls: VPC isolation, subnet separation, restricted ports, limited public exposure, and controlled routing.  
Because this is an educational lab, the network remains simple but secure.

---

## 4.3 Access Control Design
Access control defines who can access resources and what actions they can perform.  

- **IAM with least privilege**: Identities are authenticated, authorized, and mapped to policies that grant only required permissions.  
- **Role-based access**: Developers, CI/CD, and SOC analysts each have distinct roles.  
- **Principles applied**: least privilege, separation of responsibilities, strong authentication, MFA, restricted admin access, and regular reviews.  

**CI/CD Access**:  
The pipeline uses a deployment role with only the permissions required for AWS resources, avoiding unrestricted administrator rights. This minimizes impact if compromised.

---

## 4.4 Logging Architecture
Logging provides evidence about activities occurring within the environment. 

**Sources**:  
- IAM activity logs  
- AWS CloudTrail (API activity)  
- AWS CloudWatch (resource monitoring and metrics)  
- GitHub Actions logs (pipeline execution, builds, tests, scans, deployments, failures)  

Logs are collected centrally and sent to Wazuh, where detection rules generate alerts for SOC analysts.

---

## 4.5 Monitoring Architecture
Monitoring continuously observes security and operational events.  

**Focus areas**:  
- IAM: unauthorized access attempts, permission changes, suspicious identity activity  
- Cloud: API activity, configuration changes, suspicious resource activity  
- CI/CD: pipeline failures, scan failures, workflow anomalies, deployment events  
- Security tools: findings from Semgrep, Gitleaks, Trivy  

Logs flow into Wazuh, which applies detection rules and generates alerts for SOC analysts.

---

## 4.6 Detection Architecture
The monitoring system should not only collect logs; it should also help identify suspicious activity. 

Process: events generate logs → logs are collected → detection rules analyze them → suspicious activity triggers alerts → SOC analysts investigate before confirming incidents.

---

## 4.7 Security Visibility Planning
Security visibility means having enough information to understand what is happening within the environment.

| Area              | Visibility Source                          |
|-------------------|---------------------------------------------|
| IAM               | IAM activity and audit logs                 |
| GitHub            | Repository and workflow activity            |
| CI/CD             | GitHub Actions logs                         |
| Source Code       | Semgrep (static code analysis)              |
| Secrets           | Gitleaks (secret detection)                 |
| Dependencies/Images | Trivy (dependency & container scanning)   |
| AWS API Activity  | CloudTrail (API audit trail)                |
| AWS Resources     | CloudWatch (resource monitoring & metrics)  |
| SOC               | Wazuh (centralized monitoring & detection)  |


Together, these provide end-to-end visibility across identities, code, pipelines, cloud, and monitoring.

---

## 4.8 Security Control Placement
Security controls will be distributed throughout the architecture. 
- **Developer**: IAM authentication  
- **GitHub**: branch protection, access control  
- **CI/CD**: Semgrep, Gitleaks, Trivy scans  
- **Security Gate**: prevents insecure deployments  
- **AWS**: IAM, VPC, Security Groups  
- **Logging**: CloudTrail, CloudWatch  
- **SOC**: detection, alerting, investigation  

This demonstrates defense in depth because security controls are placed at multiple points rather than relying on a single security mechanism.

---

## 4.9 Preventive, Detective and Corrective Controls

The architecture uses three major categories of controls.

- **Preventive**: These attempt to stop security problems before they cause impact. Examples: IAM least privilege, MFA, branch protection, security groups, security gates  
- **Detective**: These identify security issues or suspicious activity. Examples: Semgrep, Gitleaks, Trivy, CloudTrail, CloudWatch, Wazuh detection rules  
- **Corrective**: These help resolve security incidents. Examples: credential revocation, dependency updates, configuration fixes, incident containment, remediation, recovery  

Overall flow: **Prevent → Detect → Investigate → Respond → Recover**

---

## 4.10 Security Boundaries
Security boundaries are points where access or trust needs to be controlled. 
- Developer ↔ GitHub  
- GitHub ↔ CI/CD  
- CI/CD ↔ AWS  
- Internet ↔ AWS VPC  
- AWS ↔ SOC  

At each boundary, authentication, authorization, network controls, data protection, logging, and monitoring are applied.

---

## 4.11 Complete Security Architecture
The architecture integrates all layers:  
- Developers push code to GitHub repositories.  
- GitHub Actions runs CI/CD workflows.  
- Security scanning tools (Semgrep, Gitleaks, Trivy) validate code.  
- A security gate blocks insecure deployments.  
- IAM enforces least privilege for AWS cloud resources.  
- AWS VPC and Security Groups restrict network exposure.  
- CloudTrail and CloudWatch provide logging and monitoring.  
- Logs are collected by Wazuh, which applies detection rules.  
- Alerts are generated for SOC analysts, who investigate and respond using incident-response procedures.  

---

## 4.12 Security Architecture Principles
1. Least Privilege : Give users and services only the permissions they require.
2. Defense in Depth : Use multiple security controls across different layers.
3. Secure by Design : Security should be considered during design and development rather than after deployment.
4. Visibility : Important activities should be logged and monitored.
5. Segmentation : Separate and restrict network resources where appropriate.
6. Automation : Automate security checks wherever practical.
7. Continuous Monitoring : Security events should be monitored continuously within the capabilities of the lab environment.
8. Controlled Response : Security incidents should follow a defined response process.

---

## 4.13 Final Architecture Summary
The architecture integrates IAM, Git/GitHub, CI/CD, DevSecOps tools, AWS cloud infrastructure, logging, monitoring, and SOC operations. IAM enforces least privilege, GitHub manages source code, GitHub Actions automates CI/CD, and Semgrep, Gitleaks, Trivy provide security validation. A security gate blocks insecure deployments. AWS provides cloud infrastructure with VPC and Security Groups. CloudTrail and CloudWatch deliver logging and monitoring, while Wazuh supports centralized detection. SOC analysts investigate alerts and handle incidents through a defined incident response process.
