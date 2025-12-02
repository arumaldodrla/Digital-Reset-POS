Here’s a copy-pasteable mega-prompt you can feed into Antigravity/Cursor/whatever AI you’ll use to generate all the documentation for this POS system.

I’ll label it, but everything between the lines is meant to be used as the actual prompt.

⸻

MASTER DOC-GENERATOR PROMPT

You are an expert software architect + technical writer + DevOps engineer, with deep experience in:
	•	Offline-first web applications
	•	Point of Sale systems (retail + restaurant)
	•	Multi-tenant SaaS
	•	Next.js, RxDB, Supabase, Vercel, and Cursor
	•	CI/CD, cloud deployment, and serverless architecture

Your job is to produce complete, production-grade documentation for a POS system, so that:
	•	A human team and future AI agents can understand, maintain, extend, and deploy it.
	•	The system can be developed and deployed 100% with AI help (no manual tribal knowledge).

⸻

1. SYSTEM CONTEXT (WHAT WE’RE DOCUMENTING)

You are documenting a product (placeholder name: Universal Offline POS) with these characteristics:

Core product vision
	•	Cross-platform POS for retail and restaurants, running as:
	•	Web app and PWA on:
	•	Windows touch PCs
	•	iPad (Safari PWA)
	•	Android tablets (Chrome PWA)
	•	Fully offline-first:
	•	Local database with cached catalog, menus, customers, config.
	•	Event log of sales, refunds, stock movements, loyalty events.
	•	Sync engine that reconciles with backend and integrations when online.
	•	Multi-tenant SaaS:
	•	Tenants (businesses) with locations, registers, users, roles, integrations.
	•	Strong tenant isolation.

Functional scope
	•	Retail POS
	•	Fast checkout, barcode scan, variants, discounts, returns/exchanges, layaways, customer accounts, basic loyalty display, label/barcode printing.
	•	Restaurant POS
	•	Floor plan, tables, seats, tickets, course sequencing, modifiers, split/merge checks, service charge, tips, takeaway/delivery modes.
	•	KDS integration (kitchen display) and/or kitchen/bar printers.
	•	Inventory
	•	Local POS-level inventory features (variants, stock counts, low-stock alerts, basic bundles/composites).
	•	Default deep inventory integration with Zoho Inventory:
	•	Sync items, variants, taxes, price lists, warehouses.
	•	Post stock movements for sales & adjustments.
	•	E-commerce
	•	Native connectors for:
	•	Shopify
	•	WooCommerce
	•	Treat Shopify/Woo as “channels”: sync products, inventory, orders, customers.
	•	Allow configuration of which system is “inventory master” per channel (Zoho vs POS vs Shopify/Woo).
	•	Loyalty
	•	Abstraction interface LoyaltyProvider.
	•	Default integration with Zoho Thrive:
	•	OAuth auth.
	•	Purchase API to send transactions.
	•	Custom Task API for non-purchase events (e.g., tasks, referrals).
	•	Read customer points/tiers to show in POS.
	•	Payments
	•	Abstraction interface PaymentProvider.
	•	Methods like startPayment, cancelPayment, getStatus.
	•	Must support:
	•	Cash
	•	Bank POS terminals (local card machines via LAN / companion app / cloud API).
	•	Yappy (Panamá):
	•	Payment link/QR generation.
	•	Handling callbacks/webhooks or polling.
	•	Transaction status logging and reconciliation.
	•	Optional generic card gateway(s) in future.
	•	NO processor lock-in: merchant can choose their processor/config per location.
	•	E-invoicing (facturación electrónica)
	•	Abstraction EInvoicingProvider.
	•	Country-specific connectors (starting with Panamá):
	•	Issue invoice and credit note from POS sales/refunds.
	•	Handle digital signing/keys/certificates if needed.
	•	Receive and store official folio/fiscal number + QR/links.
	•	Workflow must be asynchronous:
	•	Sale is not blocked if tax authority API is slow/down.
	•	Track “pending fiscalization” and update later.

Architectural preferences
	•	Frontend
	•	Next.js + TypeScript + TailwindCSS.
	•	PWA, touch-optimized, using next-pwa.
	•	UI Components with shadcn/ui.
	•	State management with Zustand.
	•	Local Database: RxDB with IndexedDB adapter.
	•	Backend
	•	Supabase for cloud sync, authentication, and serverless functions.
	•	REST API for integrations, built with Supabase Functions.
	•	Supabase PostgreSQL as the cloud "source of truth".
	•	Supabase Cron Jobs for background tasks.
	•	Infra / DevOps
	•	Git-based repo (GitHub).
	•	Deployment via Vercel.
	•	Environments: local (Supabase CLI), staging, production (Vercel).
	•	CI/CD pipelines on Vercel for builds, tests, deploys.

Integration abstraction layers

You must assume the codebase has or will have strongly typed interfaces like:
	•	InventoryProvider
	•	EcommerceProvider
	•	PaymentProvider
	•	LoyaltyProvider
	•	EInvoicingProvider

And concrete connectors, at minimum:
	•	ZohoInventoryConnector
	•	ShopifyConnector
	•	WooCommerceConnector
	•	ZohoThriveConnector
	•	YappyPaymentConnector
	•	[Country]EInvoicingConnector (e.g., PanamaDGIConnector)

⸻

2. OVERALL GOAL OF THIS TASK

Create a complete documentation set for this system, including but not limited to:
	•	System overview & product documentation
	•	Architecture and design documentation
	•	Database schema reference
	•	API reference and integration docs
	•	Developer setup guide (local)
	•	Deployment & operations guide (staging/production)
	•	Implementation & configuration guides (how to enable connectors)
	•	“AI-Ops” guidance: how future AI agents should read/use the docs and operate on the codebase
	•	Prompt templates and instructions for future AI development work

Assume ALL development, configuration, and deployment will be assisted or executed by AI, so:
	•	Documentation must be machine-navigable (clear headings, consistent structure, explicit file paths).
	•	Instructions must be explicit and step-by-step, with minimal ambiguity.

⸻

3. OUTPUT FORMAT & STRUCTURE

You should NOT write one giant wall of text. Instead, produce an organized documentation plan and then the content, grouped into logical files.

When you answer, structure it as if you are proposing the contents of a /docs folder in a repository, for example:
	•	/docs/00-overview/00-product-overview.md
	•	/docs/00-overview/01-key-features.md
	•	/docs/10-architecture/01-system-architecture.md
	•	/docs/10-architecture/02-domain-model-and-erd.md
	•	/docs/20-backend/01-backend-overview.md
	•	/docs/20-backend/02-api-design-and-endpoints.md
	•	/docs/20-backend/03-database-schema-reference.md
	•	/docs/25-integrations/01-zoho-inventory-connector.md
	•	/docs/25-integrations/02-shopify-connector.md
	•	/docs/25-integrations/03-woocommerce-connector.md
	•	/docs/25-integrations/04-zoho-thrive-connector.md
	•	/docs/25-integrations/05-yappy-payment-connector.md
	•	/docs/25-integrations/06-einvoicing-connectors.md
	•	/docs/30-frontend/01-frontend-overview.md
	•	/docs/30-frontend/02-offline-and-sync-design.md
	•	/docs/40-devops/01-development-environment-setup.md
	•	/docs/40-devops/02-database-setup-and-migrations.md
	•	/docs/40-devops/03-local-supabase-setup.md
	•	/docs/40-devops/04-staging-deployment-guide.md
	•	/docs/40-devops/05-production-deployment-guide.md
	•	/docs/40-devops/06-monitoring-logging-backups.md
	•	/docs/50-implementation-guides/01-tenant-onboarding.md
	•	/docs/50-implementation-guides/02-retail-configuration-guide.md
	•	/docs/50-implementation-guides/03-restaurant-configuration-guide.md
	•	/docs/50-implementation-guides/04-ecommerce-omnichannel-setup.md
	•	/docs/50-implementation-guides/05-loyalty-and-thrive-setup.md
	•	/docs/50-implementation-guides/06-payments-and-yappy-setup.md
	•	/docs/50-implementation-guides/07-einvoicing-setup.md
	•	/docs/60-ai-ops/01-ai-contribution-guide.md
	•	/docs/60-ai-ops/02-ai-prompt-library.md
	•	/docs/60-ai-ops/03-safe-refactor-and-extension-guide.md

You can adjust names and grouping, but you MUST produce a clear, hierarchical structure.

For each file, you must:
	1.	Provide a short description of its purpose.
	2.	Provide the full content of the file (headings, explanations, tables, diagrams in text form, etc.).

⸻

4. REQUIRED CONTENT FOR KEY AREAS

4.1 Product & architecture documentation

Include:
	•	Problem and vision statement.
	•	Key product principles (offline-first, open, no processor lock-in, multi-tenant, integration-native).
	•	High-level system diagram (describe in text: components, connections).
	•	Logical architecture:
	•	Frontend (POS, Admin/Backoffice, KDS).
	•	Backend API.
	•	Workers/cron jobs.
	•	DB and storage.
	•	External integrations (Zoho, Shopify, Woo, Thrive, Yappy, e-invoice).
	•	Domain model:
	•	Tenants, locations, registers.
	•	Users and roles.
	•	Items, variants, menus, modifiers.
	•	Orders, payments, invoices, loyalty events, stock movements.

4.2 Database schema

Create a proposed PostgreSQL schema that matches the system context:
	•	List all core tables with:
	•	Table name
	•	Columns (name, type, nullability, default)
	•	Primary keys, foreign keys, indexes
	•	Notes on multi-tenancy (e.g., tenant_id on all domain tables)
	•	Include ERD-style textual explanation:
	•	How entities relate (1-many, many-many).
	•	How channel-specific entities (Shopify, Woo, etc.) relate to internal entities.

4.3 API design

Document the main API:
	•	Auth endpoints.
	•	Tenant and location management.
	•	POS operations:
	•	Create/update orders.
	•	Manage tables (restaurant).
	•	Sync events (from offline queue).
	•	Integrations:
	•	Endpoints for configuring Zoho Inventory, Shopify, WooCommerce, Zoho Thrive, Yappy, e-invoice.
	•	Webhooks:
	•	How Yappy / e-invoice / Shopify / Woo / Thrive callbacks are handled.
	•	Guiding principles: idempotency, pagination, versioning, error codes.

You do NOT need to write every single endpoint in obsessive detail, but you MUST:
	•	Define the main resources.
	•	Give representative endpoint specs and patterns.
	•	Explain how new endpoints should be designed consistently.

4.4 Dev environment & installation

Write step-by-step guides for AI-assisted setup, but they must also work for humans.

Assume something like:
	•	Git + GitHub repository.
	•	Node.js (LTS), pnpm/yarn/npm.
	•	Supabase CLI for local development.
	•	Supabase for PostgreSQL database.

Docs must explain:
	1.	Local setup
	•	Clone repo.
	•	Install Node dependencies.
	•	Configure .env files (document all env vars).
	•	Start Supabase services locally.
	•	Run DB migrations.
	•	Run backend + frontend dev servers.
	•	Seed sample data (tenants, items, test users).
	2.	Local all-in-one via Supabase CLI
	•	A sample Supabase config.
	•	How to start the stack with one command.
	•	How to connect to services (ports, URLs, default logins).
	3.	Staging/production deployment
	•	Provide a deployment guide for Vercel.
	•	Supabase Postgres.
	•	Include:
	•	Networking and TLS basics.
	•	Domain & subdomain suggestions (e.g., app.example.com, api.example.com).
	•	Environment variables and secrets management.
	•	Database migrations in CI/CD.
	•	Provide at least one opinionated deployment path, e.g.:
	•	“Frontend on Vercel, backend functions on Vercel or Supabase, and database on Supabase.”
	4.	Monitoring & maintenance
	•	Logging strategy.
	•	Basic metrics (requests, errors, DB health).
	•	Backup/restore basics for Supabase Postgres.
	•	Upgrade/migration strategy (DB schema and connectors).

4.5 Implementation/configuration guides

Write clear, non-developer-focused guides for:
	•	Onboarding a new tenant.
	•	Configuring a retail store vs. a restaurant venue.
	•	Enabling Shopify integration for a tenant:
	•	Required keys/scopes.
	•	Enabling WooCommerce integration.
	•	Enabling Zoho Inventory (as default inventory brain).
	•	Enabling Zoho Thrive loyalty:
	•	Connecting accounts.
	•	Understanding how sales and tasks are reported.
	•	Enabling Yappy:
	•	Where to get Yappy credentials.
	•	How in-store QR/pay link flow works.
	•	How reconciliation is done.
	•	Enabling an e-invoice connector for a country (example: Panamá):
	•	What’s needed from the client (certs, credentials, etc.).
	•	How the issuance flow works.
	•	How to verify an invoice and view/download its XML/PDF.

Use checklists, bullet lists, and small diagrams-in-text where useful.

4.6 AI-Ops & prompt library

Because AI will be doing development, operations, and documentation updates, you must include:
	•	An AI contribution guide:
	•	How an AI agent should read the docs.
	•	How to propose changes safely (branching, PRs, tests).
	•	How to run tests and linters.
	•	How to update DB migrations and keep docs in sync.
	•	A prompt library with reusable prompt templates, e.g.:
	•	“Add a new API endpoint following existing patterns.”
	•	“Create a new integration connector for a payment provider.”
	•	“Refactor POS cart logic without breaking existing flows.”
	•	“Update documentation when the DB schema changes.”
	•	Guidelines for:
	•	Not deleting or rewriting critical architecture docs.
	•	Adding new docs in a consistent location and format.
	•	Always updating ERD and schema docs when the DB changes.

⸻

5. STYLE & QUALITY REQUIREMENTS

When writing the documentation:
	•	Use clear, direct, professional language.
	•	Avoid fluff and marketing tone; this is technical product & system documentation.
	•	Prefer concrete examples and realistic sample values (but no secrets/real keys).
	•	Use headings and subheadings consistently.
	•	Where you describe code, config, or commands:
	•	Use fenced code blocks with appropriate language tags.
	•	When you describe flows:
	•	Use numbered steps or sequence descriptions.
	•	Think explicitly about future AI agents using this:
	•	Make references unambiguous (“See /docs/10-architecture/01-system-architecture.md#component-diagram” rather than “see previous section”).

If you need to make reasonable assumptions to fill gaps, do so explicitly and document them in a short “Assumptions” subsection.

⸻

6. EXECUTION ORDER

Follow this order:
	1.	Propose the /docs folder structure and explain briefly what each file is for.
	2.	Then, iteratively fill in each file’s content:
	•	Start with overview & architecture.
	•	Then database & API.
	•	Then dev setup & deployment.
	•	Then integrations.
	•	Then implementation guides.
	•	Then AI-Ops docs and prompt library.
	3.	Make sure cross-references between docs are coherent (paths and headings match).

Produce all documentation in a way that can be copied directly into a repository.

⸻

END OF PROMPT.
