# AI-Ops: AI Prompt Library

## 1. Introduction

This library provides a set of curated, high-quality prompt templates for use with large language models (LLMs) like those in Cursor. Using these standardized prompts ensures that the generated code is consistent, follows our architectural patterns, and requires minimal refactoring.

**Core Principle**: Provide the AI with as much context as possible. Refer to specific file paths and existing patterns. Do not assume the AI knows the project structure.

---

## 2. Frontend Development Prompts

### Creating UI Components

```
# Create a new React component for the POS checkout screen

**File**: `components/organisms/CheckoutPanel.tsx`

**Task**: Create a new React component named `CheckoutPanel`. This component will display the order summary, including subtotal, tax, and total. It should also include buttons for different payment methods (Cash, Credit Card, Yappy).

**Requirements**:
- Use `shadcn/ui` components for all visual elements (`Card`, `Button`, etc.).
- Use Tailwind CSS for styling.
- The component should accept an `order` object as a prop.
- The payment buttons should be disabled if the order total is zero.
- Follow the structure of the existing `ProductGrid.tsx` component.
```

### Creating RxDB Schemas

```
# Create a new RxDB schema for customer data

**File**: `lib/db/schemas/customer.ts`

**Task**: Create a new RxDB schema for the `customers` collection.

**Context**: The schema should be based on the `customers` table defined in the main database schema reference document at `/docs/20-backend/03-database-schema-reference.md`.

**Requirements**:
- The schema should include `id`, `tenant_id`, `full_name`, `email`, and `phone` fields.
- `id` should be the primary key.
- `tenant_id` and `email` should be indexed for faster queries.
- All fields should be of type `string` except for any timestamps.
```

---

## 3. Backend Development Prompts

### Creating Supabase Functions

```
# Create a new Supabase Function to handle Zoho inventory updates

**File**: `supabase/functions/zoho-inventory-update/index.ts`

**Task**: Create a new Supabase Function that is triggered by a webhook whenever a new sale is recorded. The function should update the stock levels in Zoho Inventory.

**Context**: The design for this integration is detailed in `/docs/25-integrations/01-zoho-inventory-connector.md`.

**Requirements**:
- The function must securely retrieve the Zoho API key from environment variables.
- It should parse the incoming webhook payload to get the product SKU and quantity sold.
- It must make a POST request to the Zoho Inventory API to decrease the stock level.
- Implement robust error handling and logging.
```

### Creating Database Migrations

```
# Create a new database migration to add a `notes` field to the `orders` table

**Task**: Generate a new SQL migration file using the Supabase CLI.

**Requirements**:
- The migration should add a new column named `notes` to the `public.orders` table.
- The column should be of type `text` and should be nullable.
- Name the migration file `add_notes_to_orders`.

**Command to use**:
`supabase migration new add_notes_to_orders`

Then, populate the generated SQL file with the following DDL statement:

```sql
ALTER TABLE public.orders
ADD COLUMN notes TEXT;
```

```

### Creating RLS Policies

```
# Create a new RLS policy for the `customers` table

**Task**: Write the SQL for a new Row-Level Security (RLS) policy on the `customers` table.

**Context**: The policy must enforce our standard multi-tenancy rule, as described in the database schema reference.

**Requirements**:
- The policy should be named `"Users can only access customers from their own tenant"`.
- It should apply to `ALL` operations (SELECT, INSERT, UPDATE, DELETE).
- The policy should check that the `tenant_id` of the logged-in user matches the `tenant_id` of the customer record.
- Use the helper function `auth.uid()` to get the current user and a sub-select on the `profiles` table to get their `tenant_id`.
```

---

## 4. General & Refactoring Prompts

### Refactoring Code

```
# Refactor the `calculateTotal` function for clarity

**File**: `lib/utils/calculations.ts`

**Task**: The `calculateTotal` function is becoming difficult to read. Refactor it to improve clarity and maintainability.

**Requirements**:
- Break the function down into smaller, single-purpose helper functions (e.g., `calculateSubtotal`, `calculateTaxes`, `applyDiscounts`).
- Add JSDoc comments to each function explaining what it does, its parameters, and what it returns.
- Ensure all existing unit tests for this function continue to pass.
```

### Writing Tests

```
# Write unit tests for the new `CheckoutPanel` component

**File**: `components/organisms/CheckoutPanel.test.tsx`

**Task**: Write a comprehensive suite of unit tests for the `CheckoutPanel` component using Vitest and React Testing Library.

**Requirements**:
- Test that the component renders correctly with a given order.
- Test that the subtotal, tax, and total are displayed correctly.
- Test that the payment buttons are disabled when the order total is zero.
- Test that clicking a payment button calls the appropriate handler function.
- Mock any external dependencies or props as needed.
```
