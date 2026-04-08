# Reliability Tier Compliance & Operations Matrix

This matrix maps VGW's four-tier reliability investment model (Tier 4 Beginner → Tier 1 Gold) to the ROAD framework (Recovery, Observability, Availability, Delivery). Each tier is a **voluntary choice of investment**, not a risk rating. Requirements are **cumulative** — each tier inherits everything from the tier below plus its own additions (marked with `+`).

| Tier | Name | ROAD Maturity | SLO Range | Response SLA |
|---|---|---|---|---|
| **Tier 4** | Beginner | Reactive | < 99.5% | Next business day |
| **Tier 3** | Bronze | Proactive | 99.5%–99.9% | 4 hours (business hours) |
| **Tier 2** | Silver | Strategic | 99.9%–99.95% | 1 hour |
| **Tier 1** | Gold | Visionary | ≥ 99.95% | 15 minutes |

---

## Category 1: Observability

| Dimension | Tier 4 — Beginner | Tier 3 — Bronze | Tier 2 — Silver | Tier 1 — Gold |
|---|---|---|---|---|
| **Logging** | Meaningful, context-driven logs in non-transient storage<br>Log retention per default policy | + Structured logs with request correlation IDs<br>+ Logs queryable across services within boundary | + Contextual enrichment (user, tenant, trace ID)<br>+ Log-based alerting for error spikes | + Centralised log aggregation VGW-to-brand<br>+ Log retention policy auditable and compliance-aligned |
| **Metrics** | Host metrics (CPU, memory, disk)<br>Uptime measured | + Golden signals (latency, traffic, errors, saturation)<br>+ Business metrics captured<br>+ Deployment markers | + SLI-specific metrics per service<br>+ Alerting review cadence established<br>+ FE error tracking | + RUM (Real User Monitoring)<br>+ Continuous profiling<br>+ Synthetic testing metrics |
| **Tracing** | Not required | Edge-to-edge distributed traces instrumented<br>Traces queryable in Honeycomb/Grafana | + Traces linked to runbooks and triage procedures<br>+ Trace-based SLI derivation where applicable | + Holistic tracing VGW-to-brand<br>+ Trace sampling strategy documented and tuned |
| **Dashboards** | Basic uptime dashboard<br>SLO published on Grafana SRE Maturity Dashboard | + Golden signals dashboards<br>+ Deployment marker overlays<br>+ Business metrics dashboard | + SLI/SLO monitoring dashboards<br>+ Error budget burn-rate visualisation<br>+ Contextual alert routing dashboard | + RUM dashboards<br>+ Synthetic monitoring dashboards<br>+ Lighthouse performance reports<br>+ Cross-team service health views (incident commander perspective) |
| **Alerting** | Basic threshold alerts (service down, high CPU) | + Burn-rate alerting on SLOs<br>+ Alerts routed to contextually-appropriate destinations | + Alerting review cadence (regular tuning)<br>+ Alert-to-runbook linkage enforced<br>+ Contextually-appropriate routing validated | + Automated response triggered by alerts<br>+ Synthetic test failure alerting<br>+ Automated escalation via PagerDuty (no manual triage layer) |

---

## Category 2: Incident Response & Recovery

| Dimension | Tier 4 — Beginner | Tier 3 — Bronze | Tier 2 — Silver | Tier 1 — Gold |
|---|---|---|---|---|
| **Incident Process** | Report via standard channel<br>Major incident process followed | + Defined triage process<br>+ Severity levels documented<br>+ PIRs completed | + IR training completed for all responders<br>+ DORA metrics tracked<br>+ PIRs within 2-day SLA | + Major incident role-plays conducted<br>+ Pre-mortems before major releases<br>+ Regression tracking from PIR actions |
| **Runbooks** | Not required | Alert-linked runbooks accessible to responders | + Runbooks linked to logs/traces<br>+ Triage runbook defined<br>+ Human-triggered remediation automations | + System-triggered automated remediation<br>+ Automated remediation of common incidents with audit trail |
| **Post-Incident Review** | Not required | PIRs completed for severity incidents | + PIRs completed within 2 business days<br>+ Action items tracked to completion | + Regression tracking across PIR actions<br>+ PIR findings feed into pre-mortem process |
| **IR Training & Exercises** | Not required | Triage process defined and documented | + IR training completed<br>+ Role-play exercises conducted<br>+ DORA metrics inform training focus | + Major incident role-plays<br>+ Game days conducted regularly<br>+ Pre-mortems before major releases |
| **Recovery Mechanism** | Manual intervention via standard escalation | Human-triggered remediation via runbooks | + Human-triggered automation (scripted recovery)<br>+ Tested recovery procedures | + System-triggered automated remediation<br>+ No-ops incident response for known failure modes |

---

## Category 3: Availability & Resilience

| Dimension | Tier 4 — Beginner | Tier 3 — Bronze | Tier 2 — Silver | Tier 1 — Gold |
|---|---|---|---|---|
| **Redundancy** | Single deployment acceptable<br>Failure scenarios identified | Multi-AZ required<br>Workload failure scenarios identified | + Cross-region backups<br>+ Failover documented and tested | + Active-active or active-passive validated<br>+ Global tables/replicator where applicable |
| **Fault Tolerance** | Failure scenarios identified and documented | + Circuit breakers implemented<br>+ Graceful degradation documented | + DR plan documented<br>+ Failover testing completed<br>+ Resilience patterns applied (bulkhead, retry) | + Chaos engineering practised regularly<br>+ Fault isolation validated<br>+ Automated recovery from known faults |
| **DR Plan** | Not required | Workload failure scenarios identified<br>Restoration process documented | + DR plan documented<br>+ Load and performance tests run against recovery procedures | + DR tests (DiRT) executed regularly<br>+ DR plan validated with evidence retained |
| **Scaling** | Fixed provisioning acceptable | Right-sizing reviewed<br>Baseline performance established | + HPA enabled<br>+ Karpenter for node scaling<br>+ Capacity planning cadence | + Auto-scaling validated under load<br>+ Vertical scaling where appropriate<br>+ Automated scaling tested via chaos experiments |

---

## Category 4: Operational Reporting & SLO Governance

| Dimension | Tier 4 — Beginner | Tier 3 — Bronze | Tier 2 — Silver | Tier 1 — Gold |
|---|---|---|---|---|
| **SLI/SLO Definition** | SLIs defined<br>SLOs tracked and published on Grafana dashboard | + Burn-rate alerting configured<br>+ Error budget tracked monthly | + Error budgets implemented and monitored<br>+ Action required at 33% burn (reliability sprint) | + Error budget policy enforced<br>+ Feature freeze at 100% burn<br>+ Formal quarterly revisit |
| **SLO Review Cadence** | SLOs published (internal visibility) | + Monthly error budget review by team | + Error budget as input to sprint planning<br>+ Action thresholds trigger reliability work | + Quarterly formal SLO revisit<br>+ Error budget status in quarterly business reviews |
| **Error Budget Governance** | Informational only — no enforcement | Budget tracked monthly<br>Team reviews trends | + Action at 33% burn: reliability sprint<br>+ Budget status visible in team ceremonies | + 33% burn = reliability sprint<br>+ 100% burn = feature freeze + mandatory review<br>+ Formal error budget policy document |
| **DORA Metrics** | Not tracked | Deployment frequency tracked via OpsLevel/GH Actions | + Full DORA metrics tracked (lead time, deployment frequency, change failure rate, MTTR)<br>+ Reviewed in team ceremonies | + DORA metrics inform release strategy<br>+ Continuous improvement targets set per metric |
| **Reporting Artefacts** | SRE Maturity Dashboard access<br>Async SRE consultative review | + SRE-assisted alerting review<br>+ Observability tooling budget (Honeycomb/Grafana) | + Alerting review cadence documented<br>+ Contextual alert routing validated<br>+ PagerDuty provisioned | + Synthetic test reporting<br>+ Holistic observability dashboards VGW-to-brand<br>+ Cross-team service health views for incident commanders |

---

## Category 5: Compliance Evidence & Planning (PCI DSS, SOC 2, MGA)

| Dimension | Tier 4 — Beginner | Tier 3 — Bronze | Tier 2 — Silver | Tier 1 — Gold |
|---|---|---|---|---|
| **Backup Policy & Evidence** | Failure scenarios identified<br>Backups implied by infrastructure defaults | + Restoration process documented<br>+ Multi-AZ backups in place | + Cross-region backups with defined retention policy<br>+ Backup monitoring configured | + Backup verification automated and auditable<br>+ Backup compliance evidence retained for audit cycles |
| **Restoration Tests** | Not required | Restoration process documented (paper-based) | + Load/performance-tested restores<br>+ Restoration time validated against SLO | + Regular validated restoration drills<br>+ Evidence retained and auditable<br>+ Restoration time within RTO |
| **Business Continuity Plan** | Not required | Workload failure scenarios documented | + DR plan documented<br>+ Resilience patterns applied<br>+ BCP reviewed against compliance requirements | + BCP tested regularly<br>+ Chaos engineering validates continuity assumptions<br>+ BCP evidence auditable |
| **DR Plans** | Not required | Documented at workload level | + DR plan documented and reviewed<br>+ Recovery procedures tested | + DiRT exercises executed regularly<br>+ Findings tracked and remediated<br>+ Evidence retained for auditors |
| **DR Tests (DiRT)** | Not required | Not required | Scheduled; resilience patterns applied and load-tested | + Executed regularly with findings tracked<br>+ Remediation actions closed out<br>+ Test reports retained as compliance artefacts |
| **Runbooks as Recovery Evidence** | Not required | Alert-linked runbooks accessible to responders<br>Evidence of documented response procedures | + Runbooks linked to logs/traces with triage procedures<br>+ Human-triggered automation documented | + System-triggered automated remediation with audit trail<br>+ Remediation actions logged for compliance evidence |
| **Game Days / Tabletop Exercises** | Not required | Not required | + IR role-plays completed<br>+ IR training evidence retained | + Major incident role-plays and pre-mortems before releases<br>+ Game day findings tracked and remediated |
| **Published SLOs** | Tracked and published (internal)<br>SLIs defined — evidence of availability measurement | + Tracked, published, and alerted<br>+ Error budgets monitored monthly<br>+ Evidence of proactive availability management | + Error budgets monitored with action thresholds<br>+ 33% burn triggers reliability sprint<br>+ Suitable as evidence of availability commitments | + Error budget policy enforced with formal quarterly revisit<br>+ Feature freeze at 100% burn<br>+ Full compliance evidence of availability governance |

---

## Category 6: On-Call & Roster Model

| Dimension | Tier 4 — Beginner | Tier 3 — Bronze | Tier 2 — Silver | Tier 1 — Gold |
|---|---|---|---|---|
| **Roster Type** | No dedicated roster<br>Daytime/business-hours escalation path only | Defined escalation path<br>Best-effort on-call | Formal on-call roster with OOH via PagerDuty | + 24/7 primary + secondary roster<br>+ Follow-the-sun where needed |
| **Response SLA** | Next business day | 4 hours (business hours) | 1 hour | 15 minutes |
| **Roster Health** | Not tracked | Not tracked | Tracked with rotation fairness metrics | + Burnout prevention measures<br>+ Roster health reviewed regularly |
| **Escalation Path** | Business-hours escalation to team lead | Defined multi-level escalation<br>Severity-based routing | + PagerDuty integration<br>+ Automated escalation on acknowledgement timeout | + Secondary on-call auto-escalation<br>+ Follow-the-sun handoff procedures<br>+ Automated PagerDuty escalation (no manual triage layer) |
| **Compliance Framing** | Business-hours response acceptable for non-critical services<br>Escalation path satisfies basic SOC 2 CC7 monitoring | Defined escalation path provides evidence of incident response capability (PCI DSS 12.10.1 awareness) | Formal roster satisfies PCI DSS 12.10.1 requirement for designated incident response personnel<br>OOH coverage evidences SOC 2 A1.2 recovery capability | 24/7 roster satisfies PCI DSS 12.10.1 (personnel available around the clock for critical CDE services)<br>SOC 2 A1.2 met with tested recovery within SLO objectives |

---

## Compliance Cross-Reference

| Matrix Row | PCI DSS v4.0 | SOC 2 Trust Service Criteria | MGA Technical Standards |
|---|---|---|---|
| **Logging** | Req 10.2–10.3 (audit log events, protection of logs) | CC7.1–CC7.2 (monitoring, detection) | Player data access logging; audit trail for transactions |
| **Alerting** | Req 10.4.1 (automated mechanisms for audit log review) | CC7.2 (anomaly detection), CC7.3 (evaluate and respond) | Real-time monitoring of gaming systems |
| **Incident Process** | Req 12.10.1 (incident response plan), 12.10.2 (annual IR testing) | CC7.3 (evaluate security events), CC7.4 (respond to incidents) | Incident management for service disruptions affecting players |
| **Runbooks / Recovery Evidence** | Req 12.10.4 (personnel trained in IR duties) | CC7.4 (response procedures), A1.2 (recovery mechanisms) | Documented recovery procedures for gaming platform continuity |
| **Post-Incident Review** | Req 12.10.6 (modify IR plan based on lessons learned) | CC7.5 (recovery and lessons learned) | Post-incident analysis for player-impacting events |
| **Backup Policy & Evidence** | Req 12.5.2 (PCI DSS scope validation annually, backup of CHD systems) | A1.2 (recovery of infrastructure), A1.3 (testing of recovery) | Business continuity: data backup and protection of player funds |
| **Restoration Tests** | Req 12.10.2 (test IR plan at least annually) | A1.3 (testing recovery procedures) | Regular testing of disaster recovery for gaming systems |
| **DR Plans / DiRT** | Req 12.10.2 (annual IR plan testing) | A1.2 (recovery within objectives), A1.3 (testing) | Business continuity plans tested for gaming platform availability |
| **Business Continuity Plan** | Req 12.10.1 (IR plan addresses business-critical systems) | A1.1 (environmental protections), A1.2 (recovery mechanisms), CC9.1 (risk identification) | MGA licence condition: documented BCP for uninterrupted gaming operations |
| **Published SLOs / Error Budget** | Req 12.1 (information security policy supporting business objectives) | A1.1 (availability commitments), CC9.1 (risk assessment) | Availability commitments for player-facing gaming systems |
| **Roster / On-Call** | Req 12.10.1 (incident response personnel available 24/7 for Gold/CDE services) | A1.2 (recovery within defined timeframes), CC7.4 (response activities) | Personnel available to respond to gaming system disruptions |
| **Game Days / Tabletop** | Req 12.10.2 (IR plan testing), 12.10.4 (training) | A1.3 (testing recovery), CC7.4 (response evaluation) | Testing of operational resilience for gaming systems |
| **DORA Metrics** | — | PI1.4 (processing integrity monitoring) | — |
| **Redundancy / Fault Tolerance** | Req 12.5.2 (system component availability) | A1.1 (environmental protections), A1.2 (infrastructure recovery) | Technical infrastructure resilience for continuous gaming operations |

---

## Sources

1. **VGW ROAD to SRE Roadmap** — Recovery, Observability, Availability, Delivery maturity lanes (Reactive → Proactive → Strategic → Visionary)
2. **VGW Reliability Investment Report** — Tier definitions (§4), NFR gates (§3), ROAD tenet breakdown (§2), strategic transition plan (§5), unlock contracts
3. **VGW NFR Decisions** — Maintainability (configurability, testability, deployments, service catalogue), Performance (throughput, resource utilisation, caching), Reliability (fault tolerance, redundancy, monitoring, archival, streaming), Security (zero trust, API segregation), Modularity
4. **VGW Reliability Tier Options** — Three candidate models (Progressive, Bands, Capability Unlocks) with trade-off analysis
5. **Implementing Service Level Objectives** (Alex Hidalgo, O'Reilly) — Ch. 1–2 (reliability cost curve), Ch. 4–5 (SLO targets, error budgets, budget policies), Ch. 16 (Crawl/Walk/Run SLO advocacy), Ch. 17 (reliability reporting)
6. **PCI DSS v4.0** (PCI Security Standards Council, 2022) — Req 10 (logging/monitoring), Req 12.10 (incident response), Req 12.5.2 (scope validation/backup)
7. **SOC 2 Trust Service Criteria** (AICPA, 2017) — Availability (A1.1–A1.3), Processing Integrity (PI1), Common Criteria (CC7 monitoring, CC9 risk management)
8. **MGA Technical Standards** (Malta Gaming Authority) — Technical requirements for RNG systems, player data protection, business continuity, and operational resilience of gaming platforms
9. **Jeff Allan, "claude-skills"** (GitHub: https://github.com/Jeffallan/claude-skills) — Reference for structured prompt engineering patterns used to construct this matrix
