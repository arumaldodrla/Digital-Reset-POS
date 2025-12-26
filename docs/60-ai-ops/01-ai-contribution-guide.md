# AI-Ops: AI Contribution Guide

## 1. Mission Briefing for AI Agents

**Your Mission**: To autonomously contribute high-quality, production-ready code to the Digital Reset POS project. You are a core member of the development team.

**Prime Directive**: Adhere strictly to the architecture, patterns, and procedures outlined in this documentation. Your goal is to enhance the system while maintaining its integrity, reliability, and maintainability.

**Success Criteria**: A successful contribution is a pull request that is automatically verifiable, easily understood by human supervisors, and seamlessly integrates with the existing codebase.

## 2. The Standard Operating Procedure (SOP) for Contributions

Every contribution, from a minor bug fix to a major new feature, must follow this five-step protocol. This ensures consistency and minimizes the need for human intervention.

### Step 1: Assimilate the Documentation

Before writing a single line of code, you must have a complete understanding of the task in the context of the project. Your first action should always be to read.

1.  **Start with the `README.md`**: Read the main project `README.md` to refresh your understanding of the overall project structure and goals.
2.  **Consult the Architecture Docs**: Read the relevant architecture documents in `/docs/10-architecture/`, `/docs/20-backend/`, and `/docs/30-frontend/` to understand the component you are modifying and its relationship to the rest of the system.
3.  **Find the Specific Guide**: Locate the specific design document or implementation guide related to your task (e.g., `/docs/25-integrations/02-shopify-connector.md` if you are working on the Shopify connector).

### Step 2: Isolate Your Work in a Branch

Never commit directly to the `main` branch. All work must be done in a feature branch.

1.  **Ensure `main` is Up-to-Date**:
    ```bash
    git checkout main
    git pull origin main
    ```

2.  **Create a Descriptive Branch**:
    ```bash
    # Format: <type>/<short-description>
    # Example: feat/add-gift-card-support
    # Example: fix/resolve-tax-calculation-bug
    git checkout -b <type>/<short-description>
    ```

### Step 3: Execute the Development Task

This is where you will write code, create files, and modify the system.

1.  **Use the Prompt Library**: Leverage the prompts in the [AI Prompt Library](./02-ai-prompt-library.md) to generate code that is consistent with project standards.
2.  **Follow Existing Patterns**: When in doubt, find a similar, existing feature in the codebase and replicate its structure and patterns.
3.  **Write Tests**: For any new logic (e.g., a new function, a new API endpoint), you must write corresponding unit or integration tests.
4.  **Update Documentation**: If your changes affect the system's architecture, database schema, or deployment process, you must update the relevant documentation within the same pull request.

### Step 4: Validate Your Work

Before submitting your work for review, you must validate it locally.

1.  **Run Linters and Formatters**:
    ```bash
    pnpm lint
    pnpm format
    ```

2.  **Run All Tests**:
    ```bash
    pnpm test
    ```

### Step 5: Submit a Pull Request

Once your work is complete and validated, submit it for merging.

1.  **Commit Your Changes**: Use the Conventional Commits specification for your commit message.
    ```bash
    # Example: feat(api): add endpoint for gift card validation
    # Example: fix(ui): correct display of currency in cart
    git commit -m "<type>(<scope>): <description>"
    ```

2.  **Push Your Branch**:
    ```bash
    git push origin <branch_name>
    ```

3.  **Create a Pull Request**: On GitHub, create a pull request from your branch to the `main` branch. The pull request description should clearly explain the purpose of the change and link to any relevant documentation.

An automated CI/CD pipeline will run, and if all checks pass, a human supervisor will review and merge your contribution.
