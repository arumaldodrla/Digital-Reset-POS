# Domain Model and ERD

## 1. Core Entities

The Universal Offline POS system is built around a set of core entities that represent the main concepts of the application. The following sections describe these entities and their relationships.

### 1.1. Tenants

A **Tenant** represents a single business or organization using the POS system. Each tenant has its own isolated data, including locations, users, products, and orders.

| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary key. |
| `name` | `text` | The name of the business. |
| `created_at` | `timestamp` | The timestamp when the tenant was created. |

### 1.2. Locations

A **Location** represents a physical store or restaurant belonging to a tenant. Each tenant can have multiple locations.

| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary key. |
| `tenant_id` | `uuid` | Foreign key to the `tenants` table. |
| `name` | `text` | The name of the location (e.g., "Main Street Store"). |
| `address` | `text` | The physical address of the location. |
| `created_at` | `timestamp` | The timestamp when the location was created. |

### 1.3. Registers

A **Register** represents a single point of sale terminal at a location. Each location can have multiple registers.

| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary key. |
| `location_id` | `uuid` | Foreign key to the `locations` table. |
| `name` | `text` | The name of the register (e.g., "Front Counter"). |
| `created_at` | `timestamp` | The timestamp when the register was created. |

### 1.4. Users

A **User** represents an individual who can log in to the POS system. Each user is associated with a tenant and has one or more roles.

| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary key (from Supabase Auth). |
| `tenant_id` | `uuid` | Foreign key to the `tenants` table. |
| `email` | `text` | The user's email address. |
| `full_name` | `text` | The user's full name. |
| `created_at` | `timestamp` | The timestamp when the user was created. |

### 1.5. Roles

A **Role** defines a set of permissions for a user. Each user can have multiple roles.

| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary key. |
| `name` | `text` | The name of the role (e.g., "Admin", "Cashier"). |

### 1.6. User Roles

A **User Role** is a join table that associates users with roles.

| Column | Type | Description |
| :--- | :--- | :--- |
| `user_id` | `uuid` | Foreign key to the `users` table. |
| `role_id` | `uuid` | Foreign key to the `roles` table. |

## 2. Product Catalog Entities

### 2.1. Items

An **Item** represents a product or service that can be sold.

| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary key. |
| `tenant_id` | `uuid` | Foreign key to the `tenants` table. |
| `name` | `text` | The name of the item. |
| `description` | `text` | A description of the item. |
| `category` | `text` | The category of the item (e.g., "Drinks", "Appetizers"). |

### 2.2. Variants

A **Variant** represents a specific version of an item, such as a different size or color.

| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary key. |
| `item_id` | `uuid` | Foreign key to the `items` table. |
| `name` | `text` | The name of the variant (e.g., "Large", "Red"). |
| `price` | `numeric` | The price of the variant. |
| `sku` | `text` | The stock keeping unit (SKU) of the variant. |

### 2.3. Menus

A **Menu** is a collection of items that are available for sale at a specific location.

| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary key. |
| `location_id` | `uuid` | Foreign key to the `locations` table. |
| `name` | `text` | The name of the menu (e.g., "Lunch Menu"). |

### 2.4. Menu Items

A **Menu Item** is a join table that associates items with menus.

| Column | Type | Description |
| :--- | :--- | :--- |
| `menu_id` | `uuid` | Foreign key to the `menus` table. |
| `item_id` | `uuid` | Foreign key to the `items` table. |

### 2.5. Modifiers

A **Modifier** is an option that can be added to an item, such as "extra cheese" or "no onions".

| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary key. |
| `tenant_id` | `uuid` | Foreign key to the `tenants` table. |
| `name` | `text` | The name of the modifier. |
| `price` | `numeric` | The additional price of the modifier. |

## 3. Transactional Entities

### 3.1. Orders

An **Order** represents a single transaction, which can contain multiple items.

| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary key. |
| `register_id` | `uuid` | Foreign key to the `registers` table. |
| `total` | `numeric` | The total amount of the order. |
| `status` | `text` | The status of the order (e.g., "pending", "completed", "refunded"). |
| `created_at` | `timestamp` | The timestamp when the order was created. |

### 3.2. Order Items

An **Order Item** is a join table that associates variants with orders.

| Column | Type | Description |
| :--- | :--- | :--- |
| `order_id` | `uuid` | Foreign key to the `orders` table. |
| `variant_id` | `uuid` | Foreign key to the `variants` table. |
| `quantity` | `integer` | The quantity of the variant in the order. |
| `price` | `numeric` | The price of the variant at the time of the order. |

### 3.3. Payments

A **Payment** represents a payment made for an order.

| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary key. |
| `order_id` | `uuid` | Foreign key to the `orders` table. |
| `amount` | `numeric` | The amount of the payment. |
| `method` | `text` | The payment method (e.g., "cash", "credit_card"). |
| `created_at` | `timestamp` | The timestamp when the payment was made. |

### 3.4. Invoices

An **Invoice** represents an electronic invoice generated for an order.

| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary key. |
| `order_id` | `uuid` | Foreign key to the `orders` table. |
| `fiscal_number` | `text` | The official fiscal number of the invoice. |
| `qr_code_url` | `text` | A URL to the QR code for the invoice. |
| `created_at` | `timestamp` | The timestamp when the invoice was created. |

### 3.5. Loyalty Events

A **Loyalty Event** represents a loyalty-related action, such as earning points or redeeming a reward.

| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary key. |
| `customer_id` | `uuid` | Foreign key to the `customers` table. |
| `type` | `text` | The type of loyalty event (e.g., "earn_points", "redeem_reward"). |
| `points` | `integer` | The number of points earned or redeemed. |
| `created_at` | `timestamp` | The timestamp when the event occurred. |

### 3.6. Stock Movements

A **Stock Movement** represents a change in the stock level of a variant.

| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary key. |
| `variant_id` | `uuid` | Foreign key to the `variants` table. |
| `quantity` | `integer` | The change in quantity (positive for additions, negative for subtractions). |
| `reason` | `text` | The reason for the stock movement (e.g., "sale", "return", "adjustment"). |
| `created_at` | `timestamp` | The timestamp when the stock movement occurred. |

## 4. Entity-Relationship Diagram (Textual Description)

- A **Tenant** has many **Locations**.
- A **Location** has many **Registers** and many **Menus**.
- A **Tenant** has many **Users**, **Items**, and **Modifiers**.
- A **User** can have many **Roles** (many-to-many relationship through the `user_roles` table).
- An **Item** has many **Variants**.
- A **Menu** can have many **Items** (many-to-many relationship through the `menu_items` table).
- An **Order** belongs to a **Register** and has many **Order Items**.
- An **Order** can have many **Payments** and one **Invoice**.
- A **Customer** can have many **Loyalty Events**.
- A **Variant** can have many **Stock Movements**.
