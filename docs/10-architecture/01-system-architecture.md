# System Architecture

## 1. High-Level System Diagram

The Universal Offline POS system is designed with a modern, decoupled architecture that prioritizes offline-first functionality, scalability, and maintainability. The following diagram illustrates the high-level components and their interactions:

```
┌─────────────────────────────────────┐
│         Frontend (PWA)              │
│  Next.js 15 + TypeScript + Tailwind │
│                                     │
│  ┌──────────────────────────────┐  │
│  │   RxDB (Primary Database)    │  │
│  │   - IndexedDB storage        │  │
│  │   - Reactive queries         │  │
│  │   - Conflict resolution      │  │
│  │   - 100% offline capable     │  │
│  └──────────────────────────────┘  │
│              ↕ Sync                 │
│  ┌──────────────────────────────┐  │
│  │   Supabase Replication       │  │
│  │   - Background sync          │  │
│  │   - Conflict handling        │  │
│  │   - Never blocks UI          │  │
│  └──────────────────────────────┘  │
└─────────────────────────────────────┘
              ↕ (when online)
┌─────────────────────────────────────┐
│      Backend (Supabase Cloud)       │
│  - PostgreSQL (source of truth)     │
│  - Supabase Functions (integrations)│
│  - Supabase Auth                    │
│  - Supabase Storage                 │
└─────────────────────────────────────┘
```

## 2. Logical Architecture

The system is divided into three main logical layers:

- **Frontend**: A Progressive Web App (PWA) built with Next.js, responsible for all user-facing interactions. It contains the local database (RxDB) and is designed to be fully functional offline.
- **Backend**: A serverless backend powered by Supabase, responsible for cloud data storage, user authentication, and server-side business logic for integrations.
- **Integrations**: A set of connectors that communicate with third-party services for inventory, e-commerce, loyalty, and payments.

## 3. Component Descriptions

### 3.1. Frontend Components

| Component | Technology | Description |
| :--- | :--- | :--- |
| **POS Application** | Next.js + RxDB | The primary user interface for sales, returns, and daily operations. It runs entirely in the browser and works 100% offline. |
| **Admin/Backoffice** | Next.js | A web-based interface for managing products, customers, and system settings. It can be part of the same Next.js application or a separate one. |
| **Kitchen Display System (KDS)** | Next.js | A dedicated interface for kitchen staff to view and manage orders. It subscribes to real-time updates from the POS. |
| **Local Database** | RxDB | A reactive, offline-first database that runs in the browser. It stores all application data locally and handles data synchronization with the cloud. |

### 3.2. Backend Components

| Component | Technology | Description |
| :--- | :--- | :--- |
| **Cloud Database** | Supabase (PostgreSQL) | The central "source of truth" for all data. It stores data from all tenants and locations. |
| **Authentication** | Supabase Auth | Manages user authentication and authorization, with support for email/password, social logins, and multi-factor authentication. |
| **Serverless Functions** | Supabase Functions | Used to implement server-side business logic for integrations, webhooks, and other tasks that require a secure environment. |
| **Background Workers** | Supabase Cron Jobs | Scheduled tasks for data synchronization, report generation, and other background processes. |
| **Storage** | Supabase Storage | Used to store files, such as product images, invoices, and other documents. |

### 3.3. Integration Components

| Component | Description |
| :--- | :--- |
| **Integration Providers** | A set of abstract interfaces that define the contract for each integration type (e.g., `InventoryProvider`, `PaymentProvider`). |
| **Integration Connectors** | Concrete implementations of the provider interfaces that communicate with specific third-party services (e.g., `ZohoInventoryConnector`, `ShopifyConnector`). |

## 4. Data Flow

1. **Offline Operations**: All POS operations are first written to the local RxDB database. The UI is updated reactively, providing a fast and seamless user experience.
2. **Background Sync**: When an internet connection is available, the RxDB replication engine automatically synchronizes local changes with the Supabase backend.
3. **Conflict Resolution**: If there are conflicting changes from multiple devices, the replication engine resolves them based on a defined strategy (e.g., last-write-wins).
4. **Cloud Processing**: Once data is in the Supabase backend, it can be processed by serverless functions, trigger webhooks, or be used for reporting and analytics.
5. **Third-Party Integrations**: Serverless functions are used to communicate with third-party services, such as Zoho, Shopify, and payment gateways.

## 5. Offline-First Architecture

The offline-first architecture is the cornerstone of the Universal Offline POS system. It is achieved through the following key principles:

- **Local-First Database**: RxDB is used as the primary database for the application. All data is stored locally in the browser's IndexedDB, making it accessible even without an internet connection.
- **Reactive UI**: The UI is built with React and Zustand, which reactively update when data in the local database changes.
- **Asynchronous Synchronization**: Data is synchronized with the Supabase backend asynchronously in the background. The UI is never blocked by network requests.
- **Conflict Resolution**: The system is designed to handle data conflicts that may arise when multiple devices are used offline. RxDB provides a built-in conflict resolution mechanism that can be customized to fit the business logic.
