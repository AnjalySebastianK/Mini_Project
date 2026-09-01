# 7. Project Deliverables

The project will produce the following security deliverables for the
"Secure Cloud DevSecOps Pipeline with IAM and SOC Monitoring" project.

## 7.1 Security Project Proposal

The proposal will describe the project objectives, security goals, scope,
stakeholders, technologies, and expected outcomes.

The project focuses on securing a simulated organization's:

- IAM and access control
- AWS cloud environment
- Git and GitHub workflow
- CI/CD pipeline
- DevSecOps security controls
- Logging and monitoring
- SOC operations

## 7.2 Security Architecture Design

The architecture document will explain how the different components are
connected and secured.

Main architecture flow:

    GitHub
       |
       v
    GitHub Actions
       |
       v
    Semgrep + Gitleaks + Trivy
       |
       v
    Security Gate
       |
       v
    IAM
       |
       v
    AWS Cloud
       |
       v
    CloudTrail / CloudWatch
       |
       v
    Wazuh / SOC
       |
       v
    Detection -> Investigation -> Response

The architecture will cover network security, IAM, CI/CD security,
cloud security, logging, monitoring, and SOC visibility.

## 7.3 Threat Model Report

The Threat Model Report will identify possible security threats against
the DevSecOps and cloud environment.

It will include:

- Important assets
- Threat actors
- Attack surfaces
- Potential attack paths
- Vulnerabilities
- Threat scenarios
- Security controls
- Mitigation strategies

Main threats include:

- IAM credential compromise
- Secret exposure
- CI/CD manipulation
- Vulnerable dependencies
- Cloud misconfiguration
- Unauthorized access

## 7.4 Risk Assessment Report

The Risk Assessment Report will evaluate the risks identified during
threat modeling.

The project will use:

    Risk = Likelihood x Impact

Risks will be classified as:

    Low -> Medium -> High -> Critical

The report will also document the security controls used to reduce the
identified risks and the remaining residual risk.

## 7.5 Implementation Plan

The Implementation Plan will describe how the project will be practically
built and tested.

The planned implementation sequence is:

    1. Prepare the lab environment
    2. Configure AWS IAM
    3. Configure AWS cloud and network
    4. Set up Git and GitHub
    5. Build the CI/CD pipeline
    6. Integrate Semgrep, Gitleaks, and Trivy
    7. Configure the security gate
    8. Configure CloudTrail and CloudWatch
    9. Set up Wazuh and SOC monitoring
    10. Perform controlled security tests
    11. Investigate security alerts
    12. Perform incident response
    13. Validate and document the results

The implementation will be performed in a controlled lab environment
using test data and authorized security scenarios.

## 7.6 Final Deliverables Summary

| Deliverable | Purpose |
|-------------|---------|
| Security Project Proposal | Defines what we are building and why |
| Security Architecture Design | Explains how the environment is securely designed |
| Threat Model Report | Identifies possible threats and attack paths |
| Risk Assessment Report | Evaluates and prioritizes security risks |
| Implementation Plan | Defines how the project will be built and tested |

## 7.7 Overall Deliverable Flow

    Project Proposal
          |
          v
    Security Architecture
          |
          v
    Threat Model
          |
          v
    Risk Assessment
          |
          v
    Implementation Plan
          |
          v
    Practical Implementation
          |
          v
    Testing and Evidence
