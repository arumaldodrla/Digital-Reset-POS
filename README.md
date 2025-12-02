# Digital Reset POS

A modern, offline-first Point of Sale (POS) system for retail and restaurant businesses, designed for 100% AI-driven development.

## Overview

Digital Reset POS is a multi-tenant, cross-platform POS system built with modern web technologies. It operates seamlessly offline and synchronizes with the cloud when a connection is available, ensuring that your business never stops running.

## Tech Stack

| Component | Technology |
| :--- | :--- |
| **Frontend** | Next.js 15 + TypeScript + Tailwind CSS |
| **UI Components** | shadcn/ui |
| **Local Database** | RxDB (reactive, offline-first) |
| **State Management** | Zustand |
| **Backend** | Supabase (PostgreSQL + Serverless Functions) |
| **PWA** | next-pwa |
| **Deployment** | Vercel |
| **Development** | Cursor (AI-powered code editor) |

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

- **[00-overview](./docs/00-overview)**: Product overview and key features
- **[10-architecture](./docs/10-architecture)**: System architecture and domain models
- **[20-backend](./docs/20-backend)**: Backend API design and database schema
- **[25-integrations](./docs/25-integrations)**: Integration connectors
- **[30-frontend](./docs/30-frontend)**: Frontend architecture and offline sync design
- **[40-devops](./docs/40-devops)**: Development environment setup and deployment guides
- **[50-implementation-guides](./docs/50-implementation-guides)**: Configuration guides for various features
- **[60-ai-ops](./docs/60-ai-ops)**: AI contribution guide and prompt library

## Quick Start

### Prerequisites

- Node.js 18.x or later
- pnpm
- Docker
- Supabase CLI

### Local Development

1.  Clone the repository:

    ```bash
    git clone https://github.com/arumaldodrla/Digital-Reset-POS.git
    cd Digital-Reset-POS
    ```

2.  Install dependencies:

    ```bash
    pnpm install
    ```

3.  Start the local Supabase stack:

    ```bash
    pnpm db:start
    ```

4.  Configure environment variables:

    Create a `.env.local` file with your Supabase credentials.

5.  Start the development server:

    ```bash
    pnpm dev
    ```

6.  Open [http://localhost:3000](http://localhost:3000) in your browser.

## AI-First Development

This project is designed for 100% AI-assisted development using [Cursor](https://cursor.sh/). All documentation is structured to be machine-navigable with clear headings, consistent structure, and explicit file paths.

Refer to the [AI Contribution Guide](./docs/60-ai-ops/01-ai-contribution-guide.md) and [AI Prompt Library](./docs/60-ai-ops/02-ai-prompt-library.md) for detailed instructions on how to use AI for development.

## Contributing

This project is designed for AI-assisted development. Please refer to the [AI Contribution Guide](./docs/60-ai-ops/01-ai-contribution-guide.md) for guidelines on how to contribute.

## License

[Specify your license here]

## Contact

[Specify contact information or support channels here]
