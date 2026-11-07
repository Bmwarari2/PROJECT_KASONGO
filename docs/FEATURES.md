# Feature catalogue — Thapsus ERP

Researched against Oracle NetSuite, SAP S/4HANA Cloud and Business One, Microsoft Dynamics 365 Business Central and
Supply Chain Management, Odoo, Acumatica, Epicor Kinetic, Infor CloudSuite, Sage X3, IFS Cloud, Katana, Cin7,
Unleashed, Fishbowl and MRPeasy (`RESEARCH.md` §1, with which leaders have each feature). **Tier**: Core (needed at
launch of its pack), Advanced (second wave or higher edition), Enterprise (large or regulated customers). **Phase**:
see `PLAN.md`. Everything marked configurable is set in Studio (`suite/STUDIO.md`) without code.

## 1. Item master

| Feature | Tier | Phase |
| --- | --- | --- |
| Item types: stock, non-stock, service, kit, assembly, phantom, charge | Core | 1 |
| Variants and attributes (size and colour matrices) with SKU generation; per-variant GTIN, cost, price, weight | Core | 1 |
| Units of measure per item (purchase, stock, sales, production) with exact conversions and packaging levels (each, inner, case, pallet) | Core | 1 |
| Dual and catch-weight quantities (sell by unit, invoice by weight) | Enterprise | 0 (model), 9 (UI) |
| Kits and bundles exploded at order; assembly items | Core | 1 |
| Alternates and substitutes (sales, purchasing, BOM) with approval | Advanced | 3, 7 |
| GTINs per packaging level with check-digit validation; internal barcodes; customer and supplier part numbers | Core | 1 |
| Lifecycle statuses (draft, active, phase-out, blocked for purchase, sale or production) | Core | 1 |
| Revisions and effectivity dates on items, BOMs and routings | Advanced | 7 |
| Trade attributes: commodity codes per country, origin, preferential origin, dangerous goods, export control | Core / Advanced | 1, 5 |
| Sustainability attributes: packaging composition per level, recycled content, carbon footprint, EUDR commodity flag, substances of concern, battery data | Advanced | 1, 5, 13 |
| Supplier items: part number, pack size, MOQ, lead time, price breaks, preferred supplier | Core | 2 |
| Product information: rich descriptions, images, specifications, translations | Core | 1 |
| Categories and templates with inherited defaults (posting groups, units, tracking) | Core | 1 |
| Lot and serial control, shelf life, storage conditions, retest days | Core | 1 |

## 2. Inventory

| Feature | Tier | Phase |
| --- | --- | --- |
| Multi-site and multi-warehouse, each site in a legal entity | Core | 1 |
| Zones and bins with bin types (receiving, storage, picking, quarantine, shipping); simple or bin-managed per warehouse | Core | 1 |
| Lot tracking with full forward and backward genealogy | Core | 1 |
| Serial tracking with status history | Core | 1 |
| Expiry and best-before, FEFO, retest dates, minimum remaining shelf life on receipt | Core | 1, 4 |
| Inventory statuses separate from location (available, quarantine, blocked, damaged, inspection) | Core | 1 |
| Append-only stock transactions; derived on-hand, allocated, available, in-transit | Core | 1 |
| Adjustments with reason codes and approval above a value threshold | Core | 1 |
| Transfers with in-transit stock | Core | 1 |
| Cycle counting with ABC classes, count plans, blind counts and variance approval | Core | 1, 4 |
| Valuation: FIFO and weighted average per entity | Core | 1 |
| Valuation: standard cost with purchase price, production and revaluation variances | Advanced | 7 |
| Specific identification (serial cost); LIFO for US GAAP only | Advanced | 14 |
| Landed cost (freight, duty, insurance, brokerage) estimated on the PO and actualised | Core | 2 |
| Consignment: supplier-owned stock at our site, our stock at a customer's site | Advanced | 6 |
| Replenishment: reorder point, min–max, safety stock; drafts for approval | Core | 1 |
| Distribution requirements planning between warehouses | Advanced | 10 |
| Soft and hard reservations | Core | 3 |
| Revaluation and cost-adjustment runs | Advanced | 1, 7 |
| Negative-stock policy per site (default refuse) | Core | 1 |
| Ageing, slow-moving and dead-stock analysis | Core | 1 |
| Inventory sub-ledger reconciliation with the general ledger | Core | 1 |

## 3. Warehouse management

| Feature | Tier | Phase |
| --- | --- | --- |
| Receiving against POs and advance shipping notices; blind receiving; tolerances | Core | 2, 4 |
| Quality hold on receipt with sampling and release | Core | 4, 8 |
| Putaway suggestions, then directed putaway by zone, class, capacity and hazard | Core / Advanced | 4 |
| Picking by order and batch; then wave, zone and cluster; pick to cart | Core / Advanced | 4 |
| Pack stations with scan verification and nested containers | Core | 4 |
| Carrier labels, manifests and customs documents through an aggregator | Core | 4 |
| Cartonisation | Enterprise | Later |
| Scanner PWA: hardware wedge scanners and camera; offline queue | Core | 4 |
| GS1 Application Identifier parsing (GTIN, lot, expiry, serial, weight, SSCC) and GS1 Digital Link | Core | 4 |
| GS1-128 and SSCC pallet labels | Core | 4 |
| RFID | Enterprise | Later |
| Cross-docking | Advanced | Later |
| Pick-face replenishment and min–max per bin | Advanced | 4 |
| Labour management, task interleaving, slotting | Enterprise | Later |
| 3PL mode (client-owned stock, storage and handling billing) | Enterprise | Later |
| Dangerous-goods segregation rules | Advanced | 5 |
| Warehouse process configuration (mobile step flows, removal strategies, count policies) | Core | 4 |

## 4. Purchasing and procurement

| Feature | Tier | Phase |
| --- | --- | --- |
| Requisitions (free text, catalogue, from planning) on desktop and phone | Core | 2 |
| Approval rules (amount, category, cost centre, budget), delegation, separation of duties | Core | 2 |
| Requests for quotation, quote comparison and award | Advanced | 2 |
| Blanket and framework agreements with call-offs | Advanced | 2 |
| Purchase orders, change orders, versions, supplier confirmations | Core | 2 |
| Three-way match facts for Finance's payables (PO, receipt, invoice) with tolerances | Core | 2 |
| Supplier portal: acknowledgements, ASNs, schedules, invoice upload, certificate and compliance-reference requests | Advanced | 6 |
| Supplier scorecards (on time in full, quality, price variance) | Advanced | 8 |
| Supplier risk screening against configurable lists (sanctions, forced-labour entity lists); country risk | Advanced | 5 |
| Contracts: price agreements, validity, volume commitments, renewal alerts | Advanced | 2 |
| Incoterms 2020 and estimated landed cost on the PO | Core | 2 |
| Drop-ship and special-order POs from sales orders | Core | 2 |
| Punch-out catalogues (cXML, OCI) | Enterprise | Later |
| Spend analytics | Advanced | 2 |

## 5. Sales order management and pricing

| Feature | Tier | Phase |
| --- | --- | --- |
| Quotes and versions, or quotes from Thapsus CRM | Core | 3 |
| Sales orders with credit holds (from Finance) and compliance holds | Core | 3 |
| Available-to-promise across sites; API for CRM | Core | 3 |
| Capable-to-promise using capacity and lead times | Advanced | 10 |
| Allocation rules (priority, fair share, backorder reprocessing) | Advanced | 3 |
| Backorders, partial shipments, ship-complete | Core | 3 |
| Drop-ship and back-to-back orders | Core | 3 |
| Returns (RMA) with disposition: restock, quarantine, scrap, repair, return to supplier | Core | 3 |
| B2B ordering portal (customer catalogue and prices, reorder, status, documents) | Advanced (Core for wholesale) | 6 |
| Recurring and standing orders | Advanced | 3 |
| Retailer-specific labels and documents | Advanced | 6 |
| Price lists by currency, channel and customer group with effective dates | Core | 3 |
| Customer and contract prices; quantity breaks | Core | 3 |
| Discounts, promotions, coupons | Advanced | 3 |
| Cost-plus pricing and margin floors with approval | Advanced | 3 |
| Customer and supplier rebates with accruals | Enterprise | 6 |
| Chargebacks (US distribution) | Enterprise | 14 |
| Price simulation and mass updates with approval | Advanced | 3 |

## 6. Manufacturing (discrete)

| Feature | Tier | Phase |
| --- | --- | --- |
| Multi-level BOMs with phantoms, versions, effectivity and scrap factors | Core | 7 |
| Routings, operations, work centres, machine and labour rates (standard rates by grade) | Core | 7 |
| Master production schedule | Advanced | 7 |
| MRP with pegging and action messages; planned orders as drafts | Core / Advanced (multi-site) | 7 |
| Production orders: release, kitting, issue, progress, close | Core | 7 |
| Backflushing | Core | 7 |
| Shop-floor kiosk: clock on and off operations, quantities, scrap, downtime, work instructions; skills gating from HR | Core | 7 |
| Capacity planning (infinite load) | Core | 7 |
| Finite scheduling with a Gantt | Advanced | 10 |
| Subcontracted operations | Advanced | 7 |
| Co-products and by-products | Advanced | 7 |
| Engineer-to-order and project manufacturing | Enterprise | Later |
| Configure-to-order product configurator | Advanced | 7 |
| Costing: actual job costing, standard cost roll-up, WIP, variances | Core / Advanced | 7 |
| Disassembly and rework orders | Advanced | 7 |
| Engineering change requests and orders with impact analysis; document attachments | Advanced | 7 |
| Tooling, machine data, OEE and IoT connectors | Enterprise | Later |

## 7. Process manufacturing

| Feature | Tier | Phase |
| --- | --- | --- |
| Formulas and recipes with percentages, scaling, yield and losses | Core for the pack | 9 |
| Batch orders, intermediates, packaging BOMs | Core for the pack | 9 |
| Lot attributes and grades; blending rules | Advanced | 9 |
| Allergens and nutrition per ingredient and recipe; label data (UK and EU food information rules) | Core for the pack | 9 |
| Shelf life, FEFO, quarantine and positive release | Core for the pack | 9 |
| Catch weight | Enterprise | 9 |
| Potency and active-ingredient adjustment | Enterprise | 9 (later in pack) |
| Certificates of analysis | Advanced | 8 |
| Safety data sheets and dangerous goods per formula | Enterprise | 9 (later in pack) |
| Electronic batch records for GxP | Enterprise | Not at launch |

## 8. Quality

| Feature | Tier | Phase |
| --- | --- | --- |
| Inspection plans (receiving, in-process, final) with sampling | Advanced | 8 |
| Specifications and results per lot; out-of-spec handling | Advanced | 8 |
| Non-conformances, deviations, concessions; CAPA | Advanced | 8 |
| Recall and mock recall with timed report | Core | 8 |
| Hold and release with electronic signature and reason | Advanced | 8 |
| Supplier quality and approved supplier list | Advanced | 8 |
| Calibration records | Advanced | 8, 12 |
| Electronic records and signatures designed to 21 CFR Part 11 and EU GMP Annex 11 | Enterprise | 8 |

## 9. Planning

| Feature | Tier | Phase |
| --- | --- | --- |
| Statistical demand forecasting (moving average, exponential smoothing, Croston) with accuracy measures | Advanced | 10 |
| Safety-stock and reorder-point recommendations | Advanced | 10 |
| Distribution requirements planning | Advanced | 10 |
| Finite scheduling (deterministic heuristic) | Advanced | 10 |
| S&OP-lite monthly review | Enterprise | 10 |

## 10. Projects, services, maintenance, field service and rental

| Feature | Tier | Phase |
| --- | --- | --- |
| Projects with WBS, estimates, budgets, commitments | Advanced | 11 |
| Time (from HR or native), expenses (from Finance), materials to projects | Advanced | 11 |
| Resource planning with skills and availability from HR | Advanced | 11 |
| WIP and revenue recognition via Finance | Advanced | 11 |
| Billing: time and materials, milestone, fixed fee, retentions | Advanced | 11 |
| Construction: cost codes, subcontracts, applications for payment, valuations, variations, retentions; CIS via Finance | Advanced | 11 |
| Asset register with hierarchy and criticality, linked to Finance fixed assets and HR's equipment register | Advanced | 12 |
| Preventive maintenance by calendar, meter or condition; statutory inspection schedules as rule-pack data | Advanced | 12 |
| Maintenance work orders with labour, parts and downtime; spares | Advanced | 12 |
| Service contracts, entitlements and SLAs | Advanced | 12 |
| Dispatch board with skills and territories | Advanced | 12 |
| Offline technician PWA (job, parts, photos, signature, checklists); van stock; installed base | Advanced | 12 |
| Rental: availability calendar, contracts, period pricing, deposits, check-out and check-in, inspections, damage, utilisation | Advanced | 12 |

## 11. Shipping, commerce, EDI and multi-entity

| Feature | Tier | Phase |
| --- | --- | --- |
| Parcel carriers through an aggregator (UK, then EU and US); rate shopping; tracking | Core | 4, 13, 14 |
| Customs documents (commercial invoice, CN22/CN23), EORI, commodity codes, origin, Incoterms | Core | 4, 5 |
| Freight transport management | Enterprise | Later |
| Shopify, WooCommerce, Amazon connectors | Core | 6 |
| eBay, BigCommerce, Adobe Commerce connectors | Advanced | Later |
| Point of sale: integrate Shopify POS rather than build one | Advanced | 6 |
| EDI X12 and EDIFACT through an EDI network partner, mappings as templates | Advanced (Core for US and EU retail supply) | 6 |
| Peppol ordering, order agreement and despatch advice | Advanced | 6 |
| Multiple legal entities with shared or entity-specific items | Core | 1 |
| Intercompany orders, transfer prices, events for Finance to post and eliminate | Advanced | 6 |
| Cross-entity fulfilment; consolidated stock visibility | Advanced / Core | 6 / 1 |

## 12. Trade, product and sustainability compliance (rule-pack data)

| Feature | Market | Phase | Date that matters (`RESEARCH.md` §3) |
| --- | --- | --- | --- |
| UK packaging EPR data and returns; Plastic Packaging Tax liability | UK | 5 | In force (PPT £228.82 per tonne from 1 Apr 2026; EPR fees modulated by recyclability from 2026/27) |
| UK deposit return scheme container counts | UK | 5 | From 1 Oct 2027 |
| UK CBAM value counter, emissions data and records | UK | 5 | From 1 Jan 2027; £50,000 threshold; registration by 31 Jan 2028 for 2027 |
| Northern Ireland Intrastat | UK | 5 | In force |
| EU Intrastat (national thresholds as data) | EU | 13 | In force |
| EU CBAM threshold counter (50 tonnes), declarant data, emissions, annual declaration export | EU | 13 | Certificates from 1 Feb 2027; first declaration 30 Sep 2027 |
| EUDR upstream reference numbers per lot, propagation to sales, retention, information-system API | EU | 13 | From 30 Dec 2026 (large and medium); 30 Jun 2027 (micro and small) |
| EU packaging regulation (PPWR) data and declarations | EU | 13 | Applies from 12 Aug 2026 |
| Battery passport data; battery due diligence | EU | 13 | 18 Feb 2027; 18 Aug 2027 |
| Product passport data model with GS1 Digital Link | EU | 13 | Per product delegated acts (first expected 2026–27) |
| Forced Labour Regulation supplier and origin data; product withdrawal | EU | 13 | From 14 Dec 2027 |
| VSME-level sustainability data requests from large customers | EU | 13 | Revised standards from FY2027 |
| US tariff programmes in landed cost (stacking, metal content, refunds, drawback) | US | 14 | In force; de minimis suspended, repealed from 1 Jul 2027 |
| FSMA 204 traceability records and 24-hour spreadsheet | US | 14 | Enforcement not before 20 Jul 2028 |
| UFLPA entity screening and sub-tier mapping | US | 14 | In force |
| REACH, RoHS, WEEE declarations and substance flags | UK, EU | 13 | In force |
| Dangerous goods (ADR, IMDG, IATA) attributes and documents | All | 5 | In force (IMDG 42-24 from 1 Jan 2026) |
| UDI for medical-device suppliers | UK, EU, US | Later | In force |

## 13. Optional AI features (off by default, drafts only)

| Feature | Human step | Phase |
| --- | --- | --- |
| Supplier-document capture (invoices, delivery notes, certificates of analysis, origin, EUDR references) | Low-confidence fields confirmed; nothing posted automatically | 15 |
| Sales-order capture from email and PDF | Order created as a draft; a person releases it | 15 |
| Draft purchase orders from replenishment | Normal PO approval; never sent by the agent | 15 |
| Supplier-email reading with drafted replies | Every change and reply reviewed; auto-send off by default | 15 |
| Forecast and safety-stock explanations (methods are statistical, not AI) | Planner accepts or overrides | 10, 15 |
| Anomaly flags (adjustments, costs, yields, duplicate supplier invoices) | Investigator closes with an outcome | 15 |
| Production scheduling suggestions | Planner publishes; never schedules individuals | 15 |
| Plain-language questions over reports | Read-only; saving as a report is a user action | 15 |
| Item-data enrichment (descriptions, attributes, HS code suggestions marked advisory) | Each suggestion accepted | 15 |
| MCP server with read tools and draft-only write tools; admin roles excluded | Drafts approved in ERP | 15 |
| Predictive maintenance (needs sensor data) | Suggested work order approved | Later |

## 14. Configuration without code (Studio)

Custom fields and objects on every record; layouts per role and status; saved views; approval workflows with
thresholds, delegation and escalation; CEL business rules (for example "block shipment if the lot expires within 30
days for customer group X"); document and label templates (POs, pick lists, delivery notes, GS1 labels, certificates
of analysis); numbering per entity, site and document type; units and conversions; warehouse process flows; posting
profiles (with Finance); approval limits and separation of duties; notifications and webhooks; import mappings
(CSV, Excel, EDI); rule-pack reference data (tariffs, thresholds, CBAM codes, dangerous goods, allergens, packaging
categories); industry solution packs (wholesale, discrete, food and drink, projects and services).

## 15. Platform features buyers expect

Role-based security with field-level rules and separation of duties; append-only audit with "who changed price,
quantity or cost"; attachments in regional storage; dense tables, bulk edit, imports with validation and dry run;
reports, dashboards and schedules; REST API (OpenAPI 3.1), webhooks and events; multi-currency, multi-language,
multi-time-zone; offline-tolerant phone screens; a data-migration workbench; sandboxes with release preview; free
full export (EU Data Act).
