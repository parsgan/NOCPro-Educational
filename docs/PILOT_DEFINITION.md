# NOCPro Pilot v0.1 — Definition

## 1. Purpose
Prove a reliable, auditable vertical slice:
Zabbix -> NOCPro Intake -> Event -> Incident -> GLPI Ticket -> Recovery -> Audit

## 2. In Scope
- Authenticated ingress from Zabbix (HMAC per ADR-0007)
- Durable intake, idempotency, deduplication
- Basic correlation (same host + same trigger within window)
- Incident creation with state machine
- GLPI ticket creation and state sync (one-way NOCPro -> GLPI in Pilot;
  status polling for ticket state read-back)
- Recovery handling per D4
- Audit trail for all transitions
- RBAC: minimal roles (Operator, Viewer)
- E2E tests with synthetic data only

## 3. Out of Scope
- AI / LLM features
- Auto-Remediation
- Advanced topology correlation
- Multi-tenancy
- Advanced dashboards
- Full two-way GLPI synchronization (bidirectional write-back beyond
  status read)
- Kubernetes, microservices split
- Production deployment

## 4. Actors
- Zabbix (machine, ingress)
- NOCPro API (FastAPI)
- NOCPro Worker
- NOCPro PostgreSQL
- GLPI (test instance)
- Operator (human, RBAC)

## 5. Success Criteria
- End-to-end synthetic trigger reaches GLPI ticket in < 10s p95 in Lab.
- Duplicate alerts produce exactly one incident.
- Recovery does not auto-close incident (per D4).
- All state transitions audited.
- All tests defined in Section 4 of Execution Assignment pass.
- No mutation of Parsgan resources.
- All images pinned to explicit versions.

## 6. Non-Functional Targets (Lab only)
- Availability: single-node acceptable.
- Throughput: 5 events/sec sustained in Lab.
- Data retention: 90 days events in Pilot DB.
- Recovery: worker resumes after crash within 60s.

## 7. Constraints
- VM: 3 vCPU, 7.7 GB RAM, 35 GB free.
- Docker Engine and Compose only.
- No cloud dependency.
- No real organization data.

## 8. Exit Criteria
- All Pilot E2E scenarios Pass.
- Claude independent review complete.
- Product Owner sign-off.
- Decision on ADR-0006 / ADR-0007 finalized.