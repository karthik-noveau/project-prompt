**ESLint + Vite + React + Aliases setup 👇**

### ✅ **`vite.config.js`**

```js
import react from "@vitejs/plugin-react";
import path from "node:path";
import { fileURLToPath } from "node:url";
import { defineConfig } from "vite";

const pathURL = path.dirname(fileURLToPath(import.meta.url));

// https://vite.dev/config/
export default defineConfig({
  plugins: [react()],
  optimizeDeps: {
    exclude: ["@imgly/background-removal"],
  },
  server: {
    headers: {
      "Cross-Origin-Opener-Policy": "same-origin",
      "Cross-Origin-Embedder-Policy": "require-corp",
    },
  },
  resolve: {
    alias: {
      "@assets": path.resolve(pathURL, "./src/assets"),
      "@common": path.resolve(pathURL, "./src/common"),
      "@pages": path.resolve(pathURL, "./src/pages"),
      "@theme": path.resolve(pathURL, "./src/theme"),
    },
  },
});
```

---

### ✅ **`.vscode/settings.json`**

```json
{
  "eslint.useFlatConfig": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  },
  "eslint.validate": ["javascript", "javascriptreact"],
  "editor.formatOnSave": false
}
```

---

### ✅ **`eslint.config.js`**

```js
// ✅ ESLint 9 Flat Config — React + Vite + Hooks + Aliases
import js from "@eslint/js";
import react from "eslint-plugin-react";
import reactHooks from "eslint-plugin-react-hooks";
import importPlugin from "eslint-plugin-import";
import globals from "globals";
import path from "path";

export default [
  js.configs.recommended,

  {
    files: ["**/*.{js,jsx}"],

    languageOptions: {
      ecmaVersion: "latest",
      sourceType: "module",
      parserOptions: {
        ecmaFeatures: { jsx: true },
      },
      globals: {
        ...globals.browser, // ✅ window, document, Image, etc.
        ...globals.node, // ✅ process, __dirname, etc.
      },
    },

    plugins: {
      react,
      "react-hooks": reactHooks,
      import: importPlugin,
    },

    settings: {
      react: { version: "detect" },
      "import/resolver": {
        alias: {
          map: [
            ["@assets", path.resolve("src/assets")],
            ["@common", path.resolve("src/common")],
            ["@pages", path.resolve("src/pages")],
            ["@theme", path.resolve("src/theme")],
          ],
          extensions: [".js", ".jsx"],
        },
      },
    },

    rules: {
      // ✅ React & JSX
      "react/react-in-jsx-scope": "off",
      "react/jsx-uses-vars": "error",

      // ✅ Hooks
      "react-hooks/rules-of-hooks": "error",
      "react-hooks/exhaustive-deps": "warn",

      // ✅ Import order
      "import/order": [
        "error",
        {
          groups: [
            ["builtin", "external"],
            ["internal"],
            ["parent", "sibling", "index"],
          ],
          pathGroups: [
            { pattern: "@pages/**", group: "internal", position: "before" },
            { pattern: "@common/**", group: "internal", position: "before" },
            { pattern: "@theme/**", group: "internal", position: "before" },
            { pattern: "@assets/**", group: "internal", position: "after" },
          ],
          pathGroupsExcludedImportTypes: ["builtin"],
          "newlines-between": "always",
          alphabetize: { order: "asc", caseInsensitive: true },
        },
      ],

      // ✅ General
      "no-unused-vars": ["warn", { argsIgnorePattern: "^_" }],
    },
  },
];
```
