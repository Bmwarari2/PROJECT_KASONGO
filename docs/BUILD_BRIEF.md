# BUILD BRIEF (DRAFT): Thapsus ERP, an operations platform by Thapsus

> **Draft for the owner's approval, prepared on 2026-11-07** from the owner's request and the decisions recorded in
> `suite/SUITE_PLAN.md` §2. When approved, it becomes the source of truth for scope, in the same way as
> `PROJECT_KAREN/docs/BUILD_BRIEF.md` is for Thapsus-HR. Until then nothing is built.

You are the lead engineer building Thapsus ERP (codename PROJECT_KASONGO), a production-ready, multi-tenant ERP for
businesses of about 10 to 2,000 staff in the United Kingdom, the European Union and the United States. It is one of
five Thapsus products and must work with the others when a customer buys more than one.

First: read `CLAUDE.md`, `docs/PLAN.md`, `docs/FEATURES.md` and `docs/suite/`, then show the plan for Phase 0 and
wait for the owner to start the build.

## 1. Product position

- A modern, calm, configurable cloud ERP for the mid-market, for businesses outgrowing inventory add-ons (Cin7,
  Unleashed, Katana, MRPeasy) and spreadsheets, without NetSuite's price or a long implementation.
- Four industries on one core (owner decision D-3): wholesale and distribution; discrete manufacturing; process
  manufacturing (food and drink first); projects and services (professional services, field service, construction,
  rental).
- Strengths to lead with: compliance data on the item, lot and import line from day one (packaging EPR, CBAM, EUDR,
  US tariffs, FSMA 204); a scanner-first warehouse on any phone; no-code configuration; industry templates and a
  data-migration workbench; and, with the rest of the suite, one ledger (Finance), one customer record (CRM) and one
  workforce record (HR).
- Out of scope: its own general ledger, payables or receivables (Thapsus Finance or a ledger connector); payroll;
  acting as a carrier, customs broker or 3PL; machine control; full PLM or CAD; building a point-of-sale system;
  GxP-validated pharma at launch; native apps before the suite's native phase.

## 2. Non-negotiables

As in `CLAUDE.md`: operational integrity (immutable stock transactions, exact quantities, immutable valuation
layers, accounting events in the same transaction, complete lot genealogy); privacy and data residency (home regions
UK europe-west2, EU europe-west3, US us-east5; nothing leaves the cell); security (forced RLS, MFA, audit, ASVS L2,
no keys); quality (WCAG 2.2 AA, i18n, rules as sourced and effective-dated data); the suite design system with ERP's
accent; and optional, draft-only AI.

## 3. Scale targets (prove with load tests; record in docs/PERFORMANCE.md)

- One tenant with 2,000 staff, 3 legal entities, 20 warehouses, 50,000 items, 300 locations with bins, 5 million stock
  transactions a year.
- 500 concurrent users per tenant; 50,000 sales-order lines a day; 2,000 scans a minute in one warehouse.
- An MRP run for 100,000 item-locations within 10 minutes; a full lot trace within 2 seconds.
- p95 API latency under 300 ms for common reads and under 1 second for paginated lists.
- 99.9% availability; RPO 15 minutes; RTO 4 hours.

## 4. Architecture and stack

As in `docs/DECISIONS.md` ADR-0002 and `suite/PLATFORM.md`: TypeScript, pnpm and Turborepo; Next.js PWA (scanner and
kiosk modes); Fastify with TypeBox and OpenAPI 3.1; PostgreSQL 17 on Cloud SQL with forced RLS; the platform kit
(`@thapsus-suite/*`); Cloud Run; a PostgreSQL-backed job queue with an in-cell scheduler on a Cloud Run worker pool;
regional Pub/Sub for suite events; OpenTofu cells from the platform modules; staging equals production.

## 5. Users and roles

Thapsus back-office staff; company owner; ERP administrator; finance controller (read and approve); purchasing
manager; buyer; sales order desk; warehouse manager; warehouse operative (scanner); production planner; production
supervisor; shop-floor operator (kiosk, PIN); quality manager; maintenance planner; maintenance or field technician;
project manager; B2B portal customer user; supplier portal user. Custom roles with field-level rules, scoped by
entity, site, warehouse or team. Light users (scanner, kiosk, approver) are priced separately.

## 6. Features

`docs/FEATURES.md` is the scope: item master, inventory, warehouse, purchasing, sales and pricing, manufacturing
(discrete and process), quality, planning, projects and services, maintenance, field service, rental, shipping,
commerce and EDI, multi-entity, trade and sustainability compliance, optional AI, Studio configuration and platform
features.

## 7. Delivery phases (complete in order; lanes may run in parallel where `PLAN.md` allows)

0 Foundations · 1 Items and inventory · 2 Purchasing and landed cost · 3 Sales orders and pricing · 4 Warehouse,
scanning and shipping · 5 UK trade and packaging compliance · 6 Commerce, EDI, B2B portal and intercompany (release
W1) · 7 Discrete manufacturing · 8 Quality, traceability and e-signatures (release M1) · 9 Process manufacturing
(release P1) · 10 Planning and scheduling · 11 Projects and construction · 12 Maintenance, field service and rental
(release S1) · 13 EU pack · 14 US pack · 15 Optional AI · 16 Suite links live · 17 Native app · 18 Scale and launch
readiness. Acceptance criteria per phase: `docs/PLAN.md`.

## 8. Engineering rules

As in `CLAUDE.md`. In particular: tests first for stock, valuation, landed cost, units, MRP, pricing, accounting
events, traceability, isolation and residency; fictional data only; `pnpm verify` green at the end of every phase
with the summary printed; human-only steps in `docs/HUMAN_TODO.md`; ask before production deploys, deletions or new
recurring cost.

## 9. Documentation

README, ARCHITECTURE (with diagrams), DESIGN (pointing to the suite design system), SECURITY, DECISIONS, COSTS,
PERFORMANCE, COVERAGE (rule packs by country), SUBPROCESSORS, COMPLIANCE, HUMAN_TODO, API docs, runbooks (deploy,
rollback, restore, incident, tenant move), DPIA template, records of processing, admin and user guides per role,
and an implementation playbook for partners (migration, fit-gap, templates).

## 10. Definition of done

Every phase ticked in `docs/PLAN.md` with evidence; `pnpm verify` green; staging deployed in each region before its
production cell; smoke and load tests meeting §3; production defined and ready to deploy on the owner's approval;
all §9 documents present; every remaining human step in `docs/HUMAN_TODO.md`.
