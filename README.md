# Digital Reset POS

**The Unfailing, Autonomous, and Global POS**

Digital Reset POS is a modern, multi-tenant, cross-platform Point of Sale (POS) system designed for retail and restaurant businesses. It is defined by four core pillars:

1.  **Unyielding Reliability**: A local-first architecture guarantees 100% functionality, even without an internet connection.
2.  **Effortless Usability**: A simple, zero-training interface for cashiers, with deep, complex features for managers.
3.  **Global Reach**: Built with AI-powered internationalization (i18n), starting with English and Spanish.
4.  **Autonomous Operation**: **100% developed and maintained by AI**, with weekly self-revision and updates.

---

## The Problem We Solve

Traditional cloud-based POS systems have a critical flaw: they depend on a stable internet connection. When the connection fails, sales stop. A 2023 retail study found that **82% of businesses reported significant losses due to POS downtime** caused by internet disruptions.

**Digital Reset POS is architecturally incapable of failing due to internet connectivity issues.** The primary database runs locally on the device, and the cloud is used only for background synchronization and backup. If the internet is down for five minutes or five days, the POS continues to operate with 100% of its functionality.

---

## The Technology Stack

Our stack was chosen for its reliability, developer experience, and suitability for AI-driven development.

| Component | Technology | Purpose |
| :--- | :--- | :--- |
| **Frontend** | Next.js 15 + TypeScript | React framework with PWA support for cross-platform deployment. |
| **UI Components** | shadcn/ui + Tailwind CSS | Customizable, accessible, and touch-friendly components. |
| **Internationalization** | `next-intl` | AI-friendly framework for managing translations. |
| **Local Database** | **RxDB** + IndexedDB | **The core of our offline-first strategy.** A full-featured, reactive database running in the browser. |
| **State Management** | Zustand | Lightweight state management for UI-only state. |
| **Backend** | **Supabase** (PostgreSQL) | Cloud sync, authentication, and serverless functions. **Never blocks POS operations.** |
| **Deployment** | Vercel | Frontend hosting with automated CI/CD. |
| **Development** | Cursor | AI-powered code editor. |

---

## Documentation Index

All documentation is located in the `/docs` directory. It is organized to serve three audiences: **AI Developers**, **Project Managers**, and **Marketing Teams**.

### Overview & Vision

| Document | Description |
| :--- | :--- |
| [Executive Summary](./docs/00-overview/00-executive-summary.md) | The problem, solution, market opportunity, and strategic vision. **Start here.** |
| [Product Overview](./docs/00-overview/00-product-overview.md) | Core product principles and target audience. |
| [Key Features](./docs/00-overview/01-key-features.md) | A comprehensive list of features for retail and restaurant POS. |

### Architecture & Data Model

| Document | Description |
| :--- | :--- |
| [System Architecture](./docs/10-architecture/01-system-architecture.md) | High-level system diagram, the three layers, and data flow. |
| [Domain Model & ERD](./docs/10-architecture/02-domain-model-and-erd.md) | Plain-English data dictionary and entity-relationship diagram. |

### Internationalization (i18n)

| Document | Description |
| :--- | :--- |
| [i18n Architecture](./docs/15-internationalization/01-i18n-architecture.md) | The architecture for AI-powered translation and multi-language support. |

### Backend & Database

| Document | Description |
| :--- | :--- |
| [Backend Overview](./docs/20-backend/01-backend-overview.md) | The role of Supabase as a supporting actor, not the main system. |
| [API Design & Endpoints](./docs/20-backend/02-api-design-and-endpoints.md) | API strategy and endpoint specifications. |
| [Database Schema Reference](./docs/20-backend/03-database-schema-reference.md) | The definitive technical blueprint for all database tables, types, and RLS policies. |

### Integrations

| Document | Description |
| :--- | :--- |
| [Zoho Inventory Connector](./docs/25-integrations/01-zoho-inventory-connector.md) | Design for the inventory management integration. |
| [Shopify Connector](./docs/25-integrations/02-shopify-connector.md) | Design for the e-commerce integration. |
| [WooCommerce Connector](./docs/25-integrations/03-woocommerce-connector.md) | Design for the e-commerce integration. |
| [Zoho Thrive Connector](./docs/25-integrations/04-zoho-thrive-connector.md) | Design for the loyalty program integration. |
| [Yappy Payment Connector](./docs/25-integrations/05-yappy-payment-connector.md) | Design for the Panamanian payment gateway. |
| [E-invoicing Connectors](./docs/25-integrations/06-einvoicing-connectors.md) | Design for country-specific electronic invoicing. |

### Frontend & Offline Sync

| Document | Description |
| :--- | :--- |
| [Frontend Overview](./docs/30-frontend/01-frontend-overview.md) | Frontend architecture, technology choices, UX principles, and i18n integration. |
| [Offline & Sync Design](./docs/30-frontend/02-offline-and-sync-design.md) | Deep dive into RxDB, service workers, and conflict resolution. |

### DevOps & Deployment

| Document | Description |
| :--- | :--- |
| [Development Environment Setup](./docs/40-devops/01-development-environment-setup.md) | How to get the project running locally (with or without Docker). |
| [Database Setup & Migrations](./docs/40-devops/02-database-setup-and-migrations.md) | How to manage database schema changes. |
| [Local Supabase Setup](./docs/40-devops/03-local-supabase-setup.md) | Running a full Supabase stack locally with Docker. |
| [Staging Deployment Guide](./docs/40-devops/04-staging-deployment-guide.md) | Deploying to a staging environment for testing. |
| [Production Deployment Guide](./docs/40-devops/05-production-deployment-guide.md) | Deploying to production on Vercel. |
| [Monitoring, Logging & Backups](./docs/40-devops/06-monitoring-logging-backups.md) | Operational best practices. |

### Implementation Guides

| Document | Description |
| :--- | :--- |
| [Tenant Onboarding](./docs/50-implementation-guides/01-tenant-onboarding.md) | How to set up a new business on the platform. |
| [Retail Configuration](./docs/50-implementation-guides/02-retail-configuration-guide.md) | Configuring the POS for a retail store. |
| [Restaurant Configuration](./docs/50-implementation-guides/03-restaurant-configuration-guide.md) | Configuring the POS for a restaurant. |
| [E-commerce & Omnichannel Setup](./docs/50-implementation-guides/04-ecommerce-omnichannel-setup.md) | Connecting to Shopify or WooCommerce. |
| [Loyalty & Thrive Setup](./docs/50-implementation-guides/05-loyalty-and-thrive-setup.md) | Setting up the Zoho Thrive loyalty integration. |
| [Payments & Yappy Setup](./docs/50-implementation-guides/06-payments-and-yappy-setup.md) | Configuring payment methods. |
| [E-invoicing Setup](./docs/50-implementation-guides/07-einvoicing-setup.md) | Enabling electronic invoicing for compliance. |

### AI-Ops (For AI Developers)

| Document | Description |
| :--- | :--- |
| [AI Contribution Guide](./docs/60-ai-ops/01-ai-contribution-guide.md) | **Mission briefing for AI agents.** The standard operating procedure for developing 100% of the application. |
| [AI Prompt Library](./docs/60-ai-ops/02-ai-prompt-library.md) | Reusable prompt templates for common development tasks. |
| [Safe Refactor & Extension Guide](./docs/60-ai-ops/03-safe-refactor-and-extension-guide.md) | Best practices for modifying existing code. |

### Autonomous Operations

| Document | Description |
| :--- | :--- |
| [Self-Maintenance & Updates](./docs/65-autonomous-operations/01-self-maintenance-and-updates.md) | The architecture for weekly self-revision and autonomous updates. |

### Marketing (For Marketing Teams)

| Document | Description |
| :--- | :--- |
| [Marketing & Website Content Blueprint](./docs/70-marketing/01-marketing-and-website-content.md) | Core messages, target personas, and website content structure. |

### Market Research

| Document | Description |
| :--- | :--- |
| [Market Research Report](./market_research/market_research_report.md) | Comprehensive analysis of market size, competition, and strategic recommendations. |

---

## Quick Start

### Prerequisites

-   **Node.js** v18.x or later
-   **pnpm** (package manager)
-   **Docker** (optional, for local Supabase)

### Setup

```bash
# 1. Clone the repository
git clone https://github.com/arumaldodrla/Digital-Reset-POS.git
cd Digital-Reset-POS

# 2. Install dependencies
pnpm install

# 3. Configure environment variables
# Create a .env.local file with your Supabase credentials.
# See docs/40-devops/01-development-environment-setup.md for details.

# 4. Start the development server
pnpm dev
```

---

## Contributing

This project is **100% developed by AI**. Please refer to the [AI Contribution Guide](./docs/60-ai-ops/01-ai-contribution-guide.md) for the standard operating procedure. Human supervisors are responsible for creating issues, reviewing pull requests, and approving major updates.

---

## License

[Specify your license here]

---

**Built for reliability. Designed for AI. Ready for the world.**
