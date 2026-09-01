# CalcVoyager — UI Theme & Design System Guide

> **Official Design Specification & Component Guide for CalcVoyager Team**  
> Use this document and the accompanying stylesheet [`frontend/src/styles/design-tokens.css`](./frontend/src/styles/design-tokens.css) to build new components, pages, and interactive mathematics tools that remain 100% consistent with the platform's theme.

---

## 🎨 1. Color Palette & Domain Accents

### Brand Colors
| Role | Light Mode Hex | CSS Variable | Usage |
| :--- | :--- | :--- | :--- |
| **Primary CTA** | `#0056D2` | `--cv-blue` | Main action buttons, active navigation, certification badges |
| **Primary Hover** | `#0043a8` | `--cv-blue-hover` | Button hover and active states |
| **Secondary Accent** | `#0284c7` | `--cv-sky` | Tool links, icons, interactive highlights |
| **Sky Light** | `#e0f2fe` | `--cv-sky-light` | Soft pill backgrounds, badge highlights |

### 4 Subject Domain Colors
Every course track has a distinctive domain color:

| Subject Course | Accent Color | Variable | Example Glyph / Formula |
| :--- | :--- | :--- | :--- |
| **Calculus & Analytical Geometry** | Gold `#c28a2e` | `--cv-subject-gold` | `∫ f(x) dx` |
| **Multivariable Calculus** | Teal `#0d9488` | `--cv-subject-teal` | `∭ curl F` |
| **Linear Algebra** | Royal Blue `#2563eb` | `--cv-subject-blue` | `Ax = b` |
| **Probability & Statistics** | Purple `#7c3aed` | `--cv-subject-purple` | `P(A\|B)` |

---

## 🌓 2. Surfaces, Ink & Dark Mode Rules

CalcVoyager implements a **unified high-contrast dark mode**.

> [!IMPORTANT]
> **Strict Dark Mode Typography Rule**:  
> In dark mode, all primary headings, questions, formula text, card titles, and body content **must render in `#f8fafc`**. Avoid using faint grays for core text.

| Element | Light Mode | Dark Mode (`[data-theme="dark"]`) | Variable |
| :--- | :--- | :--- | :--- |
| **Page Background** | `#ffffff` | `#0B1120` | `--cv-bg-page` |
| **Card Surface** | `#ffffff` | `#111827` | `--cv-bg-surface` |
| **Subtle Container / Input** | `#f8fafc` | `#0f172a` | `--cv-bg-subtle` |
| **Card Borders** | `#e2e8f0` (1.5px) | `#1e293b` (1.5px) | `--cv-border` |
| **Primary Headings & Text** | `#0f172a` | `#f8fafc` | `--cv-text-primary` |
| **Secondary Text** | `#475569` | `#cbd5e1` | `--cv-text-secondary` |
| **Muted Metadata** | `#64748b` | `#94a3b8` | `--cv-text-muted` |

---

## 🔤 3. Typography Stack

```css
/* UI Typography */
font-family: Inter, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;

/* Mathematical Typography (Formulas, Badges, Integrals) */
font-family: 'Cambria Math', 'KaTeX_Main', 'Times New Roman', Georgia, serif;

/* Code & Numerical Data */
font-family: 'JetBrains Mono', 'Fira Code', Consolas, monospace;
```

### Standard Type Hierarchy
- **Page Titles (`h1`)**: `clamp(1.8rem, 3.5vw, 2.4rem)`, `font-weight: 850`, `letter-spacing: -0.02em`
- **Section Titles (`h2`)**: `1.35rem - 1.5rem`, `font-weight: 850`, `letter-spacing: -0.015em`
- **Card Titles (`h3`)**: `1.45rem - 1.55rem`, `font-weight: 800`, `line-height: 1.3`
- **Card Metadata (`span`)**: `0.92rem - 0.95rem`, `font-weight: 600`, color `var(--cv-text-muted)`
- **Card Body Text (`p`)**: `1.02rem - 1.05rem`, `line-height: 1.65`, color `var(--cv-text-secondary)`
- **Math Expression Logos**: `font-size: 1.25rem - 2.5rem`, `font-weight: 800`, `white-space: nowrap`

---

## 🧱 4. Reusable HTML & CSS Component Templates

### A. Course & Feature Card Boilerplate
```html
<div class="cv-card">
  <div class="cv-math-badge cv-math-badge--blue">
    Ax = b
  </div>
  <h3 class="cv-card-title">Linear Transformations</h3>
  <span class="cv-card-meta">2 parts · Interactive Exercises</span>
  <p class="cv-card-desc">
    Kernel, image, matrix composition, and rank-nullity representations.
  </p>
</div>
```

### B. Interactive Action Buttons
```html
<!-- Primary Action Button -->
<button class="cv-btn-primary">
  Explore Guides →
</button>

<!-- Secondary Action Button -->
<button class="cv-btn-secondary">
  Practice Problems
</button>

<!-- Category Filter Pill -->
<button class="cv-tab-pill cv-tab-pill--active">
  All Topics
</button>
```

### C. Responsive Grid Layouts
```html
<!-- 4-Column Metric / Tool Grid -->
<div class="cv-grid-4">
  <div class="cv-card">Card 1</div>
  <div class="cv-card">Card 2</div>
  <div class="cv-card">Card 3</div>
  <div class="cv-card">Card 4</div>
</div>

<!-- 2-Column Domain Grid -->
<div class="cv-grid-2">
  <div class="cv-card">Subject Track A</div>
  <div class="cv-card">Subject Track B</div>
</div>
```

---

## 🚀 5. How Teammates Can Import the Tokens

Simply import `design-tokens.css` into your stylesheet or component:

```css
@import "../styles/design-tokens.css";
```

Or in React components:
```jsx
import "../../styles/design-tokens.css";
```
