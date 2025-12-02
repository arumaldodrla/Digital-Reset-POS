# Database Schema Reference

## 1. Introduction

This document provides a reference for the PostgreSQL database schema used in the Supabase backend. The schema is designed to be normalized and scalable, with a focus on multi-tenancy and data integrity.

## 2. Core Tables

### `tenants`

Stores information about each business or organization using the system.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key, Default: `gen_random_uuid()` | Unique identifier for the tenant. |
| `name` | `text` | Not Null | The name of the business. |
| `created_at` | `timestamptz` | Not Null, Default: `now()` | Timestamp of creation. |

### `locations`

Stores information about each physical store or restaurant.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key, Default: `gen_random_uuid()` | Unique identifier for the location. |
| `tenant_id` | `uuid` | Not Null, Foreign Key to `tenants.id` | The tenant this location belongs to. |
| `name` | `text` | Not Null | The name of the location. |
| `address` | `text` | | The physical address of the location. |
| `created_at` | `timestamptz` | Not Null, Default: `now()` | Timestamp of creation. |

### `registers`

Stores information about each POS terminal.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key, Default: `gen_random_uuid()` | Unique identifier for the register. |
| `location_id` | `uuid` | Not Null, Foreign Key to `locations.id` | The location this register belongs to. |
| `name` | `text` | Not Null | The name of the register. |
| `created_at` | `timestamptz` | Not Null, Default: `now()` | Timestamp of creation. |

### `users`

Mirrors the `auth.users` table from Supabase Auth and links users to tenants.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key, Foreign Key to `auth.users.id` | Unique identifier for the user. |
| `tenant_id` | `uuid` | Not Null, Foreign Key to `tenants.id` | The tenant this user belongs to. |
| `full_name` | `text` | | The user's full name. |

### `roles` and `user_roles`

Standard role-based access control (RBAC) tables.

**`roles`**

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key, Default: `gen_random_uuid()` | Unique identifier for the role. |
| `name` | `text` | Not Null, Unique | The name of the role (e.g., "Admin", "Cashier"). |

**`user_roles`**

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `user_id` | `uuid` | Primary Key, Foreign Key to `users.id` | The user. |
| `role_id` | `uuid` | Primary Key, Foreign Key to `roles.id` | The role assigned to the user. |

## 3. Product Catalog Tables

### `items`

Stores information about products and services.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key, Default: `gen_random_uuid()` | Unique identifier for the item. |
| `tenant_id` | `uuid` | Not Null, Foreign Key to `tenants.id` | The tenant this item belongs to. |
| `name` | `text` | Not Null | The name of the item. |
| `description` | `text` | | A description of the item. |
| `category` | `text` | | The category of the item. |

### `variants`

Stores information about specific versions of items.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key, Default: `gen_random_uuid()` | Unique identifier for the variant. |
| `item_id` | `uuid` | Not Null, Foreign Key to `items.id` | The item this variant belongs to. |
| `name` | `text` | Not Null | The name of the variant (e.g., "Large", "Red"). |
| `price` | `numeric` | Not Null, Default: 0 | The price of the variant. |
| `sku` | `text` | | The stock keeping unit (SKU) of the variant. |

## 4. Transactional Tables

### `orders`

Stores information about each transaction.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key, Default: `gen_random_uuid()` | Unique identifier for the order. |
| `register_id` | `uuid` | Not Null, Foreign Key to `registers.id` | The register where the order was created. |
| `total` | `numeric` | Not Null, Default: 0 | The total amount of the order. |
| `status` | `text` | Not Null, Default: `'pending'` | The status of the order. |
| `created_at` | `timestamptz` | Not Null, Default: `now()` | Timestamp of creation. |

### `order_items`

Associates variants with orders.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key, Default: `gen_random_uuid()` | Unique identifier for the order item. |
| `order_id` | `uuid` | Not Null, Foreign Key to `orders.id` | The order this item belongs to. |
| `variant_id` | `uuid` | Not Null, Foreign Key to `variants.id` | The variant being ordered. |
| `quantity` | `integer` | Not Null, Default: 1 | The quantity of the variant. |
| `price` | `numeric` | Not Null | The price of the variant at the time of the order. |

### `payments`

Stores information about payments for orders.

| Column | Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `uuid` | Primary Key, Default: `gen_random_uuid()` | Unique identifier for the payment. |
| `order_id` | `uuid` | Not Null, Foreign Key to `orders.id` | The order this payment is for. |
| `amount` | `numeric` | Not Null | The amount of the payment. |
| `method` | `text` | Not Null | The payment method (e.g., "cash", "credit_card"). |
| `created_at` | `timestamptz` | Not Null, Default: `now()` | Timestamp of creation. |

## 5. Multi-Tenancy and RLS

- **Tenant Isolation**: All tables that contain tenant-specific data have a `tenant_id` column. This is the primary mechanism for isolating data between tenants.
- **Row-Level Security (RLS)**: Supabase's RLS is enabled on all tenant-specific tables. RLS policies ensure that users can only access data that belongs to their own tenant. A typical RLS policy would look like this:

```sql
CREATE POLICY "Enable access for users based on tenant_id" ON public.items
FOR ALL
USING (auth.uid() IN (SELECT user_id FROM user_roles WHERE tenant_id = public.items.tenant_id));
```

This policy ensures that a user can only access items that belong to the same tenant they are a member of.
