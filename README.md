# Digital Reset POS

A modern, offline-first Point of Sale (POS) system for retail and restaurant businesses, designed for 100% AI-driven development.

## Overview

Digital Reset POS is a multi-tenant, cross-platform POS system built with modern web technologies. It operates seamlessly offline and synchronizes with the cloud when a connection is available, ensuring that your business never stops running.

## Tech Stack

The system is built using the **Next.js + RxDB + Supabase** stack, specifically chosen for offline-first capabilities and AI-friendly development.

| Component | Technology | Purpose |
| :--- | :--- | :--- |
| **Frontend** | Next.js 15 + TypeScript | React framework with PWA support |
| **UI Components** | shadcn/ui + Tailwind CSS | Customizable, accessible components |
| **Local Database** | RxDB + IndexedDB | Offline-first reactive database |
| **State Management** | Zustand | Lightweight state management |
| **Backend** | Supabase (PostgreSQL) | Cloud sync and authentication |
| **Serverless Functions** | Supabase Functions | Integration logic |
| **PWA** | next-pwa | Service workers and offline assets |
| **Deployment** | Vercel | Frontend hosting and CI/CD |
| **Development** | Cursor | AI-powered code editor |

## Why This Stack?

**Critical Decision:** The original stack (Refine + Supabase) was **not suitable** for offline-first POS systems. Supabase does not provide native offline support, and Refine is designed for admin panels, not offline-first applications.

**Current Architecture:**
- **RxDB** serves as the primary database, running 100% offline in the browser
- **Supabase** is used only for cloud sync and never blocks POS operations
- **Next.js** provides the best AI training data and PWA support
- **Vercel** offers optimal deployment for Next.js applications

## Key Features

- **Offline-First**: All core POS operations work 100% offline with automatic cloud sync.
- **Cross-Platform**: Runs as a PWA on Windows, iPad, and Android tablets.
- **Multi-Tenant SaaS**: Supports multiple businesses with strong data isolation.
- **Retail POS**: Fast checkout, barcode scanning, variants, discounts, returns, and loyalty.
- **Restaurant POS**: Floor plans, table management, modifiers, split checks, and KDS integration.
- **Inventory Management**: Deep integration with Zoho Inventory.
- **E-commerce Integration**: Native connectors for Shopify and WooCommerce.
- **Loyalty Programs**: Integration with Zoho Thrive.
- **Payment Processing**: Support for cash, bank terminals, and Yappy (Panamá).
- **E-invoicing**: Country-specific electronic invoicing (starting with Panamá).

## Documentation

Complete documentation is available in the `/docs` directory:

| Directory | Description |
| :--- | :--- |
| **[00-overview](./docs/00-overview)** | Product overview and key features |
| **[10-architecture](./docs/10-architecture)** | System architecture and domain models |
| **[20-backend](./docs/20-backend)** | Backend API design and database schema |
| **[25-integrations](./docs/25-integrations)** | Integration connectors (Zoho, Shopify, WooCommerce, etc.) |
| **[30-frontend](./docs/30-frontend)** | Frontend architecture and offline sync design |
| **[40-devops](./docs/40-devops)** | Development environment setup and deployment guides |
| **[50-implementation-guides](./docs/50-implementation-guides)** | Configuration guides for various features |
| **[60-ai-ops](./docs/60-ai-ops)** | AI contribution guide and prompt library |

## Quick Start

### Prerequisites

- **Node.js** 18.x or later
- **pnpm** (package manager)
- **Docker** (only required for local Supabase development)
- **Supabase CLI** (for local database management)

**Note:** Docker is only needed if you want to run a local Supabase instance for development. You can also use a cloud Supabase project and skip Docker entirely.

### Option 1: Local Development with Supabase Cloud

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/arumaldodrla/Digital-Reset-POS.git
    cd Digital-Reset-POS
    ```

2.  **Install dependencies:**

    ```bash
    pnpm install
    ```

3.  **Create a Supabase project:**

    Go to [supabase.com](https://supabase.com) and create a new project.

4.  **Configure environment variables:**

    Create a `.env.local` file in the root directory:

    ```env
    NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
    NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
    ```

5.  **Start the development server:**

    ```bash
    pnpm dev
    ```

6.  **Open the application:**

    Navigate to [http://localhost:3000](http://localhost:3000) in your browser.

### Option 2: Local Development with Local Supabase (Requires Docker)

1.  **Follow steps 1-2 from Option 1**

2.  **Install Supabase CLI:**

    ```bash
    pnpm install -g supabase
    ```

3.  **Start the local Supabase stack:**

    ```bash
    supabase start
    ```

    This will start a local Supabase instance using Docker. The first time you run this, it will download the necessary Docker images.

4.  **Configure environment variables:**

    Create a `.env.local` file with the local Supabase credentials (displayed after running `supabase start`):

    ```env
    NEXT_PUBLIC_SUPABASE_URL=http://localhost:54321
    NEXT_PUBLIC_SUPABASE_ANON_KEY=your-local-anon-key
    ```

5.  **Start the development server:**

    ```bash
    pnpm dev
    ```

6.  **Open the application:**

    Navigate to [http://localhost:3000](http://localhost:3000) in your browser.

## AI-First Development

This project is designed for **100% AI-assisted development** using [Cursor](https://cursor.sh/). All documentation is structured to be machine-navigable with clear headings, consistent structure, and explicit file paths.

### Getting Started with AI Development

1.  **Open the project in Cursor**
2.  **Read the documentation** starting with `/docs/00-overview/00-product-overview.md`
3.  **Use the AI Prompt Library** at `/docs/60-ai-ops/02-ai-prompt-library.md` for common tasks
4.  **Follow the AI Contribution Guide** at `/docs/60-ai-ops/01-ai-contribution-guide.md`

### Example AI Prompts

```
Create a new RxDB schema for the orders collection based on the database schema in /docs/20-backend/03-database-schema-reference.md
```

```
Implement the Shopify connector following the design in /docs/25-integrations/02-shopify-connector.md
```

```
Create a new React component for the POS checkout screen using shadcn/ui components
```

## Project Structure

```
Digital-Reset-POS/
├── docs/                    # Complete documentation
│   ├── 00-overview/        # Product overview
│   ├── 10-architecture/    # System architecture
│   ├── 20-backend/         # Backend and database
│   ├── 25-integrations/    # Integration connectors
│   ├── 30-frontend/        # Frontend architecture
│   ├── 40-devops/          # DevOps and deployment
│   ├── 50-implementation-guides/  # Configuration guides
│   └── 60-ai-ops/          # AI development guides
├── app/                     # Next.js app directory (to be created)
├── components/              # React components (to be created)
├── lib/                     # Utility libraries (to be created)
└── supabase/               # Supabase migrations (to be created)
```

## Contributing

This project is designed for AI-assisted development. Please refer to the [AI Contribution Guide](./docs/60-ai-ops/01-ai-contribution-guide.md) for guidelines on how to contribute.

All contributions should:
- Follow the existing architecture patterns
- Include tests for new features
- Update documentation when making schema changes
- Use the AI Prompt Library for consistency

## Deployment

The application is designed to be deployed on **Vercel** for optimal performance with Next.js. Refer to the deployment guides:

- [Staging Deployment Guide](./docs/40-devops/04-staging-deployment-guide.md)
- [Production Deployment Guide](./docs/40-devops/05-production-deployment-guide.md)

## License

[Specify your license here]

## Contact

[Specify contact information or support channels here]

---

**Built with ❤️ for offline-first POS systems**
