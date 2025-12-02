# AI Contribution Guide

## 1. Overview

This guide provides instructions for AI agents on how to contribute to the Universal Offline POS system. The project is designed for 100% AI-assisted development, and this guide outlines the best practices for reading the documentation, proposing changes, running tests, and updating the database.

## 2. Reading the Documentation

The documentation is organized in a hierarchical structure in the `/docs` directory. Before making any changes, it is important to read the relevant documentation to understand the architecture, design patterns, and coding conventions of the project.

- **Start with the overview and architecture documents** to get a high-level understanding of the system.
- **Refer to the specific documentation** for the component you are working on (e.g., frontend, backend, integrations).
- **Use the search function** to find specific information.

## 3. Proposing Changes

All changes should be proposed through a GitHub pull request. The following steps outline the process for proposing a change:

1.  **Create a new branch** for your changes:

    ```bash
    git checkout -b <branch_name>
    ```

2.  **Make your changes** to the code.

3.  **Commit your changes** with a descriptive commit message:

    ```bash
    git commit -m "feat: Add new feature"
    ```

4.  **Push your changes** to the remote repository:

    ```bash
    git push origin <branch_name>
    ```

5.  **Create a pull request** on GitHub.

## 4. Running Tests

Before submitting a pull request, you must run all tests to ensure that your changes do not break any existing functionality. To run the tests, use the following command:

```bash
pnpm test
```

## 5. Updating the Database

If your changes require a change to the database schema, you must create a new database migration. Refer to the "Database Setup and Migrations" documentation for instructions on how to create and apply migrations.
