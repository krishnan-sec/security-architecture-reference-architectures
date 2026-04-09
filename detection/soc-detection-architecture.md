# SOC Detection Architecture

A security reference architecture for designing, operating, and improving detection capabilities within a Security Operations Center, with a focus on telemetry quality, detection logic, triage workflows, investigation support, and response integration.

---

## Overview

A SOC detection architecture defines how security-relevant signals are collected, analyzed, prioritized, and acted on across the environment.

The main challenge is not only collecting large volumes of logs. It is turning relevant telemetry into reliable detections that help analysts identify malicious activity, investigate efficiently, and respond before impact grows.

A strong detection architecture should make it clear which telemetry matters most, how detections are engineered, how alerts are enriched and triaged, how investigation workflows are supported, and how detection coverage improves over time.

---

## Security Objectives

This architecture is designed to:

- turn security telemetry into actionable detections
- improve visibility across identity, endpoint, network, cloud, application, and data activity
- reduce false negatives for high-risk attack behaviors
- reduce analyst overload from low-value or noisy alerts
- support consistent triage and investigation workflows
- improve linkage between detections, context, and response actions
- provide a repeatable model for detection coverage improvement

---

## Architectural Position

A SOC detection architecture sits at the security monitoring and operational analysis layer.

Where other architectures define preventive controls, trust models, application boundaries, and data protections, the SOC detection architecture focuses on what happens after telemetry is generated: how signals are collected, interpreted, correlated, prioritized, and used in real investigations.

Its purpose is to make monitoring operationally useful rather than log-heavy and analyst-light.

---

## Core Security Domains

## 1. Telemetry Source Coverage

Detection quality depends on telemetry quality.

A SOC should know which core control planes and business systems produce the signals needed for meaningful detection. It should also understand where visibility gaps exist and which sources are high-value enough to prioritize.

### Required controls

- inventory of major telemetry-producing systems
- coverage across identity, endpoint, network, cloud, application, and data layers
- prioritization of high-value log sources and event categories
- onboarding standards for new telemetry sources
- review of missing, degraded, or low-integrity telemetry
- ownership for key detection-supporting data sources

### Security intent

This domain ensures that detection engineering is built on deliberate visibility rather than passive accumulation of logs.

---

## 2. Normalization, Parsing, and Data Quality

Telemetry has limited value if it arrives in inconsistent, incomplete, or poorly structured forms.

A detection architecture should define how log data is parsed, normalized, mapped, and quality-checked so that detections can rely on consistent fields and context.

### Required controls

- consistent parsing and field extraction
- normalization of common entities such as user, host, IP, workload, and resource
- timestamp quality and event ordering considerations
- handling for missing or malformed data
- validation of critical fields used in detections
- monitoring for broken connectors, parser drift, or schema change impact

### Security intent

This domain reduces fragile detection logic and improves confidence that alerts are based on trustworthy telemetry.

---

## 3. Detection Logic and Analytic Content

Detection logic is the core of the SOC monitoring model.

Detections should be designed around attacker behaviors, risky control failures, and high-value misuse patterns rather than just raw event counts or generic anomaly labels.

### Required controls

- defined process for creating and tuning detections
- alignment of detections to threat scenarios, attack techniques, or abuse cases
- distinction between low-context alerts and higher-confidence detections
- version control and change management for analytic content
- review of dependencies, assumptions, and suppression logic
- retirement or refactoring of low-value detections over time

### Security intent

This domain helps the SOC move from passive event collection to deliberate detection engineering.

---

## 4. Context Enrichment and Alert Fidelity

Raw alerts are often not enough for effective triage.

A good detection architecture enriches alerts with enough context to help analysts understand why the detection fired, what asset or identity is involved, what the likely impact is, and how urgent the issue may be.

### Required controls

- enrichment of alerts with asset, identity, ownership, and sensitivity context
- linkage to host, user, workload, or tenant information where relevant
- severity and confidence models grounded in context rather than volume alone
- correlation of related events into more coherent findings where appropriate
- visibility into detection rationale and triggering conditions
- support for analyst understanding of alert provenance

### Security intent

This domain improves alert quality and reduces unnecessary triage effort.

---

## 5. Triage and Investigation Workflow Support

Detections should fit into a repeatable analyst workflow.

The SOC needs a structured way to receive, prioritize, investigate, escalate, and close alerts without losing context or creating avoidable inconsistency.

### Required controls

- alert routing and prioritization logic
- clear distinction between informational alerts and analyst-actionable detections
- investigation views that preserve supporting event context
- standard triage criteria for severity, urgency, and impact
- linkage between alerts, cases, and follow-on investigative actions
- documentation of analyst workflow expectations for major detection classes

### Security intent

This domain helps turn detections into operationally manageable investigations rather than disconnected alert streams.

---

## 6. Detection Tuning and Noise Reduction

A detection architecture should expect tuning to be continuous.

No useful detection set stays accurate forever. Environments change, attackers adapt, benign workflows evolve, and telemetry quality shifts over time.

### Required controls

- regular review of false positives and false negatives
- suppression and filtering logic with governance
- tuning feedback from analysts and incident responders
- review of environment-specific benign behaviors affecting detections
- performance and cost awareness for high-volume detections
- measurable criteria for retaining, modifying, or removing detections

### Security intent

This domain keeps the SOC usable and prevents alert fatigue from degrading real detection value.

---

## 7. Response Integration and Escalation Paths

Detection is only useful if it supports action.

A SOC detection architecture should define how alerts connect to containment, response, engineering escalation, and incident handling workflows.

### Required controls

- defined escalation paths for high-confidence detections
- integration with case management and incident workflows
- support for containment or response actions where appropriate
- clear ownership for actioning different alert types
- preservation of investigation evidence and timelines
- feedback loop from response activity into detection improvement

### Security intent

This domain makes detection part of security operations rather than a separate reporting function.

---

## 8. Detection Coverage Review and Improvement

Detection capability should be reviewed as a coverage problem, not just an alert volume problem.

A mature SOC should know which attack paths, control failures, and business-critical abuse cases are covered well, covered weakly, or not covered at all.

### Required controls

- mapping of detections to threat scenarios or attack techniques
- review of coverage across high-value assets and workflows
- periodic gap analysis for missing detections
- prioritization model for new detection development
- visibility into stale or unmaintained detections
- measurement of operational usefulness, not only alert count

### Security intent

This domain supports continuous improvement and helps ensure that monitoring effort is aligned to real risk.

---

## Security Risks Addressed

This architecture is intended to reduce the likelihood or impact of the following risks:

- high-risk attacker activity going undetected
- poor telemetry quality weakening detection reliability
- analyst overload from noisy or low-context alerts
- weak triage consistency across investigations
- slow escalation of meaningful security events
- detection blind spots around high-value systems or behaviors
- stale detection logic that no longer reflects the environment
- weak linkage between monitoring and response actions

---

## Minimum Telemetry Requirements

A SOC detection architecture should, at minimum, collect and retain:

- identity and authentication telemetry
- endpoint security events
- cloud control-plane and administrative events
- network and ingress visibility relevant to threat monitoring
- application and API security-relevant events
- privileged access activity
- data-access and data-movement events for high-value systems
- case, alert, and investigation metadata needed for operations review

This telemetry should support both real-time monitoring and retrospective investigation.

---

## Priority Detection Use Cases

Examples of high-value detections supported by this architecture include:

- suspicious privileged access activity
- credential misuse and anomalous authentication behavior
- unauthorized persistence or privilege escalation activity
- unusual administrative actions in cloud or platform control planes
- abnormal access to sensitive applications or datasets
- suspicious internal movement between workloads or services
- data export or exfiltration patterns involving high-value assets
- defense evasion activity such as disabling logging or security tooling

---

## Cross-Cloud Control Mapping

The architecture is intentionally platform-agnostic at the design level. Cloud services support implementation, but the main control concerns sit in telemetry coverage, detection engineering, triage, enrichment, and response workflows.

### Azure examples

- Monitoring and analytics: Microsoft Sentinel, Log Analytics, Azure Monitor
- Cloud telemetry: Azure Activity Logs, resource diagnostics, identity events
- Endpoint and workload context: Microsoft Defender integrations
- Investigation support: incident workflows, hunting queries, workbook-style enrichment
- Platform coverage: Entra events, cloud control-plane telemetry, application and data source integrations

### AWS examples

- Monitoring and analytics: CloudWatch, SIEM integrations, Security Hub
- Cloud telemetry: CloudTrail, service logs, VPC Flow Logs
- Threat and finding support: GuardDuty and related service findings
- Investigation support: centralized case and enrichment workflows through integrated tools
- Platform coverage: IAM events, control-plane telemetry, workload and data source integrations

---

## Design Decisions and Trade-offs

Every SOC detection architecture introduces trade-offs that should be managed deliberately.

### Broad log collection vs Operational usefulness

Collecting more data improves possible visibility, but not all data improves detection quality. Unfocused collection can increase cost and analyst burden without improving outcomes.

### High sensitivity vs Alert fatigue

Aggressive detection logic may improve early visibility, but can overwhelm analysts if context and tuning are weak.

### Correlation depth vs Complexity

More enrichment and correlation can improve fidelity, but it also increases engineering effort, processing complexity, and dependency on high-quality data.

### Fast alerting vs Investigative completeness

Early alerts improve response speed, but some detections require additional context before they become meaningfully actionable.

### Standardized detections vs Environment-specific tuning

Reusable detections improve consistency, but local business workflows, infrastructure patterns, and telemetry differences often require adaptation.

---
