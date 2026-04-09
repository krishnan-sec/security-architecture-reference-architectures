# Zero Trust Architecture

A cross-cloud security reference architecture for reducing implicit trust and making access decisions based on verified identity, device posture, session context, policy, and resource sensitivity.

---

## Overview

Zero Trust is an access and trust model, not a cloud foundation model.

Where a landing zone defines the baseline environment that workloads inherit, Zero Trust defines how users, devices, workloads, and services are verified before they are allowed to access applications, APIs, data, and management interfaces.

Its purpose is to reduce implicit trust and make access decisions based on identity, context, policy, and resource sensitivity.

---

## Security Objectives

This architecture is designed to:

- remove implicit trust from access decisions
- make identity the primary trust signal
- apply least-privilege access more consistently
- reduce lateral movement opportunities
- narrow access to specific resources and actions
- strengthen trust decisions for users, devices, and workloads
- improve visibility into authentication, authorization, and policy outcomes

---

## What Zero Trust Changes

Traditional models often assume that trust is inherited from network position, internal connectivity, or prior access.

Zero Trust changes that model by requiring verification at the point of access.

Instead of asking whether something is inside a trusted environment, Zero Trust asks:

- who is requesting access
- from what device or workload
- under what conditions
- to which exact resource
- for which exact action
- under which policy requirements

This changes trust from a broad environmental assumption into a narrower and more deliberate access decision.

---

## Core Security Domains

## 1. Identity as the Primary Trust Signal

In a Zero Trust model, identity is the starting point for access control.

Access should be based on verified identity, strong authentication, clear entitlement models, and the sensitivity of the requested action.

### Required controls

- centralized identity provider integration
- strong authentication for users and administrators
- MFA for privileged and sensitive access paths
- role-based or attribute-based authorization
- separation of human identities and workload identities
- entitlement review for privileged or high-impact access
- controlled lifecycle management for accounts and roles

### Security intent

This domain reduces dependence on location-based trust and makes access decisions more explicit and auditable.

---

## 2. Device and Session Context

Identity alone is not always enough.

Access decisions should also consider the condition of the device, the session context, and any signals that indicate elevated risk.

### Required controls

- device trust or compliance signals where applicable
- restrictions for unmanaged or unknown devices
- session-aware access controls for sensitive resources
- stronger access requirements for high-risk transactions
- evaluation of contextual signals such as location, behavior, or risk level
- revalidation for sensitive sessions where needed

### Security intent

This domain helps prevent valid credentials from being enough on their own to gain high-trust access from compromised or untrusted endpoints.

---

## 3. Resource-Level Authorization

Zero Trust narrows access to the specific resource being requested.

Users and services should not receive broad access because they are already connected to a trusted environment. Access should be evaluated per application, API, dataset, management interface, or service function.

### Required controls

- per-resource authentication and authorization
- application-aware access enforcement
- policy decisions that consider identity, context, and resource sensitivity
- reduced use of broad shared access paths
- stronger controls for administrative and high-value resources
- explicit approval paths for highly sensitive operations where required

### Security intent

This domain limits access scope and reduces the risk that broad environmental trust leads to unnecessary reach.

---

## 4. Least-Privilege by Action and Scope

Least privilege in a Zero Trust architecture should apply not only to roles, but also to actions, sessions, and workflows.

This means access should be limited to the minimum set of permissions needed for a defined purpose, and only for as long as that access is required.

### Required controls

- narrow authorization scopes
- time-bound privileged access where practical
- approval-based elevation for sensitive operations
- reduced standing privilege for administrators
- separation of read, write, approve, and administer functions
- removal of unused or excessive entitlements

### Security intent

This domain reduces the impact of compromised identities and improves control over privileged actions.

---

## 5. Workload-to-Workload Trust

Zero Trust should apply to services and workloads as well as human users.

Internal service communication should not rely on the assumption that traffic is trustworthy because it originates from inside the environment.

### Required controls

- unique identities for workloads and services
- authenticated service-to-service communication
- authorization controls between internal services
- reduction of shared static secrets where possible
- short-lived credentials or token-based trust models where practical
- explicit control of access to internal APIs, queues, and data services

### Security intent

This domain reduces over-trust in east-west communication and gives better control over internal service relationships.

---

## 6. Access to Sensitive Data and High-Value Resources

Not all resources should be treated equally.

Access to management interfaces, sensitive applications, high-value APIs, and regulated data should require stronger trust decisions than access to lower-risk resources.

### Required controls

- classification-aware access rules
- stronger authentication for high-sensitivity resources
- tighter authorization for administrative or data-sensitive actions
- access logging for critical resources
- monitored use of privileged data access paths
- additional approval or step-up controls where needed

### Security intent

This domain ensures that trust decisions reflect the sensitivity of the target resource, not only the identity of the requester.

---

## 7. Continuous Verification and Monitoring

Trust should not be treated as a permanent state.

Zero Trust depends on the ability to observe authentication events, policy decisions, entitlement changes, privileged access, and abnormal access behavior over time.

### Required controls

- authentication and sign-in logging
- policy evaluation logging
- access denial and anomaly tracking
- privileged access monitoring
- service identity usage monitoring
- integration with central detection and response workflows
- review of policy exceptions and high-risk access paths

### Security intent

This domain supports verification, detection, and ongoing refinement of trust decisions.

---

## Security Risks Addressed

This architecture is intended to reduce the likelihood or impact of the following risks:

- credential theft leading to broad access
- access based on assumed internal trust
- unmanaged or high-risk device access to sensitive services
- over-privileged users or service identities
- weak control of internal service communication
- broad access to high-value applications or data
- poor visibility into access decisions and policy failures

---

## Minimum Telemetry Requirements

A Zero Trust architecture should, at minimum, collect and retain:

- sign-in and authentication events
- MFA success and failure events
- conditional or contextual access decisions
- privileged role activation and elevation events
- application and API access logs
- access denials and policy violations
- service identity usage events where available
- administrative changes to access policy or entitlements

This telemetry should support both investigation and detection engineering.

---

## Priority Detection Use Cases

Examples of high-value detections supported by this architecture include:

- impossible travel or anomalous sign-in patterns
- repeated failed MFA or authentication bypass attempts
- privileged access from unusual contexts
- access to sensitive resources from unmanaged endpoints
- service identities accessing resources outside normal scope
- repeated access denials against protected resources
- sudden changes in access policy or entitlement assignment
- suspicious use of elevated privileges

---

## Cross-Cloud Control Mapping

The architecture is intentionally cloud-agnostic at the design level, with provider mappings used for implementation.

### Azure examples

- Identity: Microsoft Entra ID
- Access policy: Conditional Access
- Privileged access: Entra PIM
- Device posture: Intune and device compliance signals
- Workload identity: managed identities
- Monitoring: Microsoft Sentinel, Defender for Cloud

### AWS examples

- Identity: IAM, IAM Identity Center
- Access policy: IAM policies, federation controls, session conditions
- Privileged access: controlled role assumption patterns
- Device and endpoint context: integrated endpoint and access tooling depending on operating model
- Workload identity: IAM roles and service-linked identities
- Monitoring: CloudTrail, GuardDuty, Security Hub, SIEM integrations

---

## Design Decisions and Trade-offs

Every Zero Trust implementation introduces design trade-offs that need to be managed deliberately.

### Strong verification vs User friction

More verification improves access assurance, but can create unnecessary friction if controls are not aligned to resource sensitivity and business workflow.

### Fine-grained policy vs Administrative overhead

More precise authorization reduces broad access, but increases the effort needed to design, maintain, and review policy.

### Frequent revalidation vs Usability

Continuous or session-based trust checks improve responsiveness to risk, but may affect user experience and application behavior.

### Tighter service trust vs Engineering complexity

Explicit workload authentication improves internal security, but often requires application and platform changes.

### Shared policy model vs Platform-specific implementation

A common Zero Trust model across Azure and AWS improves consistency, but the actual enforcement mechanisms will differ.

---

