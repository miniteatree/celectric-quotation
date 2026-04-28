# Celectric Website Redesign Quotation

## Purpose
Client-facing quotation for Celectric website redesign and digital platform upgrade.

## Project Direction
Celectric website should be built as an **industrial catalog + enquiry platform**, not only a static company profile website.

The platform should support:
- searchable product catalog
- brand and category browsing
- quotation / enquiry flow
- product specification documents
- future client portal and order document access
- scalable product growth around **3,000+ products**

## Recommended Architecture
Use a **hybrid architecture**:
- public-facing pages are statically generated for speed and SEO
- Laravel remains on VPS for admin dashboard, APIs, quotation submit, search, filtering, and future portal features
- product updates use incremental rebuilds instead of full-site rebuilds
- Cloudflare R2 stores product images, product specification PDFs, and private client/order documents

This structure is suitable for Celectric because it keeps the public website fast while preserving dynamic business workflows.

---

## Phase 1 — Core Website + Lightweight Admin Dashboard

### Includes
- public website redesign
- homepage
- product listing pages
- product detail pages
- brand pages
- category pages
- multi-category product organisation where relevant
- contact / enquiry flow
- RFQ / quotation submit flow
- mobile responsive cleanup
- lightweight admin dashboard
- product CRUD
- category CRUD
- brand CRUD
- product image upload
- product specification PDF upload
- Cloudflare R2 storage setup for product images and product specification PDFs
- publish / unpublish control
- sorting control
- basic SEO fields
- static export foundation
- incremental rebuild flow for changed products and affected related pages

### Estimated Price
**RM 28,000 – RM 54,000**

---

## Phase 2 — Sales Flow & Lead Handling Enhancements

### Includes
- stronger CTA flow
- enquiry funnel improvements
- lead capture refinement
- better conversion-focused page structure
- autocomplete search via Laravel API
- filtering refinement via Laravel API
- related products
- related content / articles
- resource center support
- SEO landing pages
- better document grouping rules
- large-catalog browsing refinement

### Estimated Price
**RM 8,000 – RM 16,000**

---

## Phase 3 — Client Portal, Order History & Operational Enhancements

### Includes
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
- optional Odoo / CRM integration planning if needed

### Estimated Price
**RM 18,000 – RM 42,000**

---

## Recommended Total

| Structure | Estimated Amount |
|---|---:|
| Lean quote | **RM 54,000** |
| Comfortable full-scope quote | **RM 68,000 – RM 78,000** |
| Upper range | **RM 112,000** |

## Suggested Client-Facing Target
Recommended proposal target for full Phase 1–3 scope:

**RM 68,000 – RM 78,000**

If Celectric wants an MVP first, start with Phase 1 only:

**RM 28,000 – RM 54,000**

---

## Storage Recommendation
Use **Cloudflare R2** for product images, product specification PDFs, and private order/client documents.

Recommended separation:
- `product-images/` — public / CDN-friendly product images
- `product-specifications/` — public download or protected download depending on business rule
- `order-documents/` — private access only, using signed download links

Estimated Cloudflare R2 storage budget for around **3,000+ products**:
- 20GB total storage: around **RM 10/year**
- 50GB total storage: around **RM 20–30/year**
- 100GB total storage: around **RM 50–60/year**

Monthly cloud storage cost is expected to be low. The main cost is implementation: upload flow, metadata management, access control, signed links, and admin/client UI.

---

## Database / Access Recommendation
Use the same database, but separate user roles and permissions clearly.

Recommended structure:
- `users` table for login identity
- `roles` or `user_roles` for admin / client permissions
- `clients` table for client company profile
- `orders` table for order records
- `order_items` table for products/items inside each order
- `documents` table for uploaded/finalized invoices, quotations, delivery orders, receipts, or supporting files

Do **not** use a separate database schema unless the platform becomes multi-tenant SaaS in the future.

For this project, same database with role-based access is simpler, cheaper, and easier to maintain.

---

## Pricing Depends On
Final pricing depends on:
- exact product count and product data cleanliness
- content migration workload
- admin customisation depth
- number of page templates
- SEO / blog scope
- document storage and access rules
- Odoo / CRM integration complexity, if included
- final client portal workflow requirements
