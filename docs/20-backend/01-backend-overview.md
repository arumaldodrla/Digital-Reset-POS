# Backend Overview

## 1. Backend Architecture

The backend of the Universal Offline POS system is built on Supabase, a comprehensive platform that provides a PostgreSQL database, authentication, serverless functions, and storage. The backend serves as the central "source of truth" for all data and is responsible for cloud data storage, user authentication, and server-side business logic for integrations.

## 2. Key Components

| Component | Technology | Description |
| :--- | :--- | :--- |
| **Cloud Database** | Supabase (PostgreSQL) | The central database for all tenants, locations, and transactional data. |
| **Authentication** | Supabase Auth | Manages user authentication, authorization, and row-level security (RLS). |
| **Serverless Functions** | Supabase Functions | Used to implement server-side business logic for integrations, webhooks, and other tasks. |
| **Background Workers** | Supabase Cron Jobs | Scheduled tasks for data synchronization, report generation, and other background processes. |
| **Storage** | Supabase Storage | Used to store files, such as product images, invoices, and other documents. |

## 3. Data Synchronization

The backend does not directly handle offline data synchronization. Instead, it provides a set of APIs that the frontend (RxDB) can use to replicate data. The RxDB replication protocol is used to push and pull changes between the local database and the Supabase backend. This ensures that the frontend remains fully functional offline and that data is synchronized with the cloud when a connection is available.

## 4. Multi-Tenancy

The backend is designed as a multi-tenant system, with strong data isolation between tenants. This is achieved through a combination of:

- **Tenant ID**: A `tenant_id` column is added to all domain tables to associate data with a specific tenant.
- **Row-Level Security (RLS)**: Supabase's RLS is used to enforce data isolation at the database level, ensuring that users can only access data belonging to their own tenant.
