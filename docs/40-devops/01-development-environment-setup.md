# DevOps: Development Environment Setup

## 1. Philosophy: Fast, Consistent, and AI-Ready

Our development environment is designed with three goals in mind:

1.  **Fast Onboarding**: A new developer (human or AI) should be able to get the project running locally in under 15 minutes.
2.  **Consistency**: The local environment should mirror the production environment as closely as possible to prevent "it works on my machine" errors.
3.  **AI-Ready**: The setup should be simple and scriptable, allowing an AI agent to easily clone, configure, and run the project.

## 2. The Two Paths to Local Development

A developer can choose one of two paths to run the project, depending on their needs.

### Path A: The "Quick Start" Cloud Path

This is the fastest way to get started. It uses the local frontend code but connects to a **free, cloud-hosted Supabase project** for the backend database and services.

-   **Pros**: Very fast setup, no Docker required, good for frontend UI development.
-   **Cons**: Requires a constant internet connection, not suitable for developing backend functions that need to interact with a local network.

### Path B: The "Full Offline" Local Path

This path runs the **entire system locally**, including a full Supabase stack inside Docker containers. This is the recommended path for full-stack development.

-   **Pros**: Works 100% offline, perfectly mirrors the production architecture, allows for full-stack development including database migrations and serverless functions.
-   **Cons**: Requires Docker, initial setup takes a few minutes longer to download Docker images.

---

## 3. Prerequisites: The Tools of the Trade

Before you begin, ensure you have these tools installed. They are the standard for modern web development.

| Tool | What It Is | Installation |
| :--- | :--- | :--- |
| **Node.js** | The JavaScript runtime environment. | `v18.x` or later. [Download](https://nodejs.org/) |
| **pnpm** | A fast and efficient package manager. | `npm install -g pnpm` |
| **Docker** | A containerization platform. | **Required for Path B only**. [Download](https://www.docker.com/products/docker-desktop/) |
| **Supabase CLI** | A command-line tool for local Supabase. | `pnpm install -g supabase` |

## 4. Step-by-Step Setup Instructions

### Step 1: Clone the Repository

This downloads the project code to your local machine.

```bash
git clone https://github.com/arumaldodrla/Digital-Reset-POS.git
cd Digital-Reset-POS
```

### Step 2: Install Dependencies

This downloads all the necessary Node.js packages for the frontend application.

```bash
pnpm install
```

### Step 3: Configure Your Environment (Choose Path A or B)

#### For Path A (Cloud Backend):

1.  Go to [supabase.com](https://supabase.com), create a free account, and create a new project.
2.  In your Supabase project dashboard, go to `Settings` > `API`.
3.  Create a file named `.env.local` in the root of the project.
4.  Copy the `URL` and `anon (public)` key from your Supabase dashboard into the `.env.local` file:

    ```env
    NEXT_PUBLIC_SUPABASE_URL=YOUR_SUPABASE_URL
    NEXT_PUBLIC_SUPABASE_ANON_KEY=YOUR_SUPABASE_ANON_KEY
    ```

#### For Path B (Local Backend):

1.  Start the local Supabase stack using Docker.

    ```bash
    supabase start
    ```

2.  At the end of the output, the CLI will display your local API URL and keys. Copy these into a new `.env.local` file:

    ```env
    # Example values - use the ones from your CLI output
    NEXT_PUBLIC_SUPABASE_URL=http://127.0.0.1:54321
    NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
    ```

### Step 4: Apply Database Migrations (Path B Only)

If you are running Supabase locally, you need to create the database tables by applying the existing migrations.

```bash
supabase db reset
```

### Step 5: Start the Development Server

This command starts the Next.js frontend application.

```bash
pnpm dev
```

Your Digital Reset POS application is now running and accessible at **http://localhost:3000**.
