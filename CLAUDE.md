# CLAUDE.md — Thapsus ERP (PROJECT_KASONGO)

Thapsus ERP is the operations product of the Thapsus suite: inventory, warehouse, purchasing, sales orders,
manufacturing (discrete and process), quality, maintenance, projects, field service and rental, for UK, EU and US
businesses from about 10 to 2,000 staff (SMB to mid-market). It is sold on its own and as part of the suite with
Thapsus-HR (`PROJECT_KAREN`), Thapsus Finance (`PROJECT_MULLAH`), Thapsus CRM (`PROJECT_BOSSMAN`) and Thapsus Care
(`ROCHE`). **It has no general ledger of its own:** it sends accounting events to Thapsus Finance, or through a
connector to the customer's ledger (`docs/suite/INTEGRATION.md` §6).

## Status: planning

Nothing is built yet. The plan is in `docs/`. The build starts when the owner approves `docs/BUILD_BRIEF.md`.
Until then, only planning documents change. Read first: `docs/PLAN.md`, `docs/FEATURES.md`,
`docs/suite/SUITE_PLAN.md`.

## How to work in this repo

- Work the phases in `docs/PLAN.md` in order. One branch per phase (`phase-<n>-<slug>`), small Conventional
  Commits (`feat(inventory): …`, `test(mrp): …`).
- Do not stop to ask the owner questions. Make the most reasonable choice, record it in `docs/DECISIONS.md`
  (dated ADR) and carry on. Human-only steps go in `docs/HUMAN_TODO.md`; build against mocks meanwhile. Until
  Thapsus Finance publishes its ledger API, build against the contract-tested mock of it (owner decision D-7).
- **Always ask first before:** deploying to production, deleting any cloud resource or data, or adding
  recurring cost beyond the estimate in `docs/COSTS.md`.
- Never tick a PLAN item whose acceptance criteria are not proved by a test or a check in `pnpm verify`, or by a
  HUMAN_TODO entry for human-only items. Report failures and skipped steps honestly.
- Suite documents in `docs/suite/` are identical in PROJECT_MULLAH, PROJECT_BOSSMAN and PROJECT_KASONGO. Change
  all three copies in one change.

## Scope guardrails

Out of scope: a general ledger, AP or AR of its own (Thapsus Finance or a connector); running payroll; acting as a
carrier, customs broker or 3PL; device management or buying hardware; machine control (PLC/SCADA); a full PLM or
CAD system; and native mobile apps before the suite's native phase (ship an installable PWA with scanner support).

## Non-negotiables

### Operational integrity
- Every stock movement is an immutable stock transaction; on-hand, allocated and available quantities are
  derived from them. Corrections are new transactions.
- Quantities and unit conversions use exact decimals (PostgreSQL `numeric` with the item's precision), never
  floating point. Money is integer minor units plus ISO 4217.
- Valuation layers (FIFO, weighted average, standard) are immutable; a costing-method change takes effect only
  at a period boundary.
- Every change of inventory value writes its accounting event to the outbox in the same transaction. The
  inventory sub-ledger reconciles with Finance's control accounts every night.
- Lot and serial genealogy is complete forwards and backwards; a recall query answers within seconds.
- Offline scans and kiosk actions carry client UUIDs and are idempotent.
- Electronic signatures for regulated manufacturers (21 CFR Part 11 and EU GMP Annex 11 option) record the
  signer, time, meaning and the exact record signed.

### Privacy and data residency
- Thapsus is the processor; customers are controllers. UK GDPR and the Data Protection Act 2018 (as amended by the
  Data (Use and Access) Act 2025), EU GDPR, US state privacy laws.
- Home regions: **UK = europe-west2**, **EU = europe-west3** (backups only in europe-west1), **US = us-east5**
  (backups only in us-west1). All personal and business data, files, backups, logs, search indexes, caches,
  queues and emails stay there; enforced by tests for every region pair. No multi-region locations, no Cloud CDN
  for authenticated traffic, no Cloud Trace, Error Reporting or `_Default` log bucket.
- No personal data to a third party (carriers, marketplaces, EDI networks) unless listed in
  `docs/SUBPROCESSORS.md` first.

### Security
- Tenant isolation with PostgreSQL row-level security, enabled and forced, proved by tests; the app role has no
  `BYPASSRLS` and owns no tables; tenant-to-database routing is configuration.
- MFA for admins and approvers; SSO can be enforced; kiosk PIN sign-in on shared devices with auto sign-out.
- Append-only audit log. OWASP ASVS level 2. Secrets only in Secret Manager. No service-account keys; GitHub uses
  workload identity.

### Quality and design
- WCAG 2.2 AA; scanner and kiosk screens work with gloves, glare and one hand (44 px minimum targets).
- No hard-coded user-facing strings; en-GB and en-US at launch.
- Trade, product and sustainability rules (Intrastat, customs, CBAM, EUDR, packaging EPR, FSMA 204) are versioned,
  effective-dated rule-pack data with official sources and golden tests.
- Build every screen from the suite design system (`docs/suite/DESIGN_SYSTEM.md`). ERP's accent is steel; text
  links are underlined.

### AI
- Every AI feature is off by default, goes through the suite AI gateway only, drafts for a person to approve, and
  never places an order, moves stock or changes a plan on model output alone (`docs/suite/AI.md`).

## Engineering rules

- **Tests first** for stock movements, valuation and landed cost, unit conversions, MRP and allocation, pricing,
  accounting events, traceability, tenant isolation and residency.
- Fictional test data only.
- Tenant context helper for every query; new tenant table checklist (`tenant_id`, forced RLS, policy, index
  leading with `tenant_id`, audit).
- Instants as `timestamptz`; dates as `date` with the site's IANA zone; shared time utilities.
- Nothing configurable is hard-coded: warehouse processes, numbering, units, costing methods, reorder rules,
  prices, carrier settings, compliance thresholds.
- OpenAPI 3.1 first, `/v1`, contract tests; outbox in the same transaction; idempotent jobs; expand-and-contract
  migrations; scrubbed logs.
- One OpenTofu definition for staging and production; production deploys only staging-tested digests.
- PostgreSQL full-text and `pg_trgm` for search unless load tests prove otherwise.

## Commands (planned; implemented in Phase 0)

| Command | Purpose |
| --- | --- |
| `pnpm install` / `pnpm dev` | Install / run web, api and worker locally |
| `pnpm verify` | Full gate: lint, typecheck, unit, integration, contract (including the Finance ledger mock), stock and valuation invariants, tenant isolation, residency, e2e, visual regression, Lighthouse, security scan, build, OpenTofu checks |
| `pnpm db:migrate` / `pnpm db:seed` | Apply migrations / seed the fictional demo company |

## Key documents

`docs/BUILD_BRIEF.md` (draft scope) · `docs/PLAN.md` · `docs/FEATURES.md` · `docs/RESEARCH.md` ·
`docs/DECISIONS.md` · `docs/HUMAN_TODO.md` · `docs/suite/`
