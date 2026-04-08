# Service Tiers

## Overview

This framework defines graduated tiers of service to help the business determine the appropriate level of investment for each service. Each dimension is drawn from existing NFR documents and ADRs within the VGW architecture, with tier-specific targets that reflect the criticality and blast radius of the service.

## Dimensions from NFR Docs

| Dimension | NFR Source | Current NFR Values |
|---|---|---|
| **Availability Target** | NFR Catalog | T1: 99.99% (4.2 min/mo), T2: 99.9% (43 min/mo), T3: 99% (7h14m/mo) |
| **RTO** | AVAIL-002 | 24 hours (single target today) |
| **RPO** | AVAIL-002 | 10 minutes (single target today) |
| **API Response Time** | PERF-001 | T1/T2: P95<200ms, P99<500ms. T3: P95<500ms, P99<2s |
| **Event Processing Latency** | PERF-002 | <500ms/event, 5000 events/sec (T1/T2) |
| **Autoscaling** | PERF-003 | <2 min response, linear to 1000 RPS (T1/T2) |
| **Observability Coverage** | OPS-002 | 100% coverage, <5 min critical alert response |
| **Testing Coverage** | OPS-001 | >70% unit, >60% integration, contract tests |
| **Health Probes** | OPS-010 | Liveness + readiness required (all tiers) |
| **Container Labels** | OPS-009 | Full label set required (all tiers) |
| **Kafka Retention** | DATA-001 | 7 days minimum |
| **S3 Event Backup** | DATA-003 | All events to S3 in recoverable format |
| **Database Backup Frequency** | DATA-004 | Every 3 days |
| **PITR** | DATA-004 | Enabled where cost-effective |
| **Cross-Region Replication** | ADR-055 | Optional per team discretion |
| **Security (JWT/Auth)** | SEC-001 | RS256, full claim verification |
| **Idempotent Event Replay** | ADR-055 | Required for DR |

---

## Tier 1 - Critical

> Core gaming services, payment processing, player authentication

| Dimension | Target | Requirement |
|---|---|---|
| **On Call** | 24/7 on-call roster | Must |
| **Availability** | 99.99% (4.2 min/mo error budget) | Must |
| **RTO** | 4 hours | Must |
| **RPO** | 10 minutes | Must |
| **MTD** | _Business to define_ | Must |
| **API Response Time** | P95<200ms, P99<500ms, P99.9<1000ms | Must |
| **Event Processing** | <500ms/event, 5000 events/sec | Must |
| **Autoscaling** | <2 min response, linear to 1000 RPS | Must |
| **Database Backups** | Daily snapshots + PITR | Must |
| **S3 Event Backup** | All events to S3 in recoverable format | Must |
| **Kafka Event Replay** | Idempotent consumers, 7-day retention | Must |
| **Cross-Region Replication** | Cross-region backup replication | Should |
| **DR Plan** | Documented per service boundary | Must |
| **DR Tests** | Quarterly | Must |
| **Runbooks** | Full operational runbooks | Must |
| **Observability** | 100% coverage, <5 min critical alert response, custom metrics | Must |
| **Testing** | >70% unit, >60% integration, contract tests, perf baselines | Must |
| **Health Probes** | Liveness + Readiness | Must |
| **Container Labels** | Full standard label set | Must |
| **Security** | JWT RS256, full claim verification | Must |

---

## Tier 2 - Player-Facing Non-Critical

> Player engagement, notifications, promotional services

| Dimension | Target | Requirement |
|---|---|---|
| **On Call** | 24/7 on-call roster | Must |
| **Availability** | 99.9% (43 min/mo error budget) | Must |
| **RTO** | 24 hours | Must |
| **RPO** | 10 minutes | Must |
| **MTD** | _Business to define_ | Must |
| **API Response Time** | P95<300ms, P99<800ms | Must |
| **Event Processing** | <500ms/event, 5000 events/sec | Should |
| **Autoscaling** | <2 min response | Must |
| **Database Backups** | 3-day snapshots + PITR | Should |
| **S3 Event Backup** | All events to S3 in recoverable format | Should |
| **Kafka Event Replay** | Idempotent consumers, 7-day retention | Should |
| **Cross-Region Replication** | Cross-region backup replication | Could |
| **DR Plan** | Documented per service boundary | Must |
| **DR Tests** | Annually | Should |
| **Runbooks** | Full operational runbooks | Must |
| **Observability** | 100% coverage, custom metrics available | Must |
| **Testing** | >70% unit, >60% integration, contract tests | Must |
| **Health Probes** | Liveness + Readiness | Must |
| **Container Labels** | Full standard label set | Must |
| **Security** | JWT RS256, full claim verification | Must |

---

## Tier 3 - Internal

> Backoffice tools, reporting services, internal dashboards

| Dimension | Target | Requirement |
|---|---|---|
| **On Call** | Business hours on-call roster | Must |
| **Availability** | 99% (7h 14min/mo error budget) | Must |
| **RTO** | 48-72 hours | Must |
| **RPO** | 1 hour | Must |
| **MTD** | _Business to define_ | Should |
| **API Response Time** | P95<500ms, P99<2000ms | Must |
| **Event Processing** | Best effort throughput | Could |
| **Autoscaling** | Manual scaling acceptable | Could |
| **Database Backups** | 3-day snapshots (no PITR) | Must |
| **S3 Event Backup** | Events to S3 | Could |
| **Kafka Event Replay** | 7-day retention | Could |
| **Cross-Region Replication** | Not required | - |
| **DR Plan** | Documented per service boundary | Should |
| **DR Tests** | Annually | Could |
| **Runbooks** | Operational runbooks | Should |
| **Observability** | Monitoring required, relaxed alert response targets | Must |
| **Testing** | >60% unit, integration for critical paths | Must |
| **Health Probes** | Liveness + Readiness | Should |
| **Container Labels** | Full standard label set | Must |
| **Security** | JWT RS256 for external-facing interfaces | Must |

---

## Tier 4 - Best Effort

> Experimental services, dev tooling, non-critical batch jobs

| Dimension | Target | Requirement |
|---|---|---|
| **On Call** | Best effort | Could |
| **Availability** | 95% (~36h/mo error budget) | Should |
| **RTO** | Best effort | Could |
| **RPO** | Best effort | Could |
| **MTD** | _Business to define_ | Could |
| **API Response Time** | Best effort | Could |
| **Event Processing** | Best effort | Could |
| **Autoscaling** | Fixed capacity | Could |
| **Database Backups** | Weekly snapshots | Should |
| **S3 Event Backup** | Not required | - |
| **Kafka Event Replay** | Not required | - |
| **Cross-Region Replication** | Not required | - |
| **DR Plan** | Basic recovery notes | Could |
| **DR Tests** | Not required | - |
| **Runbooks** | Basic troubleshooting guide | Could |
| **Observability** | Basic monitoring (logs + health check) | Should |
| **Testing** | Unit tests | Should |
| **Health Probes** | Liveness | Should |
| **Container Labels** | Full standard label set | Must |
| **Security** | Standard auth where applicable | Should |

---

## MoSCoW Key

| Level | Meaning |
|---|---|
| **Must** | Non-negotiable for this tier. Failure to meet this is a compliance gap. |
| **Should** | Expected for this tier. Exceptions require documented justification. |
| **Could** | Recommended but optional. Implement if capacity and budget allow. |
| **-** | Not applicable or not required for this tier. |

---

## How to Use This Framework

1. **Classify your service** into the appropriate tier based on its criticality and user impact.
2. **Review the Must requirements** for that tier - these are the baseline investment needed.
3. **Assess Should and Could requirements** with the business to determine what additional investment is warranted.
4. **Document deviations** from the tier expectations with rationale and risk acceptance.

## Related Documents

- [NFR Catalog](nfr-catalog.md)
- [NFR-AVAIL-001: Infrastructure Availability](availability/nfr-avail-001-infrastructure-availability.md)
- [NFR-AVAIL-002: Disaster Recovery Objectives](availability/nfr-avail-002-disaster-recovery-objectives.md)
- [NFR-PERF-001: API Response Time](performance/nfr-perf-001-api-response-time.md)
- [NFR-PERF-002: Event Processing Performance](performance/nfr-perf-002-event-processing-performance.md)
- [NFR-PERF-003: Autoscaling Performance](performance/nfr-perf-003-autoscaling-performance.md)
- [NFR-OPS-001: Testing Coverage](operational/nfr-ops-001-testing-coverage.md)
- [NFR-OPS-002: Observability Coverage](operational/nfr-ops-002-observability-coverage.md)
- [NFR-OPS-010: Health Probe Requirements](operational/nfr-ops-010-container-workload-health-probe-requirements.md)
- [NFR-DATA-001: MSK Retention Period](data/nfr-data-001-msk-retention-period.md)
- [NFR-DATA-003: S3 Event Backup](data/nfr-data-003-s3-event-backup.md)
- [NFR-DATA-004: Database Backup and Recovery](data/nfr-data-004-database-backup-recovery.md)
- [ADR-055: Disaster Recovery Requirements V2](../decisions/0055-disaster-recovery-requirements-v2.md)
