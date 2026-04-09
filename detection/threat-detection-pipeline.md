# Threat Detection Pipeline

A security reference architecture for designing and operating the pipeline that turns raw security telemetry into prioritized findings through ingestion, normalization, enrichment, analytics, and feedback-driven improvement.

---

## Overview

A threat detection pipeline is the technical path through which security telemetry becomes a usable detection outcome.

The main challenge is not only collecting logs or writing detection rules. It is ensuring that events arrive reliably, are parsed consistently, are enriched with enough context to support analysis, and are evaluated in a way that produces useful findings rather than fragmented signal noise.

A strong detection pipeline should make it clear how telemetry enters the platform, how data quality is preserved, how analytics depend on normalized fields and context, how alerts are produced, and how the pipeline improves when detections perform poorly or telemetry changes.

---

## Security Objectives

This architecture is designed to:

- move security telemetry from source systems into usable analytic workflows
- improve consistency and reliability of parsed and normalized security data
- support enrichment of raw events with context needed for detection
- produce findings that are more meaningful than isolated raw events
- reduce pipeline breakage caused by connector drift, schema change, or incomplete data
- support repeatable engineering workflows for analytic content
- improve detection quality through feedback and pipeline-aware tuning

---

## Architectural Position

A threat detection pipeline sits between telemetry-producing systems and operational detection outcomes.

Where a SOC detection architecture focuses on analyst workflows, triage, and response integration, the threat detection pipeline focuses on the technical processing path that makes those workflows possible in the first place.

Its purpose is to make detection technically reliable, context-aware, and maintainable over time.

---

## Core Security Domains

## 1. Telemetry Ingestion

The pipeline begins with how data enters the detection platform.

Telemetry should be onboarded in a controlled way so that important sources arrive reliably, required fields are present, and ingestion failures are visible before they silently weaken detection coverage.

### Required controls

- defined onboarding process for new telemetry sources
- prioritization of high-value and security-relevant event streams
- ingestion health monitoring for connectors and collection paths
- handling for delayed, dropped, duplicated, or partial telemetry
- ownership for ingestion of major source classes
- review of ingestion dependencies for cloud, endpoint, identity, network, application, and data telemetry

### Security intent

This domain reduces silent visibility loss and ensures the pipeline starts with reliable source intake.

---

## 2. Parsing and Field Extraction

Raw telemetry has limited detection value until it is parsed into usable structures.

Parsing should be treated as a critical part of the detection pipeline because poor extraction, broken mappings, or inconsistent field names directly weaken downstream analytics.

### Required controls

- structured parsing of source-specific events
- extraction of core fields such as actor, target, action, timestamp, source, and outcome
- handling for malformed or partially structured events
- validation of fields required by analytic content
- monitoring for parser errors and schema mismatches
- version-aware handling for changing source formats where relevant

### Security intent

This domain improves the usability of telemetry and reduces fragile detection logic built on unreliable field extraction.

---

## 3. Normalization and Common Data Modeling

Different telemetry sources describe similar actions in different ways.

A detection pipeline should map important entities and actions into a more consistent structure so that analytics can work across sources without excessive source-specific logic.

### Required controls

- normalization of identities, hosts, workloads, resources, IPs, and event outcomes
- common representation of core security events where possible
- mapping of source-specific fields into analytic-friendly structures
- handling of ambiguity where sources cannot be normalized cleanly
- governance for schema changes affecting common models
- review of normalization gaps that weaken cross-source analytics

### Security intent

This domain improves portability, reuse, and consistency of detection logic across different telemetry sources.

---

## 4. Context Enrichment

Raw events often need additional context before they support meaningful detection.

Enrichment adds information such as asset criticality, identity ownership, tenant association, workload type, sensitivity level, environment, or known trust boundary relevance.

### Required controls

- enrichment with asset, identity, ownership, and environment context
- linkage to tenant, business function, or sensitivity context where relevant
- controlled use of external or internal reference data in enrichment workflows
- validation of enrichment dependencies and update cycles
- handling for missing or stale enrichment values
- review of which detections depend on enrichment to remain accurate

### Security intent

This domain improves alert fidelity and reduces the chance that raw events are evaluated without enough business or technical context.

---

## 5. Analytic Evaluation and Detection Execution

Detection logic is applied only after the data is ingested, parsed, normalized, and enriched sufficiently.

Analytics should be designed around attack behavior, misuse patterns, and control failure signals rather than just event frequency or broad anomaly labels.

### Required controls

- defined execution path for analytic rules, correlations, and detection logic
- support for threshold, sequence, behavior, and context-based detection models
- governance for rule changes and content deployment
- visibility into rule dependencies and execution assumptions
- support for testing and validation of detections before broad rollout
- review of analytic content that depends heavily on unstable data inputs

### Security intent

This domain turns processed telemetry into deliberate detection outcomes rather than passive event accumulation.

---

## 6. Finding Generation and Prioritization

The pipeline should not stop at “rule matched.”

Detection outputs should be shaped into findings that are easier to understand, rank, and investigate, especially where multiple signals or contextual indicators point to the same issue.

### Required controls

- structured generation of alerts, findings, or correlated observations
- grouping of related signals where useful
- clear distinction between low-confidence alerts and higher-confidence findings
- severity and priority shaping based on context and impact
- preservation of source evidence and analytic rationale
- routing outputs into operational workflows in a consistent format

### Security intent

This domain improves downstream usability and reduces fragmented alert handling.

---

## 7. Pipeline Reliability and Change Management

Detection pipelines break when telemetry changes, connectors fail, parsers drift, or enrichment dependencies become stale.

A strong architecture should treat reliability and change control as core pipeline concerns rather than afterthoughts.

### Required controls

- monitoring of connector health and pipeline stages
- validation of schema changes and parser updates
- deployment discipline for pipeline logic and analytic content
- rollback and recovery options for failed changes
- alerting for broken or degraded pipeline components
- ownership for pipeline engineering and maintenance responsibilities

### Security intent

This domain reduces silent detection degradation and improves trust in pipeline outputs.

---

## 8. Feedback, Tuning, and Continuous Improvement

A threat detection pipeline should improve as analysts, responders, and engineers learn from its outputs.

Feedback should not be limited to rule tuning alone. It should also inform parsing, normalization, enrichment, and source onboarding decisions.

### Required controls

- feedback loop from analysts and responders into pipeline engineering
- review of false positives, false negatives, and missed context
- tuning of analytic thresholds and grouping logic
- correction of parsing and normalization weaknesses discovered during investigations
- prioritization of new pipeline capabilities based on operational detection gaps
- retirement of low-value or brittle pipeline components over time

### Security intent

This domain keeps the pipeline aligned to real operating conditions rather than treating it as a static technical stack.

---

## Security Risks Addressed

This architecture is intended to reduce the likelihood or impact of the following risks:

- high-value telemetry never reaching the detection platform
- broken parsing or normalization weakening analytic accuracy
- detections failing because required context is missing or stale
- fragmented alert output that is difficult to triage
- silent pipeline degradation caused by connector drift or schema change
- brittle analytic logic built on unstable telemetry assumptions
- poor reuse of detections across source systems
- lack of feedback-driven improvement in detection engineering

---

## Minimum Telemetry Requirements

A threat detection pipeline should, at minimum, support ingestion and processing of:

- identity and authentication telemetry
- endpoint and workload security events
- cloud control-plane and administrative events
- network and ingress telemetry relevant to threat monitoring
- application and API security-relevant events
- privileged access and policy-change events
- data-access and data-movement events for high-value systems
- pipeline health, parser quality, and analytic execution metadata

This telemetry should support both technical pipeline monitoring and operational detection use.

---

## Priority Detection Pipeline Failure Cases

Examples of high-value issues this architecture should detect or prevent include:

- key telemetry sources silently stopping ingestion
- parser failures breaking extraction of critical fields
- normalization errors causing detections to miss core entities
- enrichment dependencies becoming stale or unavailable
- schema changes invalidating existing analytic logic
- excessive duplication of findings from one underlying event chain
- delayed ingestion causing late or misleading detections
- content deployment errors weakening or disabling active detections

---

## Cross-Cloud Control Mapping

The architecture is intentionally platform-agnostic at the design level. Cloud services support implementation, but the core concerns remain ingestion reliability, parsing quality, normalization, enrichment, analytic execution, and pipeline change control.

### Azure examples

- Ingestion and analytics: Microsoft Sentinel, Log Analytics, Azure Monitor
- Source inputs: Entra events, Azure Activity Logs, Defender integrations, application and data source connectors
- Pipeline support: analytic rules, parser logic, workbooks, hunting and enrichment workflows
- Reliability support: monitoring of connectors, schema handling, content deployment discipline

### AWS examples

- Ingestion and analytics: CloudWatch, Security Hub, SIEM integrations
- Source inputs: CloudTrail, GuardDuty findings, VPC Flow Logs, service logs, application and data source connectors
- Pipeline support: parser logic, enrichment workflows, analytic content in integrated monitoring platforms
- Reliability support: connector monitoring, schema handling, content deployment discipline

---

## Design Decisions and Trade-offs

Every threat detection pipeline introduces trade-offs that should be managed deliberately.

### Source diversity vs Engineering complexity

Onboarding more telemetry improves possible visibility, but increases parsing, normalization, and maintenance burden.

### Source-specific logic vs Common modeling

Source-specific detections may be more precise, but too much source-specific logic reduces portability and reuse.

### Heavy enrichment vs Pipeline dependency risk

More context improves alert quality, but also creates more dependencies that can fail or go stale.

### Early finding generation vs Deeper correlation

Generating alerts quickly improves responsiveness, but some findings are more useful after additional grouping or contextual evaluation.

### Rapid content change vs Stability

Frequent pipeline and detection updates improve adaptability, but weak change control can introduce breakage into active monitoring.

---
