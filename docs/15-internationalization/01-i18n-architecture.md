# Internationalization (i18n) Architecture

## 1. Philosophy: Global by Design, AI-Powered

Internationalization (i18n) is not an afterthought; it is a core architectural pillar of the Digital Reset POS system. Our goal is to create a platform that can be rapidly and accurately adapted for any language and culture, enabling global scalability from day one.

Our approach is guided by two principles:

1.  **Centralized Translations**: All user-facing strings are externalized from the code and managed in a central location.
2.  **AI-Driven Workflow**: The process of translating, reviewing, and deploying new languages is heavily automated and managed by AI agents.

## 2. The Technology Stack: `next-intl`

We will use the `next-intl` library, a best-in-class solution for internationalization in Next.js applications. It was chosen for several key reasons:

-   **Rich Formatting**: Supports complex pluralization rules, number formatting, and date/time formatting for different locales.
-   **Type Safety**: Provides TypeScript support to ensure that all translation keys are valid at compile time, preventing missing translations in production.
-   **App Router Support**: Fully compatible with the modern Next.js App Router.
-   **Simple & Scalable**: The structure of storing translations in simple JSON files is easy for both humans and AI agents to understand and manage.

## 3. The Translation File Structure

All translation strings will be stored in JSON files within the `/messages` directory.

```
/messages
├── en.json
├── es.json
└── fr.json (future)
```

Each file corresponds to a specific language locale. The structure of the JSON files is hierarchical, grouping related translations together.

**Example `en.json`:**

```json
{
  "pos": {
    "checkout": {
      "title": "Checkout",
      "pay_button": "Pay Now",
      "total_label": "Total"
    }
  },
  "admin": {
    "products": {
      "title": "Products",
      "add_new_button": "Add New Product"
    }
  }
}
```

**Example `es.json`:**

```json
{
  "pos": {
    "checkout": {
      "title": "Caja",
      "pay_button": "Pagar Ahora",
      "total_label": "Total"
    }
  },
  "admin": {
    "products": {
      "title": "Productos",
      "add_new_button": "Agregar Nuevo Producto"
    }
  }
}
```

## 4. The AI-Powered Translation Workflow

Adding a new language is a semi-automated process designed to be executed by an AI agent with human oversight.

1.  **AI Task: Create New Locale File**: An AI agent is tasked with creating a new JSON file for the target language (e.g., `fr.json`).

2.  **AI Task: Machine Translation**: The AI agent reads the `en.json` file, and for each key, it generates a translation using a large language model (LLM) with a high degree of fluency in the target language. It populates the new locale file with these translations.

    *Prompt Example*: `"Translate the following JSON value into French, preserving any variables: 

    {\"pay_button\": \"Pay Now\"}"`

3.  **Human Review (Optional but Recommended)**: For critical UI elements, the generated translations can be flagged for review by a native speaker to ensure cultural accuracy and context.

4.  **AI Task: Integrate New Locale**: The AI agent updates the `next-intl` configuration to include the new language, making it available in the application.

5.  **Automated Testing**: The CI/CD pipeline runs tests to ensure that the new translation file is valid JSON and that all keys match the source `en.json` file.

6.  **Deployment**: The new language is deployed to production.

This workflow reduces the time to add a new language from weeks to hours, making global expansion rapid and cost-effective.

## 5. Implementation in the Frontend

In the React components, we will use the `useTranslations` hook from `next-intl` to access the translated strings.

**Example Component:**

```tsx
// components/organisms/CheckoutPanel.tsx

import { useTranslations } from "next-intl";

export default function CheckoutPanel() {
  const t = useTranslations("pos.checkout");

  return (
    <div>
      <h1>{t("title")}</h1>
      <label>{t("total_label")}</label>
      <button>{t("pay_button")}</button>
    </div>
  );
}
```

This approach ensures that the code is completely decoupled from the translation strings. To display the component in a different language, we simply need to provide the appropriate translation file; no code changes are required.
