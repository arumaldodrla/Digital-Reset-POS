# Digital Reset POS

Complete documentation for a multi-tenant, offline-first Point of Sale (POS) system designed for retail and restaurant businesses.

## Overview

This repository contains comprehensive documentation for building a modern, production-ready POS system that works seamlessly across multiple platforms and operates offline-first.

## Tech Stack

The system is built using the following modern technologies:

- **Frontend**: [Refine](https://refine.dev/) (React-based framework) + TypeScript
- **Backend**: [Supabase](https://supabase.com/) (PostgreSQL database + serverless functions)
- **Deployment**: [Vercel](https://vercel.com/) (hosting and CI/CD)
- **Development**: [Cursor](https://cursor.sh/) (AI-powered code editor)

## Key Features

- **Cross-platform**: Web app and PWA support for Windows, iPad, and Android tablets
- **Offline-first**: Full functionality without internet connection, with automatic sync when online
- **Multi-tenant SaaS**: Complete tenant isolation with locations, registers, users, and roles
- **Retail POS**: Fast checkout, barcode scanning, variants, discounts, returns, layaways, and loyalty
- **Restaurant POS**: Floor plans, table management, course sequencing, modifiers, split checks, and KDS integration
- **Inventory Management**: Integration with Zoho Inventory for comprehensive stock management
- **E-commerce Integration**: Native connectors for Shopify and WooCommerce
- **Loyalty Programs**: Integration with Zoho Thrive for customer loyalty management
- **Payment Processing**: Support for cash, bank terminals, and Yappy (Panamá)
- **E-invoicing**: Country-specific electronic invoicing (starting with Panamá)

## Documentation Structure

The documentation is organized as follows:

- **00-overview**: Product overview and key features
- **10-architecture**: System architecture and domain models
- **20-backend**: Backend API design and database schema
- **25-integrations**: Integration connectors (Zoho, Shopify, WooCommerce, Thrive, Yappy, e-invoicing)
- **30-frontend**: Frontend architecture and offline sync design
- **40-devops**: Development environment setup, deployment guides, and monitoring
- **50-implementation-guides**: Configuration guides for retail, restaurant, e-commerce, loyalty, payments, and e-invoicing
- **60-ai-ops**: AI contribution guide, prompt library, and safe refactoring guidelines

## Getting Started

To generate the complete documentation set, use the master prompt located in:

**[MASTER_DOC_GENERATOR_PROMPT.md](./MASTER_DOC_GENERATOR_PROMPT.md)**

This prompt is designed to be used with AI assistants (Cursor, Claude, ChatGPT, etc.) to generate comprehensive, production-grade documentation that follows best practices and is optimized for both human developers and AI agents.

## AI-First Development

This project is designed to be developed and maintained with AI assistance. All documentation is structured to be:

- **Machine-navigable**: Clear headings, consistent structure, and explicit file paths
- **Unambiguous**: Step-by-step instructions with minimal ambiguity
- **Comprehensive**: Complete coverage of architecture, implementation, and operations

## Contributing

This repository is designed for AI-assisted development. Please refer to the AI-Ops documentation (once generated) for guidelines on:

- How to read and use the documentation
- How to propose changes safely
- How to run tests and linters
- How to update database migrations and keep docs in sync

## License

[Specify your license here]

## Contact

[Specify contact information or support channels here]
