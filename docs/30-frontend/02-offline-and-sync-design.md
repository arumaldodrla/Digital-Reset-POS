# Offline and Sync Design

## 1. Offline-First Architecture

The Universal Offline POS system is built with an offline-first architecture, meaning that the application is fully functional without an internet connection. This is achieved through the use of a local database (RxDB) and a service worker that caches all application assets.

### 1.1. Local Database (RxDB)

RxDB is a reactive, offline-first database for JavaScript applications. It is used as the primary data store for the application, and all data is stored locally in the browser's IndexedDB. This allows the application to read and write data even when there is no internet connection.

### 1.2. Service Worker

A service worker is a script that runs in the background, separate from the web page. It is used to cache all application assets, including HTML, CSS, JavaScript, and images. This allows the application to load and run even when the user is offline.

## 2. Data Synchronization

Data is synchronized between the local RxDB database and the Supabase backend using the RxDB replication protocol. The replication is bidirectional, meaning that changes can be pushed from the client to the server and pulled from the server to the client.

### 2.1. Replication Process

1.  **Push**: When a change is made on the client (e.g., a new order is created), it is first written to the local RxDB database. The replication engine then pushes the change to the Supabase backend.
2.  **Pull**: The replication engine periodically polls the Supabase backend for changes. If there are any new changes, they are pulled down to the client and written to the local RxDB database.

### 2.2. Conflict Resolution

Data conflicts can occur when the same data is modified on multiple devices while they are offline. For example, if two cashiers at the same location sell the last item in stock, a conflict will occur when they both come back online.

RxDB provides a built-in conflict resolution mechanism that can be customized to fit the business logic. The default strategy is "last-write-wins", which means that the most recent change will be saved. However, custom conflict handlers can be written to implement more complex logic, such as merging changes or prompting the user to resolve the conflict manually.

## 3. Implementation Details

### 3.1. RxDB Schema

The RxDB schema is defined in a set of JSON files that describe the collections (tables) and their properties. The schema is used to create the RxDB database and to validate data before it is written to the database.

### 3.2. Replication Endpoint

A custom API endpoint is created on the Supabase backend to handle the RxDB replication. This endpoint is responsible for receiving changes from the client, writing them to the Supabase database, and returning any new changes to the client.

### 3.3. PWA Configuration

The `next-pwa` plugin is used to configure the Next.js application as a Progressive Web App. This includes generating a service worker, creating a web app manifest, and caching all application assets.
