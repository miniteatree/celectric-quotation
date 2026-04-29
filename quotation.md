# Celectric Website Redesign Quotation

## Purpose
Client-facing quotation for Celectric website redesign and digital platform upgrade.

This quotation prices **Phase 1 only** as the MVP launch scope. Later phases are included as reference only so the client understands the future roadmap, but they are **not included in the quoted price**.

## Project Direction
Celectric website should be built as an **industrial catalog + enquiry platform**, not only a static company profile website.

The platform should support:
- searchable product catalog
- brand and category browsing
- quotation / enquiry flow
- product specification documents
- scalable product growth around **3,000+ products**
- future client portal and order document access

## Recommended Architecture
Use a **manual batch static publish architecture** for Phase 1.

Recommended setup:
- Laravel remains the source of truth for admin dashboard, product data, categories, brands, documents, RFQ, and publish control
- public website pages are generated as static HTML/JSON files during a controlled publish step
- admins can update products, categories, brands, blog posts, and documents as draft/pending changes without immediately affecting the live public site
- every 2-3 days, or whenever Celectric is ready, an admin can run a manual **Publish Static Site** action
- the publish job generates the public pages/data, deploys them to static hosting/CDN, and refreshes affected cache
- Cloudflare R2 stores product images, product specification PDFs, and future private client/order documents

Why this is recommended for Phase 1:
- the public website is fast, stable, and CDN-friendly
- product/admin work can be batched and checked before going live
- Celectric avoids the complexity of real-time incremental publishing while still getting a static public website
- Laravel still handles dynamic backend functions such as RFQ submission, configurator validation, admin management, and future integrations
- urgent updates can still be published manually whenever needed

In simple terms, Celectric staff can update many products over a few days, review them, then publish the updated static website in one controlled batch.

---

## Quoted Scope — Phase 1 Only

# Phase 1 — Core Website + Lightweight Admin Dashboard

## Phase 1 Total Price

**RM 54,000**

This price covers the core MVP website, catalog structure, enquiry flow, lightweight admin dashboard, upload/storage setup, basic launch search/filter behaviour, SEO foundation, deployment documentation, admin handover, and launch support.

---

## Phase 1 Milestone Breakdown

The project can be billed progressively after each completed milestone.

| Milestone | Scope | Billing Amount |
|---|---|---:|
| Phase 1A | Discovery, sitemap, technical planning, content/data structure confirmation | **RM 5,000** |
| Phase 1B | UI direction, agreed page templates, responsive frontend foundation, and included revision rounds | **RM 9,000** |
| Phase 1C | Product catalog structure: listing, detail, brand, category, model/configuration URL planning | **RM 10,000** |
| Phase 1D | Lightweight admin dashboard: product/category/brand CRUD, publish controls, sorting, SEO fields | **RM 12,000** |
| Phase 1E | RFQ/enquiry flow, product document upload, Cloudflare R2 storage setup, datasheet/download section | **RM 8,000** |
| Phase 1F | Manual batch static publish setup, static deployment, testing, deployment documentation, admin handover, launch support | **RM 10,000** |
|  | **Phase 1 Total** | **RM 54,000** |

---

## Phase 1 Detailed Scope

### Public Website
- website redesign
- homepage
- product listing pages
- product detail pages
- brand pages
- category pages
- enquiry / RFQ page
- blog / insights listing and article page
- resource / datasheet download sections where applicable
- multi-category product organisation where relevant
- basic launch product search and filtering, limited to keyword search, brand/category filter, and simple sorting
- selected approved model-number / configuration landing pages for Google Search
- shareable configurator URL support such as `/products/{product-slug}/configure?...`
- clean SEO URLs for approved configured model numbers such as `/configuration/{configured-part-number}`
- SEO-friendly canonical pages for selected important individual model numbers
- mobile responsive cleanup
- basic SEO fields and metadata structure

### Phase 1 Search / Filter Scope
Phase 1 includes **basic launch catalog discovery**, not a full advanced search system.

Included in Phase 1:
- product keyword search by product name, model number / part number, brand name, and category name
- basic brand and category filtering on product listing pages
- simple sorting, for example default order, A-Z, or newest if data supports it
- search/filter behavior handled as static listing/query pages where practical, with Laravel API support if a dynamic query is needed

Not included in Phase 1:
- autocomplete dropdown suggestions
- advanced faceted filtering by many technical specifications
- complex comparison tools
- typo-tolerant / fuzzy search engine setup
- analytics-driven suggested products
- AI search or semantic search

These advanced search/discovery items belong in Phase 2 after the product data structure and launch catalog are stable.

### UI / Design Scope for Phase 1B
Phase 1B includes UI direction and responsive page templates for the following agreed screens:
- homepage
- product listing page
- product detail page
- brand listing / brand detail pattern
- category listing / category detail pattern
- enquiry / RFQ page
- blog / insights listing and article pattern
- basic admin layout direction for dashboard/forms

Included revision allowance:
- 1 initial UI direction round
- up to 2 revision rounds on the agreed page templates
- responsive adjustment for desktop, tablet, and mobile layouts

Additional redesign directions, new page types, or repeated revisions after approval are treated as change requests.

### Product Catalog Foundation
- product data import preparation and import-ready field structure
- product data entry structure for catalog fields
- product category assignment
- product brand assignment
- product specification / attribute fields where needed
- product datasheet / document mapping for imported products
- related products data structure and admin linking fields for Phase 1 data/admin readiness
- model number / configuration field mapping for imported products
- canonical URL handling for individual model-number pages

### Option Architecture — Function of Each Table

The option architecture allows Celectric to manage configurable industrial products where a base product can generate multiple model numbers or part numbers based on selected options.

Recommended table functions:

| Table | Function |
|---|---|
| `products` | Stores the main/base product, such as EE650 Air Velocity Transmitter. This is the parent product page used for description, brand, category, datasheets, and general SEO. |
| `product_option_groups` | Stores option groups for one product, such as Model, Output, Probe Length, Cable Length, Protocol, and Baud Rate. Controls option order and whether a selection is required. |
| `product_option_values` | Stores selectable values inside each option group, such as T2 = Duct mount, J3 = RS485, L100 = 100mm. Each value can have a code, label, description, and optional price adjustment. |
| `product_option_rules` | Stores dependency logic between options, such as hide, allow, require, or incompatible rules. Example: cable length is not available when duct mount is selected. |
| `product_configurations` | Stores important/generated final configurations such as EE650-T2J3L100P1BD5, including selected options, SEO title, SEO description, canonical URL, and index status. |

This structure supports:
- option-based model number generation
- configurable product enquiry flow
- validation of incompatible option combinations
- SEO pages for selected important final model numbers
- future price add-on logic if Celectric wants to show pricing or internal costing later

Phase 1 covers a **configurable product foundation plus RFQ-ready configurator for the approved launch dataset only**. It is not positioned as a complete CPQ system.

Included in Phase 1:
- database structure for option groups, option values, option rules, and approved configurations
- product-page option selection UI for approved configurable products
- live model/part-number display for selected options
- shareable configuration URL restore behavior
- backend validation before RFQ acceptance
- RFQ capture of selected configuration details

Not included in Phase 1:
- full CPQ pricing engine
- automated quotation calculation
- complex engineering rule engine across the entire catalog
- inventory/stock validation
- ERP/Odoo-driven configuration sync
- public checkout or payment
- full validation of every future product combination not supplied in the launch dataset

If Celectric later wants a full CPQ system, that should be scoped as a separate Phase 2/3 module after the launch configurator data is proven.

### Manual Batch Static Publish Compatibility

This configuration architecture is compatible with manual batch static publishing:

- Laravel stores and manages products, categories, brands, option groups, option values, rules, RFQ records, and documents
- public pages are generated from Laravel/database data only when Celectric runs a controlled publish
- admins may save multiple product updates as draft or pending changes before publishing
- the static publish job can generate homepage, product pages, category pages, brand pages, blog pages, selected model-number SEO pages, JSON data files, sitemap, and robots file
- product images and PDFs remain in Cloudflare R2 and are referenced by the generated static pages
- the configurator can run interactively in the browser, while Laravel remains authoritative for RFQ validation

The configure page can be static as a page shell, while the part number changes dynamically in the browser as the user selects options.

Example:

```text
EE650 + T2 + J3 + L100 + P1 + BD5
= EE650-T2J3L100P1BD5
```

Important condition:
- customers can see the part number update immediately while selecting options
- the displayed part number is for convenience only; the backend still checks whether the selected combination is valid before accepting the enquiry
- this reduces wrong enquiries caused by invalid model combinations
- when admins update products or options, the website data should refresh automatically where needed

### Configurator vs Autocomplete / Filter

Product configuration is not the same as autocomplete or catalog filtering. This distinction is important so Phase 1 remains focused and does not become a full advanced-search project.

| Feature | Purpose | Scope Position |
|---|---|---|
| Basic product search/filter | Used on product listing pages for keyword search, brand/category filtering, and simple sorting. | Phase 1 launch scope |
| Product configurator | Used inside one approved configurable product to select options, validate compatibility, generate/display final part number, and submit RFQ. | Phase 1 approved-dataset scope |
| Autocomplete search | Used across many products to show live dropdown suggestions while typing product names, brands, categories, or model numbers. | Phase 2 enhancement |
| Advanced filtering | Used across product listing pages to narrow many products by many specs, attributes, application, performance values, or technical ranges. | Phase 2 enhancement |

Recommended interpretation:
- Phase 1 basic search/filter helps the customer find a product at launch
- Phase 2 autocomplete and advanced filtering improve discovery after launch
- configurator helps the customer choose the exact model/part number after entering one approved configurable product

### Three-Layer Product URL Architecture

Celectric should use a three-layer product URL structure:

| Layer | URL Example | Purpose |
|---|---|---|
| Main product page | `/products/ee650-air-velocity-transmitter` | Main product detail page for product description, brand/category browsing, datasheets, and general SEO. |
| Configurator page | `/products/ee650-air-velocity-transmitter/configure?45793=241952&45794=297497` | Shareable configuration page that restores selected option group/value IDs and lets the customer submit enquiry/RFQ based on a chosen configuration. |
| SEO configuration page | `/configuration/ee650-t2j3l100p1bd5` | Google-indexable final model-number page for users searching exact part numbers such as EE650-T2J3L100P1BD5. |

Recommended URL rule:
- use stable numeric option group/value IDs in query parameters for restore behavior
- display readable option codes and generated part numbers in the UI, email/RFQ, and approved SEO pages
- keep tracking parameters such as `srsltid` out of canonical URLs
- each important configured model number should have a clean canonical SEO URL
- lesser/unimportant combinations can remain shareable but noindex if needed

### Test Conditions Before Open Use

Before opening the configuration feature for public use, the following checks should pass.

Open-use validation applies to the Phase 1 launch dataset and approved configurable product set. Full validation across all future product combinations depends on final supplied data and may require separate scope.

1. Main product URL test
   - `/products/{product-slug}` loads correctly
   - product title, brand, category, datasheet, and enquiry button display correctly
   - canonical URL points to the main product page

2. Configurator URL test
   - `/products/{product-slug}/configure?...` restores selected options from URL parameters
   - invalid option combinations are blocked or clearly corrected
   - dependency rules hide or disable unavailable choices correctly
   - final generated model number matches selected option codes
   - enquiry/RFQ submission includes the selected configuration

3. SEO configuration URL test
   - `/configuration/{configured-part-number}` loads the correct product and selected options
   - page title includes the full configured model number
   - SEO description includes product name, brand, and key selected options
   - canonical URL is clean and does not include tracking parameters
   - important model-number pages are indexable
   - duplicate or low-value combinations can be marked noindex

4. Data consistency test
   - every option value belongs to the correct option group
   - every option group belongs to the correct product
   - required option groups cannot be empty
   - inactive option values cannot generate public configuration pages
   - generated part number is unique where uniqueness is required

5. RFQ/enquiry test
   - enquiry form captures product ID, configured part number, selected option labels, and selected option codes
   - admin can view the submitted configuration clearly
   - email/notification content does not lose selected option details

### Enquiry / RFQ Flow
- contact / enquiry flow
- RFQ / quotation submit flow
- enquiry form routing structure
- product-related enquiry support where applicable

### Lightweight Admin Dashboard
- product CRUD
- category CRUD
- brand CRUD
- product image upload
- product specification PDF upload
- organised product datasheet and download section
- document type labels such as datasheet, manual, certificate, and wiring diagram
- publish / unpublish control
- sorting control
- basic SEO fields

### Storage & Deployment Foundation
- Cloudflare R2 storage setup for product images and product specification PDFs
- static website generation / export setup for public pages
- manual batch publish flow from Laravel admin
- publish queue/job so site generation does not block normal admin work
- publish status tracking such as pending, building, deployed, and failed
- static deployment to Cloudflare Pages, R2 + Worker, or equivalent static hosting/CDN
- cache purge / refresh for affected public URLs after publish
- deployment-ready launch support

### Manual Batch Publish Flow
Recommended Phase 1 publishing flow:

1. Admin updates products, categories, brands, blog posts, images, or documents in Laravel
2. Changes are saved as draft/pending and do not immediately affect the live static website
3. Laravel records pending publish items such as `product.updated`, `category.updated`, or `blog.updated`
4. Admin reviews the pending changes
5. Admin clicks **Publish Static Site** when ready, for example every 2-3 days
6. Background publish job generates static HTML/JSON files from approved data
7. System deploys the generated files to the static hosting/CDN
8. System refreshes/purges affected cache where needed
9. Admin sees publish result, affected pages, and any errors

For urgent corrections, Celectric can run the publish action immediately instead of waiting for the next batch.

### Handover / Training / Warranty
Phase 1 launch handover includes:
- source code handover through the agreed repository or delivery archive
- deployment notes covering server, environment variables, queue/scheduler/cache basics, R2 storage, static publish command/process, and rollback notes
- admin user guide covering product, category, brand, blog/content, document upload, publish/unpublish, RFQ review, and manual static publish flow
- one admin training / walkthrough session, remote or in-person as agreed
- launch support during go-live

Bug-fix warranty:
- 60 days after Phase 1 launch / acceptance
- covers bugs in agreed Phase 1 functionality
- excludes new features, new page types, major design changes, third-party service outages, hosting/server issues outside the agreed setup, and issues caused by unsupported direct code/server changes after handover

---

## Billing Method

Billing can be issued after each milestone is completed and accepted.

Recommended billing flow:
1. Complete milestone scope
2. Submit milestone for review
3. Client confirms acceptance or gives revision feedback
4. Invoice the completed milestone amount
5. Continue to the next milestone

This allows the client to pay progressively based on completed work instead of paying the full Phase 1 amount upfront.

---

## Reference Roadmap Only — Not Included In Price

The following phases are included only as future reference. No price is quoted for these phases in this document.

## Phase 2 — Sales Flow & Lead Handling Enhancements

### Reference Scope Only

Phase 1 includes selected important model-number SEO pages and **basic launch search/filter** only: keyword search, brand/category filtering, and simple sorting. Phase 2 covers broader SEO expansion, autocomplete suggestions, advanced faceted filtering UX, public suggested-product display, and conversion-focused refinements.

- sales and conversion improvements after the core product data import and product structure are ready
- broader SEO landing-page expansion, optimisation, and refinement after launch data is available
- stronger CTA flow
- enquiry funnel improvements
- lead capture refinement
- better conversion-focused page structure
- autocomplete search via Laravel API
- advanced filtering UX refinement via Laravel API
- frontend display for related products / suggested products
- related content / articles
- resource center support
- SEO landing page refinement for model-number search demand
- large-catalog browsing refinement

## Phase 3 — Client Portal, Order History & Operational Enhancements

### Reference Scope Only
- client login portal
- admin-created client accounts
- client order history view
- order detail page
- order status tracking
- reorder / repeat enquiry flow
- private invoice / order / delivery order document access
- signed download links for private documents
- Cloudflare R2 private storage for order-related documents
- client profile and company information
- admin management for client accounts
- admin can assign orders to specific clients
- admin can enable / disable client accounts
- admin can reset password or send invitation link
- HubSpot CRM integration planning and connection if required
- optional Odoo / CRM integration planning if needed

---

## Estimated Timeline

Recommended Phase 1 delivery timeline: **12–18 weeks**

Indicative milestone sequence:
- Phase 1A — 1–2 weeks
- Phase 1B — 2–3 weeks
- Phase 1C — 3 weeks
- Phase 1D — 3–5 weeks
- Phase 1E — 2–3 weeks
- Phase 1F — 2–3 weeks

Timeline depends on:
- speed of content and product data preparation
- number of product records to clean or migrate
- feedback and approval turnaround time
- final admin workflow complexity

---

## Storage Recommendation
Use **Cloudflare R2** for product images, product specification PDFs, and future private order/client documents.

Recommended separation:
- `product-images/` — public / CDN-friendly product images
- `product-specifications/` — public download or protected download depending on business rule
- `order-documents/` — private access only in future phases, using signed download links

Access rules:
- product images can be public/CDN-friendly for fast website loading
- product specification PDFs can be public downloads unless Celectric wants restricted access
- order/client documents should be private and accessed through secure signed links after login in a future phase

The main implementation work is making uploads easy to manage, keeping files organised, controlling access properly, and preparing the structure for future private client documents.

---

## Architecture Note — Manual Batch Static Publish vs Laravel SSR
Laravel SSR remains simpler for always-live admin updates, but Celectric has confirmed that product updates can be accumulated and published manually in batches. For that working style, manual batch static publishing is a good Phase 1 fit.

Recommended interpretation:
- Laravel remains the backend/admin/source-of-truth
- the public website is static after each publish
- admins can update many products over 2-3 days before publishing
- RFQ, configurator validation, admin actions, and future integrations still use Laravel
- basic search/filter can be generated into static listing pages where practical, with dynamic Laravel API support if needed later

This avoids the higher complexity of real-time incremental publishing while keeping the public website fast and stable.

## Scope Assumptions

Final delivery depends on:
- product data availability and cleanliness
- final product count and import structure
- content preparation speed
- number of required page templates
- feedback and approval turnaround time
- final admin workflow requirements

Any scope outside Phase 1 can be quoted separately after Phase 1 is completed or when the client confirms the next phase requirements.
