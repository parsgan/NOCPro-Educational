# ADR-0001 — Modular Monolith

## Context
NOCPro is an Enterprise NOC Operations platform. MVP must ship fast, avoid premature distributed complexity.

## Problem
Microservices vs Modular Monolith for MVP?

## Decision
Use Modular Monolith + API-First for the MVP.

## Alternatives
- Microservices from day one
- Unstructured monolith

## Consequences
- Single deployable unit for MVP
- Strict module boundaries in code
- Migration to services only via approved ADRs

## Status
Accepted (initial).

## Date
2026-09-19