# Mobile App Architecture Review - Questions

This document contains review questions organized by AWS Well-Architected Framework's 6 Pillars.

## How to Use
- Use this file during interviews/workshops with the delivery team.
- Record answers under each pillar or in the Q&A table at the end.
- Mark unresolved items as follow-ups with owner and due date.
- Refer to `requirement.txt` for detailed scope items per pillar.

---

# PILLAR 1: OPERATIONAL EXCELLENCE
*Ability to run and observe systems, automate processes, and deliver business value.*

## 1) Development Environment
1. Is there a documented local setup guide for frontend, backend, and database access?
2. Are required versions pinned (JDK, Gradle/Maven, Android/iOS toolchains, dependencies)?
3. How long does full onboarding take for a new engineer?
4. Are environment variables and local secrets managed consistently and securely?
5. Is there parity between local development and shared environments?

## 2) Operating Environment
1. What environments exist (dev/test/stage/prod), and what are their purposes?
2. Are infrastructure and runtime configurations version-controlled (Infrastructure as Code)?
3. How are configuration differences between environments managed and audited?
4. What is the deployment frequency, and who can deploy to each environment?
5. Are region/zone strategies defined for availability and latency?

## 3) CI/CD and Release Management
1. What are mandatory quality gates before merge/release?
2. What is automated test coverage by layer (unit/integration/e2e/security)?
3. Is deployment strategy defined (blue-green/canary/rolling)?
4. Is rollback automated and tested?
5. Are release approvals and change logs traceable?
6. Are security tests (SAST/DAST) integrated into CI/CD pipeline as gates?

## 4) Observability and Incident Response
1. Can logs be correlated across services with trace/request IDs?
2. Are metrics and traces available for all critical endpoints?
3. Which alerts are actionable vs noisy (alert fatigue)?
4. Is there a documented on-call and escalation process?
5. Are incident runbooks complete and routinely updated?
6. Are postmortems performed and tracked to closure?
7. Is there a documented security incident response plan with defined roles?
8. Are security incidents tracked, investigated, and reported (RCA required)?

## 5) Operational Readiness
1. Is there configuration parity between stage and production?
2. Are secret rotation and access reviews performed on schedule?
3. Are dependency risks tracked (CVEs, outdated libs, SBOM)?
4. Are operational runbooks available for top failure scenarios?
5. Is ownership clear for each service and operational KPI?

## 6) Defect and Issue Tracking
1. What system is used to track defects/bugs (Jira, GitHub Issues, Azure DevOps, etc.)?
2. Are defects categorized by severity, type, and priority?
3. What is the defect SLA (critical/high/medium/low severity)?
4. Is there a dashboard showing defect volume, trends, and aging backlog?
5. How are defects triaged and assigned to owners?
6. Are defects linked to root cause and preventive actions?
7. What is the defect closure rate per sprint/month?
8. Is there a process to prevent recurring defects?

## 7) Business Metrics and Analytics
1. Is there a dashboard showing sales, active users, usage trends, and revenue?
2. Are request volumes tracked by feature, endpoint, and provider?
3. Is there categorization of requests (payment/delivery/user/admin/etc.)?
4. What are the key KPIs being tracked and reported monthly?
5. Is there user analytics (retention, churn, feature adoption)?
6. Are performance metrics tied to business impact (latency vs conversion)?
7. Is there a capacity planning process based on growth forecasts?
8. Are third-party provider metrics monitored (API rate limits, SLA compliance)?

## 8) Version Control and Repository Management
1. What VCS platform is used (Git, SVN), and what is the repository structure?
2. What branching strategy is implemented (Git Flow, trunk-based, release branches)?
3. Are protected branch rules enforced (code review, status checks, merge policies)?
4. Are commit message standards documented, and how is changelog managed?
5. How are releases tagged, and what versioning strategy is followed?
6. Is credential scanning and secrets detection enabled in CI/CD pipeline?
7. How are repository access controls and audit logging managed?
8. How are rollback and revert procedures handled for problematic commits/releases?

## 9) Mobile App Store Management
1. How are Apple App Store and Google Play Store accounts secured (MFA, access control)?
2. Is app signing and certificate management automated?
3. What is the beta testing process (TestFlight, Google Play Beta)?
4. Are release notes, privacy policy, and compliance documentation up-to-date?
5. Is there a staged rollout strategy with rollback capability?
6. How often are app store credentials rotated and access reviewed?
7. How is app versioning managed (semantic versioning, build numbers)?
8. Is the app submission and approval workflow documented (automated/manual)?
9. How is app store policy compliance monitored and violations remediated?
10. Is audit logging enabled for AppStore Connect and Google Play Console?

## 10) Cross-Training and Support
1. Is there a knowledge base, wiki, or documentation portal for runbooks?
2. Is there a developer onboarding program with mentoring opportunities?
3. Are single points of failure identified and mitigated for critical roles?
4. How is on-call rotation designed (fairness, load balancing, escalation)?
5. Is support tier structure defined (L1/L2/L3)?
6. Is there an incident postmortem process and lessons learned documentation?
7. Are there cross-functional knowledge transfer mechanisms and training?
8. Are backup team members identified for critical skill areas?

---

# PILLAR 2: SECURITY
*Ability to protect data, systems, and assets while delivering business value.*

## 11) Authentication and Authorization
1. What authentication mechanisms are used for mobile users and internal services?
2. How is authorization enforced (RBAC/ABAC, resource-level checks)?
3. Is multi-factor authentication (MFA) enforced for sensitive operations?
4. Are API keys, OAuth tokens, and JWTs properly validated and scoped?

## 12) Data Protection
1. How are secrets stored, rotated, and accessed? (vault, KMS, etc.)
2. Is all traffic encrypted in transit (TLS 1.2+), including service-to-service calls?
3. Is sensitive data encrypted at rest, and where are encryption keys managed and rotated?
4. Is database encryption (Transparent Data Encryption) enabled for MySQL?
5. Are database access controls and audit logging configured?

## 13) Mobile App Security
1. Are mobile apps signed and verified (certificate pinning, app attestation)?
2. Are sensitive data (credentials, tokens) stored securely in mobile keystores?
3. Are reverse engineering protections and obfuscation applied to mobile apps?
4. Are mobile apps scanned for hardcoded secrets and sensitive information?

## 14) Code and Dependency Security
1. Are SAST (Static Application Security Testing) tools integrated into CI/CD pipeline?
2. What is the SLA for fixing SAST findings (critical/high/medium/low)?
3. Are dependency vulnerabilities (CVE, dependency scanning) checked on every build?
4. Is there a Software Bill of Materials (SBOM) maintained and tracked?
5. Are third-party and open-source libraries regularly updated and audited?

## 15) Dynamic Security Testing
1. Are DAST (Dynamic Application Security Testing) scans performed regularly?
2. Is API penetration testing conducted, and what is the frequency?
3. Are security tests automated in the CI/CD pipeline or part of release gates?
4. Are security findings tracked, prioritized, and remediated on schedule?

## 16) API Rate Limiting and DDoS Protection
1. Is rate limiting implemented on APIs? What are the limits per client/endpoint?
2. Are there different rate limits for different user tiers or API plans?
3. Is there API quota management and tracking (daily/monthly limits)?
4. Is a WAF (Web Application Firewall) deployed in front of the API?
5. What DDoS protection measures are in place (traffic filtering, geo-blocking)?
6. Is the load balancer protecting against common attacks (SQL injection, XSS)?
7. Are rate limit violations logged and alerted?
8. How is API throttling communicated to clients (headers, error responses)?
9. Is there an API gateway (Kong, AWS API Gateway, etc.) enforcing policies?
10. Are rate limit metrics visible in dashboards and monitored?

## 17) Infrastructure and Network Security
1. Are network policies enforced to restrict inter-pod communication?
2. Is VPC/network segmentation implemented (public/private subnets, security groups)?

## 18) Data Governance and Compliance
1. Is data classified (public/internal/confidential/PII)?
2. Where is PII collected, stored, transmitted, and masked?
3. Are retention and deletion policies implemented and verified?
4. Is access to sensitive data audited and regularly reviewed?
5. Which compliance requirements apply (GDPR/CCPA/industry)?

## 19) Security Governance
1. Is there a security policy covering acceptable use, data handling, and access control?
2. Are security awareness and training provided to developers and operations teams?

---

# PILLAR 3: RELIABILITY
*Ability to prevent and mitigate failures in computing systems.*

## 20) Reliability and Availability
1. Are SLO/SLA targets defined per critical service?
2. What are current uptime, latency, and error-rate baselines?
3. What are RPO and RTO targets for each critical data domain?
4. Are backups tested regularly with actual restore drills?
5. Are there single points of failure in services, DB, or networking?

## 21) Container Orchestration and Infrastructure (Reliability aspects)
1. Is the backend deployed on Kubernetes, Docker Swarm, or managed service (ECS, AppEngine)?
2. Who manages the Kubernetes cluster (self-managed vs managed service like EKS/GKE/AKS)?
3. What is the node/cluster auto-scaling strategy and limits?
4. Is there a service mesh (Istio, Linkerd) for inter-service communication and observability?
5. How is service discovery configured (Kubernetes DNS, Consul, etc.)?
6. What is the container orchestration upgrade and maintenance strategy?

---

# PILLAR 4: PERFORMANCE EFFICIENCY
*Use computing resources efficiently to meet requirements and maintain efficiency as demand changes.*

## 22) Performance and Scalability
1. What are target p95/p99 latencies for key APIs?
2. Have peak and burst load tests been executed recently?
3. Where are the top bottlenecks (API, DB, cache, network)?
4. Is connection pooling tuned for MySQL and service concurrency?
5. Is there a caching strategy (client, edge, service, DB query cache)?

## 23) Container Orchestration and Infrastructure (Performance aspects)
1. How are container images built, stored, and scanned for vulnerabilities?
2. Are container image tags versioned and traceable to source code commits?
3. Are resource requests and limits defined for all pods/containers?
4. How is Infrastructure as Code managed (Terraform, CloudFormation, Helm charts)?

---

# PILLAR 5: COST OPTIMIZATION
*Run systems to deliver business value at the lowest price point.*

## 24) Cost Efficiency
1. Are cloud resources tagged by team, service, and environment?
2. Which services/resources are currently overprovisioned?
3. Are autoscaling rules tuned to real traffic patterns?
4. Are storage lifecycle policies in place (logs, backups, artifacts)?
5. Is there budget alerting and anomaly detection?

## 25) Cost Governance (FinOps)
1. Is there a monthly cost review cadence with action items?
2. Are unit economics tracked (cost per active user/transaction)?
3. Are rightsizing recommendations implemented and measured?
4. Are idle resources identified and removed automatically?
5. Are optimization results reported by team/service?

---

# PILLAR 6: SUSTAINABILITY (Optional)
*Minimizing environmental impact of cloud workloads.*

## 26) Resource Efficiency
1. Are resources allocated and scheduled in an energy-efficient manner?
2. Are idle or unused resources identified and removed?
3. Is data transfer and storage optimized for efficiency?

---

# CROSS-CUTTING GOVERNANCE

## 27) API and Microservice Governance
1. Is API versioning policy documented and followed?
2. How is backward compatibility guaranteed during releases?
3. Are service contracts tested automatically (contract testing)?
4. How are breaking schema changes approved and communicated?
5. Are retries, timeouts, circuit breakers, and idempotency standardized?

---

# CRITICAL RISKS & REMEDIATION

## 28) Priority Risk Assessment
1. What are the top 5 risks today across security, reliability, cost, and performance?
2. Which risks have no owner or no remediation plan?
3. What is the expected timeline for closing high-priority gaps?
4. Which gaps could block scale, audits, or production stability?

---

