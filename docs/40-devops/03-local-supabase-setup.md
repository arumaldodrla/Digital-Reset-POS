# Local Supabase Setup

## 1. Introduction

The Supabase CLI provides a complete local development environment that mirrors the Supabase cloud platform. This allows you to develop and test your application locally without needing an internet connection.

## 2. Starting the Local Supabase Stack

To start the local Supabase stack, run the following command:

```bash
pnpm db:start
```

This will start a set of Docker containers that run all the Supabase services, including:

- **PostgreSQL Database**: A fully functional PostgreSQL database.
- **GoTrue (Authentication)**: The authentication server that handles user sign-ups, sign-ins, and JWT generation.
- **PostgREST (API)**: A RESTful API that is automatically generated from your database schema.
- **Realtime (Real-time Engine)**: A real-time engine that allows you to subscribe to database changes.
- **Storage**: A storage server for managing files.
- **Supabase Studio**: A web-based GUI for managing your local database and other Supabase services.

## 3. Accessing Local Services

Once the local Supabase stack is running, you can access the services at the following URLs:

- **Supabase Studio**: `http://localhost:54323`
- **API URL**: `http://localhost:54321`
- **Database URL**: `postgresql://postgres:your-db-password@localhost:54322/postgres`

## 4. Stopping the Local Supabase Stack

To stop the local Supabase stack, run the following command:

```bash
pnpm db:stop
```

This will stop all the Supabase Docker containers.
