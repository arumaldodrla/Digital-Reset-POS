# Database Schema Reference

## 1. Introduction for All Audiences

This document is the definitive technical blueprint for the Digital Reset POS database, which is built on PostgreSQL and managed by Supabase. It is designed to be a single source of truth for three key groups:

-   **For AI & Human Developers**: This is your primary reference for table structures, data types, constraints, and relationships. Use this to write accurate database queries, create migrations, and understand the data model.

-   **For Project Managers**: This document provides insight into how business requirements are translated into data structures. It helps you understand the system's capabilities and the implications of new feature requests on the data model.

-   **For Marketing Teams**: While technical, this document reveals the system's core logic. Understanding how we structure data for multi-tenancy, offline sync, and integrations can provide powerful insights for creating marketing messages about the platform's robustness and flexibility.

## 2. Schema Design Principles

Our database is designed around several core principles to ensure it is secure, scalable, and maintainable.

-   **Multi-Tenancy by Design**: Every table containing business-specific data has a `tenant_id` column. This is the foundation of our ability to serve multiple businesses from a single database while guaranteeing their data is completely isolated.

-   **Universally Unique IDs (UUIDs)**: We use `uuid` for all primary keys. This is critical for our offline-first architecture, as it allows new records (like an order or a customer) to be created on any offline device without the risk of ID conflicts when the data is later synced to the cloud.

-   **Clear Naming Conventions**: Tables are named as plural nouns (e.g., `orders`, `products`). Columns use `snake_case` (e.g., `created_at`). Foreign key columns are named `singular_table_name_id` (e.g., `tenant_id`, `order_id`).

-   **Data Integrity**: We use foreign key constraints, `NOT NULL` constraints, and default values to ensure the data remains consistent and reliable.

-   **Timestamps**: All tables include `created_at` and `updated_at` timestamps to provide a clear audit trail for when data is created and modified.

---

## 3. Table Definitions

### Core Business Structure

These tables form the backbone of the multi-tenant system.

#### `tenants`

Stores information about each distinct business using the system.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key | The unique identifier for the entire business. |
| `name` | `text` | Not Null | The legal or display name of the business. |

#### `locations`

Stores information about each physical store or branch belonging to a tenant.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key | The unique identifier for the physical location. |
| `tenant_id` | `uuid` | Foreign Key to `tenants.id` | Links this location to its parent business. |
| `name` | `text` | Not Null | The name of the store (e.g., "Main Street Cafe"). |

#### `registers`

Stores information about each POS terminal or device at a location.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key | The unique identifier for the POS device. |
| `location_id` | `uuid` | Foreign Key to `locations.id` | Links this register to its physical location. |
| `name` | `text` | Not Null | The name of the register (e.g., "Front Counter"). |

### Product Catalog

These tables define the products and services a business sells.

#### `products`

Stores the core information about a product, acting as a template for its variations.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key | Unique identifier for the product. |
| `tenant_id` | `uuid` | Foreign Key to `tenants.id` | Links this product to the business that owns it. |
| `name` | `text` | Not Null | The name of the product (e.g., "T-Shirt"). |
| `description` | `text` | | A detailed description for use in e-commerce or menus. |

#### `variants`

Stores the specific, sellable versions of a product.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key | Unique identifier for the specific variant. |
| `product_id` | `uuid` | Foreign Key to `products.id` | Links this variant to its parent product. |
| `name` | `text` | Not Null | The name of the variant (e.g., "Large, Blue"). |
| `price` | `numeric` | Not Null | The selling price of this specific variant. |
| `sku` | `text` | Unique per tenant | The Stock Keeping Unit for inventory tracking. |

### Sales & Transactions

These tables record the daily business of making sales.

#### `orders`

Stores the record of a single customer transaction.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key | The unique identifier for the transaction. |
| `register_id` | `uuid` | Foreign Key to `registers.id` | The register where the sale was made. |
| `total` | `numeric` | Not Null | The final total amount of the order, including taxes and discounts. |
| `status` | `text` | Not Null | The current state of the order (e.g., `completed`, `refunded`). |

#### `order_items`

Represents a single line item within an order.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key | Unique identifier for the line item. |
| `order_id` | `uuid` | Foreign Key to `orders.id` | Links this line item to its parent order. |
| `variant_id` | `uuid` | Foreign Key to `variants.id` | The specific product variant that was sold. |
| `quantity` | `integer` | Not Null | The number of units of this variant sold. |
| `price` | `numeric` | Not Null | The price of the variant **at the time of the sale**, to preserve historical accuracy. |

#### `payments`

Stores information about how an order was paid.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key | Unique identifier for the payment. |
| `order_id` | `uuid` | Foreign Key to `orders.id` | Links this payment to its parent order. |
| `amount` | `numeric` | Not Null | The amount of the payment. An order can have multiple payments. |
| `method` | `text` | Not Null | The payment method used (e.g., `cash`, `credit_card`). |

---

## 4. Security: Row-Level Security (RLS)

**What it is, in simple terms**: Imagine the database is a giant filing cabinet with drawers for each business (tenant). Row-Level Security is like giving each employee a key that only opens the drawer belonging to their company. An employee from "Company A" can never, under any circumstances, open the drawer for "Company B".

**How it works**: We enable RLS on every table that contains tenant-specific data. We then create a security policy that checks the `tenant_id` of the currently logged-in user against the `tenant_id` of the data they are trying to access. If they don't match, the database denies access. This is not an application-level check; it is enforced directly by the database, making it extremely secure.

**Example RLS Policy**:

This policy ensures a user can only see products that belong to their own company.

```sql
-- This policy is attached to the 'products' table.
CREATE POLICY "Users can only see products from their own tenant" 
ON public.products
FOR SELECT -- This policy applies when someone tries to READ data
USING (get_my_tenant_id() = tenant_id); -- The function get_my_tenant_id() securely gets the tenant_id of the logged-in user.
```

This RLS enforcement is the cornerstone of our multi-tenant security model, making it safe to store data from multiple businesses in the same database.
