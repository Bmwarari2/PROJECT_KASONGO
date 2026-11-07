# Decisions — Thapsus ERP

Dated architecture and product decisions. Format: context, decision, consequences. Suite-wide decisions are
summarised in `docs/suite/SUITE_PLAN.md` §2; this file records how they apply here.

## ADR-0001 — Owner decisions for the new products (2026-11-07)

**Context.** The owner asked for an ERP (codename PROJECT_KASONGO) as part of a suite with Thapsus-HR, Thapsus
Care, a finance product and a CRM, and answered seven scoping questions on 2026-11-07.

**Decision.**
- Markets: UK, EU and US home-region cells from day one; UK trade and compliance content at launch; EU and US
  follow (D-1).
- Client size: SMB to mid-market, about 10 to 2,000 staff (D-2).
- Industries: wholesale and distribution, discrete manufacturing, process manufacturing, and projects and
  services (construction, contracting, professional and field services, rental), all four (D-3).
- Design: the shared suite design system with ERP's own accent (D-5).
- Mobile: an installable PWA first, with camera and hardware-scanner input and offline queues; a native app later
  for heavy offline warehouse and field-service work, reusing Care's Expo and offline stack (D-6).
- Build order: the platform kit first, then Finance, CRM and ERP in parallel; ERP builds against a contract-tested
  mock of Finance's ledger API until it is ready (D-7).

**Consequences.** One shared operational core (items, inventory, purchasing, sales, costing) serves all four
industries; each industry is a solution pack with its own modules and acceptance criteria (ADR-0004).

## ADR-0002 — Stack and platform kit (2026-11-07)

**Decision.** TypeScript, pnpm and Turborepo; `apps/web` (Next.js App Router PWA, including scanner and kiosk
modes), `apps/api` (Fastify, TypeBox, OpenAPI 3.1, `/v1`), `apps/worker` (outbox, MRP and planning runs, carrier
and marketplace sync, reorder jobs); `packages/inventory`, `packages/costing`, `packages/planning` (domain rules
with tests first), `packages/rules` (trade, product and sustainability packs), `packages/db`; shared
`@thapsus-suite/*` packages.

**Consequences.** Same as Finance ADR-0002. Planning runs (MRP) are background jobs with progress, sized for the
mid-market (hundreds of thousands of item-location pairs) and benchmarked.

## ADR-0003 — No ledger in ERP: accounting events to Finance or a connector (2026-11-07)

**Context.** The suite has one ledger (D-12). Customers who buy ERP alone still need their books updated.

**Decision.** Every transaction that changes inventory value, accrues a liability or recognises cost or revenue
writes a typed accounting event to the outbox in the same transaction (`docs/suite/INTEGRATION.md` §6). With
Thapsus Finance linked, the events go to its accounting-events API. Without it, connectors map them to journals in
Xero, QuickBooks Online, Sage or Business Central, or to a journal export file. ERP keeps operational
sub-ledgers (stock valuation layers, received-not-invoiced, WIP) and reconciles them nightly with the ledger's
control accounts.

**Consequences.** Until Finance's API is live, ERP builds against a mock generated from Finance's published OpenAPI
and AsyncAPI documents, re-pinned when Finance releases (the pattern Care uses with Thapsus-HR).

## ADR-0004 — One core, four industry packs (2026-11-07)

**Context.** D-3 asks for four industries. Building four products would be shallow; building one with no industry
fit would not sell.

**Decision.** A shared core (item master, inventory, purchasing, sales orders, pricing, costing, warehouse,
quality, planning) plus industry modules switched on per tenant and delivered with Studio solution packs:
- **Wholesale and distribution**: advanced pricing and rebates, EDI, B2B portal, eCommerce connectors, drop ship.
- **Discrete manufacturing**: BOMs, routings, MRP, production orders, shop-floor kiosk, capacity, subcontracting.
- **Process manufacturing**: formulas, batch orders, potency and catch weight, allergens, lot genealogy, recalls.
- **Projects and services**: projects and WBS, timesheets, WIP and billing, construction (retentions, valuations,
  CIS through Finance), field service, rental.
Build order inside ERP: core and wholesale first, then discrete, then process, then projects and services (each
with its own acceptance criteria), all within the suite roadmap.

**Consequences.** Each pack is sold and priced separately; the core stays free of industry-specific code paths
other than through configuration and modules.

## ADR-0005 — Exact quantities, immutable stock and valuation layers (2026-11-07)

**Decision.** Stock transactions are append-only; on-hand, allocated, available and in-transit are derived and
materialised per item, location and lot, refreshed transactionally. Quantities are `numeric` with per-item
precision and exact unit conversions. Valuation layers (FIFO receipts, average cost history, standard cost
versions) are immutable; landed cost and revaluations add adjustment layers. Negative stock is refused unless a
warehouse is configured to allow it, in which case costing is corrected when the receipt arrives.

**Consequences.** Property-based tests check that on-hand always equals the sum of transactions and that inventory
value equals the sum of open layers.

## ADR-0006 — Scanner-first warehouse and shop floor on the PWA (2026-11-07)

**Context.** D-6 puts native apps later. Warehouse and shop-floor users need fast scanning, often offline.

**Decision.** The PWA accepts hardware scanners in keyboard-wedge mode (rugged Android devices) and the camera
(`BarcodeDetector` with a WASM fallback), reads GS1 barcodes (GTIN, SSCC, batch, expiry, GS1 Digital Link and 2D
codes), queues scans offline with client UUIDs, and resolves conflicts on the server (an idempotent apply with a
review queue for anything that no longer fits, such as a location already emptied).

**Consequences.** The later native app reuses the same API and conflict rules.

## ADR-0007 — AI features are optional and draft-only (2026-11-07)

**Decision.** Every AI feature in `docs/FEATURES.md` §AI is off by default at three levels, runs only through the
suite AI gateway, and drafts for a person: suggested reorder quantities, forecast adjustments, draft purchase
orders, extracted supplier-document data. Nothing places an order, moves stock or changes a plan on model output
alone. Forecasting starts with explainable statistical methods that need no model provider at all.

**Consequences.** Each feature has an evaluation suite and a non-AI path.
