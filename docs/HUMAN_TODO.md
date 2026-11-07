# Steps only a person can take — Thapsus ERP

Suite-wide steps (repository, Google Cloud, domains, legal, certification, design partners) are in
`suite/HUMAN_TODO_SUITE.md`. These are ERP's own. Status on 2026-11-07: none done. Build against mocks and sandboxes
until each is done.

## K-1 Approve the build brief

1. Read `docs/BUILD_BRIEF.md`, `docs/PLAN.md` and `docs/FEATURES.md`.
2. Approve, or note changes, in the lead session. The build starts only after approval.

## K-2 Design partners for each industry pack (needed by Phase 6, 8, 9 and 12)

1. Find at least one UK pilot customer per pack: a wholesaler or multichannel brand (W1), a small discrete
   manufacturer (M1), a food or drink producer (P1), and a services or construction firm (S1).
2. Sign a pilot agreement and a data processing agreement before any of their real data is loaded; until then
   pilots use fictional data only.

## K-3 Carrier aggregator (Phase 4)

1. Choose a parcel-carrier aggregator that serves the UK first, then the EU and US, and can process data in the
   customer's region or under a lawful transfer (addresses of sole traders and consumers are personal data).
2. Open a developer and production account; put the API key in Secret Manager (the lead session gives the secret
   name); record it in `docs/SUBPROCESSORS.md` with purpose and location before the integration is built.

## K-4 GS1 membership (Phase 4)

1. Join GS1 UK to get a company prefix for Thapsus's own test labels and demo data, so generated GTINs and SSCCs are
   valid. Customers use their own prefixes.

## K-5 Marketplace and shop developer accounts (Phase 6)

1. Shopify Partner account; create the app listing and pass Shopify's app review (protected customer data
   requirements).
2. Amazon Selling Partner API developer registration (data protection policy questionnaire).
3. WooCommerce needs no registration (per-store keys).

## K-6 EDI network partner (Phase 6)

1. Choose an EDI network provider for X12 and EDIFACT (AS2, VAN, SFTP) with UK and US coverage; sign the reseller or
   platform agreement and DPA; record it in SUBPROCESSORS.

## K-7 EU and US compliance systems (Phases 13 and 14)

1. EUDR: register a test operator account for the EU information system (TRACES) and request API access, so the
   integration can be tested.
2. Agree with a customs broker or customs software partner the hand-off file formats for UK CDS and EU declarations
   (Thapsus does not file declarations).
3. US: confirm the source and licence of tariff reference data (HTS and Chapter 99 measures) used in landed cost.

## K-8 Pricing

1. Approve the ERP price configuration (full users by edition, light users, per-entity fee, industry packs, AI
   credits). Prices are configuration in the suite back office, never code (`suite/PLATFORM.md` §8).
