# ADR-0002 — API-First

## Context
NOCPro must integrate with Monitoring, ITSM, Infrastructure and AI components.

## Problem
Contract-first or UI-first?

## Decision
API-First: define and version the API contract before UI/integration.

## Alternatives
- UI-first
- Integration-first without a formal contract

## Consequences
- API contracts documented and versioned
- Clients consume same contract

## Status
Accepted (initial).

## Date
2026-09-19