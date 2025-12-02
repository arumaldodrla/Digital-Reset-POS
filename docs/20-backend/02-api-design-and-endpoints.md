# API Design and Endpoints

## 1. Guiding Principles

The API for the Universal Offline POS system is designed with the following principles in mind:

- **RESTful**: The API follows RESTful conventions, using standard HTTP methods (GET, POST, PUT, DELETE) and status codes.
- **Stateless**: The API is stateless, meaning that each request contains all the information needed to process it. The server does not store any client-side context.
- **Idempotent**: All `PUT` and `DELETE` requests are idempotent, meaning that multiple identical requests will have the same effect as a single request.
- **Paginated**: All list endpoints are paginated to ensure predictable performance and prevent excessive data transfer.
- **Versioned**: The API is versioned to allow for future changes without breaking existing clients. The version is included in the URL (e.g., `/api/v1/...`).
- **Secure**: All endpoints are protected by Supabase's authentication and row-level security (RLS).

## 2. Authentication

Authentication is handled by Supabase Auth. The frontend is responsible for authenticating the user and obtaining a JSON Web Token (JWT). This JWT must be included in the `Authorization` header of all API requests:

```
Authorization: Bearer <your_jwt>
```

## 3. Main Resources and Endpoints

The following sections describe the main resources and endpoints of the API. These endpoints are primarily used for integrations and administrative tasks, as the core POS functionality is handled by the offline-first RxDB database.

### 3.1. Tenants

- `GET /api/v1/tenants`: Get the current tenant's information.
- `PUT /api/v1/tenants`: Update the current tenant's information.

### 3.2. Locations

- `GET /api/v1/locations`: Get a list of all locations for the current tenant.
- `POST /api/v1/locations`: Create a new location.
- `GET /api/v1/locations/{id}`: Get a specific location.
- `PUT /api/v1/locations/{id}`: Update a specific location.
- `DELETE /api/v1/locations/{id}`: Delete a specific location.

### 3.3. Registers

- `GET /api/v1/registers`: Get a list of all registers for a specific location.
- `POST /api/v1/registers`: Create a new register.
- `GET /api/v1/registers/{id}`: Get a specific register.
- `PUT /api/v1/registers/{id}`: Update a specific register.
- `DELETE /api/v1/registers/{id}`: Delete a specific register.

### 3.4. Sync Endpoints

These endpoints are used by the RxDB replication protocol to synchronize data between the local database and the Supabase backend.

- `POST /api/v1/sync/pull`: Pull changes from the server.
- `POST /api/v1/sync/push`: Push changes to the server.

### 3.5. Integrations

These endpoints are used to configure and manage integrations with third-party services.

- `GET /api/v1/integrations`: Get a list of all configured integrations.
- `POST /api/v1/integrations/{provider}`: Configure a new integration (e.g., `zoho_inventory`, `shopify`).
- `GET /api/v1/integrations/{provider}`: Get the configuration for a specific integration.
- `PUT /api/v1/integrations/{provider}`: Update the configuration for a specific integration.
- `DELETE /api/v1/integrations/{provider}`: Delete the configuration for a specific integration.

### 3.6. Webhooks

These endpoints are used to handle webhooks from third-party services.

- `POST /api/v1/webhooks/{provider}`: Handle a webhook from a specific provider (e.g., `yappy`, `shopify`).
