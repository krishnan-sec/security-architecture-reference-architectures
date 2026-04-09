# Zero Trust Architecture

A cross-cloud security reference architecture for enforcing explicit verification, least-privilege access, and controlled trust relationships across users, devices, workloads, and data in Azure and AWS environments.

---

## Overview

Zero Trust is an architectural model based on the principle that access should not be granted because something is already inside a network boundary or connected to a trusted environment.

Access decisions should be based on verified identity, device posture, session context, resource sensitivity, and policy. Trust should be limited, continuously evaluated, and narrowed to the specific action being requested.

In practice, Zero Trust is not a single product or control. It is a way of designing access, segmentation, workload communication, and monitoring so that implicit trust is reduced across the environment.

---

## Security Objectives

This architecture is designed to:

- remove implicit trust from access decisions
- enforce least-privilege access across users, devices, and workloads
- validate identity and context before granting access
- reduce lateral movement opportunities
- improve control over service-to-service and user-to-service communication
- strengthen visibility into authentication, access, and policy enforcement events
- provide a consistent Zero Trust model across Azure and AWS

---

## Architectural Position

Zero Trust sits across multiple architecture layers rather than in a single control point.

It influences how identity is validated, how devices are evaluated, how users reach applications, how services communicate with each other, how sensitive resources are segmented, and how access decisions are monitored over time.

This means Zero Trust is best treated as a cross-cutting security architecture rather than a standalone network model.

---

## Core Security Domains

## 1. Identity-Centric Access Control

Identity is the primary decision point in a Zero Trust model.

Access should be granted based on strong identity assurance, verified authentication, role or attribute-based authorization, and the sensitivity of the requested action or resource.

### Required controls

- centralized identity provider integration
- strong authentication for workforce, administrators, and privileged users
- MFA for elevated and sensitive access paths
- role-based or attribute-based authorization models
- separation of human and workload identities
- strong lifecycle management for accounts, roles, and entitlements
- explicit review of high-risk and privileged access

### Security intent

This control domain reduces reliance on network location as proof of trust and makes access decisions more directly tied to identity assurance and authorization policy.

---

## 2. Device and Session Trust

User identity alone is not always enough to make safe access decisions.

Access should consider the condition of the device, the session context, and whether the request aligns with expected security posture.

### Required controls

- device registration or managed device posture where applicable
- evaluation of compliance, health, or risk state
- session-based policy enforcement for high-risk actions
- restrictions for unmanaged or unknown devices
- stronger verification for administrative or high-impact actions
- session monitoring and re-evaluation for sensitive access paths

### Security intent

This control domain reduces the chance that valid credentials alone are enough to gain high-trust access from compromised, untrusted, or unmanaged endpoints.

---

## 3. Resource-Level Access Decisions

In a Zero Trust architecture, access is evaluated at the resource or application layer rather than assumed by network placement.

Users and services should be granted access only to the specific applications, APIs, or datasets required for their role or transaction.

### Required controls

- application-aware access enforcement
- per-resource authentication and authorization
- policy decisions based on user, device, session, and resource sensitivity
- explicit approval paths for highly sensitive resources
- strong access controls for administrative interfaces and management planes
- removal of broad internal network trust assumptions

### Security intent

This control domain narrows access scope and prevents users or workloads from inheriting unnecessary access because of shared network location.

---

## 4. Network Segmentation and Traffic Control

Zero Trust does not eliminate network security. It changes the role of the network.

Instead of using network presence as the main trust signal, the network should be used to reduce exposure, enforce segmentation, and contain lateral movement.

### Required controls

- segmentation between users, applications, services, and data tiers
- controlled ingress and egress paths
- reduction of flat internal network models
- private connectivity for sensitive services where appropriate
- application-specific access paths rather than broad internal reachability
- inspection and enforcement points for high-value trust boundaries

### Security intent

This control domain limits movement across the environment and makes network pathways more deliberate and easier to monitor.

---

## 5. Workload and Service-to-Service Trust

Zero Trust must also apply to workload identities and service interactions.

Applications, containers, functions, and platform services should authenticate explicitly to one another rather than relying on network trust alone.

### Required controls

- unique identities for workloads and services
- authenticated service-to-service communication
- short-lived credentials or token-based access where practical
- secret reduction through managed identity patterns
- authorization controls between internal services
- segmentation of sensitive backend services and data paths

### Security intent

This control domain reduces the risk of over-trusted east-west communication and improves control over internal service relationships.

---

## 6. Data-Centric Protection

Access decisions should reflect the sensitivity of the data being accessed, not only the identity of the caller.

Higher-risk data requires stronger authentication, tighter authorization, clearer monitoring, and more deliberate access paths.

### Required controls

- classification-aware access design
- encryption at rest and in transit
- tighter access controls for sensitive datasets
- monitored administrative access to data services
- approval or step-up controls for sensitive operations where needed
- access logging for high-value data resources

### Security intent

This control domain makes resource sensitivity part of the trust decision and reduces the risk of broad access to critical data stores.

---

## 7. Continuous Monitoring and Policy Enforcement

Zero Trust depends on visibility.

Authentication, authorization, policy decisions, privilege use, and trust-boundary crossings should all produce telemetry that supports both detection and review.

### Required controls

- sign-in and authentication logging
- policy decision logging
- privileged access monitoring
- access denials and anomalous behavior tracking
- session and token-related telemetry where relevant
- integration with central monitoring, detection, and response workflows

### Security intent

This control domain supports verification, investigation, and continuous improvement of access controls over time.

---

## Security Risks Addressed

This architecture is intended to reduce the likelihood or impact of the following risks:

- credential theft leading to broad internal access
- excessive trust based on network location
- lateral movement across shared environments
- unmanaged device access to sensitive applications
- weak service-to-service trust controls
- over-privileged access to management planes or sensitive data
- lack of visibility into access decisions and policy failures

---

## Minimum Telemetry Requirements

A Zero Trust architecture should, at minimum, collect and retain:

- sign-in events and authentication logs
- MFA events and failures
- conditional or contextual access decisions
- privileged role activation and administrative actions
- application access logs
- device compliance or trust-state signals where used
- service identity and token-related events where available
- access denials, anomalous session activity, and policy violations

This telemetry should support both investigation and detection engineering.

---

## Priority Detection Use Cases

Examples of high-value detections supported by this architecture include:

- impossible travel or anomalous login patterns
- repeated failed MFA or authentication bypass attempts
- privileged access from unusual devices or contexts
- access to sensitive applications from unmanaged endpoints
- service identities accessing resources outside expected scope
- abnormal east-west traffic between segmented workloads
- sudden changes in access policy or entitlement assignment
- repeated access denials against sensitive resources

---

## Cross-Cloud Control Mapping

The architecture is intentionally cloud-agnostic at the design level, with provider mappings used for implementation.

### Azure examples

- Identity: Microsoft Entra ID
- Access policy: Conditional Access
- Privileged access: Entra PIM
- Device posture: Intune and device compliance signals
- Application proxy and access patterns: Entra Application Proxy, private access patterns
- Workload identity: managed identities
- Monitoring: Microsoft Sentinel, Defender for Cloud

### AWS examples

- Identity: IAM, IAM Identity Center
- Access policy: IAM policies, session controls, federation controls
- Privileged access: role assumption and controlled elevation patterns
- Device and endpoint context: integrated endpoint and access tooling depending on operating model
- Workload identity: IAM roles and service-linked identities
- Monitoring: CloudTrail, GuardDuty, Security Hub, SIEM integrations

---

## Design Decisions and Trade-offs

Every Zero Trust implementation introduces design trade-offs that should be managed deliberately.

### Strong verification vs User friction

More authentication checks and contextual controls improve trust decisions, but can create friction if applied without regard to business workflow and resource sensitivity.

### Fine-grained access control vs Operational complexity

More precise authorization reduces unnecessary access, but increases the effort needed to design, maintain, and review policy.

### Session control vs Performance and Usability

Continuous session evaluation improves responsiveness to risk, but may affect user experience or application behavior in some cases.

### Broad segmentation vs Application dependency challenges

Reducing implicit connectivity improves containment, but can expose hidden application dependencies that require redesign.

### Cross-cloud consistency vs Platform-specific capability depth

A shared model across Azure and AWS improves governance and portability, but implementation details may differ significantly by platform.

---


