# Research — Thapsus ERP

> Research dossier prepared on 2026-11-07 for the plan in `PLAN.md` and `FEATURES.md`. Every regulatory fact carries its
> source and status (in force, adopted with a date, proposed, industry, unverified). Facts are re-checked when the matching phase
> starts; anything marked UNVERIFIED must be checked against the primary source before it becomes rule-pack data.
> Where this dossier and the plan differ, the plan records the reason (for example, the owner chose all four industries, D-3,
> where §2.2 recommends fewer at launch).


- **Date:** 7 November 2026
- **Prepared for:** Thapsus product planning (KASONGO ERP, alongside MULLAH finance, BOSSMAN CRM, Thapsus-HR and Thapsus Care)
- **Method:** web search (standard and extended) and direct reads of official pages (EUR-Lex, European Commission, GOV.UK, legislation.gov.uk, FDA, Federal Register, CBP, Microsoft Learn, vendor pricing pages). Where only secondary sources (law firms, consultancies, vendor blogs) were available, this is stated. The web-search budget for this session ran out near the end (see "Things I could not verify").
- **Status legend used for every regulatory fact:**
  - **IN FORCE** — law that applies now.
  - **ADOPTED, APPLIES FROM <date>** — law adopted but obligations not yet applying.
  - **PROPOSED** — Commission/government proposal or draft not yet law.
  - **INDUSTRY** — voluntary standard or industry milestone, not law.
  - **UNVERIFIED** — could not confirm against a primary or reliable source.
- **Feature tier legend:** **Core** = needed at launch; **Advanced** = second wave / higher edition; **Enterprise** = large or regulated customers.
- **Competitor abbreviations:** NS = Oracle NetSuite; S4 = SAP S/4HANA Cloud Public Edition; B1 = SAP Business One; BC = Microsoft Dynamics 365 Business Central; SCM = Dynamics 365 Supply Chain Management; OD = Odoo; AC = Acumatica; EP = Epicor Kinetic; IN = Infor CloudSuite Industrial (SyteLine) and, where noted, Infor M3/CloudSuite Food & Beverage; X3 = Sage X3; IFS = IFS Cloud; KT = Katana; C7 = Cin7; UL = Unleashed; FB = Fishbowl; MR = MRPeasy.

---

## 0. Executive summary

1. **The regulatory calendar is the strongest buying trigger for a new ERP in 2026–2028.** Dated obligations that need item-, lot- or shipment-level data an ERP owns: EU PPWR (applies 12 Aug 2026), EUDR (30 Dec 2026 for large/medium operators; 30 Jun 2027 micro/small), EU CBAM certificate sales (1 Feb 2027) and first annual declaration (30 Sep 2027), UK CBAM (1 Jan 2027), EU battery passport (18 Feb 2027), battery due diligence (18 Aug 2027), UK deposit return scheme (1 Oct 2027), EU Forced Labour Regulation (14 Dec 2027), FSMA 204 enforcement (not before 20 Jul 2028), CSDDD (26 Jul 2029). An ERP that ships "compliance data on the item, lot and import line" from day one has a clear story.
2. **EU CBAM's 50-tonne annual de minimis is real and in force** (Regulation (EU) 2025/2083, published Oct 2025): the definitive period started 1 Jan 2026; certificate sales start 1 Feb 2027; first annual declaration 30 Sep 2027. A downstream extension to about 180 steel/aluminium-intensive products from 1 Jan 2028 is still in trilogue (PROPOSED).
3. **UK CBAM is legislated** (Finance Act 2026 Part 5; SIs 2026/809 and 2026/830): starts 1 Jan 2027, £50,000 12-month value threshold (not the EU's mass test), registration opens 1 Jan 2028 with a 31 Jan 2028 deadline for 2027 triggers.
4. **EUDR was amended again in December 2025 (Regulation (EU) 2025/2650)** and the Commission's May 2026 review explicitly ruled out a further delay. Downstream operators and traders no longer file their own due diligence statements; they must collect and keep upstream reference numbers. A delegated act of 13 Jul 2026 changes product scope (newly added products from 30 Dec 2027; removals such as leather and some rubber articles), subject to Parliament/Council scrutiny.
5. **Omnibus I is law** (Directive (EU) 2026/470, OJ 26 Feb 2026, in force 18 Mar 2026): CSRD now only for EU companies with >1,000 employees and >€450m turnover; CSDDD only >5,000 employees and >€1.5bn, applying from 26 Jul 2029. Most Thapsus mid-market customers fall out of CSRD scope but will receive **value-chain data requests capped at the voluntary standard (VSME)** — an ERP feature, not a reporting obligation.
6. **US tariffs changed basis in 2026:** the Supreme Court struck down IEEPA tariffs on 20 Feb 2026 (Learning Resources v. Trump, 6–3); the replacement 10% Section 122 surcharge expired 24 Jul 2026; Section 301 "forced labour" tariffs and expanded Section 232 duties (metals at 50% with UK reductions, semiconductors, trucks, timber, pharma) now dominate; the $800 de minimis is suspended by CBP rule (June 2026) and statutorily repealed from 1 Jul 2027. Landed cost needs stacking rules by HTS Chapter 99 code, component origin and refund tracking — a differentiator few SMB tools handle.
7. **FSMA 204:** the July 2028 date is real for enforcement (Congress directed FDA not to enforce before 20 Jul 2028 and FDA says it will comply), but I found **no final rule** codifying the extension — FDA's page (updated 4 Nov 2026) still describes it as proposed.
8. **AI in ERP has moved to "agents that draft, humans approve".** Shipped examples: Business Central Sales Order Agent and Payables Agent (GA, 2026 wave 1); D365 SCM Supplier Communications/Procurement Agent (production-ready preview, auto-send off by default); NetSuite AI Connector Service (hosted MCP server respecting role permissions, Administrator role blocked); Acumatica anomaly detection on any inquiry; Epicor Prism (18+ agents in UK/EU, MCP); IFS Loops digital workers; Odoo 19 AI agents and MCP (19.4). An MCP server per region plus "draft-only" agents is now table stakes for 2027.
9. **Vertical recommendation:** enter with (1) **wholesale distribution and multichannel product brands**, (2) **light discrete / assemble- and make-to-order manufacturing** (businesses outgrowing Katana, MRPeasy, Unleashed, Cin7 plus Xero/QuickBooks), then (3) **food and beverage (process-lite)** within 12–18 months. These share one data model, are underserved in UK mid-market cloud, and are where the 2026–2028 regulation (PPWR/pEPR, EUDR, FSMA 204, CBAM, UFLPA/FLR) bites hardest. Defer construction, pharma (GxP validation), rental and retail POS.
10. **Implementation risk is the market's pain point:** Gartner forecasts that by 2027 more than 70% of recently implemented ERP initiatives will fail to fully meet their original business goals; Panorama's 2026 ERP Report found more than a quarter of projects over budget, chiefly from "fatal misfits" found late. No-code configuration, industry templates and data-migration tooling are commercial differentiators, not nice-to-haves.

**Surprises:** EU REACH full revision was abandoned (April 2026) in favour of annex amendments; EU GMP Annex 11/Chapter 4 revisions and the new AI Annex 22 were still not final in autumn 2026, and draft Annex 22 bars generative AI from critical GMP uses; UK Intrastat now applies only to Northern Ireland movements; Germany raised its Intrastat arrivals threshold to €3m in 2025 so only 2.7% of German importers still report; the €3 EU duty on low-value parcels started 1 Jul 2026; ISO 9001:2026 was published on 16 Sep 2026.

---

## 1. Feature catalogue benchmarked against leaders

### 1.0 The competitive set at a glance

| Vendor / product | Typical segment | Delivery | Strengths relevant to KASONGO | Notes |
|---|---|---|---|---|
| Oracle NetSuite (NS) | SMB to upper mid-market, multi-entity | Multi-tenant SaaS | OneWorld multi-subsidiary, wholesale distribution, eCommerce (SuiteCommerce), SuiteCloud platform, AI Connector (MCP) | Quote-based; heavy partner ecosystem (SuiteApps) |
| SAP S/4HANA Cloud Public Edition (S4) | Upper mid-market to enterprise | SaaS (GROW with SAP) | Breadth, Universal Journal, EWM, QM, PP/DS, Joule agents, clean-core extensibility | Fit-to-standard methodology |
| SAP Business One (B1) | Small to lower mid-market | On-prem / partner-hosted | Breadth for price, add-on ecosystem (e.g. WMS, food) | Not multi-tenant SaaS |
| Microsoft Dynamics 365 Business Central (BC) | SMB to lower mid-market | SaaS (Microsoft) | Large UK/EU partner channel, AppSource extensions, Shopify connector, Sales Order Agent | Essentials $80, Premium $110 per user/month (US list) |
| Dynamics 365 Supply Chain Management (SCM) | Upper mid-market / enterprise | SaaS | Advanced WMS, process manufacturing, TMS, planning optimisation | $210 per user/month, 20-seat minimum |
| Odoo (OD) | Micro to mid-market | SaaS / Odoo.sh / on-prem | Breadth of apps (MRP, PLM, Quality, Maintenance, Rental, Field Service, POS, eCommerce), Studio, low price | Open-core; Odoo 19 (Sept 2025) AI agents |
| Acumatica (AC) | Mid-market | SaaS / private cloud | Manufacturing and distribution editions, construction edition, APS, configurator, unlimited users | Resource-based pricing |
| Epicor Kinetic (EP) | Discrete manufacturing mid-market | SaaS / on-prem | Job shop / make-to-order, MES, APS, CPQ, Prism AI agents | Strong in US discrete |
| Infor CloudSuite Industrial (IN) | Discrete / configure-to-order mid-market | SaaS (AWS) | CPQ, APS, Factory Track (MES/WMS) | Infor M3 covers process / F&B |
| Sage X3 (X3) | Mid-market process and distribution (UK, FR, US) | SaaS / on-prem | Lot, potency, quality, F&B and chemicals | Strong UK/FR presence |
| IFS Cloud (IFS) | Upper mid-market / enterprise, asset-heavy | SaaS / on-prem | EAM, field service, project-based manufacturing, IFS Loops agents | Leader in service/asset industries |
| Katana (KT) | Small manufacturers / DTC makers | SaaS | Shopify-first MRP, simple shop floor app | Free (≤30 SKUs) and quote-based Advantage |
| Cin7 Core / Omni (C7) | Small to lower mid-market product sellers | SaaS | Multichannel inventory, integrations, B2B/POS/ForesightAI add-ons | $349–$1,199/month (Core) |
| Unleashed (UL) | Small manufacturers / wholesalers (NZ, UK, AU, US) | SaaS | Batch/serial, B2B store, Xero integration | $99–$729/month list |
| Fishbowl (FB) | Small manufacturers / warehouses (US), QuickBooks users | Desktop + cloud | QuickBooks companion inventory/MRP | Quote-based |
| MRPeasy (MR) | Small manufacturers (10–200 staff) | SaaS | Surprisingly complete MRP/APS-lite, transparent pricing | $49–$149 per user/month |

Sources: vendor product and pricing pages listed in section 7; [Microsoft BC pricing](https://www.microsoft.com/en-us/dynamics-365/products/business-central/pricing); [Microsoft SCM pricing](https://www.microsoft.com/en-us/dynamics-365/products/supply-chain-management/pricing); [Odoo pricing](https://www.odoo.com/pricing); [Acumatica pricing](https://www.acumatica.com/pricing/); [MRPeasy pricing](https://www.mrpeasy.com/pricing/); [Cin7 pricing](https://www.cin7.com/pricing/); [Unleashed pricing](https://www.unleashedsoftware.com/pricing); [Katana pricing](https://katanamrp.com/pricing/).

> Caveat on attributions in the tables below: "leaders with it" reflects vendor documentation and product knowledge; individual attributions were spot-checked, not exhaustively verified, and many mid-market gaps are filled by marketplace add-ons (AppSource, SuiteApps, Odoo Apps). Treat a missing vendor as "not native or not confirmed", not "impossible".

### 1.1 Item / product master

| Feature | Tier | Leaders with it | Notes for KASONGO |
|---|---|---|---|
| Item types: stock, non-stock, service, kit, assembly, phantom, charge | Core | All | One `item` table with typed behaviour; service items needed for field service and projects |
| Variants and attributes (size/colour matrices, attribute-driven SKU generation) | Core | NS (matrix items), BC (variants), OD, AC (matrix items), KT, C7, S4, SCM (product dimensions) | Generate variant SKUs from attribute sets; per-variant GTIN, cost, price, weight |
| Units of measure with per-item conversions (purchase, stock, sales, production), decimal precision, packaging hierarchy (each → inner → case → pallet) | Core | All | Store quantities as exact decimals with a base UoM; conversions as rational factors; never floats |
| Dual / catch-weight UoM (sell by each, invoice by kg) | Enterprise (F&B vertical) | SCM, S4, IFS, Infor M3; mid-market mostly via add-ons | Design the quantity model to hold a secondary quantity per transaction line from day one even if UI ships later |
| Kits / bundles (explode at order) and assembly BOMs (assemble to stock/order) | Core | NS, BC, OD, AC, KT, C7, UL, MR | Kits must allocate components for ATP |
| Alternates / substitutes (sales substitution, purchasing alternates, BOM alternates) | Advanced | BC (item substitutions), S4, SCM, OD (alternative products), X3 | Rule: substitute only with approval when customer-specific |
| GTIN and barcodes per item and per UoM/package level (GTIN-8/12/13/14), internal barcodes, customer/supplier part numbers | Core | All | Validate GTIN check digits; one item may have many GTINs (one per packaging level) |
| Item lifecycle status (draft, active, phase-out, blocked for purchase/sale/production) | Core | All majors | Status gates enforced by policy, configurable per tenant |
| Revisions and effectivity dates on item, BOM and routing | Advanced | EP, IN, AC (ECC), OD (PLM), MR (Enterprise), S4, SCM | Effective-dated rows (`valid_from`/`valid_to`) fit the Thapsus pattern |
| Trade and compliance attributes: HS/CN/HTS code per country, country of origin, preferential origin, dangerous goods (UN number, class, packing group), export control classification | Core (HS, origin), Advanced (DG, export control) | S4, SCM, X3, IFS, NS (partial), BC (tariff no.) | Needed for Intrastat, CBAM, US tariff stacking, customs, ADR/IMDG |
| Sustainability attributes: packaging composition (material, weight, recyclability rating), carbon footprint, recycled content, EUDR commodity flag, REACH SVHC flags, battery data | Advanced | S4 (Sustainability Footprint Management), SCM (via Microsoft Sustainability tools); few mid-market natively | Differentiator — see 1.21 and section 3 |
| Supplier items: vendor part no., pack size, MOQ, lead time, price breaks, preferred supplier | Core | All | Feeds replenishment and RFQ |
| Product information (rich descriptions, images, multilingual text, specs) — "PIM-lite" | Core / Advanced | OD, NS, C7, AC (commerce), S4 | i18n catalogues already a Thapsus rule |
| Item templates / categories with inherited defaults (posting groups, UoM, tracking) | Core | All | Category-driven defaults reduce setup errors |
| Lot/serial control flags, shelf life, storage conditions, retest days | Core | All | Drives receiving and picking rules |

### 1.2 Inventory

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Multi-warehouse / multi-site, per-site parameters | Core | All | Site belongs to a legal entity (for intercompany) |
| Locations / bins / zones, bin types (receiving, storage, picking, quarantine, shipping) | Core | All majors; SMB tools vary | Bins optional per warehouse ("simple" vs "directed" mode, as BC and OD do) |
| Lot/batch tracking with genealogy | Core | All | Full forward/backward trace in one query; needed for recalls, FSMA 204, EUDR |
| Serial tracking | Core | All | Serial status history |
| Expiry, best-before, FEFO picking, retest dates, shelf-life on receipt (minimum remaining life) | Core for F&B; Core generally | BC (FEFO), OD (FEFO removal), NS, AC, X3, S4, SCM, MR (Professional), UL, C7 | FEFO as a removal strategy setting |
| Inventory statuses (available, quarantine, blocked, damaged, in inspection) | Core | SCM, S4, X3, IFS, OD (via locations), BC (via bins/blocked) | Status is separate from location |
| Cycle counting with ABC classes, count plans, blind counts, variance approval | Core | All majors | Mobile counting; approval thresholds by value |
| Valuation: FIFO, weighted (moving) average | Core | All | Per item or per category; per legal entity |
| Valuation: standard cost with purchase price, production and revaluation variances | Advanced | BC, NS, OD, AC, S4, SCM, X3, EP, IN | Variance postings go to MULLAH (section 5) |
| Specific identification (serial cost), LIFO (US only) | Advanced | BC (specific, LIFO), NS (LIFO), AC (specific) | LIFO not permitted under IFRS; US GAAP only |
| Landed cost (freight, duty, insurance, brokerage) allocated by value/weight/volume/quantity, estimated at PO then actualised | Core (import-heavy UK/EU/US customers) | BC (item charges), NS, OD, AC, X3, S4, SCM, C7 | Must support US tariff stacking and duty refunds (section 3.13) |
| Consignment: vendor-owned stock at our site; our stock at customer site | Advanced | S4, SCM, IFS, OD (owner on stock) | Ownership dimension on stock quant |
| Transfers between sites with in-transit stock and transfer pricing | Core | All | Intercompany transfers handled in 1.17 |
| Replenishment: reorder point, min–max, safety stock, lead-time based, multi-warehouse (DRP) | Core (ROP/min–max), Advanced (DRP) | All; DRP in SCM, S4, NS (Supply Planning), EP | Suggestions → approved POs/transfers (draft-first, matches AI pattern) |
| Reservations / soft and hard allocation | Core | All majors | Needed for ATP and priority allocation |
| Adjustments with reason codes, approval above threshold, audit | Core | All | Append-only stock ledger (`stock_move` events) |
| Revaluation and cost adjustment runs | Advanced | BC (Adjust Cost – Item Entries), NS, S4 (Material Ledger), OD | Batch job; posts to ledger |
| Negative-stock policy per site | Core | All | Default: disallow |
| Inventory ageing, slow-moving and dead-stock analysis | Core | All majors | Feeds AI optimisation later |

### 1.3 Warehouse management (WMS)

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Receiving against PO / advance shipping notice (ASN), blind receiving, over/under tolerance | Core | All majors | ASN via EDI 856 / DESADV / Peppol Despatch Advice |
| Quality hold on receipt, sampling, release | Core (simple), Advanced (inspection plans) | SCM, S4, X3, OD (Quality), NS (QM SuiteApp), MR | Links to section 1.9 |
| Putaway: simple suggestions → directed rules (by zone, item class, capacity, hazard class) | Core (simple), Advanced (directed) | SCM, S4 EWM, NS WMS, OD (putaway rules), BC (directed put-away), AC | |
| Picking: single-order, batch, wave, zone, cluster; pick-to-cart | Core (order, batch), Advanced (wave, zone, cluster) | SCM, S4 EWM, NS WMS, OD (batch/wave transfers), AC, BC (basic), C7 (advanced WMS on Advanced plan) | |
| Packing station, pack verification by scan, packages and nested containers | Core | All majors | |
| Shipping: carrier labels, manifests, customs documents | Core (via aggregator) | OD, NS, AC, SCM, C7 | See 1.16 |
| Cartonisation (box selection by dimensions/weight) | Enterprise | SCM (container packing), S4 EWM; others via add-ons | Phase 3 |
| Mobile barcode scanning on Android/iOS and rugged devices; PWA | Core | All majors (BC mobile/partner apps, NS WMS mobile, OD Barcode, SCM Warehouse Management mobile app, AC, MR) | Thapsus ships PWAs (no native apps) — must work with hardware scanner keyboard wedge and camera scanning |
| GS1-128 / SSCC pallet labels, GS1 DataMatrix and QR (GS1 Digital Link) parsing | Core for retail-facing distribution | SCM, S4 natively; most mid-market via add-ons | Parse GS1 Application Identifiers (01 GTIN, 10 lot, 17 expiry, 21 serial, 00 SSCC) on every scan — cheap differentiator |
| RFID | Enterprise | S4 EWM, SCM (partner), IFS | Later |
| Cross-docking | Advanced | SCM, S4 EWM | |
| Pick-face replenishment, min/max per bin | Advanced | SCM, S4, NS WMS, BC | |
| Labour management, task interleaving, slotting | Enterprise | SCM, S4 EWM | Labour comes from Thapsus-HR |
| 3PL mode: client-owned stock, storage and handling billing | Enterprise / vertical | Specialist WMS; SCM/NS via partners | Option for distribution vertical |
| Dock and yard scheduling | Enterprise | SCM, S4 | Later |
| Dangerous-goods segregation and storage rules | Advanced | S4, SCM, IFS | Link to DG item attributes |

### 1.4 Purchasing and procurement

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Purchase requisitions (free text, catalogue, from planning) | Core | All majors | Care homes need simple requisitions from mobile |
| Approval workflows (amount, category, cost centre, budget check), delegation and out-of-office | Core | All | No-code rules engine (section 6) |
| RFQ / sourcing events, alternative quotes comparison, award | Advanced | OD (alternative RFQs, comparison screen in 19.1), S4 (Bid Analysis Agent), SCM, NS, AC | |
| Blanket / framework agreements, scheduling agreements, call-offs | Advanced | BC (blanket orders), OD (blanket agreements), NS, S4, SCM | Care groups buy on frameworks |
| Purchase orders, change orders, confirmations, revisions | Core | All | Versioned; supplier confirmation status |
| Three-way match handoff to AP (PO–receipt–invoice) with tolerances | Core | All (BC Payables Agent automates matching) | AP itself lives in MULLAH; ERP supplies PO and receipt facts |
| Supplier portal: PO acknowledgement, ASN, delivery schedule, invoice upload, document requests (certificates, EUDR references) | Advanced | OD (portal), S4/Ariba, SCM (vendor collaboration, Supplier Engagement preview Aug 2026), IFS, NS (partial) | Data collection for EUDR, CBAM emissions, FLR due diligence |
| Supplier scorecards (on-time-in-full, quality PPM, price variance, responsiveness) | Advanced | S4, SCM, IFS, EP, NS (reports) | |
| Supplier risk: sanctions/denied-party screening, financial, ESG, forced-labour (UFLPA entity list), EUDR country risk | Advanced / Enterprise | S4 (Ariba), SCM (partners); rare in mid-market | Differentiator; screening provider must be in SUBPROCESSORS |
| Contracts: price agreements, validity, volume commitments, renewal alerts | Advanced | S4, SCM, IFS, OD | |
| Incoterms 2020 on PO, estimated landed cost on PO | Core | OD (default Incoterms per vendor in 19.4), SCM, S4, NS | |
| Drop-ship and special-order POs from sales orders | Core | All majors | |
| Punch-out catalogues (cXML/OCI) | Enterprise | S4/Ariba, SCM | Later |
| Spend analytics | Advanced | All majors via BI | |

### 1.5 Sales order management

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Quotes/estimates, versions, conversion to order (CRM may originate — section 5.2) | Core | All | BOSSMAN owns opportunity; KASONGO owns fulfilment quote lines and ATP |
| Sales orders, holds (credit hold from MULLAH AR, compliance hold) | Core | All | |
| Available-to-promise (ATP) across sites | Core | All majors | API for BOSSMAN |
| Capable-to-promise (CTP) using capacity and lead times | Advanced | BC (CTP), SCM, S4 (aATP), EP, IN, AC | |
| Allocation rules (priority customers, fair share, backorder reprocessing) | Advanced | S4 (aATP backorder processing), SCM | |
| Backorders, partial shipments, ship-complete flags | Core | All | |
| Drop ship, back-to-back (special order) | Core | All majors | |
| Returns / RMA with disposition (restock, quarantine, scrap, repair, return to vendor) | Core | All majors (MR RMA on Enterprise) | |
| B2B ordering portal (customer-specific catalogue and prices, reorder, order status) | Advanced (Core for distribution vertical) | OD (eCommerce B2B), NS (SuiteCommerce), C7 (add-on), UL (B2B store), AC, MR (Professional) | PWA |
| Order capture from email/PDF (AI drafts) | Advanced | BC Sales Order Agent (GA 2026 wave 1) | Draft-only; see section 4 |
| Multi-warehouse sourcing rules, distributed order management | Advanced / Enterprise | SCM, S4, NS | |
| Recurring / standing orders | Advanced | NS, OD, SCM | |
| Customer-specific labelling and documents (ASN, packing list formats) | Advanced | SCM, S4, EDI partners | Retailer compliance |

### 1.6 Pricing

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Price lists by currency, channel, customer group, with effective dates | Core | All | Money in integer minor units + ISO 4217 |
| Customer-specific and contract prices | Core | All | |
| Quantity breaks / tiered pricing | Core | All (MR on Professional) | |
| Discounts (line, order, mix-and-match), promotions, coupons | Advanced | OD, NS, AC, SCM, C7 | |
| Cost-plus and margin-floor rules with approval below floor | Advanced | SCM, NS, AC | |
| Customer rebates (accruals, settlements) and supplier rebates | Enterprise | SCM (rebate management), S4 (settlement management), EP (Prophet 21) | Accruals post to MULLAH |
| Chargebacks (US distribution: manufacturer–distributor price agreements) | Enterprise (US distribution) | EP (Prophet 21), Infor distribution, SCM via partners | US-only; defer |
| Price simulation and mass updates with approval | Advanced | S4, SCM, NS | |

### 1.7 Manufacturing (discrete)

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Multi-level BOMs, phantoms, versions, effectivity, scrap factors | Core | All manufacturing products | |
| Routings, operations, work centres, machine and labour rates, setup/run/queue/move times | Core | All except some SMB tools | Labour rates from HR are grade-based standard rates (section 5.3) |
| Master production schedule (MPS) | Advanced | MR (Enterprise), OD, BC, NS, AC, EP, IN, S4, SCM | |
| MRP (multi-level, multi-site, pegging, action messages) | Core (single-site), Advanced (multi-site) | All | Output = draft planned orders requiring approval |
| Production / work orders: release, kitting/picking, issue, report progress, close | Core | All | |
| Backflushing (component consumption at operation or completion) | Core | All majors, MR, KT | |
| Shop-floor control / MES-lite: kiosk or tablet clock-on/off by operation, quantities, scrap, downtime, work instructions | Core / Advanced | OD (Shop Floor), NS (Advanced Manufacturing), EP (Advanced MES), IN (Factory Track), AC, KT (shop floor app), MR | Must integrate with HR clocking without double counting |
| Capacity planning (infinite, load charts) | Core | All majors | |
| Finite scheduling / advanced planning and scheduling (APS), drag-and-drop Gantt | Advanced / Enterprise | AC (APS), EP, IN, SCM, S4 (PP/DS), MR (backward scheduling, parallel ops), OD (work order planning) | Candidate for AI optimisation |
| Subcontracting / outsourced operations (send components, receive finished goods) | Advanced | OD, MR, NS (outsourced manufacturing), BC, SCM, S4 | |
| Co-products and by-products | Advanced | OD, MR, SCM, S4, X3 | |
| Engineer-to-order / project manufacturing (WBS-linked) | Enterprise | IFS, EP, IN, S4 | |
| Configure-to-order product configurator (rules, generates BOM/routing/price) | Advanced | AC (Product Configurator), EP (CPQ), IN (CPQ), MR, SCM (product configuration), S4 (variant configuration) | Valuable for make-to-order entry vertical |
| Costing: standard cost roll-up, actual job costing, WIP, production variances | Core (actual/job), Advanced (standard + variances) | All majors | Postings in section 5.1 |
| Disassembly and rework orders | Advanced | MR, OD, SCM, S4 | |
| Tooling and fixture management | Enterprise | EP, IN, IFS | Later |
| Machine data / OEE / IoT connectors | Enterprise | EP, IN, IFS, S4 | Later |

### 1.8 Process manufacturing (food and beverage, chemicals, cosmetics, nutraceuticals, pharma)

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Formulas / recipes with percentages, scaling, yield, losses | Advanced (Core for F&B vertical) | SCM, S4, X3, IN (M3), IFS; specialists Aptean, BatchMaster, Deacom | |
| Batch orders with batch size, consolidated batch orders | Advanced | SCM, S4, X3 | |
| Potency / active-ingredient adjustment of quantities | Enterprise | SCM, S4, X3, Infor M3, specialists | Chemicals, nutraceuticals |
| Catch weight | Enterprise | SCM, S4, IFS, Infor M3 | Meat, cheese, fish |
| Lot attributes and grades (Brix, fat %, moisture), lot-to-lot blending rules | Advanced | SCM (batch attributes), S4 (classification), X3 | |
| Allergen and nutritional data, label data generation (UK FIR 2014 / EU FIC 1169/2011) | Advanced (vertical) | Specialists; partial in X3, SCM via partners | Overlaps with Thapsus Care catering |
| Shelf life, FEFO, quarantine and positive release | Core for vertical | All process products | |
| Packaging BOMs, intermediates, co-/by-products | Advanced | SCM, S4, X3, OD | |
| Certificates of analysis (generate outbound, capture inbound against specification) | Advanced | X3, SCM, S4, IFS, NS (QM SuiteApp) | |
| Safety data sheets and dangerous goods data per formula | Enterprise | S4 (EHS), SCM partners | |
| Electronic batch records with e-signatures (GxP) | Enterprise | S4, specialist MES | Part 11 / Annex 11 (section 3.16) — defer |

### 1.9 Quality management

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Inspection plans: receiving, in-process, final; sampling (fixed, %, AQL) | Advanced | OD (Quality), NS (QM SuiteApp), MR (Professional), EP, IN, X3, S4 (QM), SCM (quality orders), IFS | BC relies on AppSource add-ons |
| Specifications and test results per lot, out-of-spec handling | Advanced | Same | |
| Non-conformance reports, deviations, concessions | Advanced | Same | |
| CAPA (root cause, actions, effectiveness check) | Advanced | EP, IN, S4, IFS, OD (quality alerts) | |
| Certificates of analysis | Advanced | X3, SCM, S4, NS | |
| Recalls and mock recalls: trace report, customer list, stock freeze in one action | Core (for F&B entry) / Advanced | All with lot tracking; full workflow in X3, S4, specialists | BRCGS requires timed traceability tests; FSMA 204 requires records within 24 hours |
| Hold/release with electronic signature and reason | Advanced / Enterprise | S4, SCM, IFS | |
| Supplier quality (supplier corrective action requests, audits, approved supplier list) | Advanced | S4, IFS, EP | |
| Gauge calibration | Advanced | via EAM in IFS, S4, OD (Maintenance) | |

### 1.10 Engineering change and PLM-lite

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Engineering change requests/orders with approval workflow, impact analysis (where-used, open orders, stock) | Advanced | OD (PLM), AC (Engineering Change Control), EP (PLM), S4 (Change Record Management — now with a Joule agent), SCM (engineering change management), MR (revision control) | |
| BOM/routing revisions with effectivity, document attachments (CAD, drawings), revision release | Advanced | Same | Files in regional storage only |
| Integration hooks to CAD/PDM (SolidWorks PDM, Autodesk Vault, Onshape) | Enterprise | EP, IN, IFS, S4 | Later |

### 1.11 Maintenance / EAM

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Asset/equipment register with hierarchy, location, criticality, warranty | Advanced | IFS (leader), S4 (PM), SCM (Asset Management), OD (Maintenance), EP, MR (Enterprise) | Must reconcile with HR asset register and MULLAH fixed assets (section 5.3) |
| Preventive maintenance by calendar, meter or condition; statutory inspection schedules | Advanced | Same | Care homes: LOLER 6-monthly hoist examinations (section 5.4) |
| Maintenance work orders, labour, parts, downtime, costs | Advanced | Same | |
| Spare parts (MRO) inventory and reorder | Advanced | Same | Reuses inventory engine |
| Calibration records | Advanced | IFS, S4, OD | |
| Predictive maintenance (sensor data, anomaly models) | Enterprise | IFS, S4, IN, EP | Optional AI (section 4) |

### 1.12 Projects and professional services

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Projects/jobs with WBS, budgets, estimates vs actuals | Advanced | NS (projects, SRP), BC (Jobs), OD (Project), AC (Projects, Construction), D365 Project Operations, S4, IFS, EP | |
| Timesheets (from Thapsus-HR), expenses, materials to project | Advanced | Same | HR owns time capture; ERP consumes approved time |
| Resource planning (skills, availability from HR rotas/leave) | Advanced | NS SRP, D365 PO, OD (Planning), IFS | |
| WIP, revenue recognition, project accounting | Advanced | Same | Accounting entries in MULLAH |
| Billing: time and materials, milestone, fixed fee, retentions | Advanced | Same | Invoices raised in MULLAH AR |

### 1.13 Field service

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Service contracts, entitlements, SLAs | Advanced | IFS (leader), D365 Field Service, BC (Service, Premium), OD (Field Service), AC (Field Service), NS (Field Service Management) | |
| Scheduling and dispatch board, skills/territory matching | Advanced | Same; IFS Loops digital workers for dispatch | Skills from Thapsus-HR |
| Offline-capable mobile technician app (job, parts, photos, signature, checklists) | Advanced | Same | PWA with offline sync |
| Van stock as inventory locations, parts consumption | Advanced | Same | |
| Installed base / serialised customer assets, service history | Advanced | Same | |

### 1.14 Rental and subscriptions

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Rental orders, availability calendar, period pricing (hour/day/week/month), deposits | Advanced | OD (Rental); specialists (Wynne RentalMan, Point of Rental, MCS); BC/SCM via partners | Niche; defer |
| Check-out/check-in, damage, cleaning/inspection between hires, utilisation | Advanced | Same | Reuses EAM |
| Subscriptions and recurring billing | Advanced | NS (SuiteBilling), OD (Subscriptions), S4 | Billing belongs in MULLAH/BOSSMAN; ERP handles recurring fulfilment |

### 1.15 Demand planning, forecasting and supply chain planning

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Statistical demand forecasting (seasonality, intermittent demand), forecast consumption | Advanced | NS (Demand Planning), BC (forecasts), OD (forecast-based purchasing), SCM (Demand planning), C7 (ForesightAI add-on), UL (Pro), MR (Enterprise), EP (Smart Inventory Planning and Optimization) | Optional AI (section 4) |
| Safety stock and reorder-point recommendations | Advanced | Same | Draft-and-approve |
| Distribution requirements planning between warehouses | Advanced | SCM, S4, NS (Supply Planning), EP | |
| Supply chain orchestration / control tower, exception management | Enterprise | S4 (Supply Chain Orchestration H1 2026), SCM, NS | |
| Sales and operations planning (S&OP) | Enterprise | S4 (IBP), SCM, IN | Later |

### 1.16 Transport and shipping

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Parcel carrier integration via aggregators (labels, tracking) for UK (Royal Mail, DPD, Evri, DHL, UPS, FedEx), EU, US (UPS, FedEx, USPS) | Core | OD (native connectors), NS (UPS/FedEx/USPS), AC, C7, SCM | Aggregator becomes a sub-processor (addresses = personal data for sole traders/consumers) |
| Rate shopping across carriers | Advanced | NS, OD, C7, AC | |
| Customs documents (commercial invoice, CN22/CN23), EORI, HS, origin, Incoterms | Core | Same | |
| Freight TMS (load building, route planning, freight audit) | Enterprise | SCM (TMS), S4 (TM) | Later |
| Dangerous goods shipping documents | Advanced | S4, SCM | |

### 1.17 Multi-entity and intercompany trade

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Multiple legal entities in one tenant, shared or entity-specific item master | Core | NS (OneWorld — leader), BC, OD, AC, SCM, S4 | Entity = MULLAH company |
| Intercompany purchase ↔ sales order mirroring, automatic receipt on shipment | Advanced | NS, BC (intercompany), OD (inter-company rules), AC, SCM, S4 | |
| Transfer pricing rules (cost-plus, list) and handoff of intercompany postings/eliminations to ledger | Advanced | Same | ERP computes transfer price; MULLAH posts and eliminates |
| Cross-entity fulfilment (ship from another entity's warehouse) | Advanced | NS, SCM, S4 | |
| Consolidated stock visibility | Core | All | |

### 1.18 eCommerce and marketplace connectors

| Connector | Tier | Leaders with it | Notes |
|---|---|---|---|
| Shopify (orders, stock, products, prices, fulfilments, refunds) | Core | BC (Microsoft-built connector), KT, C7, UL, AC, NS (via partners), OD (apps) | Highest-demand connector for target verticals |
| WooCommerce | Core | KT, C7, UL, OD (apps) | |
| Amazon (SP-API: orders, FBA inventory, listings) | Core / Advanced | AC, C7, OD, KT, NS (partners) | |
| eBay | Advanced | OD, C7 | |
| BigCommerce | Advanced | AC, C7, NS (partners) | |
| Adobe Commerce (Magento) | Advanced | C7, NS/BC (partners) | |
| Native B2B storefront | Advanced | OD, NS (SuiteCommerce), UL, AC | |

### 1.19 Point of sale (optional)

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Store POS with offline mode, payments, receipts, stock decrement | Advanced (optional) | OD (POS), NS (POS), C7 (add-on), D365 Commerce, AC (via Shopify POS) | Recommend integrating Shopify POS rather than building; payments and card data stay out of scope (PCI DSS) |

### 1.20 EDI

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| ANSI X12: 850 PO, 855 PO ack, 856 ASN, 810 invoice, 846 inventory, 940/945 warehouse orders (3PL) | Advanced (Core for US distribution) | EP, X3, S4 (IDoc mapping), SCM/BC/NS/AC via partners (SPS Commerce, TrueCommerce, Orderful) | Integrate with an EDI network provider; keep mappings as no-code templates |
| UN/EDIFACT: ORDERS, ORDRSP, DESADV, INVOIC, INVRPT, PRICAT | Advanced (Core for EU retail supply) | Same | |
| Peppol BIS 3 post-award: Ordering, Order Agreement, Despatch Advice (plus Billing in MULLAH) | Advanced (UK public sector/NHS, Nordics, Benelux) | OD (Peppol), S4, specialist access points | OpenPeppol lists Ordering 3.x, Order Agreement 3.0 and Despatch Advice 3.x ([Peppol BIS 3](https://docs.peppol.eu/poacc/upgrade-3/); [post-award documentation](https://peppol.org/documentation/technical-documentation/post-award-documentation/)) |
| Peppol pre-award (eTendering) | Enterprise | Specialist | Not researched in depth (UNVERIFIED) |
| AS2/SFTP/VAN connectivity | Advanced | Via providers | |

### 1.21 Sustainability data

| Feature | Tier | Leaders with it | Notes |
|---|---|---|---|
| Packaging composition per item and per packaging level (material, weight, recycled content, recyclability/RAM rating, household vs non-household) and period reporting | Core (UK) / Advanced | Rare natively; mostly spreadsheets or specialist tools | Directly drives UK pEPR, Plastic Packaging Tax, EU PPWR, DRS (section 3.9) — strong differentiator |
| Product carbon footprint per item / BOM roll-up, emission-factor library, supplier-provided PCFs | Advanced | S4 (Sustainability Footprint Management), SCM (Microsoft sustainability tools) | |
| CBAM embedded emissions per import line, supplier installation data, authorised declarant status | Advanced (importers of steel, aluminium, cement, fertiliser, hydrogen) | S4 and specialists | Section 3.2–3.3 |
| EUDR: commodity flag, geolocation of plots, due diligence statement / reference numbers per lot | Advanced (F&B, timber, furniture, rubber, leather) | Specialists; S4 partners | Section 3.4 |
| Digital Product Passport data model (materials, substances, repair, carrier: GS1 Digital Link QR) | Enterprise | Specialists | Battery passport from 18 Feb 2027 |
| REACH SVHC and RoHS declarations per item, SCIP notification data | Advanced | S4 (EHS), specialists | Section 3.14 |

### 1.22 Cross-cutting platform capabilities (expected by buyers)

| Capability | Tier | Notes |
|---|---|---|
| Role-based security with field-level restrictions; segregation of duties (e.g. PO creator ≠ approver) | Core | Mirrors Thapsus non-negotiables |
| Append-only audit of every change; "who changed price/quantity/cost" history | Core | Needed for Part 11-style customers later |
| Document attachments with regional storage | Core | |
| Saved views, filters, dense tables, bulk edit, import/export (CSV/XLSX) with validation and dry run | Core | Data migration is a top failure cause (section 7.4) |
| Reporting / BI, KPIs, scheduled reports | Core | |
| Open REST API (OpenAPI 3.1), webhooks, events | Core | |
| Multi-currency, multi-language, multi-time-zone | Core | Thapsus i18n rules |
| Offline-tolerant mobile (warehouse, field service) | Advanced | |

---

## 2. Industry verticals

### 2.1 Must-haves and dominant competitors by vertical

| Vertical | Must-have features | Who dominates (mid-market cloud) | Fit for KASONGO |
|---|---|---|---|
| **Discrete manufacturing** (engineered products, components, assembly) | Multi-level BOM/routings, MRP, shop-floor kiosk, capacity/APS, job costing, ECO/revisions, subcontracting, quality inspections, serial tracking, configurator for CTO | US: Epicor Kinetic, Infor CloudSuite Industrial, Plex (Rockwell), Acumatica; UK/EU: BC + ISVs, IFS (upper), SAP B1/S4, Sage 200/X3; SMB: Katana, MRPeasy, Fishbowl | **Strong** for light/assemble- and make-to-order; avoid heavy ETO at first |
| **Process — food and beverage** | Recipes, lots, FEFO, shelf life, allergens, catch weight, yield, CoA, recall in minutes, FSMA 204 KDE/CTE records, BRCGS/ISO 22000 evidence, retailer EDI, GS1 labels | Sage X3, SCM, S4, Infor M3/CloudSuite F&B, Aptean (food & beverage editions), Deacom (ECI), BatchMaster; BC + food ISVs in UK/EU | **Good** as third vertical; regulatory pressure (FSMA 204, EUDR for cocoa/coffee/palm/soy/cattle, pEPR/DRS) |
| **Process — chemicals, coatings** | Formulas with potency, SDS/GHS, dangerous goods, REACH/CLP, batch genealogy, tolling | S4, X3, SCM, Datacor, Deacom | Later — compliance data heavy |
| **Process — cosmetics** | Formulas, batch, EU Cosmetics Regulation product information file, INCI, lot traceability, retailer EDI | X3, BC/NS + ISVs | Later (adjacent to F&B) |
| **Process — pharma / nutraceuticals** | GMP batch records, e-signatures (Part 11/Annex 11), validation, quarantine/release by QP, serialisation (FMD/DSCSA) | S4, Infor, specialist MES; nutraceuticals: Deacom, X3, BatchMaster | **Avoid at launch** — validation burden; revisit with a "GxP pack" |
| **Wholesale distribution** | Multi-warehouse, bins, scanning, pick/pack/ship, landed cost, replenishment, customer-specific pricing, rebates, B2B portal, EDI, drop ship, back-to-back, carrier integration, serial/lot | NS (very strong), Epicor Prophet 21/Eclipse (US), Infor distribution, AC, BC + ISVs, SAP B1; SMB: Cin7, Unleashed | **Strong** — widest market, data model reused by every other vertical |
| **Retail and eCommerce (brands, DTC/omnichannel)** | Shopify/Amazon connectors, multichannel stock sync, POS integration, returns, 3PL integration, variants, demand forecasting | NS, Cin7, Brightpearl (Sage), Linnworks (UK), Odoo, BC + Shopify connector | **Strong** when combined with distribution; avoid building POS |
| **Construction and contracting** | Job costing with cost codes, commitments, subcontracts, retentions, applications for payment, UK CIS, plant hire, timesheets, change orders | US: Trimble Viewpoint, Sage Intacct Construction, Acumatica Construction, CMiC, Procore (project management); UK: COINS, Eque2, Sage | **Avoid** — finance-heavy, specialist incumbents, depends on MULLAH maturity |
| **Professional services** | Projects, resource planning, timesheets, utilisation, T&M/milestone billing, revenue recognition | NS (SRP/OpenAir), Certinia, Kantata, D365 Project Operations, Deltek | **Not ERP-led** — better served by MULLAH + Thapsus-HR + a projects module later |
| **Field service** | Scheduling/dispatch, mobile offline app, contracts/SLAs, van stock, installed base | IFS, D365 Field Service, Salesforce Field Service, ServiceTitan (US trades), PTC ServiceMax | **Good adjacency** — reuses Thapsus-HR rotas/skills and care-home facilities; second wave |
| **Rental / equipment hire** | Availability calendar, period pricing, check-out/in, inspections between hires, utilisation, damage billing | Wynne Systems (RentalMan), Point of Rental, MCS (UK), Odoo Rental, BC/SCM ISVs | **Niche** — defer |

Notes: dominance statements are qualitative (vendor positioning and analyst coverage); I found no credible public market-share data split by vertical and region (see "Things I could not verify").

### 2.2 Recommendation: entry verticals

**Recommend 1 + 2 at launch, 3 as the first follow-on (12–18 months):**

1. **Wholesale distribution and multichannel product businesses (UK first, then EU and US).**
   - Largest addressable base; requirements are well understood and mostly "Core" in section 1.
   - The data model (items, UoM, lots, bins, landed cost, price lists, ATP) is reused by every later vertical, so nothing is throwaway.
   - Clear graduation path from Cin7, Unleashed, Linnworks and Xero/QuickBooks add-ons; buyers want multi-entity, landed cost and EDI without NetSuite's price.
   - Regulatory hooks unique to Thapsus' UK/EU/US footprint: pEPR packaging data, Plastic Packaging Tax, PPWR, CBAM thresholds, US tariff stacking, Intrastat (NI and EU), UFLPA/FLR supplier screening.
   - Synergy: BOSSMAN (CRM) for quote-to-cash; MULLAH for AR/AP; Thapsus Care purchasing as an early internal reference customer for procurement.

2. **Light discrete manufacturing — assemble-to-order, make-to-order and small-batch makers (10–500 staff).**
   - The SMB MRP tier (Katana, MRPeasy, Fishbowl, Unleashed) proves demand; customers outgrow them on multi-entity, finance depth, quality and WMS — exactly where KASONGO + MULLAH would sit.
   - Thapsus-HR already has clocking, rotas, skills — a native shop-floor kiosk tied to HR clocking and skills/certification gating is a differentiator few competitors integrate cleanly.
   - Keep ETO, APS and MES depth for later tiers.

3. **Food and beverage (process-lite: recipes, lots, FEFO, allergens, yield; catch weight later).**
   - Highest regulatory pull: FSMA 204 records (enforcement from 20 Jul 2028), EUDR (cocoa, coffee, palm oil, soy, cattle, rubber, wood — from 30 Dec 2026), UK DRS (1 Oct 2027), pEPR fee modulation from 2026/27, PPWR (12 Aug 2026), BRCGS/ISO 22000 traceability tests.
   - Builds on lots/FEFO from vertical 1 and production from vertical 2.
   - Synergy with Thapsus Care catering (recipes, allergen data, stock) and an existing customer base in UK care.

**Why not the others at launch:** construction and professional services depend on ledger/project-accounting depth that MULLAH will still be building; pharma requires validated GxP processes and e-signatures (section 3.16); rental and POS are niches with entrenched specialists; field service is a strong second-wave adjacency once HR scheduling integration is proven.

---

## 3. Regulation and compliance relevant to ERP (as of 7 November 2026)

### 3.0 Summary table

| # | Regime | Jurisdiction | Status | Key dates | ERP data / feature impact |
|---|---|---|---|---|---|
| 3.1 | Intrastat | UK (NI only), EU member states | IN FORCE | UK NI: arrivals > £500k, dispatches > £250k; DE: arrivals €3m, dispatches €1m (from Jan 2025) | Commodity code, net mass, supplementary units, nature of transaction, delivery terms, partner VAT ID, country of origin per line; monthly export |
| 3.2 | EU CBAM | EU | IN FORCE (definitive period) | Definitive 1 Jan 2026; 50-tonne annual threshold; certificate sales 1 Feb 2027; first annual declaration 30 Sep 2027; downstream extension from 2028 PROPOSED | Track CBAM goods by CN code, net mass per importer per year, embedded emissions per supplier installation, authorised-declarant status |
| 3.3 | UK CBAM | UK | ADOPTED, APPLIES FROM 1 Jan 2027 | £50,000 12-month look-back / 30-day look-forward; registration opens 1 Jan 2028, deadline 31 Jan 2028 for 2027 triggers | Value of CBAM goods per rolling 12 months, emissions data, records from 1 Jan 2027 |
| 3.4 | EUDR | EU | ADOPTED, APPLIES FROM 30 Dec 2026 (large/medium) and 30 Jun 2027 (micro/small) | Newly added products from 30 Dec 2027 (delegated act pending scrutiny) | Commodity flag, geolocation, DDS/declaration reference numbers per lot and per sale, retention |
| 3.5 | ESPR / DPP | EU | IN FORCE (framework); product rules mostly not yet adopted | Unsold apparel/footwear destruction ban for large firms from 19 Jul 2026; first product delegated acts (steel/iron) expected 2026–27 | DPP data model, GS1 Digital Link carriers, unsold goods disclosure |
| 3.6 | EU Batteries Regulation | EU | IN FORCE; due diligence ADOPTED, APPLIES FROM 18 Aug 2027 | Battery passport 18 Feb 2027 | Battery category, passport ID/QR, supply-chain due diligence data |
| 3.7 | CSRD/ESRS, CSDDD after Omnibus I | EU | IN FORCE (Directive (EU) 2026/470); revised ESRS delegated act adopted 3 Jul 2026 (scrutiny) | CSRD transposition 19 Mar 2027; CSDDD applies 26 Jul 2029 | Supplier-level ESG data, VSME-capped requests from customers |
| 3.8 | EU Forced Labour Regulation 2024/3015 | EU | ADOPTED, APPLIES FROM 14 Dec 2027 | Guidelines published 26 Jun 2026; risk database delayed | Supplier/product-origin traceability, ability to withdraw products |
| 3.9 | UK pEPR, Plastic Packaging Tax, DRS; EU PPWR | UK / EU | pEPR IN FORCE; PPT IN FORCE; DRS ADOPTED, APPLIES FROM 1 Oct 2027; PPWR IN FORCE, applies 12 Aug 2026 | PPT £228.82/t from 1 Apr 2026; pEPR large-producer reporting every 6 months | Packaging composition per item, tonnage by material, nation and household/non-household, recycled content |
| 3.10 | Customs (UK CDS, S&S GB; EU UCC, ICS2, customs reform, €3 low-value duty) | UK / EU | IN FORCE; EU customs reform politically agreed 26 Mar 2026 | S&S GB for EU imports from 31 Jan 2025; ICS2 all modes from 1 Sep 2025; €3 duty from 1 Jul 2026; EU Data Hub for e-commerce Jul 2028 | HS codes, origin, Incoterms, EORI, declarations data, broker integration |
| 3.11 | UFLPA | US | IN FORCE (since 21 Jun 2022) | Entity list 187 entities after 3 Aug 2026 expansion | Supplier and sub-tier mapping, origin evidence |
| 3.12 | FSMA 204 food traceability | US | Rule IN FORCE; compliance date extension PROPOSED; Congress barred enforcement before 20 Jul 2028 | Enforcement not before 20 Jul 2028 | KDEs per CTE, traceability lot codes, 24-hour sortable spreadsheet |
| 3.13 | US tariffs 2025–2026 | US | IN FORCE (s.232, s.301); IEEPA tariffs invalid since 20 Feb 2026; s.122 expired 24 Jul 2026 | De minimis suspended (CBP rules, Jun 2026); statutory repeal 1 Jul 2027 | Landed cost with stacking, component origin, metal content, HTS Chapter 99, refunds |
| 3.14 | REACH, RoHS, WEEE | EU / UK | IN FORCE; EU REACH revision dropped (Apr 2026); UK REACH deadline extension laid Mar 2026 (status UNVERIFIED); WEEE revision PROPOSED (Circular Economy Act) | UK REACH first deadline was 27 Oct 2026 (proposed move to 27 Oct 2029) | SVHC flags, SCIP data, RoHS declarations, EEE producer data |
| 3.15 | GS1 (GTIN, SSCC, Digital Link, Sunrise 2027) | Global | INDUSTRY | US retail POS 2D-ready target 2027 | GS1 AI parsing, Digital Link URIs, SSCC labels |
| 3.16 | 21 CFR Part 11; EU GMP Annex 11 (and draft Annex 22) | US / EU | Part 11 IN FORCE; Annex 11 (2011) IN FORCE; revisions PROPOSED (drafts Jul 2025) | No final revision date as of Sep 2026 | Audit trails, e-signatures, validation evidence |
| 3.17 | UDI / QMSR / EUDAMED | US / EU | IN FORCE; FDA QMSR effective 2 Feb 2026; EUDAMED 4 modules mandatory from 28 May 2026 | Legacy device registration ~27–28 Nov 2026 (sources differ) | UDI-DI/PI on items and lots, label data |
| 3.18 | ISO 9001:2026, ISO 22000, BRCGS | Global | INDUSTRY | ISO 9001:2026 published 16 Sep 2026; transition expected to ~Sep 2029 | Traceability, CAPA, document control, supplier approval |
| 3.19 | Dangerous goods (ADR, IMDG, IATA) | International | IN FORCE | IMDG Amendment 42-24 mandatory 1 Jan 2026; IATA DGR 67th edition for 2026 | UN number, class, packing group, LQ/EQ, DG documents |
| 3.20 | Adjacent: EU AI Act, UK e-invoicing, ViDA | EU / UK | AI Act IN FORCE (Digital Omnibus Reg (EU) 2026/1744); UK e-invoicing from Apr 2029 announced; ViDA adopted | Annex III high-risk from 2 Dec 2027 | Governs optional AI; Peppol ordering/despatch alongside MULLAH invoicing |

### 3.1 Intrastat

- **UK — IN FORCE, Northern Ireland only.** You must register if, in a calendar year, you receive more than **£500,000** of goods from the EU into Northern Ireland or move more than **£250,000** of goods from Northern Ireland to the EU. GOV.UK states: "You do not need to use Intrastat for goods you move between Great Britain (England, Wales and Scotland) and the EU." Declarations are monthly. Source: [GOV.UK — Intrastat](https://www.gov.uk/intrastat). The old UK-wide £1.5m arrivals threshold (2015) is obsolete ([HMRC brief 47 (2014)](https://www.gov.uk/government/publications/revenue-and-customs-brief-47-2014-changes-to-the-intrastat-arrival-threshold-from-1-january-2015/revenue-and-customs-brief-47-2014-changes-to-the-intrastat-arrival-threshold-from-1-january-2015)).
- **EU — IN FORCE, thresholds set nationally** under the European Business Statistics framework, reviewed annually.
  - **Germany:** dispatches **€1m**, arrivals **€3m**, applying retroactively from reporting month January 2025; in 2025 only 2.7% of German importing businesses still had to report ([Destatis threshold notice](https://www.destatis.de/DE/Themen/Wirtschaft/Aussenhandel/anmeldeschwellen-2025.html); [Destatis press release 20 Aug 2026](https://www.destatis.de/DE/Presse/Pressemitteilungen/2026/08/PD26_297_51.html)). I found no 2026 change.
  - **France:** no numeric threshold; customs notifies businesses that must report (secondary sources: [Eurofiscalis](https://www.eurofiscalis.com/en/eu-intrastat-thresholds/), [Marosa](https://marosavat.com/resources/intrastat-thresholds)) — UNVERIFIED against DGDDI.
  - **Netherlands:** threshold removed in 2023; reporting "on demand" of CBS (secondary sources as above) — UNVERIFIED against CBS.
- **ERP implication:** keep the threshold table as effective-dated configuration per country (never hard-coded); compute running totals per legal entity per flow; produce national file formats. Data per line: CN8 code, partner country, country of origin, nature of transaction, mode of transport, delivery terms, net mass, supplementary units, statistical value, partner VAT ID (dispatches).

### 3.2 EU CBAM

- **IN FORCE (definitive period since 1 Jan 2026).** Regulation (EU) 2023/956 as amended by **Regulation (EU) 2025/2083** (CBAM simplification, published in the OJ in October 2025; Commission news dated 20 Oct 2025). Sources: [EUR-Lex 2025/2083](https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=OJ%3AL_202502083); [Commission — officially published simplifications](https://taxation-customs.ec.europa.eu/news/officially-published-simplifications-carbon-border-adjustment-mechanism-cbam-2025-10-20_en); [CBAM definitive regime](https://taxation-customs.ec.europa.eu/carbon-border-adjustment-mechanism/cbam-definitive-regime_en); [CBAM entered into force 1 Jan 2026](https://taxation-customs.ec.europa.eu/news/cbam-successfully-entered-force-1-january-2026-2026-01-14_en).
- **50-tonne threshold — verified.** A single mass-based threshold of **50 tonnes** net mass per importer per calendar year, aggregated across all CN codes, replaced the €150-per-consignment exemption. Importers above it must be **authorised CBAM declarants**; importers below it are exempt but must indicate the exemption in the customs declaration. Hydrogen and electricity are excluded from the threshold (always require authorisation). The Commission expects it to exempt about 182,000 importers while still covering over 99% of in-scope emissions.
- **Dates:** certificate sales start **1 Feb 2027** (moved from 1 Jan 2026); annual declaration due **30 Sep** of the following year — first deadline **30 Sep 2027** for 2026 imports; quarterly holding requirement reduced to 50% (secondary sources: [Gleiss Lutz](https://www.gleisslutz.com/en/know-how/eu-simplifies-cbam-regulation-omnibus-simplification-initiative), [Reed Smith](https://www.reedsmith.com/our-insights/blogs/viewpoints/102lr9t/what-you-need-to-know-as-cbam-simplification-comes-into-effect/)).
- **Downstream extension — PROPOSED.** December 2025 Commission package adds about 180 steel/aluminium-intensive downstream products from **1 Jan 2028** plus anti-circumvention measures. Parliament voted to extend (Sept 2026) and favoured a wider list; trilogue continuing as of October 2026 ([PwC NL](https://www.pwc.nl/en/insights-and-publications/tax-news/other/ec-proposes-cbam-expansion-to-180-downstream-products.html); [EPRS briefing Jul 2026](https://eprs.europarl.europa.eu/contents/publications/EPRS/2026/07/EPRS_BRI(2026)789314.html)).
- **ERP implication:** flag CBAM goods by CN code; accumulate net mass per importer per year with an alert approaching 50 t; store supplier installation IDs and embedded emissions (direct/indirect, default vs actual values); export data for the declaration; landed-cost line for estimated certificate cost.

### 3.3 UK CBAM

- **ADOPTED, APPLIES FROM 1 January 2027.** Legal basis: Finance Act 2026 Part 5; the Carbon Border Adjustment Mechanism (Calculation of CBAM Rate and Determination of Carbon Price Relief) Regulations 2026 (SI 2026/809, made 13 Jul 2026) and the Transitory Provision Regulations 2026 (SI 2026/830). Sources: [legislation.gov.uk SI 2026/809](https://www.legislation.gov.uk/uksi/2026/809/made); [SI 2026/830](https://www.legislation.gov.uk/uksi/2026/830/made); [HMRC — work out the date you need to register](https://www.gov.uk/guidance/work-out-the-date-youll-need-to-register-for-carbon-border-adjustment-mechanism-cbam); [CBAM policy summary](https://www.gov.uk/government/publications/carbon-border-adjustment-mechanism-cbam-policy-summary/carbon-border-adjustment-mechanism-cbam-policy-summary).
- **Threshold:** registration obligation arises once CBAM goods worth **£50,000** or more were imported in the preceding 12 months (tested on the first day of each month) or are expected within the next 30 days. This is a **value** test, unlike the EU's 50-tonne mass test. (The 2024 consultation's £10,000 threshold is superseded.)
- **Registration:** online registration opens **1 Jan 2028**; businesses that trigger in 2027 have until **31 Jan 2028**.
- **Sectors:** aluminium, cement, fertilisers, hydrogen, iron and steel (electricity excluded) — per secondary sources and the GOV.UK factsheet ([factsheet](https://www.gov.uk/government/publications/factsheet-carbon-border-adjustment-mechanism-cbam/factsheet-carbon-border-adjustment-mechanism)).
- **First return/payment 31 May 2028 for 2027:** reported by one secondary source only — UNVERIFIED.
- **ERP implication:** rolling 12-month value counter per legal entity (GBP), 30-day forward look from open POs, records kept from 1 Jan 2027 regardless of threshold.

### 3.4 EU Deforestation Regulation (EUDR)

- **ADOPTED, APPLIES FROM 30 December 2026** (large and medium operators, and micro/small operators already covered by the EU Timber Regulation) and **30 June 2027** (other micro and small operators). Amended by **Regulation (EU) 2025/2650** (agreed December 2025). Sources: [Commission — product scope and tools update, 13 Jul 2026](https://environment.ec.europa.eu/news/commission-updates-product-scope-and-tools-support-eudr-2026-07-13_en); [Commission Access2Markets news](https://trade.ec.europa.eu/access-to-markets/en/news/delay-until-december-2026-and-other-developments-implementation-eudr-regulation); [Stibbe](https://www.stibbe.com/publications-and-insights/the-amended-eudr-what-has-changed-and-what-has-remained).
- **Review outcome (May 2026):** the Commission's Article 34 simplification review confirmed the 30 Dec 2026 date and said a further legislative simplification proposal was not appropriate "at this stage" ([Hogan Lovells](https://www.hlc.com/en/publications/eu-deforestation-regulation-commission-publishes-simplification-package-ahead-of-december-2026); [Arendt](https://www.arendt.com/news-insights/news/eudr-simplification-review-published-what-the-2026-package-means-for-in-scope-companies/)).
- **Key simplifications in 2025/2650:** downstream operators and traders **no longer submit their own due diligence statements** — they collect and keep the reference number of the initial (upstream) statement; non-SME downstream operators and traders still register in the information system; micro and small primary operators in low-risk countries file a one-off **simplified declaration** and receive a declaration identifier ([EY](https://globaltaxnews.ey.com/news/2026-0237); [NI Assembly annex on 2025/2650](https://www.niassembly.gov.uk/globalassets/committee-blocks/windsor-framework-democratic-scrutiny-committee/reg-eu-20252650/annex-f---2025-2650.pdf)). Commentators flag a gap: between 30 Dec 2026 and 30 Jun 2027 downstream actors must collect identifiers that micro/small primary operators are not yet obliged to issue.
- **Scope changes (13 Jul 2026):** a delegated act updating Annex I (removes e.g. cattle hides, skins and leather, re-treaded tyres, soybeans for sowing, some vulcanised rubber articles, conveyor belts, vehicle seats; adds soluble coffee, certain palm-oil derivatives, frozen cattle tongues) — **subject to Parliament/Council scrutiny**; newly added products apply from **30 Dec 2027**. An implementing act set the technical rules for the information system (APIs). Status of the delegated act after scrutiny: UNVERIFIED.
- **ERP implication:** commodity/EUDR flag on items (by CN code); per-lot storage of upstream DDS reference numbers and declaration identifiers; propagation to sales documents; geolocation polygons (for operators that place on the market first); five-year record retention; API integration with the EU information system (TRACES).

### 3.5 ESPR and Digital Product Passports

- **IN FORCE (framework regulation)** — Regulation (EU) 2024/1781 (ESPR). Product-specific requirements (including DPPs) apply only once delegated acts are adopted for each product group.
- **Working plan 2025–2030** adopted 16 April 2025: priority groups include textiles/apparel, furniture, tyres, mattresses, iron and steel, aluminium; iron and steel act expected 2026, textiles and others 2027, with ~18-month transitions (secondary sources: [Renoon](https://www.renoon.com/blog/delegated-acts-for-digital-product-passport-explainer-and-current-status), [PSQR](https://psqr.eu/publications-resources/espr-updates-april25/)). As of mid-2026 secondary sources reported **no product delegated act finalised** — UNVERIFIED as of November 2026.
- **Unsold goods:** ban on destroying unsold apparel and footwear applies to large enterprises from **19 July 2026** (medium enterprises later) — ADOPTED and now applying; secondary source only.
- **DPP registry:** ESPR requires a Commission DPP registry by 19 July 2026 — UNVERIFIED (not confirmed in sources found).
- **Battery passport:** see 3.6 — the first mandatory DPP in practice (18 Feb 2027).
- **ERP implication:** a flexible, versioned "product passport" record per item/model/batch with GS1 Digital Link carrier; supplier data requests; keep it schema-driven because delegated acts will define fields per product group.

### 3.6 EU Batteries Regulation

- **IN FORCE** — Regulation (EU) 2023/1542.
- **Battery passport: ADOPTED, APPLIES FROM 18 February 2027** for LMT batteries, industrial batteries > 2 kWh and EV batteries, with QR-code requirements on the same date. Some passport content (carbon footprint, recycled content, due diligence report) depends on separate implementing rules still pending ([technology.org Oct 2026](https://www.technology.org/2026/10/19/eu-battery-rules-february-2027-removable-batteries-passport/); [Circularise](https://www.circularise.com/blogs/eu-battery-passport-regulation-requirements)).
- **Due diligence: ADOPTED, APPLIES FROM 18 August 2027** — postponed two years by Regulation (EU) 2025/1561 ("stop-the-clock", Council adoption July 2025): [Council press release 18 Jul 2025](https://www.consilium.europa.eu/en/press/press-releases/2025/07/18/simplification-council-adopts-law-to-stop-the-clock-on-due-diligence-rules-for-batteries/). Commission guidelines deadline moved to 26 Jul 2026.
- **Turnover threshold increase (€40m → €150m) — PROPOSED** in the May 2025 Omnibus IV package; adoption status UNVERIFIED ([CECE](https://www.cece.eu/news/eu-batteries-regulation-the-commission-key-changes-to-due-diligence-policy)).
- **ERP implication:** battery category and chemistry on item, passport ID and QR link per battery/batch, cobalt/lithium/nickel/natural graphite supplier due diligence data.

### 3.7 CSRD/ESRS and CSDDD after Omnibus I

- **Omnibus I — IN FORCE.** Directive (EU) 2026/470 published in the OJ on **26 February 2026**, in force **18 March 2026** ([Latham & Watkins](https://www.lw.com/en/insights/eu-sustainability-omnibus-published-in-the-official-journal); [Linklaters](https://sustainablefutures.linklaters.com/post/102mkjf/eu-omnibus-i-directive-published-in-the-official-journal-of-the-eu); [Arthur Cox](https://www.arthurcox.com/insights/omnibus-i-directive-published-revised-scope-and-reduced-obligations-under-csrd-and-csddd/)).
  - **CSRD scope:** EU companies exceeding **both** €450m net turnover **and** 1,000 employees. Member States transpose by **19 March 2027**. One source says new thresholds apply to financial years from 1 Jan 2027 — UNVERIFIED (single source). Earlier "stop-the-clock" Directive (EU) 2025/794 had already deferred waves 2 and 3.
  - **CSDDD scope:** >5,000 employees and >€1.5bn turnover; transposition by **26 July 2028**; companies comply from **26 July 2029** ([Global Policy Watch](https://www.globalpolicywatch.com/2026/02/eu-csddd-csrd-omnibus-published-in-official-journal-transposition-delegated-acts-and-guidelines-are-next/)).
- **Revised ("simplified") ESRS and voluntary standard — ADOPTED by the Commission on 3 July 2026 as delegated acts, subject to Parliament/Council scrutiny** (two months, extendable). One act revises ESRS (amending Delegated Regulation (EU) 2023/2772); the other establishes the voluntary standard (formerly VSME) for companies outside CSRD scope, which also acts as the **value-chain cap** — in-scope companies cannot require more than that from smaller "protected" suppliers. Application: financial years from 1 Jan 2027, with optional early use for 2026 ([Mayer Brown](https://www.mayerbrown.com/en/insights/publications/2026/07/european-commission-adopts-revised-european-sustainability-reporting-standards); [Debevoise](https://www.debevoise.com/insights/publications/2026/10/european-commission-adopts-revised-esrs-and-volunt)). OJ publication: UNVERIFIED.
- **ERP implication:** most mid-market customers are out of CSRD scope but will be asked by large customers for VSME-level data (energy, emissions, product footprints). Provide a "customer sustainability data request" pack from ERP data (purchased materials, energy items, transport, waste) rather than full ESRS reporting.

### 3.8 EU Forced Labour Regulation

- **ADOPTED, APPLIES FROM 14 December 2027** — Regulation (EU) 2024/3015, in force since 13 Dec 2024. Prohibits placing on, or exporting from, the EU market products made with forced labour; enforcement by product withdrawal/disposal decisions.
- Commission guidelines (due 14 Jun 2026) published **26 June 2026**, OJ notice 3 Sep 2026; the public **forced-labour risk database is late** (not live as of September 2026); Member States must notify penalty regimes by 14 Dec 2026 ([Sedex](https://www.sedex.com/blog/eu-forced-labour-regulation-guidelines-and-supply-chain-implications/); [Hogan Lovells](https://hlc.com/en/publications/eu-forced-labour-regulation-key-takeaways-from-the-european-commissions-june-2026-guidelines); [Osborne Clarke Sept 2026](https://www.osborneclarke.com/insights/regulatory-outlook-september-2026-modern-slavery); [EP Legislative Observatory](https://oeil.europarl.europa.eu/oeil/en/document-summary?id=1799238)).
- **ERP implication:** supplier and manufacturer identity per lot/batch, origin evidence, ability to block and recall specific lots; shared with UFLPA (3.11).

### 3.9 Packaging: UK pEPR, Plastic Packaging Tax, UK DRS, EU PPWR

**UK packaging extended producer responsibility (pEPR) — IN FORCE.**
- **Who:** obligated if you supplied/imported **more than 25 tonnes** of packaging in the UK in the previous year **and** turnover **£1m or more**. **Large producer:** over 50 tonnes and turnover above £2m — reports every 6 months and pays waste disposal fees to PackUK; **small producer:** reports annually by 1 April ([GOV.UK — who is affected](https://www.gov.uk/guidance/extended-producer-responsibility-for-packaging-who-is-affected-and-what-to-do); [GOV.UK — report packaging data](https://www.gov.uk/guidance/check-if-you-need-to-report-packaging-data)).
- **Fees 2025/26 (confirmed):** per tonne — plastic £423, fibre-based composite £461, wood £280, aluminium £266, steel £259, other £259, paper and card £196, glass £192 ([GOV.UK 2025 base fees](https://www.gov.uk/government/publications/extended-producer-responsibility-for-packaging-2025-base-fees/extended-producer-responsibility-for-packaging-2025-base-fees)).
- **From 2026/27, fees are modulated** by recyclability (RAM rating: green below, amber at, red above base); illustrative plastic: green £415, amber £455, red £545 per tonne ([GOV.UK illustrative fees 2026](https://www.gov.uk/government/publications/illustrative-waste-disposal-fees-2026-extended-producer-responsibility-for-packaging/year-2-illustrative-waste-disposal-fees-extended-producer-responsibility-for-packaging); [PackUK modulation statement](https://www.gov.uk/government/publications/extended-producer-responsibility-for-packaging-modulated-disposal-fees/packuk-extended-producer-responsibility-epr-for-packaging-producer-disposal-fees-modulation-statement)). Confirmed year-2 fees were not published as of early November 2026; PackUK intends notices of liability by end of November 2026 (secondary sources) — UNVERIFIED.
- **Reporting cadence (large producers):** January–June data by 1 October; July–December by 1 April (secondary sources: [House of Commons Library](https://commonslibrary.parliament.uk/research-briefings/cbp-10352/)).

**Plastic Packaging Tax — IN FORCE.** **£228.82 per tonne from 1 April 2026** (was £223.69 in 2025/26) on plastic packaging components with **less than 30% recycled plastic** ([GOV.UK — PPT steps](https://www.gov.uk/guidance/check-if-you-need-to-register-for-plastic-packaging-tax); [Finance Act 2021 Part 2](https://www.legislation.gov.uk/ukpga/2021/26/part/2)).

**UK deposit return scheme (drinks containers) — ADOPTED, APPLIES FROM 1 October 2027** (England, Northern Ireland, Scotland; Wales position differs — UNVERIFIED); producers register with the deposit management organisation (UK DMO) before launch and pay fees by containers placed on the market ([Brodies](https://brodies.com/insights/environmental-social-and-governance/towards-a-uk-deposit-return-scheme-uk-government-reaffirms-its-commitment-to-an-october-2027-launch/); [ERP UK Aug 2026](https://erp-recycling.org/uk/news-and-events/2026/08/uk-deposit-return-scheme-are-you-ready-for-2027/)).

**EU Packaging and Packaging Waste Regulation (PPWR) — IN FORCE, generally applies from 12 August 2026** (Regulation (EU) 2025/40; in force 11 Feb 2025). Harmonised labelling applies from **12 August 2028 at the earliest** (24 months after the implementing act, which slipped beyond its Aug 2026 deadline). Producer registration/EPR, operator identification and declarations of conformity are among the August 2026 obligations ([Intertek](https://www.intertek.com/products-retail/insight-bulletins/2026/1536-eu-ppwr-requirements-effective-from-august/); [business.gov.uk PPWR page](https://www.business.gov.uk/campaign/europe/european-union-eu-regulations/eu-packaging-and-packaging-waste-regulation-eu-ppwr/); [Commission C(2026) 3702](https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=PI_COM%3AC%282026%293702)).

**ERP implication (high value):** packaging specification per item and per packaging level (material by category, weight, recycled content, recyclability rating, household/non-household, nation of sale); compute tonnage by period from shipments/receipts; PPT liability on manufactured/imported plastic components; DRS container counts; PPWR declarations. Very few mid-market ERPs do this natively.

### 3.10 UK and EU customs

- **UK Customs Declaration Service (CDS) — IN FORCE.** CDS replaced CHIEF for imports from 1 Oct 2022 (exports followed later) ([GOV.UK news](https://www.gov.uk/government/news/one-month-left-for-importers-to-move-to-single-customs-platform)).
- **UK safety and security (S&S GB) declarations for EU → GB imports — IN FORCE since 31 January 2025** (waiver ended); carrier is responsible; reduced dataset (20 mandatory fields) ([GOV.UK](https://www.gov.uk/government/publications/preparing-for-the-new-safety-and-security-declaration-requirements/get-ready-for-safety-and-security-declaration-requirements-for-importing-goods-from-the-eu)).
- **UK Single Trade Window — paused** for 2025–26 for affordability ([GOV.UK research](https://www.gov.uk/government/publications/exploring-changes-to-safety-and-security-declaration-requirements/research-exploring-changes-to-safety-and-security-declaration-requirements)). Current status beyond that: UNVERIFIED.
- **EU Union Customs Code and ICS2 — IN FORCE.** ICS2 Release 3 (road and rail) started 1 Apr 2025; fully operational for all modes from **1 Sep 2025**, with temporary derogations to 31 Dec 2025 ([Commission ICS2 R3 complete](https://taxation-customs.ec.europa.eu/news/transition-ics2-release-3-complete-limited-temporary-derogations-some-member-states-2025-08-29_en)).
- **EU €3 customs duty on low-value parcels — IN FORCE from 1 July 2026** (Regulation (EU) 2026/382 removed the €150 duty relief; interim until the Data Hub, ~July 2028); per-item vs per-consignment basis described inconsistently by sources ([Commission news 29 Jun 2026](https://commission.europa.eu/news-and-media/news/ensuring-fairness-and-safety-eur3-customs-duty-low-value-parcels-2026-06-29_en)).
- **EU customs reform — political agreement 26 March 2026 (PROPOSED until formally adopted):** EU Customs Authority (Lille), EU Customs Data Hub; e-commerce data to the Hub from July 2028; other businesses optional from 2031; full new UCC by 2034 ([Commission representation](https://cyprus.representation.ec.europa.eu/news/commission-welcomes-historic-agreement-reform-eu-customs-union-2026-03-26_en); [Finnish Customs](https://tulli.fi/en/customs-reform)). Formal adoption: UNVERIFIED.
- **ERP implication:** commodity codes per destination, origin and preferential origin evidence (UK–EU TCA), Incoterms, EORI per entity, customs value build-up, integration with customs brokers/software (not building declaration filing ourselves).

### 3.11 US UFLPA

- **IN FORCE since 21 June 2022** — rebuttable presumption that goods made wholly or partly in Xinjiang or by listed entities are made with forced labour.
- DHS added **43 entities on 31 Jul 2026** (Federal Register 3 Aug 2026), bringing the Entity List to **187**; 19 of the additions are outside Xinjiang; CBP detention activity had fallen since Jan 2025 but the expansion is read as a new enforcement wave ([Covington](https://www.cov.com/en/news-and-insights/insights/2026/08/dhs-expands-uflpa-entity-list-amid-intensifying-enforcement-landscape); [Kelley Drye](https://www.kelleydrye.com/viewpoints/blogs/trade-and-manufacturing-monitor/u-s-government-announces-largest-expansion-of-the-uflpa-entity-list-in-history-continues-focus-on-forced-labor-trade-enforcement); [Thompson Hine](https://www.thompsonhinesmartrade.com/2026/07/dhs-updates-uflpa-entity-list-with-43-additional-chinese-companies/)).
- **ERP implication:** supplier and sub-tier manufacturer records, screening against the Entity List (as configurable reference data, updated), mill/melt certificates and origin documents attached to lots.

### 3.12 US FSMA 204 (Food Traceability Rule)

- **Rule IN FORCE** (21 CFR Part 1 Subpart S). Original compliance date **20 January 2026**.
- **Extension:** FDA **proposed** (August 2025) moving the compliance date 30 months to **20 July 2028**. The Continuing Appropriations Act 2026 **directed FDA not to enforce the rule before 20 July 2028**, and FDA "intends to comply with this Congressional directive". FDA's page (content current as of 4 Nov 2026) still calls the extension proposed and does not say it was finalised ([FDA FSMA 204 page](https://www.fda.gov/food/food-safety-modernization-act-fsma/fsma-final-rule-requirements-additional-traceability-records-certain-foods); [Federal Register proposed extension](https://www.federalregister.gov/documents/2025/08/07/2025-14967/requirements-for-additional-traceability-records-for-certain-foods-compliance-date-extension)). FDA held a public meeting on lot-level traceability on 15 June 2026 ([FDA meeting](https://www.fda.gov/food/workshops-meetings-webinars-food-and-dietary-supplements/fda-public-meeting-challenges-and-solutions-lot-level-food-traceability-06152026)).
- **Verdict on the brief's "verify extension to July 2028":** **partly verified** — enforcement from 20 Jul 2028 is effectively set by Congress; a final rule codifying it: UNVERIFIED (not found).
- **ERP implication:** Food Traceability List items flagged; capture Key Data Elements for each Critical Tracking Event (harvesting, cooling, initial packing, first land-based receiving, shipping, receiving, transformation) including traceability lot code and its source; produce an electronic sortable spreadsheet within 24 hours of an FDA request.

### 3.13 US tariffs 2025–2026 (landed cost and classification)

- **IEEPA tariffs — invalid.** On **20 February 2026** the Supreme Court held 6–3 in *Learning Resources, Inc. v. Trump* that IEEPA does not authorise tariffs ([Justia](https://supreme.justia.com/cases/federal/us/607/24-1287/); [A&O Shearman](https://www.aoshearman.com/en/insights/scotus-rejects-ieepa-tariffs-refund-opportunities-and-uncertainty-emerge)). Collection reportedly ended 24 Feb 2026; refunds are being handled through the Court of International Trade and CBP and are not automatic ([CBP IEEPA FAQ](https://www.cbp.gov/trade/programs-administration/trade-remedies/IEEPA-FAQ); [Troutman](https://www.troutman.com/insights/getting-duties-back-where-recovery-stands-under-ieepa-section-122-and-section-301-forced-labor-tariffs/)).
- **Section 122 — expired.** A 10% global surcharge imposed after the ruling ran its 150-day statutory term and **expired 24 July 2026**; a CIT ruling against it (May 2026) only helped three named plaintiffs (secondary sources: [Z2Data](https://www.z2data.com/insights/how-the-termination-of-section-122-tariffs-impacts-your-supply-chain/), [Kroll](https://www.kroll.com/en/publications/a-tale-of-tariff-substitution)).
- **Section 301 "forced labour" tariffs — IN FORCE from 24 July 2026:** reported additional 10% or 12.5% on imports from ~60 economies; products under Section 232 typically exempt; further Section 301 actions (industrial overcapacity) pending (secondary sources: [Wiley tracker](https://www.wiley.law/trump-administration-tariff-tracker), [Wipfli](https://www.wipfli.com/insights/articles/tariff-update-new-section-301-tariffs-section-232-and-more)). Exact rates/country list: UNVERIFIED against USTR notices.
- **Section 232 — IN FORCE**, restructured April 2026: full-value tariffs on steel, aluminium, certain copper and derivative articles at **50%**, with reduced rates for certain UK products and for derivatives made entirely of US-origin metal; a later proclamation set certain copper articles and derivatives at 25% ([Federal Register 2026-06960](https://www.federalregister.gov/documents/2026/04/09/2026-06960/strengthening-actions-taken-to-adjust-imports-of-aluminum-steel-and-copper-into-the-united-states); [White House annexes](https://www.whitehouse.gov/wp-content/uploads/2026/04/ANNEXES-I-A-I-B-II-III-IV.pdf)). Also semiconductors 25% (from 15 Jan 2026, with exemptions), medium/heavy trucks and parts 25%, buses 10%, softwood timber/lumber 10%, upholstered wooden furniture and kitchen cabinets/vanities 25% or 15% (CBP factsheets conflict), pharmaceuticals (CSMS 70054007, 28 Sep 2026; rates not confirmed) ([CBP tariff overview Feb 2026](https://www.cbp.gov/sites/default/files/2026-02/U.S.%20Tariff%20Overview%20February%202026_0.pdf); [CBP trade remedies](https://www.cbp.gov/trade/programs-administration/trade-remedies)).
- **De minimis — suspended.** EO 14324 (30 Jul 2025) suspended the $800 de minimis for all countries from 29 Aug 2025; after the IEEPA ruling CBP issued interim final rules (published 24 Jun 2026) **indefinitely suspending** it for all modes; the statutory exemption is **repealed from 1 July 2027** by the One Big Beautiful Bill Act ([Federal Register IFR](https://www.federalregister.gov/documents/2026/06/24/2026-12670/indefinite-suspension-of-the-de-minimis-exemption-for-merchandise-arriving-through-all-modes-other); [KPMG](https://kpmg.com/us/en/taxnewsflash/news/2026/06/cbp-suspends-de-minimis-exemption.html)).
- **ERP implication:** tariff programme as effective-dated reference data (HTS + Chapter 99 + country + programme + stacking/exclusion rules + metal content basis), never code; landed-cost estimates on PO lines; component-level origin and metal content (value of steel/aluminium/copper content); duty-paid tracking per entry for refunds and drawback; scenario costing ("what if origin changes"). This is a strong US differentiator for distributors and makers.

### 3.14 REACH, RoHS, WEEE

- **EU REACH (Regulation (EC) 1907/2006) — IN FORCE.** Article 33 obligation to communicate SVHC presence above 0.1% w/w in articles and the SCIP database notification (Waste Framework Directive Art 9) continue. **Full REACH revision dropped:** Commissioner Roswall told MEPs on 27 April 2026 the Commission would not table the revision proposal and would instead simplify through annex amendments (comitology) ([Sustainability in Business blog](https://www.sustainabilityinbusiness.blog/2026/04/commission-officially-sets-aside-plans-for-a-full-revision-of-reach/)) — secondary source; primary statement UNVERIFIED.
- **UK REACH — IN FORCE.** Draft REACH (Amendment) (No 2) Regulations 2026 (laid 24 Mar 2026) move transitional registration deadlines from 27 Oct 2026/2028/2030 to **27 Oct 2029/2030/2031** and adopt the Alternative Transitional Registration model (ATRm) with hazard conclusions rather than full datasets ([Welsh Government written statement](https://www.gov.wales/written-statement-reach-amendment-no-2-regulations-2026); [Hansard debate 8 Jun 2026](https://hansard.parliament.uk/commons/2026-06-08/debates/d223fa39-c061-4f29-9d90-9cc3cd841457/DraftREACH(Amendment)(No2)Regulations2026)). Whether made and in force: UNVERIFIED.
- **RoHS (Directive 2011/65/EU) — IN FORCE**; no recast proposal found (UNVERIFIED).
- **WEEE (Directive 2012/19/EU) — IN FORCE**; revision expected inside the EU **Circular Economy Act** (autumn 2026) — PROPOSED/UNVERIFIED ([Mondaq](https://www.mondaq.com/eu-weee-directive-reform-tighter-rules-rising-costs/1846942); [Landbell 2026 outlook](https://landbell-group.com/news/focus-on-2026/)). UK WEEE reform: not researched (UNVERIFIED).
- **ERP implication:** substance declarations per item/supplier, SVHC candidate list as updatable reference data, RoHS/REACH certificates with expiry, EEE category and weight for WEEE producer reporting.

### 3.15 GS1 standards

- **INDUSTRY standards.** GTIN (8/12/13/14), SSCC (18-digit pallet/logistic unit), GLN (locations), GS1-128, GS1 DataMatrix, GS1 Digital Link URIs.
- **Sunrise 2027 — INDUSTRY milestone (not law):** GS1 US goal for US retail POS to read 2D barcodes (GS1 DataMatrix, QR with GS1 Digital Link) by end-2027; UPC/EAN continue to scan; dual marking during transition. The global GS1 guideline ("Ambition 2027") sets minimum capability to process the GTIN from 2D symbols ([GS1 US Sunrise 2027](https://www.gs1us.org/industries-and-insights/by-topic/sunrise-2027); [GS1 2D in retail guideline](https://ref.gs1.org/guidelines/2d-in-retail/)).
- **ERP implication:** generate and parse GS1 Application Identifiers (lot 10, expiry 17, serial 21, weight 310n) and Digital Link URIs; SSCC generation from the tenant's GS1 company prefix; label templates (GS1-128 pallet labels) — cheap to build, valued by retailers and needed for DPP carriers.

### 3.16 Electronic records and signatures: 21 CFR Part 11, EU GMP Annex 11 (and draft Annex 22)

- **21 CFR Part 11 — IN FORCE** (US FDA): trustworthy electronic records and signatures — validation, secure computer-generated time-stamped audit trails, authority checks, signature manifestation (name, date/time, meaning), signature/record linking.
- **EU GMP Annex 11 (2011) and Chapter 4 — IN FORCE.** Revised Annex 11 and Chapter 4 and a **new Annex 22 (Artificial Intelligence)** were published as drafts on 7 July 2025 (consultation closed 7 Oct 2025); an EMA workshop was held 30 Jun–1 Jul 2026; **no final texts as of late September 2026** — PROPOSED. Draft Annex 22 restricts critical GMP use to static, deterministic models and says generative AI/LLMs should not be used in critical GMP applications, though EMA is reconsidering ([Epista](https://www.epista.com/knowledge/preparing-for-emas-2026-good-manufacturing-practice-gmp-revisions-chapter-4-annex-11-annex-22); [IntuitionLabs](https://intuitionlabs.ai/articles/eu-gmp-annex-22-ai-compliance-pharma-2)). Secondary sources; EudraLex page not re-read.
- **ERP implication:** to serve regulated manufacturers later, build now: immutable audit trails (already a Thapsus rule), re-authentication signatures with meaning, reason-for-change prompts, validation documentation pack per release, configuration change control. Keep AI out of GMP-critical decisions by design.

### 3.17 Medical devices: UDI, FDA QMSR, EUDAMED

- **FDA UDI rule (21 CFR Parts 801 and 830, GUDID) — IN FORCE** (from prior knowledge; not re-read this session).
- **FDA QMSR — IN FORCE from 2 February 2026:** 21 CFR Part 820 now incorporates ISO 13485:2016 (and ISO 9000:2015 clause 3) by reference; FDA moved from QSIT to compliance programme 7382.850; records made before 2 Feb 2026 need not be recreated ([FDA QMSR](https://www.fda.gov/medical-devices/postmarket-requirements-devices/quality-management-system-regulation-qmsr); [FDA QMSR FAQ](https://www.fda.gov/medical-devices/quality-management-system-regulation-qmsr/quality-management-system-regulation-frequently-asked-questions)).
- **EU MDR/IVDR EUDAMED — IN FORCE (mandatory use of four modules from 28 May 2026)** following Commission Decision (EU) 2025/2371 (27 Nov 2025): actor registration, UDI/device registration, notified bodies and certificates, market surveillance. Registration of devices already on the market by about **27/28 Nov 2026** (BSI vs HPRA differ); vigilance module expected 2027 ([HPRA](https://www.hpra.ie/news-events/news/article/mandatory-use-of-eudamed-modules-for-medical-devices); [DNV](https://www.dnv.com/article/eudamed-mandatory-use-what-manufacturers-need-to-know/)).
- **ERP implication:** UDI-DI on item/packaging level, UDI-PI (lot, serial, expiry, manufacture date) on lots, label generation; device history record linkage. Enterprise tier; possibly relevant to care-sector suppliers.

### 3.18 ISO 9001, ISO 22000, BRCGS — what certifiers expect of an ERP

- **ISO 9001:2026 — INDUSTRY standard, published 16 September 2026** per certification bodies; three-year transition expected (to ~15 Sep 2029) but IAF transition rules not yet confirmed in sources found ([NSF](https://www.nsf.org/in/en/knowledge-library/iso-90012026-published-on-september-16-2026-what-quality-leaders-need-to-know); [TÜV SÜD](https://www.tuvsud.com/en/knowledge-hub/articles/iso-9001-2026-everything-you-need-to-know-about-the-new-revision); [LRQA](https://www.lrqa.com/en/latest-news/iso-9001-publication-date-confirmed/)).
- **ISO 22000:2018** (food safety management) — INDUSTRY; **BRCGS Food Safety Issue 9** (August 2022) current; Issue 10 timing UNVERIFIED (forum speculation of 2027). BRCGS requires periodic traceability tests completed within a short time limit (four hours under Issue 9 — from prior knowledge, UNVERIFIED this session).
- **What auditors look for in ERP:** controlled item/specification master with revisions; approved supplier list and supplier performance; lot traceability forward/backward with timed test reports; non-conformance and CAPA records; calibration and maintenance records; training/competence evidence (from Thapsus-HR); document control; customer complaints linked to lots; management review KPIs.

### 3.19 Dangerous goods

- **IN FORCE (international regimes, updated biennially):** ADR 2025 (road, Europe/UK), IMDG Code **Amendment 42-24 mandatory from 1 January 2026** ([IMO amendment cycle](https://wwwcdn.imo.org/localresources/en/publications/Documents/IMDG%20Code/IMDG%20Code%20Amendment%20Cycle%20-%202025-2034.pdf)), IATA DGR **67th edition** for 2026; US 49 CFR (HMR). ADR 2025 transitional end date (30 Jun 2025): UNVERIFIED.
- **ERP implication:** UN number, proper shipping name, class, packing group, limited/excepted quantity, tunnel code, marine pollutant flag on items; segregation in storage; DG declarations on shipments; versioned reference data by edition.

### 3.20 Adjacent regulation affecting ERP design

- **EU AI Act — IN FORCE**, amended by the Digital Omnibus on AI (**Regulation (EU) 2026/1744**, OJ 24 Jul 2026 per secondary sources): Annex III stand-alone high-risk obligations moved to **2 December 2027**; Annex I product-embedded systems to 2 Aug 2028; GPAI obligations and transparency duties largely on original timeline ([Orrick](https://www.orrick.com/en/Insights/2026/07/EU-AI-Act-Update-Digital-Omnibus-Finalizes-8-Compliance-Changes); [Cooley](https://cdp.cooley.com/digital-ai-omnibus-delays-key-deadlines-introduces-new-rules/)). Most ERP AI features (forecasting, document capture) are not Annex III high-risk; anything that allocates work or evaluates workers (shop-floor scheduling by person, performance) can touch the "employment" category — keep person-level decisions out of AI scope.
- **UK mandatory e-invoicing — announced (Budget 2025), effective April 2029** for B2B and B2G VAT invoices, Peppol as core framework; legislation planned in Finance Bill 2026-27 — PROPOSED/announced ([GOV.UK e-invoicing roadmap](https://www.gov.uk/government/publications/e-invoicing-implementation-roadmap/roadmap-for-e-invoicing-implementation)). Mostly MULLAH; KASONGO should support Peppol ordering/despatch so the whole order-to-invoice chain is Peppol-native.
- **EU ViDA — IN FORCE** (Council Directive (EU) 2025/516): Member States may mandate domestic e-invoicing now; intra-EU B2B e-invoicing and digital reporting from **1 July 2030** (secondary sources: [KPMG](https://kpmg.com/be/en/insights/my-tax-compass/indirect-tax-insights/political-agreement-reached-on-the-eu-vat-in-the-digital-age-proposal.html), [PwC Malta](https://www.pwc.com/mt/en/publications/vat/digital-reporting-and-e-invoicing-in-the-eu.html)).
- **EU General Product Safety Regulation (EU) 2023/988** — applies since 13 Dec 2024 (prior knowledge; not re-verified): traceability and recall duties for consumer products — supports lot/serial traceability and recall features.

---

## 4. AI in ERP in 2026

### 4.1 What the leaders actually ship (status as found)

| Vendor | Shipped / generally available | Preview or announced | Interoperability |
|---|---|---|---|
| **SAP** | Joule copilot across S/4HANA Cloud; embedded AI; 14 Joule agents announced at SAP Connect Oct 2025 incl. **Production Planning and Operations Agent** (checks prerequisites and releases production orders when conditions are met; GA planned Q1 2026); Change Record Management Agent; **Bid Analysis Agent** (procurement, GA planned Q1 2026); Supply Chain Orchestration embedded AI (H1 2026); Joule Studio (GA planned Dec 2025) ([SAP News Oct 2025](https://news.sap.com/2025/10/sap-connect-business-ai-new-joule-agents-embedded-intelligence/)) | SAP Connect Oct 2026: agents for Manufacturing Assistant (detect plant-floor disruptions), Supply Chain Planning Assistant (sense/simulate/resolve exceptions), Business Network Assistant (supplier/logistics collaboration), GA reported Q4 2026 ([SAPinsider](https://sapinsider.org/blogs/sap-connect-2026-how-new-agents-will-detect-and-respond-to-supply-disruptions)) | Storefront MCP server for Commerce Cloud (planned Q2 2026); MCP gateway in Integration Suite; A2A in development (secondary: [AIMultiple](https://aimultiple.com/sap-ai-agents)) — UNVERIFIED for S/4HANA Public Edition |
| **Oracle NetSuite** | Bill Capture (OCR + ML extraction from vendor bills, PO matching); generative text assist; NetSuite 2026.1 (Feb 2026): AI close and cash-management features, AI agents for planning and reconciliation, supply-chain and demand analytics templates ([Rand Group](https://www.randgroup.com/insights/oracle-netsuite/netsuite-2026-1-release-ai-driven-finance-operations-and-automation-enhancements/); [Sikich](https://www.sikich.com/insight/netsuite-2026-1-ai-features-whats-new/)) | "NetSuite Next" (SuiteWorld Oct 2025) rollout — UNVERIFIED; SuiteAgents framework (developer-built agents on SuiteCloud) | **AI Connector Service**: hosted MCP server (OAuth 2.0, respects role permissions, Administrator role blocked) exposing records, reports, saved searches and SuiteQL to external assistants; announced 7 Oct 2025 ([Computer Weekly](https://www.computerweekly.com/news/366632408/SuiteWorld-2025-NetSuite-unveils-AI-innovations-for-future-business); [KORE1](https://www.kore1.com/netsuite-mcp-connector/)) |
| **Microsoft Business Central** | 2026 wave 1 (v28): **Sales Order Agent GA** — monitors a shared mailbox, reads customer requests, creates draft quotes/orders for human review; **Payables Agent GA** (vendor invoices); Copilot features (marketing text, bank reconciliation, analysis assist) ([Microsoft Learn 2026 wave 1](https://learn.microsoft.com/en-us/dynamics365/release-plan/2026wave1/smb/dynamics365-business-central/planned-features)) | Expense agent (preview May 2026); custom agent designer (preview); wave 2 (v29, Oct 2026) improved PO matching | **MCP server** for BC with telemetry and audit logs (enhancements June 2026) |
| **Dynamics 365 SCM** | Demand planning with AI forecasting; Copilot in planning workspaces | **Procurement Agent / Supplier Communications Agent — production-ready preview** (GA planned Mar 2026 not confirmed): classifies vendor emails as confirmations/change requests, drafts PO follow-up emails; **sending without review is optional and off by default**; Excel attachments (2026 wave 1); Supplier Engagement workspace preview (Aug 2026) ([Learn — Procurement Agent](https://learn.microsoft.com/en-us/dynamics365/supply-chain/procurement/procurement-agent-overview); [follow-up](https://learn.microsoft.com/en-us/dynamics365/supply-chain/procurement/procurement-agent-supplier-com-follow-up); [Supplier Engagement blog](https://www.microsoft.com/en-us/dynamics-365/blog/it-professional/2026/08/06/supplier-engagement-supply-chain-management/)) | Copilot Studio, Dataverse, MCP |
| **Odoo** | Odoo 19 (Sept 2025): AI agents grounded in uploaded documents, **AI fields**, "Ask AI" natural-language search (Ctrl+K), AI in server actions and email templates; Purchase: forecast-based purchasing, alternative RFQs; long-standing OCR document digitisation for bills ([Odoo 19 release notes](https://www.odoo.com/odoo-19-release-notes)) | 19.1 file Q&A in agents; **19.4: automatic AI model selection and MCP connection** ([Odoo 19.4 notes](https://www.odoo.com/odoo-19-4-release-notes)) | MCP (19.4) |
| **Acumatica** | 2026 R1 (GA March 2026): **AI Studio**; **anomaly detection** applicable to any Generic Inquiry; AP **document recognition** (creates bills for review); expense automation; conversational data analysis; file classification ([Acumatica 2026 R1 blog](https://www.acumatica.com/blog/acumatica-2026-r1-acumatica-ai-enabled-product-release-delivers-intelligence/); [MYOB release note — anomaly detection](https://help.myob.com.au/advanced/Docs/Published/ReleaseNotes/RN_2026_R1_Finance_AnomalyDetection_GI.html)) | AI Assistant (limited/experimental access); AI agents previewed Jan 2026 | — |
| **Epicor** | **Epicor Prism**: vertical AI agents inside Kinetic (cloud); 18+ agents launched in UK/selected Europe; **Agent Foundry** for building agents (May 2026) ([BusinessWire May 2026](https://www.businesswire.com/news/home/20260519098303/en/Epicor-Introduces-Agentic-AI-Stack-to-Power-Action-Across-ERP-Workflows); [PortalERP](https://portalerp.com/article/epicor-expands-embedded-ai-platform-to-europe)) | 30+ more agents in development (planning, compliance, invoicing, logistics, sustainability) | Open **MCP** connections to Kinetic business logic |
| **IFS** | **IFS Loops** digital workers (Oct 2025: 10 workers, 50 skills — field dispatch, supplier coordination, customer order management, inventory replenishment) ([IFS](https://www.ifs.com/news/product/ifs-loops)) | **Loops Agent Studio** (April 2026) for custom digital workers ([IFS Apr 2026](https://www.ifs.com/en/insights/news/ifs-loops-launches-agent-studio)); claims of 60% fully automated agentic transactions (secondary, [ERP Today](https://erp.today/ifs-h1-2026-results-industrial-ai-growth/)) | — |
| **SMB tools** | Cin7 ForesightAI forecasting (add-on); Unleashed demand forecasting (Pro plan) | — | — |

### 4.2 Concrete AI feature list for KASONGO, with guardrails

All features: **off by default**, enabled per tenant, per feature and per role; routed through the shared Thapsus AI gateway; inference pinned to the tenant's home region (model availability per Google Cloud region to be confirmed — UNVERIFIED); every output is a **draft or recommendation** with an evidence panel; nothing posts to stock, ledger or a supplier without a named human approval; all prompts, inputs references, outputs and decisions audit-logged; a deterministic non-AI fallback exists for every workflow.

| # | Feature | Who ships something similar | How it stays optional | How it stays explainable | Human approval |
|---|---|---|---|---|---|
| 1 | **Demand forecasting** (statistical first: exponential smoothing, Croston for intermittent; ML optional) | NS, SCM, OD, C7, UL, EP, S4 | Feature flag; default is plain moving average / manual forecast | Show method, history window, seasonality, accuracy (MAPE/bias) per item; compare to naive forecast | Planner accepts/overrides forecast versions; overrides recorded with reason |
| 2 | **Inventory optimisation — safety stock and reorder-point suggestions** | EP (SIPO), NS, SCM, C7 | Suggestions list only | Show service-level target, lead-time variability, demand variability, formula used | Approve per item or in bulk with thresholds; changes effective-dated |
| 3 | **Supplier risk signals** (late deliveries trend, quality PPM, price drift; optional external sanctions/UFLPA/ESG data) | S4 (Ariba), SCM | Off; external data sources individually opt-in and listed as sub-processors | Score broken into contributing factors with links to transactions | Buyer decides actions (block, dual-source); no automatic blocking except explicit sanctions-list rule configured by admin |
| 4 | **Purchase-order automation — draft POs from MRP/reorder suggestions** | SAP Bid Analysis, IFS digital workers (replenishment), BC agents | Agent disabled by default; per-supplier allow-list | Each draft links to the triggering demand/stock signal and price source | PO approval workflow unchanged; agent never sends to supplier |
| 5 | **Supplier communication agent** (reads supplier emails: confirmations, date changes; drafts chasers) | SCM Supplier Communications Agent (auto-send off by default) | Off; mailbox connection explicit | Highlights extracted fields and source sentence | User reviews every proposed PO change and every outbound email; optional auto-send only for templated chasers, admin-enabled |
| 6 | **Document capture of supplier documents** (invoices, delivery notes, CoAs, certificates of origin, EUDR references, mill certificates) | NS Bill Capture, AC document recognition, OD digitisation, BC Payables Agent | Off; OCR provider/model must be region-pinned and in SUBPROCESSORS | Side-by-side field-to-image highlighting, confidence per field | Low-confidence fields require confirmation; documents never auto-posted |
| 7 | **Sales order capture from email/PDF** | BC Sales Order Agent (GA) | Off | Matches shown (customer, items, prices, dates) with alternatives | Order created as draft; human releases |
| 8 | **Predictive maintenance** (meter/sensor trends, failure prediction) | IFS, S4, EP | Off; requires IoT data feed | Show signal, threshold, model confidence, similar past failures | Creates suggested maintenance work order; supervisor approves |
| 9 | **Anomaly detection** (unusual stock adjustments, price/cost outliers, duplicate supplier invoices, negative margins, shrinkage) | AC (any inquiry), NS, S4 | Off; per-inquiry enablement | Show baseline, deviation and the specific records | Alerts only; investigator closes with outcome (feedback loop) |
| 10 | **Production scheduling optimisation** (finite capacity, sequence-dependent setups) | S4 (PP/DS + Joule agent), EP, AC APS, IFS | Off; deterministic APS heuristic is the default | Show objective (due-date adherence, setup time), constraints, and why an order moved | Planner publishes schedule; no automatic release to shop floor; never schedules individuals by AI (AI Act employment risk) |
| 11 | **Natural-language queries and reports** ("which lots of X shipped to Y last month?") | OD Ask AI, AC conversational analysis, SAP Joule, NS | Off | Show generated query/filter and data source; results are read-only | Read-only; saving as report requires user |
| 12 | **Agents that draft orders/POs/transfers for approval** (multi-step) | BC agents, SAP Joule agents, IFS Loops, Epicor Prism | Off; per-agent permission set narrower than the user's | Plan and tool calls shown step-by-step; replayable log | Mandatory approval gate before any state change; budget/quantity caps |
| 13 | **MCP server** exposing KASONGO read tools and draft-only write tools to customers' own assistants | NS AI Connector Service, BC MCP server, Epicor MCP, Odoo 19.4 MCP, SAP (Commerce/Integration Suite) | Off by default; per-tenant enablement, OAuth scopes, admin roles excluded (as NetSuite does) | Tool descriptions and per-call audit; rate limits | Write tools create drafts only; human approval in KASONGO UI |
| 14 | **Item master enrichment** (descriptions, attributes, HS code suggestions, packaging material classification) | OD AI fields, S4 | Off | Suggested value with reasoning and source text | User accepts each suggestion; HS code suggestions flagged as advisory (customs liability stays with importer) |
| 15 | **Landed-cost/tariff scenario assistant** | Few | Off | Shows the tariff rules (reference data) applied | Advisory only |

**Design rules derived from the market:** (a) "draft then approve" is the industry norm (BC, SCM, SAP procurement boundary statement); (b) admin/elevated roles excluded from agent connectors (NetSuite); (c) auto-send off by default (SCM); (d) GMP customers: no generative AI in GMP-critical decisions (draft Annex 22); (e) agents act with a scoped service identity, never the user's full rights; (f) cost and usage metering per tenant (AI credits) for pricing.

---

## 5. Integration points

### 5.1 ERP ↔ accounting ledger (MULLAH)

**Principle:** KASONGO keeps the operational sub-ledgers (stock ledger, cost layers, WIP, open receipts) and sends **balanced posting requests** to MULLAH's general ledger via the transactional outbox (same transaction as the stock move), with an idempotency key per business event. MULLAH owns chart of accounts, periods, AP/AR, tax and consolidation. Account determination (which GL account) is configuration in KASONGO keyed by entity × item posting group × location × transaction type (as BC's posting groups and SAP's account determination do).

| Business event (KASONGO) | Typical posting (perpetual inventory) | Notes |
|---|---|---|
| Goods receipt against PO | Dr Inventory / Cr GRNI (goods received not invoiced; NetSuite "Inventory Received Not Billed"; SAP GR/IR) | Standard cost: Dr Inventory at standard, Cr GRNI at PO price, difference to purchase price variance |
| Supplier invoice matched (in MULLAH AP) | Dr GRNI / Cr AP; invoice price variance to PPV or back to inventory if stock remains (average/FIFO) | Needs ERP cost layers to revalue on-hand stock |
| Landed cost actualised | Dr Inventory (or COGS if sold) / Cr landed-cost accrual (freight/duty clearing) | Estimated at receipt, trued-up later |
| Sales shipment | Dr COGS / Cr Inventory | Revenue posts from MULLAH AR invoice; shipped-not-invoiced accrual optional |
| Customer return | Dr Inventory (or returns/quarantine) / Cr COGS | |
| Stock adjustment / cycle count | Dr/Cr Inventory adjustment (shrinkage) / Cr/Dr Inventory | Reason code → account |
| Transfer between sites (same entity) | Dr Inventory-in-transit / Cr Inventory; then Dr Inventory / Cr in-transit | |
| Intercompany sale/transfer | Seller: Dr IC receivable / Cr IC revenue; Dr COGS / Cr Inventory. Buyer: Dr Inventory / Cr IC payable | Transfer price from KASONGO; eliminations in MULLAH |
| Material issue to production | Dr WIP / Cr Inventory (raw materials) | Backflush may defer |
| Labour and machine time on job | Dr WIP / Cr Labour applied / Overhead applied | Uses standard labour rates by grade (not individual pay) |
| Finished goods receipt | Dr Inventory (FG) / Cr WIP | |
| Production order close | Variances (material usage, rate, efficiency, scrap, overhead) Dr/Cr Variance accounts / Cr/Dr WIP | Standard costing |
| Standard cost revaluation | Dr/Cr Inventory / Cr/Dr Revaluation | Effective-dated cost versions |
| Scrap / write-off / obsolescence provision | Dr Scrap expense / Cr Inventory; provision via MULLAH | |
| Consignment consumption | Dr Inventory or COGS / Cr AP (vendor) | Ownership change triggers posting |
| Rebate accruals | Dr Rebate expense / Cr Accrued rebates (customer); supplier: Dr Receivable / Cr COGS or Inventory | |
| Cost adjustment run (FIFO/average re-costing after late invoices) | Dr/Cr Inventory / Cr/Dr COGS | Batch, period-aware |

**Real-time vs batch at the leaders:**
- **NetSuite:** posts GL impact at the transaction in real time (item receipt hits Inventory and Inventory Received Not Billed; bill clears it) ([community explanation](https://community.oracle.com/netsuite/english/discussion/4257815/inventory-billed-not-received)) — official docs not reached (403).
- **SAP S/4HANA:** Universal Journal (ACDOCA) stores inventory valuation and Material Ledger data in the same table as GL — real-time single source; Material Ledger mandatory, actual costing optional and run at period end ([SAP PRESS blog](https://blog.sap-press.com/the-material-ledger-and-actual-costing-with-sap-s4hana); [PIKON](https://www.pikon.com/en/blog/introduction-to-s4hana-material-ledger-and-actual-costing/)).
- **Business Central:** each inventory transaction creates item ledger and value entries; value entries reach the GL either immediately (**Automatic Cost Posting**) or by the **Post Inventory Cost to G/L** batch job; **Adjust Cost – Item Entries** is a separate (scheduled) batch for cost re-calculation ([Microsoft Learn — inventory posting](https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-inventory-posting)).
- **Odoo:** perpetual ("automated") valuation posts journal entries at each stock move; periodic ("manual") valuation leaves stock valuation to period-end entries (from Odoo documentation knowledge; Odoo 19 doc page did not render — UNVERIFIED for v19 changes).

**Recommendation:** near-real-time posting requests per event (outbox → MULLAH), with **batch cost-adjustment runs** and a **period-close reconciliation report** (stock sub-ledger vs GL control accounts by entity/location/account). Respect MULLAH period locks (post to next open period with a flag). Multi-currency: ERP sends transaction currency and amounts in minor units; MULLAH applies rates.

### 5.2 ERP ↔ CRM (BOSSMAN)

| Data / flow | Master | Direction | Mechanism |
|---|---|---|---|
| Customer account (sold-to, ship-to, bill-to), credit limit, payment terms | Prospects in BOSSMAN; trading accounts shared party record; credit in MULLAH | Bidirectional (party service) | Shared Thapsus "party" identity; events |
| Product catalogue (items, variants, UoM, descriptions, images, availability flags) | KASONGO | ERP → CRM | Events + API |
| Price lists, customer-specific prices, discounts, margin floors | KASONGO (pricing engine) | ERP → CRM, or CRM calls ERP pricing API at quote time | Synchronous price API preferred to avoid drift |
| Configurable products (CPQ) | KASONGO configurator rules | CRM embeds configurator | API/embedded UI |
| Quote | BOSSMAN owns the commercial quote; KASONGO validates lines (price, ATP, lead time) | CRM → ERP (validation) | Synchronous |
| ATP / CTP and promise dates | KASONGO | CRM → ERP request/response | Synchronous API with caching |
| Order creation (quote accepted) | KASONGO order | CRM → ERP | Command with idempotency key |
| Order status, allocations, shipments, tracking, backorders, returns | KASONGO | ERP → CRM | Events |
| Invoices, payments, overdue status | MULLAH | Finance → CRM | Events |
| Customer service cases linked to lots/serials (complaints) | BOSSMAN case; ERP lot/serial | Bidirectional | Links |

Quote-to-cash sequence: opportunity (BOSSMAN) → quote with ERP pricing/ATP → acceptance → sales order (KASONGO) → credit check (MULLAH) → allocation/pick/pack/ship (KASONGO) → invoice (MULLAH AR, triggered by shipment event) → payment (MULLAH) → status back to BOSSMAN.

### 5.3 ERP ↔ HR (Thapsus-HR)

| Data / flow | Master | Notes |
|---|---|---|
| Worker identity, organisation, site, cost centre, employment status | Thapsus-HR | Minimal fields to ERP: worker ID, display name, site, department, active flag (data minimisation) |
| Labour cost rates | KASONGO holds **standard labour rates by grade/work centre** (configured), optionally derived from HR pay bands | Avoid importing individual pay into ERP; HR never runs payroll, so actual pay is not in the suite anyway |
| Skills, certifications, training (forklift licence, food hygiene, GMP training, LOLER competent person, gas/electrical tickets) with expiry | Thapsus-HR | ERP **gates** operations: only certified workers can be assigned to/clock onto operations requiring a skill; expired certs block; audit-logged |
| Rotas and availability, leave | Thapsus-HR | Feeds capacity of labour-constrained work centres and field-service dispatch |
| Attendance clocking (in/out of shift) | Thapsus-HR | Source of truth for hours worked |
| Job/operation time (clock on/off a work order, maintenance job, project task) | KASONGO shop floor / mobile | Reconcile: job time within attendance; unallocated time report; one kiosk login for both (single sign-on) |
| Timesheets for projects | Thapsus-HR approves time | ERP consumes approved time for project costing |
| Asset register (assets issued to people: laptops, PPE, vans, tools) | Thapsus-HR asset register | ERP EAM owns plant/equipment maintenance; MULLAH owns fixed-asset accounting; one shared asset ID across all three |

Privacy: shop-floor productivity data is employee personal data; keep person-level analytics opt-in and out of AI decision-making (AI Act employment category; UK GDPR).

### 5.4 ERP ↔ care sector (Thapsus Care)

| Area | ERP capability used | Care-specific notes |
|---|---|---|
| **Procurement of consumables** (continence products, PPE, wound care, cleaning chemicals, nutrition supplements) | Requisitions from each home/unit (mobile), par levels per location, framework agreements, group purchasing across homes (multi-entity), supplier catalogues, three-way match | Care groups buy under frameworks and supplier catalogues; Peppol ordering is used in UK public sector (NHS) — relevance to private care providers UNVERIFIED |
| **Catering stock** | Recipes (menu items as BOMs), ingredient stock with lots and expiry (FIFO/FEFO), allergen data per ingredient and recipe (14 regulated allergens under UK Food Information Regulations), supplier specifications, stock counts per kitchen, waste recording | Allergen and dietary (IDDSI texture) data are safety-critical for residents; the resident's dietary needs stay in Thapsus Care — ERP only supplies recipe/ingredient facts |
| **Facilities maintenance** | EAM: asset register per home (hoists, slings, bath lifts, lifts, boilers, fire systems, nurse-call), PM schedules, contractor work orders, certificates | LOLER: equipment for lifting people and lifting accessories (e.g. slings) must be thoroughly examined at least every **6 months** (12 months other lifting equipment) by a competent person, with reports stating the next due date ([HSE — thorough examinations](https://www.hse.gov.uk/work-equipment-machinery/thorough-examinations-lifting-equipment.htm); [HSE HSG220 care homes](https://books.hse.gov.uk/gempdf/hsg220.pdf)). Other statutory schedules (legionella, gas, electrical, fire) should be configurable reference data, not hard-coded |
| **Medicines stock** | Out of KASONGO scope | Keep controlled drugs, MAR and medicines stock in Thapsus Care (clinical safety, DCB0129, separation of duties); ERP may only supply supplier/pricing data for non-medicinal consumables |
| **Linen, uniforms, equipment issue** | Inventory + HR asset register | |

### 5.5 Cross-product integration architecture (recommendations)

- **Shared platform masters:** party (customer/supplier/organisation), worker, location/site, item (for products that sell items), legal entity — each with one owning product and event-carried state transfer to others.
- **Same home region for all products of a tenant** (UK/EU/US cell); cross-product calls stay inside the cell; no cross-region replication.
- **Contracts:** OpenAPI 3.1 for commands/queries; versioned event schemas (outbox) for facts; idempotency keys on every command.
- **Identity:** one tenant directory, SSO across products; agent/service identities scoped per product.

---

## 6. No-code customisation and upgrade safety

### 6.1 How the leaders do it

| Vendor | No-code / low-code configuration | Pro-code extension | Upgrade-safety mechanism |
|---|---|---|---|
| **Business Central** | Personalisation (users) and customisation (admins) of pages, profiles/role centres, Word/RDLC/Excel report layouts, workflows (approval templates), number series, configuration packages, Power Automate | AL extensions (per-tenant or AppSource apps) | Base application cannot be modified in SaaS; only extensions via events/interfaces; Microsoft runs updates twice yearly with extension compatibility checks ([BC developer overview](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/devenv-dev-overview)) — from documentation knowledge |
| **NetSuite** | SuiteBuilder (custom fields, custom records, custom forms), SuiteFlow (point-and-click workflows/approvals), Advanced PDF/HTML templates, saved searches, SuiteAnalytics | SuiteScript (JavaScript), SuiteCloud Development Framework (SDF), SuiteApps; SuiteAgents | Customisations sit on a metadata layer above the multi-tenant core; twice-yearly upgrades preserve customisations; sandbox release preview |
| **Odoo** | **Odoo Studio** (fields, views, reports, automated actions, approval rules, new models) — included in Custom plan | Python modules (Odoo framework), Odoo.sh | Odoo's upgrade service migrates standard data and Studio customisations; custom code must be ported per major version (main TCO pain point) |
| **SAP S/4HANA Cloud Public Edition** | Key-user extensibility: custom fields and logic, custom business objects, custom CDS views, forms, workflows (Fiori apps) | Developer extensibility with ABAP Cloud on released APIs; side-by-side on SAP BTP | **Clean core**: August 2025 guidance grades extensions **A** (released APIs) to **D** (modifications, not clean core); only released objects allowed in Public Edition ([SAP News Aug 2025](https://news.sap.com/2025/08/extend-sap-s4hana-cloud-right-way-clean-clear/); [ASUG](https://www.asug.com/insights/sap-updates-clean-core-guidance-to-help-customers-clarify-extensibility-criteria)) |
| **Acumatica** | Customisation projects via UI (fields, screens), Generic Inquiries, dashboards, workflow engine, business events, import/export scenarios | C#/.NET customisation projects | Packaged customisation projects validated on upgrade |
| **D365 SCM** | Personalisation, workspaces, workflow, configurable mobile app menus for warehouse, Power Platform | X++ extensions (no overlayering) | One Version continuous updates; extension model |
| **Epicor Kinetic** | Application Studio (layouts), BPMs (business process management rules, low-code), dashboards | Code BPMs, functions | Upgrade-aware BPM framework |
| **IFS Cloud** | Configurations (custom fields, pages, workflows, lobbies) | Tailoring via APIs | "Evergreen" releases (twice yearly), configuration layer preserved |

### 6.2 What customers configure without code (target catalogue for KASONGO)

| Configurable element | Tier | Notes |
|---|---|---|
| Custom fields on standard records (typed: text, number, money, date, choice, lookup, file), with validation and permissions | Core | Stored in typed extension columns/JSONB with schema registry; searchable; included in API and exports |
| Custom records/objects with relationships, list/detail pages | Advanced | E.g. "supplier certification", "inspection checklist" |
| Form/page layouts, field visibility and required-ness by role, status or entity | Core | |
| Saved views, filters, column sets, dashboards | Core | |
| Workflows and approvals (state machines with conditions, thresholds, parallel approvers, delegation, escalation, SLAs) | Core | Declarative; versioned; simulation mode |
| Business rules (validations, defaults, calculated fields) using a sandboxed expression language (no arbitrary code) | Core | E.g. "block shipment if lot expires within 30 days for customer group X" |
| Document layouts (POs, picking lists, delivery notes, invoices-of-goods, labels incl. GS1-128/SSCC, CoAs) with template editor | Core | Locale-aware; per legal entity/brand |
| Numbering series per entity/site/document type with gaps policy | Core | |
| Units of measure, conversions, packaging levels | Core | |
| Warehouse process configuration: receiving/putaway/picking strategies, removal strategies (FIFO/FEFO), mobile screen flows (scan steps), cycle-count policies | Core / Advanced | Like D365 mobile menu items, Odoo operation types, BC warehouse setup |
| Posting/account determination matrices | Core | Owned with MULLAH |
| Approval limits and segregation-of-duties rules | Core | |
| Notifications and webhooks (events → email/Teams/Slack/webhook) | Core | |
| Import templates and mappings (CSV/XLSX/EDI) | Core | |
| Reference data packs: tariffs, Intrastat thresholds, CBAM CN codes, DG classes, allergen lists, packaging categories — effective-dated, sourced, verified-on dates | Core | Mirrors Thapsus "rules as data" principle |
| Industry templates (distribution, light manufacturing, F&B) | Core | Speeds implementation (section 7.4) |

### 6.3 Upgrade-safety design for KASONGO

1. **No tenant code in the core.** All customisation is metadata (fields, rules, workflows, layouts) or out-of-process extensions calling published APIs/events (SAP "Level A" equivalent).
2. **Released-API contract:** only versioned `/v1` APIs and published event schemas are extension points; deprecations follow a documented window.
3. **Metadata is versioned and validated** against each release in CI; a customer "upgrade impact report" lists customisations touching changed objects (as SAP's clean-core checks and Acumatica's validation do).
4. **Expression language, not scripts**, for rules: sandboxed, deterministic, time-bounded, no network access; unit-testable in the UI.
5. **Sandbox tenants** in the same region with copy-down of configuration (not personal data by default) and release preview.
6. **Configuration as data in Postgres with RLS**, exportable/importable between tenants (template marketplace later).
7. **Per-tenant feature flags** to stage new behaviour.

---

## 7. Market and pricing

### 7.1 Published or reported price points

| Product | Model | Price (USD unless stated) | Source / status |
|---|---|---|---|
| Business Central Essentials / Premium / Team Members | Per user per month, annual | **$80 / $110 / $8**; from 1 Jan 2027 bundles with Microsoft 365 Copilot Business at $95 / $125 | [Microsoft BC pricing](https://www.microsoft.com/en-us/dynamics-365/products/business-central/pricing); [Partner Center Nov 2026](https://learn.microsoft.com/en-us/partner-center/announcements/2026-november) |
| Dynamics 365 Supply Chain Management | Per user per month | **$210** (min 20 seats); Premium **$300** (min 10); attach $30 | [Microsoft SCM pricing](https://www.microsoft.com/en-us/dynamics-365/products/supply-chain-management/pricing); [Licensing deck Mar 2026](https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/bade/documents/products-and-services/en-us/bizapps/Dynamics-365-Licensing-Deck-March-2026-PUB.pdf) |
| Odoo One App / Standard / Custom | Per user per month | Free (one app) / **$31.10** (list $38.90) / **$61.00** (list $76.20); light users $8.90; Studio, multi-company, API only in Custom | [Odoo pricing](https://www.odoo.com/pricing) (promotional first-year discount; monthly/annual labelling unclear on page) |
| Oracle NetSuite | Base licence (platform fee) + per user + modules; annual contracts | Not published; third-party estimates ~$999/month base and ~$99+/user/month; total first-year $100k–$500k mid-market | UNVERIFIED (NetSuite pricing page returned 403; [CostBench](https://costbench.com/compare/acumatica-vs-oracle-netsuite/), [ERP Research](https://erpresearch.com/compare/acumatica-vs-oracle-netsuite)) |
| Acumatica | Resource/transaction-based, by applications, **unlimited users** | Quote only; third-party total cost $75k–$350k | [Acumatica pricing](https://www.acumatica.com/pricing/); estimates UNVERIFIED |
| SAP S/4HANA Cloud Public; SAP B1; Epicor; Infor; Sage X3; IFS | Quote / partner pricing (FUE-based for SAP) | Not published | — |
| Katana | Free (≤30 SKUs, unlimited users) / Advantage (custom annual contract incl. implementation) | Advantage price not published; older plans ~$299/month reported | [Katana pricing](https://katanamrp.com/pricing/) |
| MRPeasy Starter / Professional / Enterprise / Unlimited | Per user per month (monthly billing; annual "1 month free") | **$49 / $69 / $99 / $149**; Unlimited 2-user minimum; from 11th user $79 per 10-user bundle | [MRPeasy pricing](https://www.mrpeasy.com/pricing/) |
| Cin7 Core Standard / Pro / Advanced; Omni | Plan per month with included users and order volumes | **$349** (5 users, 6k orders/yr) / **$599** (10 users, MRP) / **$1,199** (15 users, advanced WMS); Omni custom; B2B portal, POS, ForesightAI are add-ons | [Cin7 pricing](https://www.cin7.com/pricing/) |
| Unleashed Lite / Core / Pro | Plan per month + extra users | **$99 / $399 / $729** list (3/3/5 users; extra $69–$89 per user); onboarding $449 / $799 / $5,549 | [Unleashed pricing](https://www.unleashedsoftware.com/pricing) (90% promo on Core/Pro until 30 Nov 2026) |
| Fishbowl | Quote; implementation package mandatory | ~$349–$675/month reported | UNVERIFIED (aggregators) |

### 7.2 Packaging patterns observed

- **Per named user, tiered by edition** (BC Essentials/Premium; Odoo Standard/Custom; MRPeasy tiers): simple, predictable; editions gate manufacturing/service/Studio.
- **Base platform fee + users + modules** (NetSuite): high floor, revenue grows with modules.
- **Light/limited users** at low prices (BC Team Members $8, Odoo light users $8.90) for occasional approvers and shop-floor staff — important for warehouses and kiosks.
- **Unlimited users, pay for resources/applications** (Acumatica): attractive to companies with many occasional users (warehouse, shop floor).
- **Plan by order volume and integrations with bundled users** (Cin7, Unleashed): SMB-friendly.
- **Free tier with hard limits** (Katana ≤30 SKUs; Odoo one app).
- **Add-ons for AI forecasting, B2B portal, POS** (Cin7) and **Copilot bundles** (Microsoft, from 2027) — AI monetised as add-on or credits.

**Suggested for KASONGO (to validate):** per-full-user editions (Essentials: distribution; Manufacturing; Enterprise), free or very cheap "operational users" (scanner/kiosk/approver) to undercut per-seat rivals on warehouse headcount, a modest per-entity platform fee, AI as metered credits (off by default), and suite discounts when bought with MULLAH/BOSSMAN/HR. Prices belong in billing configuration, not code.

### 7.3 Implementation duration and cost

- **Panorama Consulting 2026 ERP Report** (released 4 Mar 2026): more than a quarter of organisations exceeded budgets, mainly from "additional technology needs" after late discovery of "fatal misfits" ([Panorama press release](https://www.panorama-consulting.com/panorama-consulting-group-releases-latest-study-of-erp-implementation-outcomes-across-the-globe/)). A secondary summary reports a **median timeline of about 9 months** and almost a quarter over schedule, from 170 organisations surveyed Jan 2025–Jan 2026 ([rework.com guide](https://resources.rework.com/guides/choosing-software/erp-implementation-guide)) — UNVERIFIED against the full report.
- **SMB tools:** self-serve to guided onboarding measured in weeks; Unleashed onboarding $449–$5,549; Katana Advantage bundles implementation in the annual contract; Odoo offers fixed "Success Packs" for companies under 50 staff (prices not on the pricing page).
- **Mid-market cloud (NetSuite, Acumatica, BC):** third-party estimates of implementation from roughly NZ$80k–300k (ANZ guide) and total first-year costs of $75k–$500k — UNVERIFIED (vendor-comparison sites).
- **Upper mid-market / enterprise (S/4HANA, SCM, IFS):** typically 9–18+ months with system integrators — general industry knowledge, not verified this session.

### 7.4 Why ERP implementations fail

- **Gartner:** "by 2027, more than 70% of recently implemented ERP initiatives will fail to fully meet their original business goals"; a Gartner director added about 25% fail catastrophically; root cause cited is technology-centric approaches that ignore stakeholder engagement ([Gartner insight page](https://www.gartner.com/en/information-technology/insights/what-it-leaders-must-do-to-avoid-disappointing-erp-initiatives); [The Register, Nov 2025](https://www.theregister.com/2025/11/13/erp_disaster_gartner/)). (Gartner page returned 403 to direct fetch; wording taken from search extracts.)
- **Panorama 2026:** "fatal misfits" found late → added technology, scope expansion, custom builds → overruns.
- **Recurring causes (synthesis):** weak executive sponsorship and change management; over-customisation (vs configuration); poor data migration and master-data quality; unclear process design / fit-gap done late; under-resourced internal team; unrealistic timelines; inadequate testing and training; integration complexity; partner capability gaps.
- **Product responses KASONGO can build in:** industry templates and guided setup; data-migration workbench (staging, validation, dry-run, reconciliation reports); fit-gap assessment tool against templates; configuration (not code) for variance; sandbox with release preview; in-app guidance and role-based training content; adoption analytics.

---

## 8. Recommended launch scope (for planning)

| Wave | Scope |
|---|---|
| **v1 (launch, distribution + light manufacturing, UK first)** | Item master (variants, UoM, GTIN, kits), multi-warehouse inventory with bins, lot/serial/expiry/FEFO, FIFO and average costing, landed cost (incl. tariff reference data), cycle counting, PWA scanning with GS1 parsing, receiving/putaway/pick/pack/ship (order and batch picking), requisitions/POs/approvals/blanket orders, three-way-match handoff, sales orders/ATP/backorders/drop ship/RMA, price lists and customer pricing, BOMs/routings/work orders/MRP/backflush/shop-floor kiosk (HR-integrated), basic inspections and recall trace, Shopify/WooCommerce/Amazon connectors, carrier aggregator, multi-entity and intercompany transfers, posting to MULLAH, BOSSMAN quote-to-cash APIs, packaging data for pEPR/PPT, Intrastat (NI + EU), no-code fields/rules/workflows/layouts |
| **v2 (+12 months)** | Standard costing with variances, wave/zone picking, supplier portal, scorecards, EDI (X12/EDIFACT via provider) and Peppol ordering/despatch, B2B portal, demand forecasting and safety-stock suggestions (optional AI), quality plans/NCR/CAPA/CoA, EAM (incl. care-home facilities), ECO/revisions, configurator, finite scheduling, CBAM/EUDR/FSMA 204 data packs, F&B recipes/allergens/yield, MCP server (draft-only writes) |
| **v3** | Catch weight, potency, field service, rental, cartonisation, DRP/S&OP, DPP data model, GxP pack (e-signatures, validation docs), predictive maintenance, rebates/chargebacks |

---

## Sources

**EU law and Commission**
- EUR-Lex, Regulation (EU) 2025/2083 (CBAM simplification): https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=OJ%3AL_202502083
- Commission, CBAM simplifications officially published (20 Oct 2025): https://taxation-customs.ec.europa.eu/news/officially-published-simplifications-carbon-border-adjustment-mechanism-cbam-2025-10-20_en
- Commission, CBAM definitive regime: https://taxation-customs.ec.europa.eu/carbon-border-adjustment-mechanism/cbam-definitive-regime_en
- Commission, CBAM entered into force 1 Jan 2026: https://taxation-customs.ec.europa.eu/news/cbam-successfully-entered-force-1-january-2026-2026-01-14_en
- European Parliament EPRS briefing on CBAM extension (Jul 2026): https://eprs.europarl.europa.eu/contents/publications/EPRS/2026/07/EPRS_BRI(2026)789314.html
- Commission, EUDR product scope and tools update (13 Jul 2026): https://environment.ec.europa.eu/news/commission-updates-product-scope-and-tools-support-eudr-2026-07-13_en
- Commission Access2Markets, EUDR delay and developments: https://trade.ec.europa.eu/access-to-markets/en/news/delay-until-december-2026-and-other-developments-implementation-eudr-regulation
- Northern Ireland Assembly annex on Regulation (EU) 2025/2650: https://www.niassembly.gov.uk/globalassets/committee-blocks/windsor-framework-democratic-scrutiny-committee/reg-eu-20252650/annex-f---2025-2650.pdf
- Council press release, battery due diligence stop-the-clock (18 Jul 2025): https://www.consilium.europa.eu/en/press/press-releases/2025/07/18/simplification-council-adopts-law-to-stop-the-clock-on-due-diligence-rules-for-batteries/
- Commission, ICS2 Release 3 complete: https://taxation-customs.ec.europa.eu/news/transition-ics2-release-3-complete-limited-temporary-derogations-some-member-states-2025-08-29_en
- Commission, €3 customs duty on low-value parcels: https://commission.europa.eu/news-and-media/news/ensuring-fairness-and-safety-eur3-customs-duty-low-value-parcels-2026-06-29_en
- Commission representation, customs reform agreement (26 Mar 2026): https://cyprus.representation.ec.europa.eu/news/commission-welcomes-historic-agreement-reform-eu-customs-union-2026-03-26_en
- Commission, PPWR implementing document C(2026) 3702: https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=PI_COM%3AC%282026%293702
- EP Legislative Observatory, Forced Labour Regulation: https://oeil.europarl.europa.eu/oeil/en/document-summary?id=1799238
- Destatis, Intrastat thresholds from Jan 2025: https://www.destatis.de/DE/Themen/Wirtschaft/Aussenhandel/anmeldeschwellen-2025.html
- Destatis press release (20 Aug 2026): https://www.destatis.de/DE/Presse/Pressemitteilungen/2026/08/PD26_297_51.html
- Finnish Customs, EU customs reform: https://tulli.fi/en/customs-reform

**UK government and legislation**
- GOV.UK Intrastat: https://www.gov.uk/intrastat
- HMRC Revenue and Customs Brief 47 (2014): https://www.gov.uk/government/publications/revenue-and-customs-brief-47-2014-changes-to-the-intrastat-arrival-threshold-from-1-january-2015/revenue-and-customs-brief-47-2014-changes-to-the-intrastat-arrival-threshold-from-1-january-2015
- HMRC, UK CBAM registration date: https://www.gov.uk/guidance/work-out-the-date-youll-need-to-register-for-carbon-border-adjustment-mechanism-cbam
- HMRC, UK CBAM policy summary: https://www.gov.uk/government/publications/carbon-border-adjustment-mechanism-cbam-policy-summary/carbon-border-adjustment-mechanism-cbam-policy-summary
- GOV.UK CBAM factsheet: https://www.gov.uk/government/publications/factsheet-carbon-border-adjustment-mechanism-cbam/factsheet-carbon-border-adjustment-mechanism
- SI 2026/809: https://www.legislation.gov.uk/uksi/2026/809/made
- SI 2026/830: https://www.legislation.gov.uk/uksi/2026/830/made
- pEPR who is affected: https://www.gov.uk/guidance/extended-producer-responsibility-for-packaging-who-is-affected-and-what-to-do
- pEPR reporting: https://www.gov.uk/guidance/check-if-you-need-to-report-packaging-data
- pEPR 2025 base fees: https://www.gov.uk/government/publications/extended-producer-responsibility-for-packaging-2025-base-fees/extended-producer-responsibility-for-packaging-2025-base-fees
- pEPR illustrative fees 2026: https://www.gov.uk/government/publications/illustrative-waste-disposal-fees-2026-extended-producer-responsibility-for-packaging/year-2-illustrative-waste-disposal-fees-extended-producer-responsibility-for-packaging
- PackUK modulation statement: https://www.gov.uk/government/publications/extended-producer-responsibility-for-packaging-modulated-disposal-fees/packuk-extended-producer-responsibility-epr-for-packaging-producer-disposal-fees-modulation-statement
- Plastic Packaging Tax: https://www.gov.uk/guidance/check-if-you-need-to-register-for-plastic-packaging-tax
- Finance Act 2021 Part 2: https://www.legislation.gov.uk/ukpga/2021/26/part/2
- S&S GB declarations for EU imports: https://www.gov.uk/government/publications/preparing-for-the-new-safety-and-security-declaration-requirements/get-ready-for-safety-and-security-declaration-requirements-for-importing-goods-from-the-eu
- CDS migration news: https://www.gov.uk/government/news/one-month-left-for-importers-to-move-to-single-customs-platform
- HMRC research on STW pause: https://www.gov.uk/government/publications/exploring-changes-to-safety-and-security-declaration-requirements/research-exploring-changes-to-safety-and-security-declaration-requirements
- E-invoicing roadmap: https://www.gov.uk/government/publications/e-invoicing-implementation-roadmap/roadmap-for-e-invoicing-implementation
- Welsh Government statement on REACH (Amendment) (No 2) Regulations 2026: https://www.gov.wales/written-statement-reach-amendment-no-2-regulations-2026
- Hansard, Draft REACH (Amendment) (No 2) Regulations 2026: https://hansard.parliament.uk/commons/2026-06-08/debates/d223fa39-c061-4f29-9d90-9cc3cd841457/DraftREACH(Amendment)(No2)Regulations2026
- House of Commons Library, packaging EPR: https://commonslibrary.parliament.uk/research-briefings/cbp-10352/
- HSE, thorough examinations of lifting equipment: https://www.hse.gov.uk/work-equipment-machinery/thorough-examinations-lifting-equipment.htm
- HSE HSG220 Health and safety in care homes: https://books.hse.gov.uk/gempdf/hsg220.pdf
- business.gov.uk, EU PPWR: https://www.business.gov.uk/campaign/europe/european-union-eu-regulations/eu-packaging-and-packaging-waste-regulation-eu-ppwr/

**US government**
- FDA FSMA 204 rule page: https://www.fda.gov/food/food-safety-modernization-act-fsma/fsma-final-rule-requirements-additional-traceability-records-certain-foods
- Federal Register, FSMA 204 compliance date extension (proposed): https://www.federalregister.gov/documents/2025/08/07/2025-14967/requirements-for-additional-traceability-records-for-certain-foods-compliance-date-extension
- FDA public meeting on lot-level traceability: https://www.fda.gov/food/workshops-meetings-webinars-food-and-dietary-supplements/fda-public-meeting-challenges-and-solutions-lot-level-food-traceability-06152026
- FDA QMSR: https://www.fda.gov/medical-devices/postmarket-requirements-devices/quality-management-system-regulation-qmsr
- FDA QMSR FAQ: https://www.fda.gov/medical-devices/quality-management-system-regulation-qmsr/quality-management-system-regulation-frequently-asked-questions
- Supreme Court, Learning Resources v. Trump (Justia): https://supreme.justia.com/cases/federal/us/607/24-1287/
- CBP IEEPA FAQ: https://www.cbp.gov/trade/programs-administration/trade-remedies/IEEPA-FAQ
- CBP trade remedies: https://www.cbp.gov/trade/programs-administration/trade-remedies
- CBP US tariff overview (Feb 2026): https://www.cbp.gov/sites/default/files/2026-02/U.S.%20Tariff%20Overview%20February%202026_0.pdf
- Federal Register, Section 232 metals restructuring (Apr 2026): https://www.federalregister.gov/documents/2026/04/09/2026-06960/strengthening-actions-taken-to-adjust-imports-of-aluminum-steel-and-copper-into-the-united-states
- White House annexes (Apr 2026): https://www.whitehouse.gov/wp-content/uploads/2026/04/ANNEXES-I-A-I-B-II-III-IV.pdf
- Federal Register, de minimis indefinite suspension IFR (24 Jun 2026): https://www.federalregister.gov/documents/2026/06/24/2026-12670/indefinite-suspension-of-the-de-minimis-exemption-for-merchandise-arriving-through-all-modes-other

**Standards bodies and industry**
- GS1 US Sunrise 2027: https://www.gs1us.org/industries-and-insights/by-topic/sunrise-2027
- GS1 2D in retail guideline: https://ref.gs1.org/guidelines/2d-in-retail/
- Peppol BIS 3: https://docs.peppol.eu/poacc/upgrade-3/
- OpenPeppol post-award documentation: https://peppol.org/documentation/technical-documentation/post-award-documentation/
- IMO IMDG Code amendment cycle: https://wwwcdn.imo.org/localresources/en/publications/Documents/IMDG%20Code/IMDG%20Code%20Amendment%20Cycle%20-%202025-2034.pdf
- HPRA, EUDAMED mandatory use: https://www.hpra.ie/news-events/news/article/mandatory-use-of-eudamed-modules-for-medical-devices
- DNV, EUDAMED: https://www.dnv.com/article/eudamed-mandatory-use-what-manufacturers-need-to-know/
- NSF, ISO 9001:2026 published: https://www.nsf.org/in/en/knowledge-library/iso-90012026-published-on-september-16-2026-what-quality-leaders-need-to-know
- TÜV SÜD, ISO 9001:2026: https://www.tuvsud.com/en/knowledge-hub/articles/iso-9001-2026-everything-you-need-to-know-about-the-new-revision
- LRQA, ISO 9001 publication date: https://www.lrqa.com/en/latest-news/iso-9001-publication-date-confirmed/

**Law-firm and secondary analysis (used where primary text not reached)**
- Latham & Watkins, Omnibus I published: https://www.lw.com/en/insights/eu-sustainability-omnibus-published-in-the-official-journal
- Linklaters, Omnibus I: https://sustainablefutures.linklaters.com/post/102mkjf/eu-omnibus-i-directive-published-in-the-official-journal-of-the-eu
- Arthur Cox, Omnibus I: https://www.arthurcox.com/insights/omnibus-i-directive-published-revised-scope-and-reduced-obligations-under-csrd-and-csddd/
- Global Policy Watch (Covington), Omnibus I: https://www.globalpolicywatch.com/2026/02/eu-csddd-csrd-omnibus-published-in-official-journal-transposition-delegated-acts-and-guidelines-are-next/
- Mayer Brown, revised ESRS adopted: https://www.mayerbrown.com/en/insights/publications/2026/07/european-commission-adopts-revised-european-sustainability-reporting-standards
- Debevoise, revised ESRS and voluntary standard: https://www.debevoise.com/insights/publications/2026/10/european-commission-adopts-revised-esrs-and-volunt
- Gleiss Lutz, CBAM simplification: https://www.gleisslutz.com/en/know-how/eu-simplifies-cbam-regulation-omnibus-simplification-initiative
- Reed Smith, CBAM simplification: https://www.reedsmith.com/our-insights/blogs/viewpoints/102lr9t/what-you-need-to-know-as-cbam-simplification-comes-into-effect/
- PwC NL, CBAM downstream extension: https://www.pwc.nl/en/insights-and-publications/tax-news/other/ec-proposes-cbam-expansion-to-180-downstream-products.html
- Stibbe, amended EUDR: https://www.stibbe.com/publications-and-insights/the-amended-eudr-what-has-changed-and-what-has-remained
- Hogan Lovells, EUDR simplification package: https://www.hlc.com/en/publications/eu-deforestation-regulation-commission-publishes-simplification-package-ahead-of-december-2026
- Arendt, EUDR review: https://www.arendt.com/news-insights/news/eudr-simplification-review-published-what-the-2026-package-means-for-in-scope-companies/
- EY Global Tax News, EUDR: https://globaltaxnews.ey.com/news/2026-0237
- Sedex, Forced Labour Regulation guidelines: https://www.sedex.com/blog/eu-forced-labour-regulation-guidelines-and-supply-chain-implications/
- Hogan Lovells, FLR guidelines: https://hlc.com/en/publications/eu-forced-labour-regulation-key-takeaways-from-the-european-commissions-june-2026-guidelines
- Osborne Clarke, regulatory outlook Sept 2026: https://www.osborneclarke.com/insights/regulatory-outlook-september-2026-modern-slavery
- Covington, UFLPA entity list expansion: https://www.cov.com/en/news-and-insights/insights/2026/08/dhs-expands-uflpa-entity-list-amid-intensifying-enforcement-landscape
- Kelley Drye, UFLPA: https://www.kelleydrye.com/viewpoints/blogs/trade-and-manufacturing-monitor/u-s-government-announces-largest-expansion-of-the-uflpa-entity-list-in-history-continues-focus-on-forced-labor-trade-enforcement
- Thompson Hine, UFLPA: https://www.thompsonhinesmartrade.com/2026/07/dhs-updates-uflpa-entity-list-with-43-additional-chinese-companies/
- A&O Shearman, IEEPA ruling: https://www.aoshearman.com/en/insights/scotus-rejects-ieepa-tariffs-refund-opportunities-and-uncertainty-emerge
- Troutman, duty recovery: https://www.troutman.com/insights/getting-duties-back-where-recovery-stands-under-ieepa-section-122-and-section-301-forced-labor-tariffs/
- Z2Data, Section 122 termination: https://www.z2data.com/insights/how-the-termination-of-section-122-tariffs-impacts-your-supply-chain/
- Kroll, tariff substitution: https://www.kroll.com/en/publications/a-tale-of-tariff-substitution
- Wiley tariff tracker: https://www.wiley.law/trump-administration-tariff-tracker
- Wipfli tariff update: https://www.wipfli.com/insights/articles/tariff-update-new-section-301-tariffs-section-232-and-more
- KPMG, de minimis: https://kpmg.com/us/en/taxnewsflash/news/2026/06/cbp-suspends-de-minimis-exemption.html
- Intertek, PPWR August 2026: https://www.intertek.com/products-retail/insight-bulletins/2026/1536-eu-ppwr-requirements-effective-from-august/
- Brodies, UK DRS: https://brodies.com/insights/environmental-social-and-governance/towards-a-uk-deposit-return-scheme-uk-government-reaffirms-its-commitment-to-an-october-2027-launch/
- ERP UK, DRS readiness: https://erp-recycling.org/uk/news-and-events/2026/08/uk-deposit-return-scheme-are-you-ready-for-2027/
- Epista, EU GMP 2026 revisions: https://www.epista.com/knowledge/preparing-for-emas-2026-good-manufacturing-practice-gmp-revisions-chapter-4-annex-11-annex-22
- IntuitionLabs, Annex 22: https://intuitionlabs.ai/articles/eu-gmp-annex-22-ai-compliance-pharma-2
- Orrick, AI Act Digital Omnibus: https://www.orrick.com/en/Insights/2026/07/EU-AI-Act-Update-Digital-Omnibus-Finalizes-8-Compliance-Changes
- Cooley, Digital AI Omnibus: https://cdp.cooley.com/digital-ai-omnibus-delays-key-deadlines-introduces-new-rules/
- Sustainability in Business, REACH revision set aside: https://www.sustainabilityinbusiness.blog/2026/04/commission-officially-sets-aside-plans-for-a-full-revision-of-reach/
- Mondaq, WEEE reform: https://www.mondaq.com/eu-weee-directive-reform-tighter-rules-rising-costs/1846942
- CECE, battery due diligence changes: https://www.cece.eu/news/eu-batteries-regulation-the-commission-key-changes-to-due-diligence-policy
- technology.org, EU battery rules Feb 2027: https://www.technology.org/2026/10/19/eu-battery-rules-february-2027-removable-batteries-passport/
- Renoon, DPP delegated acts: https://www.renoon.com/blog/delegated-acts-for-digital-product-passport-explainer-and-current-status
- KPMG Belgium, ViDA: https://kpmg.com/be/en/insights/my-tax-compass/indirect-tax-insights/political-agreement-reached-on-the-eu-vat-in-the-digital-age-proposal.html
- Eurofiscalis, EU Intrastat thresholds: https://www.eurofiscalis.com/en/eu-intrastat-thresholds/

**Vendors (AI, product, pricing)**
- SAP News, Joule agents (Oct 2025): https://news.sap.com/2025/10/sap-connect-business-ai-new-joule-agents-embedded-intelligence/
- SAPinsider, SAP Connect 2026 agents: https://sapinsider.org/blogs/sap-connect-2026-how-new-agents-will-detect-and-respond-to-supply-disruptions
- SAP News, clean core (Aug 2025): https://news.sap.com/2025/08/extend-sap-s4hana-cloud-right-way-clean-clear/
- ASUG, clean core guidance: https://www.asug.com/insights/sap-updates-clean-core-guidance-to-help-customers-clarify-extensibility-criteria
- Computer Weekly, SuiteWorld 2025: https://www.computerweekly.com/news/366632408/SuiteWorld-2025-NetSuite-unveils-AI-innovations-for-future-business
- KORE1, NetSuite MCP connector: https://www.kore1.com/netsuite-mcp-connector/
- Rand Group, NetSuite 2026.1: https://www.randgroup.com/insights/oracle-netsuite/netsuite-2026-1-release-ai-driven-finance-operations-and-automation-enhancements/
- Microsoft Learn, BC 2026 wave 1 planned features: https://learn.microsoft.com/en-us/dynamics365/release-plan/2026wave1/smb/dynamics365-business-central/planned-features
- Microsoft Learn, BC inventory posting: https://learn.microsoft.com/en-us/dynamics365/business-central/design-details-inventory-posting
- Microsoft Learn, SCM Procurement Agent: https://learn.microsoft.com/en-us/dynamics365/supply-chain/procurement/procurement-agent-overview
- Microsoft Learn, PO follow-up with Procurement Agent: https://learn.microsoft.com/en-us/dynamics365/supply-chain/procurement/procurement-agent-supplier-com-follow-up
- Microsoft blog, Supplier Engagement (Aug 2026): https://www.microsoft.com/en-us/dynamics-365/blog/it-professional/2026/08/06/supplier-engagement-supply-chain-management/
- Microsoft BC pricing: https://www.microsoft.com/en-us/dynamics-365/products/business-central/pricing
- Microsoft SCM pricing: https://www.microsoft.com/en-us/dynamics-365/products/supply-chain-management/pricing
- Microsoft licensing deck (Mar 2026): https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/bade/documents/products-and-services/en-us/bizapps/Dynamics-365-Licensing-Deck-March-2026-PUB.pdf
- Microsoft Partner Center announcements (Nov 2026): https://learn.microsoft.com/en-us/partner-center/announcements/2026-november
- Odoo 19 release notes: https://www.odoo.com/odoo-19-release-notes
- Odoo 19.4 release notes: https://www.odoo.com/odoo-19-4-release-notes
- Odoo pricing: https://www.odoo.com/pricing
- Acumatica 2026 R1: https://www.acumatica.com/blog/acumatica-2026-r1-acumatica-ai-enabled-product-release-delivers-intelligence/
- MYOB Acumatica release note, anomaly detection: https://help.myob.com.au/advanced/Docs/Published/ReleaseNotes/RN_2026_R1_Finance_AnomalyDetection_GI.html
- Acumatica pricing: https://www.acumatica.com/pricing/
- BusinessWire, Epicor agentic AI stack (May 2026): https://www.businesswire.com/news/home/20260519098303/en/Epicor-Introduces-Agentic-AI-Stack-to-Power-Action-Across-ERP-Workflows
- PortalERP, Epicor Prism in Europe: https://portalerp.com/article/epicor-expands-embedded-ai-platform-to-europe
- IFS Loops: https://www.ifs.com/news/product/ifs-loops
- IFS Loops Agent Studio: https://www.ifs.com/en/insights/news/ifs-loops-launches-agent-studio
- ERP Today, IFS H1 2026: https://erp.today/ifs-h1-2026-results-industrial-ai-growth/
- MRPeasy pricing: https://www.mrpeasy.com/pricing/
- Katana pricing: https://katanamrp.com/pricing/
- Cin7 pricing: https://www.cin7.com/pricing/
- Unleashed pricing: https://www.unleashedsoftware.com/pricing
- Panorama Consulting 2026 ERP Report release: https://www.panorama-consulting.com/panorama-consulting-group-releases-latest-study-of-erp-implementation-outcomes-across-the-globe/
- Gartner, avoid disappointing ERP initiatives: https://www.gartner.com/en/information-technology/insights/what-it-leaders-must-do-to-avoid-disappointing-erp-initiatives
- The Register on Gartner ERP (Nov 2025): https://www.theregister.com/2025/11/13/erp_disaster_gartner/
- rework.com ERP implementation guide (secondary summary of Panorama 2026): https://resources.rework.com/guides/choosing-software/erp-implementation-guide

---

## Things I could not verify

1. **FSMA 204 final rule:** no final rule codifying 20 Jul 2028 found; FDA's own page (4 Nov 2026) still calls the extension proposed. Enforcement deferral rests on the Continuing Appropriations Act 2026 directive.
2. **UK CBAM first return/payment date** (31 May 2028) and quarterly cadence after 2027 — single secondary source.
3. **EU CBAM downstream extension** final product list and anti-circumvention text — trilogue ongoing as of October 2026.
4. **EUDR delegated act of 13 Jul 2026** — whether scrutiny ended without objection and it has entered into force.
5. **ESPR:** whether any product-group delegated act (iron and steel) has been adopted by November 2026; whether the DPP registry went live by 19 Jul 2026; the medium-enterprise date for the unsold-goods ban.
6. **Battery due-diligence threshold change** (€40m → €150m) — proposal status.
7. **CSRD first application year** under Omnibus I (FY2027 claim from one source); OJ publication of the revised ESRS and voluntary standard delegated acts.
8. **US Section 301 "forced labour" tariffs** — exact rates and country list (secondary sources only); pharmaceutical Section 232 rates; timber/furniture rate conflict (25% vs 15%).
9. **IEEPA refund mechanics** (CBP portal/process) — not confirmed against CBP primary guidance.
10. **UK pEPR 2026/27 confirmed fees and invoice timing**; UK DRS position in Wales and which body runs producer registration.
11. **UK REACH (Amendment) (No 2) Regulations 2026** — whether made and in force; primary source for the EU REACH revision being dropped; RoHS recast; UK WEEE reforms (not researched).
12. **France and Netherlands Intrastat** rules — only secondary sources.
13. **EU customs reform** formal adoption; €3 duty basis (per item vs per consignment); UK Single Trade Window current status.
14. **EU GMP Annex 11/22 final texts** — none found up to late September 2026; EudraLex not re-read.
15. **EUDAMED legacy registration deadline** (27 vs 28 Nov 2026); FDA UDI details (from prior knowledge).
16. **BRCGS Issue 10 timing** and the four-hour traceability test (prior knowledge); IAF transition rules for ISO 9001:2026; ADR 2025 transitional date.
17. **EU AI Act Digital Omnibus** regulation number/date (secondary sources disagree slightly on dates).
18. **Vendor AI status:** SAP agents' GA dates and MCP/A2A for S/4HANA Public Edition; "NetSuite Next" availability; D365 SCM Supplier Communications Agent GA (still preview in docs); Acumatica AI Assistant GA; Epicor agent availability details.
19. **Vendor pricing:** NetSuite, Acumatica, Fishbowl, SAP, Epicor, Infor, Sage X3 and IFS prices are not published; third-party estimates only. Katana older plan prices. Odoo monthly vs annual labelling.
20. **Implementation statistics:** Panorama 2026 median 9-month timeline (secondary summary); exact Gartner wording (page blocked; taken from search extracts).
21. **Market share by vertical/region** — no credible public data found; vertical dominance in section 2 is qualitative.
22. **Competitor feature attributions** in section 1 are from vendor documentation and product knowledge, spot-checked rather than exhaustively verified; marketplace add-ons often fill gaps.
23. **Google Cloud regional availability of AI models** in europe-west2, europe-west3 and us-east5 — not researched; must be confirmed before committing to region-pinned AI.
24. **Peppol pre-award (eTendering)** specifications and Peppol use by UK private care providers — not researched.
25. **Search budget:** the session's web-search limit was reached near the end, so a few planned checks (Birmingham City Council Oracle overrun as a UK failure case, official Cin7/Unleashed verification beyond pricing pages, NetSuite official pricing) could not be run; a follow-up session can complete them.
