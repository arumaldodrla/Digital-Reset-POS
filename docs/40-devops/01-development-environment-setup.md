# Development Environment Setup

## 1. Prerequisites

Before you begin, ensure you have the following installed on your local machine:

- **Node.js**: Version 18.x or later.
- **pnpm**: A fast and disk-space-efficient package manager for Node.js.
- **Docker**: A platform for developing, shipping, and running applications in containers.
- **Supabase CLI**: A command-line interface for managing your local Supabase environment.

## 2. Local Setup

1.  **Clone the repository**:

    ```bash
    git clone https://github.com/arumaldodrla/Digital-Reset-POS.git
    cd Digital-Reset-POS
    ```

2.  **Install Node.js dependencies**:

    ```bash
    pnpm install
    ```

3.  **Configure environment variables**:

    Create a `.env.local` file in the root of the project and add the following environment variables:

    ```
    NEXT_PUBLIC_SUPABASE_URL=http://localhost:54321
    NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
    SUPABASE_DB_PASSWORD=your-db-password
    ```

    You can find the values for these variables in the output of the `supabase start` command (see the "Local Supabase Setup" section).

4.  **Start the development servers**:

    This will start the Next.js frontend development server.

    ```bash
    pnpm dev
    ```

5.  **Seed sample data**:

    To populate your local database with sample data, run the following command:

    ```bash
    pnpm db:seed
    ```

## 3. AI-Assisted Development

This project is designed for 100% AI-assisted development using [Cursor](https://cursor.sh/). To get started:

1.  Open the project in Cursor.
2.  Use the built-in AI chat to ask questions, generate code, and refactor your application.
3.  Refer to the AI-Ops and prompt library documentation for more information on how to effectively use AI for development.
