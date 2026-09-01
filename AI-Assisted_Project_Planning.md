# 6. AI-Assisted Project Planning

## 6.1 Introduction
AI can support project planning by suggesting threats, reviewing architectures, discussing risks, and generating documentation.  
Final decisions must always be validated by the project engineer.

---

## 6.2 Threat Modeling Assistance
AI helps identify threats across IAM, GitHub, CI/CD, AWS, dependencies, Docker, logging, monitoring, and SOC.  
Examples: credential exposure, pipeline manipulation, excessive permissions, vulnerable dependencies, cloud misconfiguration.  
**Principle:** AI assists threat identification, not replaces analysis.

---

## 6.3 Architecture Reviews
AI can highlight weaknesses such as missing controls, excessive permissions, weak segmentation, or missing monitoring.  
Suggestions (e.g., add MFA, least privilege, improve logging) must be reviewed before use.

---

## 6.4 Risk Assessment Discussions
AI can discuss likelihood, impact, and mitigations of risks.  
Example: IAM credential compromise → Likelihood 4, Impact 5, Risk Score 20.  
AI helps explain reasoning but human validation is required.

---

## 6.5 Documentation Generation
AI can organize notes into structured documents: proposals, threat models, risk registers, implementation plans, incident reports, README files, summaries.  
Human review ensures accuracy.

---

## 6.6 AI-Assisted Workflow
Steps:  
1. Project requirement  
2. AI assistance (threats, architecture, risks, documentation)  
3. Human review  
4. Validation  
5. Final decision  

---

## 6.7 Validating AI Outputs
AI outputs must be checked for:  
- Technical accuracy  
- Trusted sources (vendor docs, standards, best practices)  
- Feasibility (scope, resources, time)  
- Security effectiveness (tested in controlled environment)  

---

## 6.8 Examples
- **Gitleaks Validation:** Test with dummy secret → detection → pipeline failure → deployment blocked.  
- **IAM Validation:** Authorized actions allowed, unauthorized denied.  

---

## 6.9 Limitations
AI may provide incorrect, outdated, overly complex, or context-missing recommendations.  
Sensitive data should not be shared with AI.  
Human expertise remains essential.

---

## 6.10 Principles
- Do not blindly trust AI  
- Validate outputs with documentation and testing  
- Keep AI within project scope  
- Protect sensitive information  

---

## 6.11 Usage Examples
| Project Area     | AI Assistance                                |
|------------------|----------------------------------------------|
| Threat Modeling  | Suggest threats and attack paths             |
| Architecture     | Identify design weaknesses                   |
| Risk Assessment  | Discuss likelihood, impact, mitigations      |
| Documentation    | Generate structured reports                  |
| CI/CD            | Explain pipeline errors and security concepts|
| IAM              | Suggest permission models                    |
| SOC              | Analyze detection concepts                   |
| Incident Response| Structure response procedures                |

---

## 6.12 Human-in-the-Loop
AI provides recommendations → human reviews → accept/reject → test → validate → implement.  
Security decisions are never automated blindly.

---

## 6.13 Final Model
AI supports threat modeling, architecture review, risk discussion, and documentation.  
Human review ensures verification, feasibility, and effectiveness before final decisions.
