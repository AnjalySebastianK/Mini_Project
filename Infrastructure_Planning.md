# Infrastructure Planning

## 1. Network Design
The project will use a cloud-based network environment in **AWS**. The network is designed to provide isolation, controlled access, and limited exposure of resources. Only the required resources and ports will be exposed.

**Main Network Components**
- **VPC**: Provides an isolated virtual network in AWS.  
- **Subnets**: Separate resources into logical network segments.  
- **Internet Gateway**: Provides internet connectivity where required.  
- **Route Tables**: Control how network traffic is routed.  
- **Security Groups**: Control allowed inbound and outbound traffic.  
- **Cloud Resources**: Host the components required for the project.  

---

## 2. Security Controls
Security controls will be applied at different layers of the infrastructure.

**Identity Controls**
- IAM roles and policies  
- Least privilege  
- MFA where applicable  
- Separate permissions for different users/services  
- Controlled CI/CD deployment permissions  

**Network Controls**
- VPC isolation  
- Security Groups  
- Limited open ports  
- Restricted access to cloud resources  
- Avoid unnecessary public exposure  

**CI/CD Controls**
- GitHub repository access control  
- Branch protection  
- Pull Request review  
- Security scanning  
- Security gates  

**Application/Code Security**
The CI/CD pipeline will use:  
| Tool     | Purpose                   |  
|----------|---------------------------|  
| Semgrep  | Static security analysis  |  
| Gitleaks | Secret detection          |  
| Trivy    | Vulnerability scanning    |  

**Monitoring Controls**
- CloudTrail  
- CloudWatch  
- Wazuh/SOC monitoring  
- Security alerts  
- Detection rules  

The overall approach follows **defense in depth**, meaning multiple security controls are used instead of relying on a single control.

---

## 3. Logging Strategy
Logging is required to provide visibility into activities occurring throughout the environment. 
Logs will be collected or reviewed from:  
- IAM Activity  
- CloudTrail  
- CloudWatch  
- CI/CD  
- Security Scanners  
- SOC Monitoring  

**CloudTrail**  
CloudTrail will be used primarily to record AWS API activity and provide an audit trail of actions performed within the AWS environment.
Important information may include:
- Identity
- Action performed
- Resource
- Time
- Source information
- Success/failure status

**CloudWatch**  
CloudWatch will be used for appropriate AWS resource monitoring, metrics, and log-related visibility.  

**CI/CD Logs**  
GitHub Actions logs will show:  
- Pipeline execution  
- Build results  
- Test results  
- Security-scan results  
- Deployment results  
- Pipeline failures  

**Security Scan Results**  
Evidence from Semgrep, Gitleaks, and Trivy will support troubleshooting and investigation.  

**Logging Principle**  
The project will follow the log of important security events, protect the logs, and make   relevant information available for investigation.

---

## 4. Monitoring Requirements
Monitoring will identify abnormal, unauthorized, or potentially dangerous activity.  

**IAM Monitoring**
- Authentication/access activity  
- Permission changes  
- Role activity  
- Unauthorized actions  

**Cloud Monitoring**
- AWS API activity  
- Resource activity  
- Security-related events  
- Configuration changes  

**CI/CD Monitoring**
- Pipeline failures  
- Security-scan failures  
- Unexpected workflow activity  
- Deployment activity  

**Security Monitoring**
- Exposed secrets  
- Vulnerabilities  
- Suspicious cloud activity  
- Repeated failed actions  
- Other selected security events  

The monitoring system should provide enough information for analysts to investigate events effectively.  

---

## 5. Incident Response Planning
The project will include a basic incident-response process for handling security events.  

**Planned Process**
1. **Detection** – Identify suspicious or insecure events using logs, tools, or monitoring.  
2. **Alert** – Generate or surface an alert for the SOC analyst.  
3. **Triage** – Assess whether the alert is legitimate, expected, or malicious.  
4. **Investigation** – Analyze logs and evidence to determine:  
   - What happened?  
   - Who performed the action?  
   - When did it happen?  
   - What resource was affected?  
   - Was the activity authorized?  
   - What is the potential impact?  
5. **Containment** – Prevent further damage.  
6. **Remediation** – Fix the underlying issue (e.g., correct IAM permissions, remove secrets, update dependencies, fix insecure code).  
7. **Recovery** – Restore normal operation and verify resolution.  
8. **Lessons Learned** – Document root cause, what happened, controls that worked/failed, and improvements needed.  

---

## 2.7 Infrastructure Planning Summary
The infrastructure will be designed around five main principles:
1. Controlled network access using VPCs, subnets, and Security Groups.  
2. Least-privilege access using IAM.  
3. Defense in depth with multiple security controls.  
4. Security visibility through logging and monitoring.  
5. Rapid response through SOC monitoring and incident-response procedures.  
