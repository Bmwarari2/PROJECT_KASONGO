# Development plan — Thapsus ERP (PROJECT_KASONGO)

Status: plan for owner approval, 2026-11-07. Scope: `FEATURES.md`. Research and dates: `RESEARCH.md`. Suite context:
`suite/SUITE_PLAN.md` (stages and owner decisions D-1 to D-15), `suite/INTEGRATION.md` (who owns what; the posting
contract with Finance).

## 1. Shape of the plan

- **One core, four industry packs** (owner decision D-3, ADR-0004). Phases build the shared core first, then the
  packs in this order: wholesale and distribution → discrete manufacturing → process manufacturing (food and drink
  first) → projects and services (professional services, field service, construction, rental).
- **Why this order.** The research (`RESEARCH.md` §2.2) shows wholesale has the widest market and its data model is
  reused by every other pack. Construction depends on Finance's depth (CIS, retentions, project accounting), so it
  comes last. Regulated pharma (GxP validation) and a point-of-sale system stay out of scope at launch; the
  electronic-signature design (Phase 8) keeps the GxP door open.
- **Releases.** Each release is sellable on its own: **W1** wholesale (UK), **M1** discrete manufacturing (UK),
  **P1** food and drink (UK), **S1** projects and services (UK), then **EU** and **US** packs.
- **Parallel build** (D-7). Finance's ledger is built at the same time, so ERP posts to a contract-tested mock of
  Finance's accounting-events API from Phase 0. Phase 16 swaps the mock for the live API.
- **Every phase ends** with `pnpm verify` green, docs updated, this file ticked with evidence, and a commit. Nothing is
  ticked without a test or check that proves it, or a HUMAN_TODO entry for a human-only step.

## 2. Phases and suite stages

| Phase | Name | Suite stage | Release |
| --- | --- | --- | --- |
| 0 | Foundations on the platform kit | 0 | — |
| 1 | Items and inventory | 1 | W1 |
| 2 | Purchasing and landed cost | 1 | W1 |
| 3 | Sales orders and pricing | 1 | W1 |
| 4 | Warehouse, scanning and shipping | 2 | W1 |
| 5 | UK trade and packaging compliance | 2 | W1 |
| 6 | Commerce, EDI, B2B portal and intercompany | 2 | W1 |
| 7 | Discrete manufacturing | 2 | M1 |
| 8 | Quality, traceability and electronic signatures | 2 | M1 |
| 9 | Process manufacturing (food and drink first) | 3 | P1 |
| 10 | Planning and scheduling | 3–4 | M1+ |
| 11 | Projects and professional services, construction | 4 | S1 |
| 12 | Maintenance, field service and rental | 4 | S1 |
| 13 | EU pack | 4 | EU |
| 14 | US pack | 4 | US |
| 15 | Optional AI features | 3–4 | Each release |
| 16 | Suite links live | 3 | All |
| 17 | Native app for warehouse and field service | 4 | — |
| 18 | Scale and launch readiness | 2–5, continuous | All |

## 3. Phases

### Phase 0 — Foundations on the platform kit

- Monorepo (`apps/web`, `apps/api`, `apps/worker`, `packages/inventory`, `packages/costing`, `packages/planning`,
  `packages/rules`, `packages/db`) on `@thapsus-suite/*`; `pnpm verify` with every gate in CLAUDE.md.
- Tenancy with forced RLS, the isolation suite, Thapsus ID sign-in, roles and permissions catalogue
  (`erp.<module>.<action>`), audit, outbox, i18n, the suite shell with ERP's accent, Studio wired to ERP records.
- **Quantity and unit library**: exact decimals, per-item precision, unit conversions as exact factors, packaging
  hierarchies; property-based tests.
- **Accounting events**: the outbox writer and the event catalogue (`INTEGRATION.md` §6) with a mock of Finance's API
  built from Finance's published documents; a ledger connector port (Xero, QuickBooks Online, Sage, Business Central,
  file export) with contract-tested mocks.
- OpenTofu cell and global roots from the platform modules; UK staging deployed after the owner approves `COSTS.md`.
- Fictional seed company (a UK wholesaler with two warehouses) and a synthetic mid-market generator (50,000 items,
  300 locations, 5 million stock transactions, 3 legal entities).

**Acceptance:** isolation suite fails on any table without a policy; residency tests for every region pair;
the accounting-events schema is published as AsyncAPI and contract-tested against the mock; seed and generator run
in CI; Lighthouse and axe gates pass on the shell.

### Phase 1 — Items and inventory (W1)

- Item master: types (stock, non-stock, service, kit, assembly, phantom), variants and attributes with SKU
  generation, units and packaging levels, GTINs per level with check-digit validation, customer and supplier part
  numbers, categories with inherited defaults, lifecycle statuses, trade attributes (commodity codes per country,
  origin), packaging composition per packaging level (used in Phase 5), lot and serial flags, shelf life.
- Sites, warehouses, zones and bins (simple or bin-managed per warehouse); inventory statuses (available, quarantine,
  blocked, damaged, inspection) separate from location.
- Append-only stock transactions; derived on-hand, allocated, available, in-transit; lot and serial genealogy.
- Adjustments with reason codes and approval above a value threshold; transfers with in-transit; cycle counts with
  ABC classes, blind counts and variance approval; negative-stock policy per site (default refuse).
- Valuation per entity: FIFO and weighted average (standard cost in Phase 7); cost layers; revaluation; every value
  change emits its accounting event.
- Replenishment suggestions: reorder point, min–max, safety stock (manual), as drafts a buyer approves.
- Reports: stock on hand and value, ageing, slow-moving, movements, valuation reconciliation against the ledger.

**Acceptance:** property tests (on-hand equals the sum of transactions; value equals the sum of open layers); a
recall-style trace returns forward and backward genealogy in under 2 seconds on the synthetic tenant; every value
change produces exactly one accounting event; the nightly reconciliation flags an injected difference.

### Phase 2 — Purchasing and landed cost (W1)

- Requisitions (desktop and phone) with Studio approval rules (amount, category, cost centre, budget check),
  delegation and separation of duties (requester never approves).
- Supplier procurement attributes (approved status, lead times, MOQ, price breaks, catalogues); supplier identity and
  bank details read from Finance when linked (`INTEGRATION.md` §4).
- Purchase orders, change orders and versions, supplier confirmations, Incoterms 2020, blanket orders with call-offs,
  drop-ship and special orders from sales orders.
- Receipts against POs and advance shipping notices, tolerances, quality hold, returns to supplier.
- Received-not-invoiced accrual events; the three-way match facts that Finance's payables use.
- Landed cost: estimated on the PO (freight, duty, insurance, brokerage), allocated by value, weight, volume or
  quantity, trued up when actual charges arrive (inventory or cost of sales).

**Acceptance:** golden tests for landed-cost allocation and true-up; a PO-to-receipt-to-bill flow reconciles to zero
on the received-not-invoiced account against the Finance mock; approval rules are configured in Studio, not code.

### Phase 3 — Sales orders and pricing (W1)

- Quotes (created here, or arriving from Thapsus CRM), sales orders, holds (credit hold read from Finance; compliance
  holds), available-to-promise across sites, soft and hard allocation, backorders, partial and ship-complete,
  drop-ship and back-to-back orders, recurring orders.
- Returns (RMA) with disposition: restock, quarantine, scrap, repair, return to supplier.
- Pricing engine: price lists by currency, channel and customer group with effective dates; customer and contract
  prices; quantity breaks; line and order discounts; promotions; margin floors with approval below floor; a price
  simulation and mass update with approval.
- Billing events: on shipment, an invoice request to Finance (or the ledger connector), with cost-of-sales events.
- A synchronous price and availability API for CRM.

**Acceptance:** pricing golden tests (precedence, effective dates, currency, rounding in minor units); ATP tests
across sites with allocations and transfers; a quote-to-cash run against the Finance mock produces matching revenue
and cost-of-sales events.

### Phase 4 — Warehouse, scanning and shipping (W1)

- Scanner-first PWA screens (ADR-0006): keyboard-wedge and camera scanning; GS1 Application Identifier parsing (GTIN,
  lot, expiry, serial, weight, SSCC) and GS1 Digital Link; offline queue with client UUIDs and server-side conflict
  review.
- Receiving and putaway (suggested, then directed by zone, class and capacity); picking by order and batch, then wave,
  zone and cluster; pack stations with scan verification and nested containers; pick-face replenishment.
- Labels and documents: GS1-128 and SSCC pallet labels from the tenant's GS1 company prefix, delivery notes, packing
  lists, commercial invoices and CN22/CN23, all as Studio templates.
- Shipping through a carrier aggregator (UK first: Royal Mail, DPD, Evri, DHL, UPS, FedEx), rate shopping, tracking
  back to the order and to CRM.
- Warehouse process configuration in Studio (mobile step flows, removal strategies FIFO and FEFO, count policies).

**Acceptance:** e2e on a phone viewport with a simulated wedge scanner; an offline pick of 200 lines replays exactly
once; labels validate against GS1 check digits; WCAG 2.2 AA with 44 px targets on every scanner screen.

### Phase 5 — UK trade and packaging compliance (W1)

Rule-pack data, effective-dated with sources (`RESEARCH.md` §3):
- **Packaging**: UK packaging EPR data per item and packaging level (material, weight, recycled content, recyclability
  rating, household or not, nation of sale); period tonnage from shipments and receipts; Plastic Packaging Tax
  liability for manufactured or imported plastic components below 30% recycled content; drinks deposit return scheme
  container counts (scheme starts 1 Oct 2027).
- **UK CBAM** (from 1 Jan 2027): flags on CBAM goods by commodity code, a rolling 12-month value counter per entity
  against the £50,000 threshold with the 30-day forward look from open POs, and emissions data per supplier
  installation.
- **Customs data**: commodity codes per destination, origin and preferential-origin evidence (UK–EU trade agreement),
  EORI per entity, Incoterms; broker hand-off files (Thapsus does not file declarations).
- **Intrastat for Northern Ireland** movements (thresholds as data).
- **Dangerous goods** attributes (UN number, class, packing group, limited quantity) and shipping documents.
- **Supplier risk screening** against configurable reference lists (sanctions, forced-labour entity lists) as data.

**Acceptance:** golden tests per pack value with its source URL and checked date; a test fails on any threshold or
rate literal in code; a packaging return for a fictional producer reproduces a hand-calculated example.

### Phase 6 — Commerce, EDI, B2B portal and intercompany (W1 complete)

- Connectors: Shopify (orders, stock, products, prices, fulfilments, refunds), WooCommerce, Amazon (SP-API); eBay,
  BigCommerce and Adobe Commerce later. Each connector listed in SUBPROCESSORS before it is built.
- EDI through an EDI network partner: X12 (850, 855, 856, 810, 846) and EDIFACT (ORDERS, ORDRSP, DESADV, INVOIC,
  INVRPT) with mappings as Studio templates; Peppol ordering and despatch advice through the suite's Peppol partner.
- B2B ordering portal (PWA): customer catalogue and prices, reorder, order status, documents.
- Rebates (customer and supplier) with accruals as accounting events.
- Intercompany: mirrored purchase and sales orders between entities, transfer prices, intercompany events for
  Finance to post and eliminate.
- Data-migration workbench: staged import from spreadsheets and from Cin7, Unleashed, Katana and Business Central
  exports, with validation, dry run and reconciliation reports (the research's top cause of failed ERP projects).

**Release W1 gate:** a design-partner wholesaler runs a month of fictional operations end to end in staging; every
acceptance criterion above holds; HUMAN_TODO items for carrier, EDI and marketplace accounts are done or marked.

### Phase 7 — Discrete manufacturing (M1)

- Multi-level BOMs (phantoms, versions, effectivity, scrap), routings, operations and work centres with machine and
  labour rates (standard rates by grade, never individual pay; `RESEARCH.md` §5.3).
- Production orders: release, kitting, issue, backflush, progress, scrap, close; disassembly and rework orders;
  co-products and by-products; subcontracted operations.
- MRP (single site, then multi-site) with pegging and action messages, producing **draft** planned orders for approval;
  MPS; infinite capacity load.
- Shop-floor kiosk (PWA): clock on and off operations, quantities, scrap, downtime, work instructions; job time
  reconciled with Thapsus-HR attendance when linked; operations that need a skill or certificate refuse a worker
  without a valid one (read from HR).
- Costing: actual job costing, standard cost roll-up with versions, production variances; WIP accounting events.
- Configure-to-order product configurator (rules generate BOM, routing and price) and engineering change orders
  with revisions and where-used impact.

**Acceptance:** MRP golden scenarios (multi-level, lead-time offsets, lot sizing, safety stock); variance golden
tests; WIP rolls to zero on order close; kiosk works offline for a shift and reconciles.

### Phase 8 — Quality, traceability and electronic signatures (M1 complete)

- Inspection plans (receiving, in-process, final) with sampling; specifications and results per lot; holds and
  release; non-conformances, deviations and concessions; CAPA; supplier quality and approved supplier list;
  calibration records.
- Certificates of analysis (inbound captured against specification; outbound generated).
- Recall and mock recall: trace, affected customers, stock freeze in one action, with a timed test report.
- Electronic signatures designed to 21 CFR Part 11 and EU GMP Annex 11: re-authentication, meaning, signer and time,
  link to the exact record version; reason-for-change prompts; configuration change control. Offered as an option;
  full GxP validation packs are not in scope at launch.

**Release M1 gate:** a design-partner manufacturer runs fictional orders end to end; a mock recall completes inside
the configured limit on the synthetic tenant.

### Phase 9 — Process manufacturing, food and drink first (P1)

- Formulas and recipes with percentages, scaling, yield and losses; batch orders; intermediates; packaging BOMs.
- Lot attributes and grades; FEFO and minimum remaining shelf life on receipt and dispatch; positive release.
- Allergens (the 14 regulated allergens) and nutrition per ingredient and recipe; label data for UK and EU food
  information rules.
- Catch weight (sell by unit, invoice by weight) on the quantity model designed in Phase 0.
- Retailer requirements: GS1 labels, EDI (Phase 6), timed traceability tests (BRCGS and ISO 22000 evidence).
- Chemicals and cosmetics follow later in this pack: potency, safety data sheets, product information files.

**Release P1 gate:** a design-partner food producer runs fictional batches; allergen and recall tests pass.

### Phase 10 — Planning and scheduling

- Statistical demand forecasting (moving average, exponential smoothing with seasonality, Croston for intermittent
  demand) with accuracy measures and planner overrides recorded with reasons.
- Safety-stock and reorder-point recommendations from service-level targets; distribution requirements planning
  between warehouses.
- Finite-capacity scheduling with a deterministic heuristic and a drag-and-drop Gantt; never schedules individual
  people by AI (`RESEARCH.md` §3.20).
- S&OP-lite: one monthly demand and supply review screen.

**Acceptance:** forecast methods match reference implementations on public test series; schedule respects capacity
and calendars in golden scenarios; a planning run for the synthetic tenant completes within its benchmark.

### Phase 11 — Projects and professional services, construction (S1)

- Projects and WBS, estimates and budgets, commitments, time (from Thapsus-HR when it is the owner, otherwise native
  timesheets), expenses (from Finance), materials from stock; resource planning using skills and availability from HR.
- WIP and revenue recognition via accounting events to Finance; billing by time and materials, milestones, fixed fee
  and retentions, invoiced through Finance.
- Construction: cost codes, subcontracts, applications for payment and valuations, variations (change orders),
  retentions, plant usage; CIS deductions handled in Finance.

**Acceptance:** project P&L reconciles with Finance; golden tests for each billing method and retention release.

### Phase 12 — Maintenance, field service and rental (S1 complete)

- Maintenance: asset register with hierarchy (linked to Finance fixed assets and HR's equipment register by one
  shared asset id), preventive schedules by calendar, meter or condition, statutory inspection schedules as rule-pack
  data (for example LOLER six-monthly examinations of equipment for lifting people), work orders with labour, parts and
  downtime, spares on the inventory engine.
- Field service: contracts, entitlements and SLAs; dispatch board matching skills and territories (skills from HR);
  offline technician PWA (job, parts, photos, signature, checklists); van stock as locations; installed base.
- Rental: availability calendar, rental contracts with period pricing and deposits, check-out and check-in, inspection
  between hires, damage charges, utilisation.

**Release S1 gate:** design partners in services and construction run fictional projects; field-service PWA passes
the offline test.

### Phase 13 — EU pack

Ready for EU customers on the obligations already in force by then (`RESEARCH.md` §3): EU Intrastat with national
thresholds as data; EU CBAM (50-tonne annual threshold counter, declarant data, emissions per installation, annual
declaration export); EUDR (commodity flags, upstream due-diligence reference numbers per lot, propagation to sales
documents, five-year retention, information-system API); packaging regulation (PPWR) data; battery passport data
(from 18 Feb 2027); a versioned product-passport data model with GS1 Digital Link carriers; Forced Labour Regulation
supplier and origin data (from 14 Dec 2027); VSME-level sustainability data requests from customers; EU languages
required by the first EU customers.

### Phase 14 — US pack

Tariff programmes as data (HTS and Chapter 99 codes, stacking and exclusions, metal content, country of origin) in
landed cost, with duty-paid tracking for refunds and drawback; FSMA 204 Key Data Elements for each Critical Tracking
Event and the 24-hour sortable spreadsheet (enforcement not before 20 Jul 2028); UFLPA entity screening and sub-tier
mapping; US carriers (UPS, FedEx, USPS); US units and date formats; sales tax through Finance's tax engine.

### Phase 15 — Optional AI features

Off by default, through the suite AI gateway, drafts only (`suite/AI.md`, ADR-0007): supplier-document capture;
sales-order capture from email and PDF; draft purchase orders from replenishment; supplier-email reading with drafted
replies (never auto-sent by default); forecast and safety-stock explanations; anomaly flags; plain-language questions
over reports; item-data enrichment (HS code suggestions marked advisory); an MCP server with read and draft-only tools.
Each feature ships with its evaluation suite and non-AI fallback.

### Phase 16 — Suite links live

Finance: replace the mock with the live accounting-events API; credit checks; supplier and customer financial fields.
CRM: catalogue, prices and availability to CRM; quote to order; status back. HR: workers, skills and certificates,
attendance and job-time reconciliation. Care (UK only): requisitions for consumables and catering, stock at homes,
maintenance work orders (medicines stock never). All per `suite/INTEGRATION.md` with its test list.

### Phase 17 — Native app for warehouse and field service

Expo app reusing Thapsus Care's offline stack and `@thapsus-suite/ui-native`, for heavy offline use; same API and
conflict rules as the PWA (D-6).

### Phase 18 — Scale and launch readiness

Load tests against the mid-market targets (500 concurrent users per tenant; 50,000 order lines a day; MRP for 100,000
item-locations within 10 minutes; p95 under 300 ms for common reads); threat model; ASVS L2 review; penetration test;
accessibility audit; restore and zone-failure drills; staging in each region before its production cell; runbooks.

## 4. Dependencies

| Needs | From | By phase |
| --- | --- | --- |
| Platform kit packages (core, db, auth, Studio, shell) | `PROJECT_ATLAS` | 0 |
| Finance accounting-events API (mock first, live later) | Finance Phase 1 (mock), Finance Stage 3 (live) | 0 / 16 |
| Customer and supplier financial fields | Finance | 2–3 (mock), 16 |
| Quote acceptance, catalogue consumers | CRM | 16 |
| Workers, skills, attendance | Thapsus-HR partner scopes (`PROJECT_KAREN/docs/SUITE_INTEGRATION_PLAN.md` S.5) | 7 (mock), 16 |
| Peppol partner | Finance | 6 |

## 5. Risks specific to ERP

| Risk | Mitigation |
| --- | --- |
| Breadth of four industries | Core first; packs released one by one with their own gates; design partners per pack |
| Inventory value drifting from the ledger | Events in the same transaction; nightly reconciliation; property tests |
| Data migration failures (the main cause of ERP failure in the research) | Migration workbench in Phase 6; dry runs and reconciliation reports; partner playbooks |
| Regulation changing under us (CBAM extension, EUDR scope, US tariffs) | Every value is effective-dated rule-pack data with a source; a quarterly re-check per pack |
| Offline conflicts on the warehouse floor | Client UUIDs, idempotent apply, a review queue, tests with replay |
