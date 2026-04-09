# Data Protection Architecture

A security reference architecture for protecting sensitive, regulated, and business-critical data across storage, processing, access, transfer, and retention lifecycles in cloud and SaaS environments.

---

## Overview

Data protection is the architecture discipline concerned with how data is classified, accessed, stored, moved, processed, retained, and deleted.

The main security question is not only whether the surrounding system is secure. It is whether the data itself remains appropriately protected as it moves across applications, services, storage platforms, users, administrative workflows, analytics processes, and operational support paths.

A strong data protection architecture should make it clear what data matters most, who should be allowed to access it, under what conditions it can be moved or transformed, how it is protected cryptographically, and how its handling can be monitored over time.

---

## Security Objectives

This architecture is designed to:

- protect sensitive and regulated data throughout its lifecycle
- reduce unnecessary access to high-value data
- apply consistent controls across storage, processing, and transfer paths
- support classification-aware access and handling decisions
- reduce data exposure through administrative, operational, and integration paths
- improve visibility into sensitive data access and movement
- support secure retention, archival, and deletion practices

---

## Architectural Position

A data protection architecture sits at the information and control layer.

Where cloud architecture provides hosting foundations, Zero Trust focuses on trust decisions, and application security protects service boundaries, data protection focuses on the data itself: how it is identified, how its sensitivity affects architecture decisions, and how protection remains effective across many technical environments and workflows.

Its purpose is to make data security explicit rather than incidental.

---

## Core Security Domains

## 1. Data Classification and Criticality

Not all data needs the same level of protection.

A data protection architecture should begin by making sensitivity, business value, regulatory impact, and operational criticality visible enough to influence design decisions.

### Required controls

- defined classification levels for data sensitivity
- identification of regulated, confidential, and high-value data types
- ownership for major data domains and repositories
- mapping of classification to control requirements
- review of datasets that combine multiple sensitive data types
- identification of systems that create, process, or store high-impact data

### Security intent

This domain ensures that protection decisions are tied to the importance of the data rather than applied uniformly or inconsistently.

---

## 2. Data Access Control

Access to data should be narrower than access to the surrounding application or infrastructure.

A person, service, or workflow may be allowed to use part of a system without needing broad access to all underlying data handled by that system.

### Required controls

- role-based or attribute-based access to data resources
- least-privilege access for users, administrators, and services
- separation of duties for administration, approval, and operational handling
- narrower controls for highly sensitive data domains
- controlled break-glass and support access to sensitive data
- periodic review of high-risk data permissions

### Security intent

This domain reduces broad exposure of sensitive data and helps prevent system-level access from automatically becoming data-level access.

---

## 3. Data Storage Protection

Sensitive data should remain protected where it is stored, whether in databases, object storage, file systems, data lakes, search platforms, backups, or derived stores.

Storage design should reflect both confidentiality and resilience requirements.

### Required controls

- encryption at rest for sensitive data stores
- restricted administrative access to storage platforms
- segmentation of high-value datasets where needed
- review of derived, replicated, cached, and indexed data stores
- secure backup and recovery protections
- controlled handling of snapshots, exports, and replicas

### Security intent

This domain reduces exposure through the storage layer and prevents overlooked copies of data from becoming weak points.

---

## 4. Data Transfer and Movement Control

Data often becomes more exposed when it moves than when it sits at rest.

Transfers between services, pipelines, analytics platforms, integration layers, external parties, and operational tools should be treated as explicit security events.

### Required controls

- encryption in transit for sensitive transfers
- controlled and approved transfer paths
- minimization of unnecessary data movement
- review of external integrations and third-party data flows
- stronger controls for bulk export, replication, and cross-boundary sharing
- logging of high-risk data movement events

### Security intent

This domain reduces uncontrolled spread of sensitive data and makes movement pathways easier to review and monitor.

---

## 5. Data Processing and Transformation

Data protection should continue during processing, not stop once access has been granted.

Applications, analytics jobs, reporting workflows, batch processes, and transformation pipelines may all introduce new exposure paths.

### Required controls

- secure handling of sensitive data in processing workflows
- minimization of broad data access for background jobs and analytics pipelines
- protection of temporary processing stores and intermediate outputs
- review of transformation workflows that combine or enrich sensitive data
- controls for test, staging, and development use of production-like data
- stronger handling for automated decision paths involving sensitive information

### Security intent

This domain reduces the chance that processing paths quietly weaken data protections established elsewhere.

---

## 6. Encryption, Keys, and Cryptographic Protection

Encryption is one part of data protection, but it is not a complete strategy on its own.

Its value depends on where it is applied, who can access keys, how key usage is governed, and whether encryption meaningfully changes the exposure risk.

### Required controls

- encryption at rest and in transit where required by sensitivity
- managed key services with clear ownership and lifecycle control
- separation of key access from routine platform or application access
- rotation and review expectations for key material where relevant
- stronger controls for highly sensitive encryption contexts
- review of where encryption does and does not mitigate operational risk

### Security intent

This domain strengthens confidentiality and reduces dependence on storage or transport protections alone.

---

## 7. Retention, Archival, and Deletion

Data protection must include decisions about how long data is kept, where it is archived, and how it is removed when no longer required.

Long retention increases operational and regulatory value in some cases, but it also increases exposure.

### Required controls

- defined retention requirements for sensitive data classes
- approved archival locations and controls
- restrictions on indefinite retention without justification
- secure deletion and disposal processes where feasible
- review of retained backups, archives, and historical extracts
- controls for legal hold or exception handling where required

### Security intent

This domain reduces avoidable long-term exposure and supports more deliberate lifecycle management of sensitive information.

---

## 8. Monitoring, Auditability, and Data Access Visibility

Sensitive data handling should be observable enough to support investigation, assurance, and abuse detection.

A secure data architecture should provide visibility into who accessed high-value data, how it was moved, when permissions changed, and whether handling patterns deviated from expectation.

### Required controls

- audit logging for sensitive data access
- monitoring of privileged or bulk data access
- logging of exports, transfers, and replication events
- visibility into permission and policy changes affecting data stores
- monitoring of unusual access patterns across high-value datasets
- forwarding of relevant events to central monitoring and detection workflows

### Security intent

This domain improves the ability to detect misuse, investigate incidents, and review whether data protection controls remain effective over time.

---

## Security Risks Addressed

This architecture is intended to reduce the likelihood or impact of the following risks:

- excessive access to sensitive or regulated data
- data exposure through storage misconfiguration or overlooked replicas
- insecure transfers of sensitive data
- unnecessary propagation of data into analytics, reporting, or test environments
- weak control of administrative access to data platforms
- ineffective use of encryption and key controls
- excessive retention of sensitive data
- poor visibility into data access and movement

---

## Minimum Telemetry Requirements

A data protection architecture should, at minimum, collect and retain:

- sensitive data access events
- privileged administrative access to data stores
- permission and policy changes affecting protected datasets
- export, replication, and transfer events
- key and secret access events affecting protected data
- backup, archival, and restore activity
- bulk query or extraction activity where relevant
- abnormal access patterns involving high-value datasets

This telemetry should support incident response, detection engineering, and governance review.

---

## Priority Detection Use Cases

Examples of high-value detections supported by this architecture include:

- unusual access to sensitive datasets
- privileged access to data stores outside expected patterns
- bulk export or extraction of protected data
- replication or transfer of sensitive data to unapproved locations
- unexpected use of high-risk keys or encryption contexts
- access to regulated data from unusual services or identities
- policy changes that weaken protection of critical datasets
- repeated access to archived or infrequently used sensitive data

---

## Cross-Cloud Control Mapping

The architecture is intentionally cloud-agnostic at the design level. Cloud services support implementation, but the main control concerns sit in classification, access design, storage protection, movement control, key governance, retention, and monitoring.

### Azure examples

- Data platforms: Azure SQL, Storage Accounts, Cosmos DB, Synapse, Data Lake services
- Access control: Microsoft Entra ID, RBAC, service identity patterns
- Encryption and keys: Azure Key Vault, platform encryption capabilities
- Monitoring: Azure Monitor, Log Analytics, Microsoft Sentinel
- Governance support: policy controls, data access auditing, storage security features

### AWS examples

- Data platforms: RDS, S3, DynamoDB, Redshift, analytics and data lake services
- Access control: IAM, IAM roles, service identity patterns
- Encryption and keys: AWS KMS, Secrets Manager, platform encryption capabilities
- Monitoring: CloudTrail, CloudWatch, GuardDuty, Security Hub, SIEM integrations
- Governance support: bucket policies, data access auditing, storage security features

---

## Design Decisions and Trade-offs

Every data protection architecture introduces trade-offs that should be managed deliberately.

### Broad availability vs Narrow access

Making data widely accessible improves usability and analytics value, but increases the number of paths through which sensitive data can be exposed.

### Shared storage efficiency vs Stronger separation

Shared data platforms improve operational efficiency, but can make access control, monitoring, and blast-radius reduction more difficult.

### Rich analytics vs Minimization discipline

More data improves insight and product value, but can weaken protection if sensitive fields are replicated into unnecessary pipelines and workspaces.

### Strong retention for business value vs Long-term exposure

Keeping data longer may support legal, operational, or analytical needs, but increases the impact of compromise and the burden of protection.

### Encryption coverage vs Operational complexity

Broader cryptographic control improves confidentiality, but key management, access review, and operational recovery become more complex.

---
