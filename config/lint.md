# Lint & Build Config

One-time setup for new React + Vite + TypeScript projects.
After this runs, AI output is verified by ESLint and tsc — style and type issues stop reaching review.

## `tsconfig.json`

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true,
    "baseUrl": "./",
    "paths": {
      "@assets/*": ["src/assets/*"],
      "@common/*": ["src/common/*"],
      "@pages/*": ["src/pages/*"],
      "@theme/*": ["src/theme/*"]
    }
  },
  "include": ["src"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```

## `tsconfig.node.json`

```json
{
  "compilerOptions": {
    "composite": true,
    "skipLibCheck": true,
    "module": "ESNext",
    "moduleResolution": "bundler",
    "allowSyntheticDefaultImports": true
  },
  "include": ["vite.config.ts"]
}
```

## `.vscode/settings.json`

```json
{
  "eslint.useFlatConfig": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  },
  "eslint.validate": ["javascript", "javascriptreact", "typescript", "typescriptreact"],
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "dbaeumer.vscode-eslint"
}
```

## `vite.config.ts`

```ts
import react from "@vitejs/plugin-react";
import path from "node:path";
import { fileURLToPath } from "node:url";
import { defineConfig } from "vite";

const __dirname = path.dirname(fileURLToPath(import.meta.url));

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      "@assets": path.resolve(__dirname, "./src/assets"),
      "@common": path.resolve(__dirname, "./src/common"),
      "@pages":  path.resolve(__dirname, "./src/pages"),
      "@theme":  path.resolve(__dirname, "./src/theme"),
    },
  },
  server: {
    headers: {
      "Cross-Origin-Opener-Policy": "same-origin",
      "Cross-Origin-Embedder-Policy": "require-corp",
    },
  },
});
```

## `eslint.config.js`

```js
import js from "@eslint/js";
import eslintPluginImport from "eslint-plugin-import";
import react from "eslint-plugin-react";
import reactHooks from "eslint-plugin-react-hooks";
import reactRefresh from "eslint-plugin-react-refresh";
import simpleImportSort from "eslint-plugin-simple-import-sort";
import globals from "globals";
import tseslint from "typescript-eslint";

export default tseslint.config(
  {
    ignores: ["dist", "node_modules", "eslint.config.js"],
  },
  {
    files: ["**/*.{js,jsx,ts,tsx}"],
    extends: [js.configs.recommended, ...tseslint.configs.recommended],
    languageOptions: {
      parserOptions: {
        ecmaVersion: "latest",
        sourceType: "module",
        ecmaFeatures: { jsx: true },
        project: ["./tsconfig.json"],
      },
      globals: globals.browser,
    },
    plugins: {
      react,
      "react-hooks": reactHooks,
      "react-refresh": reactRefresh,
      "simple-import-sort": simpleImportSort,
      import: eslintPluginImport,
    },
    rules: {
      ...react.configs.recommended.rules,
      ...reactHooks.configs.recommended.rules,

      "react/prop-types": "off",
      "react/react-in-jsx-scope": "off",

      "react-refresh/only-export-components": ["warn", { allowConstantExport: true }],

      "no-unused-vars": "off",
      "@typescript-eslint/no-unused-vars": ["error", { argsIgnorePattern: "^_" }],

      "no-console": "error",

      "react-hooks/exhaustive-deps": "error",

      "@typescript-eslint/no-explicit-any": "error",
      "@typescript-eslint/no-non-null-assertion": "error",

      "simple-import-sort/imports": [
        "error",
        {
          groups: [
            ["^react", "^react-dom"],
            ["^antd", "^lucide-react", "^@?\\w"],
            ["^@assets(/.*|$)", "^@common(/.*|$)", "^@pages(/.*|$)", "^@theme(/.*|$)"],
            ["^\\.{1,2}/"],
            ["^\\u0000", "^.+\\.(css|scss)$"],
            ["^.+\\.(png|jpe?g|gif|svg|webp|mp4|mp3|ogg|wav)$"],
          ],
        },
      ],
      "simple-import-sort/exports": "error",
      "import/newline-after-import": ["error", { count: 1 }],
    },
  },
);
```

## Install

```bash
npm install -D \
  typescript \
  @types/react \
  @types/react-dom \
  eslint \
  @eslint/js \
  typescript-eslint \
  eslint-plugin-react \
  eslint-plugin-react-hooks \
  eslint-plugin-react-refresh \
  eslint-plugin-simple-import-sort \
  eslint-plugin-import \
  globals
```
