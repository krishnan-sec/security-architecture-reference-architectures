# PII Security Architecture

A security reference architecture for protecting personally identifiable information across collection, storage, processing, sharing, retention, and deletion workflows in cloud and SaaS environments.

---

## Overview

PII security focuses on protecting data that can identify, relate to, describe, or be linked to an individual.

While general data protection covers many forms of sensitive and business-critical information, PII requires additional attention because the risks are not limited to confidentiality loss. PII can also create privacy harm, identity linkage risk, regulatory exposure, operational misuse, and customer trust impact.

A strong PII security architecture should make it clear where PII enters the environment, how it is classified, who can access it, how it is used, whether it is being combined with other data in risky ways, how it is shared, and how it is removed when no longer needed.

---

## Security Objectives

This architecture is designed to:

- protect PII across collection, storage, processing, and sharing paths
- reduce unnecessary collection and unnecessary retention of PII
- limit who can access PII and under what conditions
- reduce the risk of linkage, overexposure, and misuse
- support safer handling of PII in product, support, analytics, and operational workflows
- improve visibility into where PII exists and how it moves
- support privacy-aware deletion, correction, and access workflows

---

## Architectural Position

A PII security architecture sits at the intersection of security, privacy, and data governance.

Where a broader data protection architecture focuses on sensitive data more generally, PII security focuses specifically on information about individuals and the risks created when that information is collected, combined, exposed, or retained longer than necessary.

Its purpose is to make handling of personal data deliberate, narrow, and observable.

---

## Core Security Domains

## 1. PII Identification and Classification

PII cannot be protected well if it is not identified clearly.

The architecture should make it possible to distinguish between direct identifiers, indirect identifiers, sensitive personal data, and data combinations that materially increase identification risk.

### Required controls

- clear identification of PII data types
- separation of direct identifiers, indirect identifiers, and sensitive personal data
- ownership for systems and datasets containing PII
- classification rules that reflect privacy and regulatory impact
- review of datasets that combine multiple identifying attributes
- visibility into where PII is collected, derived, or transformed

### Security intent

This domain ensures that personal data is treated according to its identification risk rather than handled as ordinary business data.

---

## 2. Collection Minimization and Purpose Control

PII collection should be deliberate and limited.

A system should collect only the personal data needed for a defined purpose, and that purpose should influence how the data is stored, used, shared, and retained.

### Required controls

- minimization of collected personal data fields
- clear mapping between collection purpose and processing use
- avoidance of unnecessary sensitive personal data collection
- review of product and workflow changes that expand PII collection
- restrictions on reuse of PII for unrelated purposes without review
- stronger justification for bulk or background collection of personal data

### Security intent

This domain reduces exposure by limiting the amount of personal data entering the environment in the first place.

---

## 3. Access Control for PII

Access to PII should be narrower than general system access.

The architecture should distinguish between users, support teams, analysts, administrators, and services that require different levels of access to personal data.

### Required controls

- role-based or attribute-based access for PII-bearing systems
- least-privilege access to personal data stores and views
- separation of support, analytics, operational, and administrative access paths
- stronger controls for high-risk or large-scale PII access
- controlled break-glass access with review and logging
- periodic review of access to systems containing sensitive personal data

### Security intent

This domain reduces unnecessary exposure of personal data to internal users, services, and workflows.

---

## 4. Storage, Segregation, and Protection of PII

PII should remain protected wherever it is stored, including primary systems, search layers, reporting stores, caches, archives, and backups.

Special attention should be given to places where PII is copied or duplicated beyond the primary business workflow.

### Required controls

- encryption at rest for PII-bearing stores
- restricted administrative access to PII repositories
- segregation of sensitive personal data where needed
- review of duplicated, indexed, cached, or exported PII
- secure backup and recovery protections
- stronger controls for repositories containing large volumes of personal data

### Security intent

This domain reduces the chance that personal data exposure occurs through overlooked or secondary storage paths.

---

## 5. Processing, Linking, and Derived Data Risk

PII risk often increases when personal data is transformed, enriched, matched, or combined with other datasets.

Even where individual datasets appear low-risk, combining them may create stronger identification power than intended.

### Required controls

- review of workflows that join or enrich personal data
- minimization of broad internal use of identifying fields
- controls for pseudonymized or tokenized processing where appropriate
- protection of temporary processing outputs and derived datasets
- review of analytics and reporting use cases involving linked personal data
- stronger controls for automated decisions or profiling-related workflows where relevant

### Security intent

This domain reduces identification risk created by internal data combination and derived processing.

---

## 6. Sharing, Export, and External Transfer of PII

PII becomes harder to control once it is exported, integrated, shared with third parties, or moved across trust boundaries.

For that reason, sharing and transfer paths should be narrow, approved, and observable.

### Required controls

- approved and documented sharing paths for PII
- encryption in transit for transfers involving personal data
- minimization of fields shared with third parties and internal consumers
- review of bulk export workflows
- restrictions on ad hoc extraction of personal data
- logging of high-risk sharing and transfer events

### Security intent

This domain reduces uncontrolled distribution of PII beyond its intended use and accountability boundary.

---

## 7. Retention, Deletion, and Subject Rights Support

PII should not be kept longer than necessary without a defined reason.

A strong architecture should also support the ability to find, correct, export, or delete personal data where legal, operational, or customer obligations require it.

### Required controls

- defined retention requirements for PII categories
- secure deletion processes where feasible
- review of retained archives, backups, and historical extracts containing PII
- ability to locate PII across major systems and stores
- support for correction, access, export, or deletion workflows where required
- exception handling for legal hold or mandatory retention scenarios

### Security intent

This domain reduces long-term privacy exposure and supports more controlled lifecycle management for personal data.

---

## 8. Monitoring, Auditability, and PII Access Visibility

A secure PII architecture should make it possible to understand who accessed personal data, which systems moved it, when permissions changed, and whether unusual patterns of use occurred.

### Required controls

- audit logging for access to PII-bearing systems
- monitoring of privileged and bulk access to personal data
- logging of exports, transfers, and sensitive administrative actions
- visibility into permission changes affecting PII repositories
- monitoring of unusual access to large volumes of personal data
- forwarding of relevant events to central monitoring and detection workflows

### Security intent

This domain improves detection, investigation, and assurance for personal data handling.

---

## Security Risks Addressed

This architecture is intended to reduce the likelihood or impact of the following risks:

- unnecessary collection of personal data
- excessive internal access to PII
- personal data exposure through duplicated or secondary storage
- increased identification risk through data linking and enrichment
- uncontrolled transfer or export of personal data
- excessive retention of PII
- weak support for deletion or correction workflows
- poor visibility into personal data access and movement

---

## Minimum Telemetry Requirements

A PII security architecture should, at minimum, collect and retain:

- access events for systems containing PII
- privileged and bulk query activity involving personal data
- permission and policy changes affecting PII-bearing stores
- export, transfer, and sharing events for PII
- deletion, correction, and subject-rights workflow events where relevant
- backup, archival, and restore activity involving PII repositories
- administrative actions affecting privacy-sensitive configurations
- abnormal access patterns involving large or sensitive personal data sets

This telemetry should support both incident investigation and privacy-aware governance review.

---

## Priority Detection Use Cases

Examples of high-value detections supported by this architecture include:

- unusual access to large volumes of PII
- privileged access to sensitive personal data outside expected patterns
- extraction or export of personal data to unapproved destinations
- repeated access to personal data by users or services without clear need
- creation of new copies, reports, or indexes containing PII
- policy changes that weaken protection of personal data stores
- abnormal activity involving deletion or correction workflows
- unusual access to infrequently used or archived PII datasets

---

## Cross-Cloud Control Mapping

The architecture is intentionally cloud-agnostic at the design level. Cloud services support implementation, but the main control concerns sit in identification of PII, minimization, access control, storage protection, controlled sharing, retention, and auditability.

### Azure examples

- Data platforms: Azure SQL, Storage Accounts, Cosmos DB, data lake and analytics services
- Access control: Microsoft Entra ID, RBAC, service identity patterns
- Encryption and keys: Azure Key Vault, platform encryption capabilities
- Monitoring: Azure Monitor, Log Analytics, Microsoft Sentinel
- Governance support: policy controls, audit logging, storage security features

### AWS examples

- Data platforms: RDS, S3, DynamoDB, analytics and data lake services
- Access control: IAM, IAM roles, service identity patterns
- Encryption and keys: AWS KMS, Secrets Manager, platform encryption capabilities
- Monitoring: CloudTrail, CloudWatch, GuardDuty, Security Hub, SIEM integrations
- Governance support: policy controls, audit logging, storage security features

---

## Design Decisions and Trade-offs

Every PII security architecture introduces trade-offs that should be managed deliberately.

### Product utility vs Minimization

Collecting and storing more personal data may improve product features or analytics, but it increases privacy exposure and security burden.

### Broad operational visibility vs Privacy restriction

Support and operational teams may want richer access to customer records, but wider visibility into personal data creates unnecessary internal exposure.

### Rich analytics vs Linkage risk

Combining datasets improves insight, but can create much stronger identification risk than intended.

### Long retention vs Long-term exposure

Keeping personal data longer may help operations or compliance in some cases, but it also increases the harm caused by compromise or misuse.

### Flexible sharing vs Loss of control

External integrations and exports may be operationally useful, but personal data becomes harder to govern once it leaves the primary control boundary.

---
