# 🏗️ Project Architecture & Code Standards

### ✅ **AI-SAFE & PRODUCTION-READY VERSION (Refined)**

---

## ⚠️ **MANDATORY AI COMPLIANCE NOTICE**

During **any** code generation, refactoring, documentation, or architecture tasks:

- ✅ The AI must **strictly follow all rules, structures, conventions, and examples** in this document.
- ❌ No creative variations, assumptions, reorganizing, renaming, or restructuring.
- ❌ No introducing new folders (e.g., `/lib`, `/shared`, `/helpers`, etc.).
- ✅ When any detail is unclear, **AI must ask the user before generating code**.
- ✅ All generated components must adhere to naming, folder, and styling rules.

---

# ✅ 1. Folder Structure Standards (Refined)

```
src/
  assets/
    ├── logo/
    ├── icons/
    ├── page-name/

  common/                         → Shared logic, components, utilities
    ├── components/               // Multi-use UI components
    ├── utils/                    // Shared utilities
    │     ├── background.removal.js
    │     ├── drag.js
    │     └── index.js            // Mandatory export-aggregator
    ├── constants/
    │     └── index.js            // Mandatory export-aggregator
    └── hooks/
          ├── processed.image.js
          └── index.js            // Mandatory export-aggregator

  pages/
    page-name/
      ├── index.jsx
      ├── slider/                 // Page-specific reusable subcomponents
      │     └── index.js
      ├── style.module.css
      ├── utils.js
      └── constants.js

  theme/
    ├── override.css              // Base resets
    ├── colors.css                // Color variables & gradients
    └── font.css                  // Font variables
```

### ✅ Additional Rules

- All pages **must** include their own `style.module.css`.
- Each page contains **only** the logic and helpers specific to that page.
- Large JSX files must be broken into `slider/` or additional subcomponents.

---

# ✅ 2. General Rules (Refined)

### 📁 Feature-Based Structure

- Every page manages its own logic, components, utils, and styling.
- Shared logic lives **only** inside `/common/`.

### ♻️ Shared Logic

| Use Case                      | Folder                |
| ----------------------------- | --------------------- |
| Shared reusable UI components | `/common/components/` |
| Shared utilities              | `/common/utils/`      |
| Shared constants              | `/common/constants/`  |
| Shared hooks                  | `/common/hooks/`      |

❌ Never duplicate logic between pages.
✅ Always export through each folder's `index.js` for unified imports.

---

# ✅ 3. Naming Conventions (Refined)

| Entity                    | Rule                     | Example                              |
| ------------------------- | ------------------------ | ------------------------------------ |
| Folders                   | kebab-case               | `image-crop/`, `file-uploader/`      |
| Component file            | `index.jsx`              | `common/components/button/index.jsx` |
| Subcomponent file         | dot.notation             | `slider.image.preview.jsx`           |
| Style file                | `style.module.css`       | `pages/home/style.module.css`        |
| Utility / constant file   | lowercase                | `utils.js`, `constants.js`           |
| Advanced utility file     | dot notation             | `grid.update.sx.js`                  |
| Component names (JSX)     | PascalCase               | `export function ImageCrop()`        |
| Hook names                | camelCase + "use" prefix | `useProcessedImage()`                |
| CSS Class Names (Modules) | camelCase                | `.previewContainer`                  |

---

# ✅ 4. Styling Conventions (Refined)

- ✅ Use **CSS Modules** for every component & page.
- ✅ Use `/theme` only for:

  - Colors
  - Typography
  - Base resets

- ❌ No inline styles.
- ❌ No Tailwind, Styled Components, Emotion, SCSS.
- ✅ Use CSS variables defined in `/theme/colors.css` and `/theme/font.css`.

**Example:**

```css
.container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.imagePreview {
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.actionButton {
  margin-top: 12px;
}
```

---

# ✅ 5. AI Behavior & Enforcement (Refined)

## 🔒 5.1 Code Generation Rules

The AI must:

- ✅ Mirror the folder & file structure **exactly**.
- ✅ Always generate:

  - `index.jsx`
  - `style.module.css`

- ✅ Split large components into subcomponents.
- ✅ Use central `index.js` for imports.
- ❌ Never create unknown folders.
- ❌ Never merge unrelated utilities/hooks.

---

## 📏 5.2 File Formatting Rules

- Max file size: **~200 lines**.
- Imports must follow order:

  1. React
  2. External libraries
  3. Internal modules
  4. CSS module

---

## 🧩 5.3 Error Prevention

- ❌ Never hallucinate logic or names.
- ❌ Never restructure without user approval.
- ✅ If any ambiguity → **stop and ask the user**.

---

## ✅ 5.4 AI Self-Check Before Returning Code

Before sending final output, AI must validate:

1. ✅ All files named correctly
2. ✅ Proper folder locations
3. ✅ Component includes matching `style.module.css`
4. ✅ No Tailwind / inline styles
5. ✅ Logic is modular
6. ✅ Imports follow centralized structure
7. ✅ No new or unapproved folder names
