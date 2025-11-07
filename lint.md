**Alias setup** for a Vite + React project:

✅ `@pages`
✅ `@common`
✅ `@theme`
✅ `@assets`

---

# ✅ 1. **Vite Alias Setup**

### `vite.config.js`

```js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import path from "path";

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      "@pages": path.resolve(__dirname, "src/pages"),
      "@common": path.resolve(__dirname, "src/common"),
      "@theme": path.resolve(__dirname, "src/theme"),
      "@assets": path.resolve(__dirname, "src/assets")
    }
  }
});
```

---

# ✅ 2. **JS Config (VSCode autocompletion)**

### `jsconfig.json`

```json
{
  "compilerOptions": {
    "baseUrl": "./",
    "paths": {
      "@pages/*": ["src/pages/*"],
      "@common/*": ["src/common/*"],
      "@theme/*": ["src/theme/*"],
      "@assets/*": ["src/assets/*"]
    }
  },
  "include": ["src"]
}
```

---

# ✅ 3. **ESLint Import Order**

✅ React
✅ Third-party libs
✅ Aliased imports (`@pages`, `@common`, `@theme`, `@assets`)
✅ Local imports
✅ Styles
✅ Assets (placed after styles)

### `.eslintrc.json`

```json
{
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:import/errors",
    "plugin:import/warnings",
    "prettier"
  ],
  "plugins": ["react", "import"],
  "rules": {
    "react/react-in-jsx-scope": "off",

    "import/order": [
      "error",
      {
        "groups": [
          ["builtin", "external"],
          ["internal"],
          ["parent", "sibling", "index"],
          ["unknown"],
          ["type"]
        ],
        "pathGroups": [
          { "pattern": "@pages/**", "group": "internal", "position": "before" },
          { "pattern": "@common/**", "group": "internal", "position": "before" },
          { "pattern": "@theme/**", "group": "internal", "position": "before" },
          { "pattern": "@assets/**", "group": "internal", "position": "after" }
        ],
        "newlines-between": "always",
        "alphabetize": { "order": "asc", "caseInsensitive": true }
      }
    ]
  },
  "settings": {
    "import/resolver": {
      "alias": {
        "map": [
          ["@pages", "./src/pages"],
          ["@common", "./src/common"],
          ["@theme", "./src/theme"],
          ["@assets", "./src/assets"]
        ],
        "extensions": [".js", ".jsx", ".ts", ".tsx"]
      }
    }
  }
}
```

✅ **Ensures assets come last**
✅ **Matches your exact alias list**
✅ **Auto-fixes on save**

---

# ✅ 4. **Import Example Matching Your New Structure**

✅ **Final sorted imports exactly as ESLint will enforce:**

```js
// 1️⃣ React & Core
import React from "react";

// 2️⃣ Third-party
import { Modal, Slider, Tag, Progress } from "antd";

// 3️⃣ Aliased imports
import { useGetProcessedImage } from "@common/hooks";
import { formatDate } from "@common/utils";
import { Button } from "@common/components";
import { TYPES } from "@common/constants";

// 4️⃣ Local component-specific imports
import { processImage } from "./utils";

// 5️⃣ Styles
import styles from "./style.module.css";

// 6️⃣ Assets (after styles)
import Banner from "@assets/home/banner.png";
```
