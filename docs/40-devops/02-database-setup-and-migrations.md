# Database Setup and Migrations

## 1. Local Database Setup

The local database is managed by the Supabase CLI. To start the local Supabase stack, which includes a PostgreSQL database, run the following command:

```bash
pnpm db:start
```

This will start a Docker container with a PostgreSQL database and all the other Supabase services. The first time you run this command, it will download the necessary Docker images, which may take a few minutes.

## 2. Database Migrations

Database migrations are managed by the Supabase CLI. Migrations are stored in the `supabase/migrations` directory.

### 2.1. Creating a New Migration

To create a new migration, first make your changes to the local database using a GUI tool like the Supabase Studio (available at `http://localhost:54323` when the local Supabase stack is running) or by running SQL commands directly. Once you have made your changes, run the following command to create a new migration file:

```bash
pnpm db:new-migration <migration_name>
```

Replace `<migration_name>` with a descriptive name for your migration (e.g., `create_orders_table`).

### 2.2. Applying Migrations

To apply all pending migrations to your local database, run the following command:

```bash
pnpm db:up
```

### 2.3. Resetting the Database

To reset your local database and apply all migrations from scratch, run the following command:

```bash
pnpm db:reset
```

This is useful when you want to start with a clean database or if you have made changes to existing migration files.
