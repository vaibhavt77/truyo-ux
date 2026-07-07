# Truyo Design System Reference

> **Source:** [Truyo Design System V1.0](https://www.figma.com/design/bOIvSDTKqhglrwVAMNhmqY/Truyo-Design-System-V1.0?node-id=4-2&m=dev)
> **File key:** `bOIvSDTKqhglrwVAMNhmqY`
> **Library key:** `lk-8ecc115b083d04b8163cef3ce922b9ce2deb730644632d98a364c5ae49f04a31a3d1e470be30a6f59b357751e7b69ee5ebe3ca6810bd55d0f2c11ba6ff8670bd`
> **Companion library (also subscribed):** IE Design Standard System
> **Project:** Truyo Platform
> **Audience:** UX/UI designers (hi-fi Figma work) + developers (HTML/CSS/React prototype)
> **Last synced:** 2026-06-22

---

## 1. Purpose of This Document

This is the single source of truth for designers and developers building **Truyo hi-fidelity mockups and HTML prototypes**. It mirrors the Truyo Design System V1.0 Figma library so the team can:

1. **Designers** — reach for the correct component, variant, and token when promoting low-fi frames to hi-fi.
2. **Developers** — translate Figma artifacts into HTML/CSS (and later React) using exact token values, type styles, and elevation rules.
3. **QA / Review** — verify that every Truyo screen uses sanctioned tokens, components, and states.

**Rule of thumb:** if it's not in this document, it's not approved for Truyo product screens. New patterns must be added to Truyo first, then mirrored here.

---

## 2. Foundations

### 2.1 Brand & Tone (visual)
- **Aesthetic:** Clean, dense, data-forward enterprise UI for privacy, consent, and configuration workflows.
- **Visual hierarchy:** Decision-first. Use color and weight to surface task-critical changes and states, not decoration.
- **Color discipline:** Neutral by default. Color only signals **status, severity, or interaction state** — never decoration.

### 2.2 Grid & Layout
| Property | Value |
|---|---|
| Base unit | **8px** — all padding, gap, margin values are multiples of 8 |
| Canvas (desktop) | **1440px** primary, 1280px secondary breakpoint |
| Columns | 12 columns · 80px side margins · 24px gutters · 82px column width |
| Sticky elements | Filter bar, decision snapshot strip, action footer |

### 2.3 Border Radius
Use the smallest radius that reads correctly at the component scale. Truyo defaults:

| Token (CSS) | Value | Use |
|---|---|---|
| `--radius-sm` | 4px | Inputs, badges, tags, table cells |
| `--radius-md` | 6px | Buttons, menu items |
| `--radius-lg` | 8px | Cards, dialogs, dropdowns |
| `--radius-pill` | 999px | Pills, segmented control thumb |

### 2.4 Elevation (Effect Styles)
Source: Truyo `Elevation/*` styles.

| Token | Use | CSS |
|---|---|---|
| `Elevation/01 - Cards` | Cards, raised table rows, sticky bars | `box-shadow: 0 2px 4px #1D212D14, 0 0 2px #1D212D14, 0 0 1px #1D212D33;` |
| `Elevation/02 - Menus & Modals` | Dropdowns, popovers, modals, drawers | `box-shadow: 0 16px 32px #1D212D1A, 0 1px 4px #1D212D26, 0 0 1px #1D212D33;` |
| `Focus/Primary` | Outer focus ring (keyboard navigation) | `box-shadow: 0 0 0 3px #007AFF4D, 0 0 0 1px #FFFFFF99;` |
| `Focus/Primary - Inner` | Inset focus (inside inputs/segmented control) | `inset 0 0 0 4px #007AFF4D, inset 0 0 0 2px #FFFFFF99;` |

> **Accessibility rule:** Every interactive element MUST show `Focus/Primary` (or `Focus/Primary - Inner` where outer ring would clip) on `:focus-visible`.

---

## 3. Color Tokens

All colors are sourced from Truyo `Tokens/color/*`. **Designers** must apply Figma variables (never raw hex). **Developers** consume them as CSS custom properties.

### 3.1 Primitive Scale (raw palette)

| Name | Hex | Use |
|---|---|---|
| Neutral/50 | `#FBFCFE` | Page background tint |
| Neutral/100 — Light BG | `#F5F8FA` | Section background |
| Neutral/200 — Darker BG, Light Border | `#E9F0F4` | Subtle dividers, zebra rows |
| Neutral/300 — Border | `#D3DFE7` | Default border |
| Neutral/400 | `#A8B9CA` | Disabled foreground / muted icon |
| Neutral/500 — Graphics, Large AA Text | `#798AA3` | Icon default, large text |
| Neutral/600 — AA Text | `#5D6C87` | Secondary text |
| Neutral/700 — AAA Text | `#455068` | Body text |
| Neutral/800 — AAA Text Dark | `#2E3748` | Strong text |
| Neutral/900 — AAA Text Darkest | `#1D212D` | Headings, primary text |
| Primary/200 — Light Border | `#DCF2FE` | Primary tint background |
| Primary/300 — Border | `#BBE2FD` | Primary border |
| Primary/500 — Graphics, Large AA Text | `#3E87F4` | Primary graphic |
| Primary/600 — AA Text | `#5B42E3` | Primary interactive (border-active) |
| Primary/700 — AAA Colorful | `#0E3ED0` | Primary action / link |
| Primary/800 — AAA Dark | `#0522A0` | Primary hover/pressed |
| Critical/100 — Light BG | `#FEF4F5` | Critical surface |
| Critical/200 — Light Border | `#FEEAED` | Critical border tint |
| Critical/500 — Graphics, Large AA Text | `#F64669` | Critical graphic |
| Critical/600 — AA Text | `#DD214F` | Critical text |
| Critical/700 — AAA Colorful | `#A3072B` | Critical action |
| Critical/900 — AAA Text Darkest | `#4B0012` | Critical strong text |
| Warning/200 — Light Border | `#FDEFB0` | Warning border tint |
| Warning/500 — Graphics, Large AA Text | `#CE7100` | Warning graphic |
| Warning/600 — AA Text | `#AB5200` | Warning text |
| Warning/700 — AAA Colorful | `#863A00` | Warning action |
| Warning/800 — AAA Dark | `#602400` | Warning strong text |
| Positive/200 — Light Border | `#D6FC92` | Positive border tint |
| Positive/400 | `#6ACE13` | Positive graphic |
| Positive/700 — AAA Colorful | `#235C04` | Positive action |
| Promote/200 — Light Border | `#F5EBFE` | Promote tint |
| Promote/500 — Graphics, Large AA Text | `#A967F8` | Promote graphic |
| Promote/700 — AAA Colorful | `#5824D4` | Promote action |
| Promote/800 — AAA Dark | `#3016A0` | Promote strong text |

### 3.2 Semantic Tokens (USE THESE — not primitives)

#### Text
| Token | Hex | Use |
|---|---|---|
| `text-default` | `#04070E` | Primary text |
| `text-primary` | (Primary/700) | Primary action labels, links |
| `text-tertiary-dark` | `#6E7E94` | Tertiary metadata |
| `text-critical-darker` | `#AF324B` | Critical text |
| `text-warning-dark` | `#D88D33` | Warning text |
| `text-positive-dark` | `#3E8E09` | Positive text |
| `text-neutral-darkest` | `#434C5A` | Neutral emphasis |

#### Icon
| Token | Hex |
|---|---|
| `icon-default` | `#94A1B5` |
| `icon-dark` | `#798AA3` |
| `icon-primary` | (Primary/700) |
| `icon-critical-darker` | `#AF324B` |
| `icon-warning-dark` | `#D88D33` |
| `icon-positive-dark` | `#3E8E09` |
| `icon-neutral-darkest` | `#434C5A` |

#### Surface (backgrounds)
| Token | Hex | Use |
|---|---|---|
| `surface-lightest` | `#FFFFFF` | Page / card background |
| `surface-lighter` | (Neutral/50) | Subtle alt surface |
| `surface-light` | (Neutral/100) | Section background |
| `surface-primary` | (Primary/700) | Primary CTA fill |
| `surface-primary-hover` | (Primary/800) | Primary hover |
| `surface-primary-active` | — | Primary pressed |
| `surface-primary-focused` | — | Primary focused |
| `surface-primary-disabled` | — | Primary disabled |
| `surface-blue-light` | — | Info / neutral-info background |
| `surface-green-light` | `#F7FDEF` | Positive background |
| `surface-yellow-light` | — | Warning background |
| `surface-critical-lightest` | `#FEEDF0` | Critical background |
| `surface-neutral-lightest` | `#F2F3F6` | Neutral chip / tag background |
| `surface-warning-light` | `#FAF1E6` | Warning background |
| `table-header` | `#FDFDFD` | Table header default |
| `table-header-hover` | `#F6F5FE` | Table header hover |
| `table-header-active` | `#F9F8FE` | Sorted/active column header |

#### Border
| Token | Hex |
|---|---|
| `border-default` | `#D5DBE2` |
| `border-default-light` | `#E6E6E6` |
| `border-dark` | (referenced by name) |
| `border-darker` | `#94A1B5` |
| `border-darkest` | `#798AA3` |
| `border-hover` | (referenced by name) |
| `border-active` | `#5B42E3` |
| `border-disabled` | (referenced by name) |
| `border-white` | `#FFFFFF` |
| `border-critical-dark` | `#AF324B` |
| `border-warning-dark` | `#D88D33` |
| `border-positive-dark` | `#3E8E09` |

> **Truyo mapping:** see [§7. Truyo Status Mapping](#7-truyo-status-mapping) for how semantic tokens map to reusable status and confidence states.

### 3.3 CSS Variables (drop-in)

```css
:root {
  /* Neutral */
  --color-neutral-50:  #FBFCFE;
  --color-neutral-100: #F5F8FA;
  --color-neutral-200: #E9F0F4;
  --color-neutral-300: #D3DFE7;
  --color-neutral-400: #A8B9CA;
  --color-neutral-500: #798AA3;
  --color-neutral-600: #5D6C87;
  --color-neutral-700: #455068;
  --color-neutral-800: #2E3748;
  --color-neutral-900: #1D212D;

  /* Primary */
  --color-primary-200: #DCF2FE;
  --color-primary-300: #BBE2FD;
  --color-primary-500: #3E87F4;
  --color-primary-600: #5B42E3;
  --color-primary-700: #0E3ED0;
  --color-primary-800: #0522A0;

  /* Critical */
  --color-critical-100: #FEF4F5;
  --color-critical-200: #FEEAED;
  --color-critical-500: #F64669;
  --color-critical-600: #DD214F;
  --color-critical-700: #A3072B;
  --color-critical-900: #4B0012;

  /* Warning */
  --color-warning-200: #FDEFB0;
  --color-warning-500: #CE7100;
  --color-warning-600: #AB5200;
  --color-warning-700: #863A00;
  --color-warning-800: #602400;

  /* Positive */
  --color-positive-200: #D6FC92;
  --color-positive-400: #6ACE13;
  --color-positive-700: #235C04;

  /* Promote */
  --color-promote-200: #F5EBFE;
  --color-promote-500: #A967F8;
  --color-promote-700: #5824D4;
  --color-promote-800: #3016A0;

  /* Semantic — text */
  --text-default:           #04070E;
  --text-primary:           var(--color-primary-700);
  --text-tertiary-dark:     #6E7E94;
  --text-critical-darker:   #AF324B;
  --text-warning-dark:      #D88D33;
  --text-positive-dark:     #3E8E09;
  --text-neutral-darkest:   #434C5A;

  /* Semantic — icon */
  --icon-default:           #94A1B5;
  --icon-dark:              #798AA3;
  --icon-primary:           var(--color-primary-700);
  --icon-critical-darker:   #AF324B;
  --icon-warning-dark:      #D88D33;
  --icon-positive-dark:     #3E8E09;
  --icon-neutral-darkest:   #434C5A;

  /* Semantic — surface */
  --surface-lightest:           #FFFFFF;
  --surface-lighter:            var(--color-neutral-50);
  --surface-light:              var(--color-neutral-100);
  --surface-primary:            var(--color-primary-700);
  --surface-primary-hover:      var(--color-primary-800);
  --surface-blue-light:         #EAF4FE;
  --surface-green-light:        #F7FDEF;
  --surface-yellow-light:       #FDF6E3;
  --surface-critical-lightest:  #FEEDF0;
  --surface-neutral-lightest:   #F2F3F6;
  --surface-warning-light:      #FAF1E6;
  --table-header:               #FDFDFD;
  --table-header-hover:         #F6F5FE;
  --table-header-active:        #F9F8FE;

  /* Semantic — border */
  --border-default:         #D5DBE2;
  --border-default-light:   #E6E6E6;
  --border-darker:          #94A1B5;
  --border-darkest:         #798AA3;
  --border-active:          var(--color-primary-600);
  --border-critical-dark:   #AF324B;
  --border-warning-dark:    #D88D33;
  --border-positive-dark:   #3E8E09;
}
```

---

## 4. Typography

**Font family:** `Inter` (loaded via Google Fonts or local). Fallback stack: `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif`.

> **Inter quirk:** In Figma the styles read **"Semi Bold"** (with space) and **"Extra Bold"** — keep this exact casing when matching in CSS via `font-weight`.

### 4.1 Type Scale

| Token | Family | Weight | Size | Line height | Tracking | Use |
|---|---|---|---|---|---|---|
| `48/Semi Bold` | Inter | 600 | 48 | 64 | -2 | Page hero / KPI hero |
| `20/Medium` | Inter | 500 | 20 | 32 | -1.7 | Screen / section title |
| `16/Semibold` | Inter | 600 | 16 | 24 (1.5) | -1.1 | Card title, table title |
| `16/Medium` | Inter | 500 | 16 | 24 (1.5) | -1.1 | Strong row title |
| `16/Regular` | Inter | 400 | 16 | 24 | -1.1 | Lead body |
| `14/Bold` | Inter | 700 | 14 | 24 | -0.6 | Strong inline emphasis |
| `14/Semi Bold` | Inter | 600 | 14 | 24 | -0.6 | Button label, column header |
| `14/Medium` | Inter | 500 | 14 | 24 | -0.6 | Strong body |
| `14/Regular` | Inter | 400 | 14 | 24 | -0.6 | Body default |
| `Content/14/Regular` | Inter | 400 | 14 | 20 | -0.6 | Dense table cell body |
| `12/Regular` | Inter | 400 | 12 | 16 | 0 | Label, column header |
| `Content/12/Regular` | Inter | 400 | 12 | 18 | 0.25 | Dense metadata |
| `Meta/Label` | Inter | 400 | 12 | 16 | -0.5 | Metadata caption |
| `11/Regular` | Inter | 400 | 11 | 16 | 0.5 | Timestamp, helper text |

### 4.2 CSS Utility Classes

```css
.t-hero       { font: 600 48px/64px Inter; letter-spacing: -2px; }
.t-title      { font: 500 20px/32px Inter; letter-spacing: -1.7px; }
.t-h3-semi    { font: 600 16px/1.5 Inter; letter-spacing: -1.1px; }
.t-h3-med     { font: 500 16px/1.5 Inter; letter-spacing: -1.1px; }
.t-h3-reg     { font: 400 16px/24px Inter; letter-spacing: -1.1px; }
.t-body-bold  { font: 700 14px/24px Inter; letter-spacing: -0.6px; }
.t-body-semi  { font: 600 14px/24px Inter; letter-spacing: -0.6px; }
.t-body-med   { font: 500 14px/24px Inter; letter-spacing: -0.6px; }
.t-body       { font: 400 14px/24px Inter; letter-spacing: -0.6px; }
.t-cell       { font: 400 14px/20px Inter; letter-spacing: -0.6px; }
.t-label      { font: 400 12px/16px Inter; letter-spacing: 0; }
.t-meta       { font: 400 12px/18px Inter; letter-spacing: 0.25px; }
.t-caption    { font: 400 11px/16px Inter; letter-spacing: 0.5px; }
```

---

## 5. Spacing, Sizing & Motion

### 5.1 Spacing Scale (multiples of 8, with 4px half-step)

| Token | Value | Common use |
|---|---|---|
| `--space-1` | 4px | Icon ↔ label inside compact button |
| `--space-2` | 8px | Default gap between adjacent atoms |
| `--space-3` | 12px | Form field internal spacing |
| `--space-4` | 16px | Group gap, card padding, row gap in tables |
| `--space-5` | 24px | Section gap, column gutter |
| `--space-6` | 32px | Page section separation |
| `--space-8` | 48px | Major section break |
| `--space-10` | 64px | Page-level breathing room |

### 5.2 Size Tokens

| Token | Value | Use |
|---|---|---|
| `--row-h-header` | 32px | Standard table header height |
| `--row-h-body` | 48px | Standard table body row height |
| `--row-h-dense` | 40px | Dense table row (optional toggle) |
| `--ctrl-h-sm` | 28px | Small button / tag |
| `--ctrl-h-md` | 36px | Default input / button |
| `--ctrl-h-lg` | 44px | Hero CTA / primary form button |
| `--icon-sm` | 16px | Inline / cell icon |
| `--icon-md` | 20px | Button / nav icon |
| `--icon-lg` | 24px | Toolbar / illustration icon |

### 5.3 Motion

| Token | Duration | Easing | Use |
|---|---|---|---|
| `--motion-fast` | 120ms | `cubic-bezier(0.2, 0, 0.38, 0.9)` | Hover, focus, micro state |
| `--motion-base` | 200ms | `cubic-bezier(0.2, 0, 0.38, 0.9)` | Dropdowns, tabs, toggles |
| `--motion-slow` | 320ms | `cubic-bezier(0.2, 0, 0.13, 1.5)` | Drawer/modal entrance |

> **Reduced motion:** Always honor `prefers-reduced-motion: reduce` — replace transitions with instant state changes.

---

## 6. Components Catalog

> Component names below are the exact Figma Truyo component names. When working in Figma, **insert from library — never detach**. In code, follow the structure here; the prototype repo will host the React/HTML implementations.

### 6.1 Component Inventory

| Group | Component (Figma) | Variants captured | Truyo usage examples |
|---|---|---|---|
| **Action** | `Button - v2` | Type (Primary/Secondary/Ghost/Destructive), Size (sm/md/lg), Icon (none/leading/trailing/only), State (default/hover/active/focused/disabled/loading) | Save / Submit / Escalate; page and row actions |
| | `Icon Button` | Size + State | Row actions, toolbar |
| | `Area Button` | — | Large clickable card areas |
| | `Button menu item` | — | Inside dropdown menus |
| **Form** | `Text Field` | Size + State + Validation | Reason capture, search, comments |
| | `Checkbox` | Default/Checked/Indeterminate/Disabled + Hover/Focus | Bulk selection in data tables |
| | `Switch` | On/Off + Disabled | Toggle preferences and feature settings |
| | `Radio` | Selected/Unselected + State | Single-choice in forms |
| | `Label` | Required/Optional | Field labels |
| **Selection** | `Menu` | Static / Filterable | Dropdowns, column chooser |
| | `Segmented control` | 2/3/4 segments + State | Role or view switchers |
| | `Stepwise-stepper` | Active step / Completed / Disabled | Multi-step setup and approval flows |
| **Feedback** | `Alert` | Info / Success / Warning / Critical | Inline page banners |
| | `Badge` | Color + Size + Style | KPI deltas, count indicators |
| | `Tags` | Color + Removable | Filter chips, status tags |
| **Overlay** | `Dialog` / `Dialog Modal` | Size + With/without close + With/without footer | Confirmation, edit, and approval modals |
| **Identity** | `Avatar` | Size + Type (image/initials/icon) + Status | User menu, assignee, escalation target |
| | `User menu` | — | App header right-side |
| **Table (composite)** | `Row Title Cell` | Selected / Active | Primary-column record ID cell |
| | `Table Cell - Actions` | 1/2/3/4 icon-button + button + description | Row actions column |
| | (See [§6.7](#67-table-pattern) for full table spec) | — | Request, preference, and operations tables |
| **Display** | `type` | text component | Inline text utilities |
| | `Formatting bar` | — | Comment / reason rich-text input |
| | `Schema` | — | Data structure visualization |
| | `Data Discovery` | — | Search / filter shell |
| **Iconography** | (Streamline Core / Lucide) | — | All icons must come from the Truyo icon set |

### 6.2 Button — `Button - v2`

**Anatomy:** `[leading icon?] [label] [trailing icon?]`

| Variant | Surface | Text | Border | Hover |
|---|---|---|---|---|
| **Primary** | `surface-primary` (`#0E3ED0`) | `#FFFFFF` | none | `surface-primary-hover` (`#0522A0`) |
| **Secondary** | `surface-lightest` | `text-default` | `border-default` | `surface-light` |
| **Ghost** | transparent | `text-primary` | none | `surface-light` |
| **Destructive** | `Critical/700` (`#A3072B`) | `#FFFFFF` | none | `Critical/900` (`#4B0012`) |

**Sizes:** sm=28px (12/Regular), md=36px (14/Semi Bold), lg=44px (14/Semi Bold).
**Padding:** sm 8/12, md 8/16, lg 12/20. Icon-only buttons are square at the same height.
**States:** `:hover`, `:active`, `:focus-visible` (apply `Focus/Primary`), `:disabled` (40% opacity + `cursor: not-allowed`), `loading` (replace label with spinner; keep width fixed).

**HTML reference**
```html
<button class="btn btn--primary btn--md">
  <span class="btn__icon" aria-hidden="true">…</span>
  <span class="btn__label">Override status</span>
</button>
```

### 6.3 Text Field — `Text Field`
- Container: 36px (md) height, 6px radius, `border-default` 1px, `surface-lightest` fill.
- Padding: 8px / 12px. Label: `t-label` above. Helper text: `t-caption` below.
- States: default · hover (`border-darker`) · focus (`border-active` + `Focus/Primary - Inner`) · error (`border-critical-dark`, helper `text-critical-darker`) · disabled (`surface-light`, `text-tertiary-dark`).

### 6.4 Checkbox · Switch · Radio
- 16×16 footprint; 20×20 hit area minimum 24×24.
- Selected fill: `surface-primary`. Focus ring: `Focus/Primary`.
- Switch thumb: white, 16px circle, 200ms slide.
- All three require an associated `<label>` and `aria-checked` / `aria-pressed` where appropriate.

### 6.5 Badge & Tag
- **Badge** — single character/number, 16–20px tall, pill, used for counts and small deltas.
- **Tag** — chip with optional remove icon; used for filters and status pills (severity, confidence).
- Colorways pull from semantic surfaces: Critical / Warning / Positive / Promote / Neutral.

### 6.6 Dialog / Modal — `Dialog Modal`
- Width: 480 / 560 / 720 (sm/md/lg). Radius 8px. `Elevation/02`.
- Structure: `header (title + close)` → `body` → `footer (secondary + primary CTA)`.
- Overlay: `#1D212D` at 40% opacity.
- Focus trapped; ESC closes; first focusable element receives focus on open.
- Used for confirmation dialogs, approval flows, and editing forms.

### 6.7 Table Pattern
The table is a primary composite in Truyo for operational and administrative workflows.

**Structural rules (must preserve from Truyo):**
- 32px header height · 48px body row height (default) · 40px when dense mode is on.
- Column groups: `[checkbox] [sortable data columns] [tags] [actions]`.
- Sortable header states: `Sort=None / Ascending / Descending` × `Hover=Yes / No`.
- Row cell states: `default / hover / selected / active-editing / new-value`.
- Cell variants supported: text, description (multi-line), tag, switch, checkbox, avatar / avatar-group, icon, action (1–4 buttons), payment method.
- Composite examples available: bulk-action bar, edit columns, filtering.

**Example mapping**
| Table column | Component / token |
|---|---|
| Selection checkbox | `Checkbox` (header + row) |
| Record ID | `Row Title Cell` |
| Primary status | text + `Tags` (color = status) |
| Secondary status | text + `Tags` |
| Confidence score | `Badge` (color = confidence band) |
| Key metric delta | `t-body-semi`, color from severity |
| Last updated | `t-meta` + icon-positive / icon-warning |
| Actions | `Table Cell - Actions` (3-icon variant) |

### 6.8 Alert
- 4 variants: Info (`surface-blue-light` + `border-default`), Success (`surface-green-light` + `border-positive-dark`), Warning (`surface-warning-light` + `border-warning-dark`), Critical (`surface-critical-lightest` + `border-critical-dark`).
- Anatomy: icon · title · body · optional action link · optional dismiss `Icon Button`.

### 6.9 Avatar / User Menu
- Sizes: 24 / 32 / 40 / 48px square, fully rounded.
- Initials use `t-body-semi`; auto-color from name hash within Promote / Primary / Positive / Warning families.
- `User menu` wraps avatar with chevron and triggers a `Menu`.

### 6.10 Segmented Control
- Used for role or mode switch patterns (for example, Admin / Operator).
- Sizes sm (28) / md (36). Selected thumb: `surface-lightest` over `surface-neutral-lightest` track; selected label `text-default`, unselected `text-tertiary-dark`.

### 6.11 Stepwise-stepper
- Horizontal stepper for onboarding, setup, and review workflows.
- Step states: Completed (filled positive) · Active (primary outline) · Disabled (neutral).

---

## 7. Truyo Status Mapping

The mapping below is the **canonical bridge** between Truyo product semantics and Truyo color tokens. Do not invent new colors per screen — re-use these.

### 7.1 Decision and workflow states
| Truyo state | Token | Hex | Background | Border |
|---|---|---|---|---|
| **Approved / Completed** | `text-positive-dark` | `#3E8E09` | `surface-green-light` | `border-positive-dark` |
| **Needs review** | `text-warning-dark` | `#D88D33` | `surface-warning-light` | `border-warning-dark` |
| **Action required** | `text-critical-darker` | `#AF324B` | `surface-critical-lightest` | `border-critical-dark` |
| **Verified** | `text-positive-dark` | `#3E8E09` | `surface-green-light` | `border-positive-dark` |
| **Paused** | `text-tertiary-dark` | `#6E7E94` | `surface-neutral-lightest` | `border-default` |
| **Stale** | `text-warning-dark` | `#D88D33` | `surface-warning-light` | `border-warning-dark` |

### 7.2 Confidence score bands (Badge color)
| Score | Confidence | Token | Surface |
|---|---|---|---|
| 0.80 – 1.00 | High — one-click accept | Positive | `surface-green-light` / `Positive/700` |
| 0.50 – 0.79 | Medium — review evidence | Warning | `surface-warning-light` / `Warning/700` |
| 0.00 – 0.49 | Low — investigate | Critical | `surface-critical-lightest` / `Critical/700` |

### 7.3 SLA status badges
| Badge | Token |
|---|---|
| Within buffer | Positive |
| At risk | Warning |
| Breach likely | Critical |

### 7.4 Severity badges
| Badge | Token |
|---|---|
| Critical | `Critical/700` |
| High | `Critical/500` |
| Medium | `Warning/600` |
| Low | `Neutral/600` |

---

## 8. Accessibility Standards (WCAG 2.2 AA target)

1. **Color contrast** — Body text against background ≥ 4.5:1 (use `text-default` / `text-neutral-darkest` on light surfaces). Large text ≥ 3:1. Never rely on color alone — pair with icon + label.
2. **Focus visibility** — `Focus/Primary` ring on every interactive element. Never remove with `outline: none` unless an equivalent visual replaces it.
3. **Keyboard** — All interactions reachable via Tab; logical order; ESC closes overlays; Enter activates; Space toggles selectables.
4. **Hit target** — Minimum 24×24 visible target with 44×44 effective hit area for primary actions.
5. **Motion** — Honor `prefers-reduced-motion: reduce`.
6. **Form fields** — Always paired with `<label>`; errors announced via `aria-live="polite"`; helper text linked via `aria-describedby`.
7. **Status communication** — All status colors paired with an icon (Positive/Warning/Critical icon set) and text label so colorblind users get equivalent information.
8. **Tables** — Use proper `<table>`, `<thead>`, `<th scope="col">`; sort state announced via `aria-sort`; row selection via `aria-selected`.

---

## 9. Component → Code Translation Cheat Sheet

| Figma component | HTML structure | CSS class hook | React (future) |
|---|---|---|---|
| `Button - v2` | `<button class="btn btn--primary btn--md">` | `.btn`, `.btn--{variant}`, `.btn--{size}`, `.btn--icon-only` | `<Button variant="primary" size="md" icon={…} />` |
| `Icon Button` | `<button class="icon-btn icon-btn--md">` | `.icon-btn` | `<IconButton icon={…} label="…" />` |
| `Text Field` | `<label class="field"><span class="field__label">…</span><input class="field__input" /></label>` | `.field`, `.field--error`, `.field--disabled` | `<TextField …/>` |
| `Checkbox` | `<label class="cb"><input type="checkbox" class="cb__input"><span class="cb__box"></span><span class="cb__label">…</span></label>` | `.cb`, `.cb--indeterminate` | `<Checkbox …/>` |
| `Switch` | `<label class="sw"><input type="checkbox" class="sw__input"><span class="sw__track"><span class="sw__thumb"/></span></label>` | `.sw` | `<Switch …/>` |
| `Tags` | `<span class="tag tag--warning">…<button class="tag__close">…</button></span>` | `.tag`, `.tag--{tone}`, `.tag--removable` | `<Tag tone="warning">…</Tag>` |
| `Badge` | `<span class="badge badge--critical">12</span>` | `.badge`, `.badge--{tone}`, `.badge--{size}` | `<Badge tone="critical">…</Badge>` |
| `Alert` | `<div role="alert" class="alert alert--warning">…</div>` | `.alert`, `.alert--{tone}` | `<Alert tone="warning" title="…" />` |
| `Dialog Modal` | `<div role="dialog" aria-modal="true" class="modal">…</div>` | `.modal`, `.modal__header`, `.modal__body`, `.modal__footer` | `<Modal …/>` |
| `Segmented control` | `<div role="tablist" class="seg">…</div>` | `.seg`, `.seg__option--selected` | `<Segmented …/>` |
| Table | `<table class="tbl">` + `<th scope="col" aria-sort="…">` | `.tbl`, `.tbl--dense`, `.tbl__row--selected` | `<DataTable …/>` |

---

## 10. Working in Figma — Designer Rules

1. **Always insert from `Truyo Design System V1.0`.** If a needed component is missing, request it in the Truyo file — do not build a local copy in product files.
2. **Use variables, not raw colors.** Apply Figma Variables from `Tokens/color/*`. Same for typography styles (e.g., `14/Regular`).
3. **Respect variant property names** so Code Connect mapping is preserved (`Type`, `Size`, `State`, `Icon`).
4. **Required state frames per screen** (suffix naming):
   ```
   [ScreenID]_Default
   [ScreenID]_Loading
   [ScreenID]_Empty
   [ScreenID]_Error
   [ScreenID]_Success           (where a commit action exists)
   [ScreenID]_PermissionLimited (where role-gating applies)
   ```
5. **Auto-layout everywhere.** Padding & gap values must be from the spacing scale (§5.1).
6. **Two reference files** — both libraries are subscribed; prefer Truyo first, fall back to `IE Design Standard System` only for assets Truyo lacks (after consultation).

---

## 11. Working in Code — Developer Rules

1. **Tokens are the contract.** Use `var(--token-name)`. Do not hard-code hex values inside component CSS.
2. **One CSS variable file** (e.g., `tokens.css`) imported once at the app root — paste from §3.3.
3. **Component CSS** — follow BEM (`block__element--modifier`). Names align with the cheat sheet in §9 so future Code Connect mapping is straightforward.
4. **Focus-visible** — every interactive element ships `:focus-visible` styles using `Focus/Primary` shadow recipe.
5. **No third-party UI libraries** for prototype components yet — mirror Truyo directly so visual parity with Figma is exact.
6. **Inter font** — load only weights actually used: 400, 500, 600, 700.
7. **Dark mode** — out of scope for v1 unless explicitly requested by Product.
8. **Responsive** — desktop-first (1440 / 1280). Define mobile behavior when product requirements require it.

---

## 12. Cross-Reference

- [README.md](README.md) — repository overview
- [UXUI_Requirements_Understanding.md](UXUI_Requirements_Understanding.md) — Truyo Silo Extension UX/UI requirements
- [Documents/Truyo_Silo_Extension_PRD.md](Documents/Truyo_Silo_Extension_PRD.md) — product requirements document

---

## 13. Change Log

| Date | Change | Source |
|---|---|---|
| 2026-06-22 | v1.0 — Initial design system reference compiled from Truyo Design System V1.0 (variables, components, type, effects). | Figma file `bOIvSDTKqhglrwVAMNhmqY` |
| 2026-07-07 | v1.1 — Removed project-specific references and normalized this document as Truyo's own design system reference. | Internal documentation update |

> **When Truyo updates** — re-pull variable defs and component lists, then bump the version in §13 and adjust §3 / §6 deltas only. Do not rewrite the document.
