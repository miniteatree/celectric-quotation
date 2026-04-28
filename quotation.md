# Celectric Website Redesign Proposal

## Purpose
Client-facing proposal for Celectric website redesign and digital platform upgrade.

This version is prepared **without pricing** for online review and scope discussion.

## Project Direction
Celectric website should be built as an **industrial catalog + enquiry platform**, not only a static company profile website.

The platform should support:
- searchable product catalog
- brand and category browsing
- quotation / enquiry flow
- product specification documents
- future client portal and order document access
- scalable product growth around 3,000+ products

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

---

## Recommended Commercial Structure
- Start with Phase 1 as the MVP launch scope
- Add Phase 2 after the main website structure is stable
- Keep Phase 3 as the client portal and operational expansion phase

---

## Storage Recommendation
Use **Cloudflare R2** for product images, product specification PDFs, and private order/client documents.

Recommended separation:
- `product-images/` — public / CDN-friendly product images
- `product-specifications/` — public download or protected download depending on business rule
- `order-documents/` — private access only, using signed download links

Access rules:
- product images can be public/CDN-friendly for fast website loading
- product specification PDFs can be public downloads unless Celectric wants restricted access
- order/client documents must be private and accessed through secure signed links after login

The main implementation work is upload flow, metadata management, access control, signed links, and admin/client UI.

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

## Scope Depends On
Final scope depends on:
- exact product count and product data cleanliness
- content migration workload
- admin customisation depth
- number of page templates
- SEO / blog scope
- document storage and access rules
- Odoo / CRM integration complexity, if included
- final client portal workflow requirements
