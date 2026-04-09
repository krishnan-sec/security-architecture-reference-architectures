# Security Architecture Reference Architectures

End-to-end security reference architectures for cloud and SaaS platforms, connecting business risk, security design principles, control implementation, and detection engineering across Azure and AWS environments.

---

## Overview

This repository contains architecture-level security designs for modern enterprise and product environments.

It is intended to show how security architecture can be expressed as clear, reusable reference models across cloud, application, data, and detection domains.

The goal is not only to describe controls, but to show how trust boundaries, access models, operational visibility, and protection requirements fit together across real-world platforms.

---

## Repository Structure

## Cloud Architectures

- [Cloud Secure Landing Zone](cloud/cloud-secure-landing-zone.md)
- [Zero Trust Architecture](cloud/zero-trust-architecture.md)
- [Multi-Tenant SaaS Security](cloud/multi-tenant-saas-security.md)

## Application Architectures

- [Secure API Platform](application/secure-api-platform.md)
- [Event-Driven Security](application/event-driven-security.md)
- [Microservices Security](application/microservices-security.md)

## Data Architectures

- [Data Protection Architecture](data/data-protection-architecture.md)
- [PII Security Architecture](data/pii-security-architecture.md)

## Detection Architectures

- [SOC Detection Architecture](detection/soc-detection-architecture.md)
- [Threat Detection Pipeline](detection/threat-detection-pipeline.md)

---

## What These Architectures Cover

These reference architectures are intended to describe:

- security objectives and architectural intent
- core control domains
- trust boundaries and access considerations
- operational and monitoring implications
- design decisions and trade-offs
- patterns that can be reused across platforms and teams

---

## Design Principles

Common themes across the repository include:

- identity as a primary control plane
- least privilege and explicit authorization
- controlled trust boundaries
- secure service-to-service interaction
- tenant and data isolation
- observability as a security requirement
- detection-informed architecture
- repeatable and reviewable design patterns

---

## How to Use This Repository

Each architecture document is structured to help security engineers, architects, and reviewers understand:

- the business and technical context
- the core architecture components
- the major security control domains
- the threats the design is intended to address
- the logging, telemetry, and detection needs
- the trade-offs and implementation considerations
- the related reusable patterns and supporting repositories

These documents can be used as:

- architecture review inputs
- design baselines
- portfolio artifacts
- discussion starters for engineering and security teams
- reusable reference material for future design work
