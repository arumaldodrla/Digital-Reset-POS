# AI Prompt Library

## 1. Overview

This document provides a library of reusable prompt templates for common development tasks. These prompts are designed to be used with AI assistants like Cursor to accelerate development and ensure consistency.

## 2. General Prompts

### Create a new component

```
Create a new React component called `<ComponentName>` that displays `<description>`. The component should be created in the file `components/organisms/<ComponentName>.tsx`. Use shadcn/ui components and Tailwind CSS for styling.
```

### Create a new API endpoint

```
Create a new API endpoint at `/api/v1/<resource>` that `<description>`. The endpoint should be created in a new Supabase Function called `<function-name>`. Follow the existing patterns for authentication and error handling.
```

### Create a new database migration

```
Create a new database migration to `<description>`. The migration should be created using the Supabase CLI and should be named `<migration_name>`.
```

## 3. Frontend Prompts

### Create a new page

```
Create a new page at `/<page-url>` that displays `<description>`. The page should be created in the file `app/<page-url>/page.tsx`. Use the existing layout and UI components.
```

### Create a new RxDB schema

```
Create a new RxDB schema for the `<collection_name>` collection. The schema should have the following properties:

- `<property_name>`: `<property_type>`
- `<property_name>`: `<property_type>`

The schema should be created in the file `lib/db/schemas/<collection_name>.ts`.
```

## 4. Backend Prompts

### Create a new Supabase Function

```
Create a new Supabase Function called `<function-name>` that `<description>`. The function should be created in the file `supabase/functions/<function-name>/index.ts`.
```

### Create a new RLS policy

```
Create a new RLS policy on the `<table>` table that `<description>`. The policy should be named `<policy_name>`.
```
