# 🎨 Design System Tokens

A token-based design system with programmatic color palette generation, dark theme architecture, and semantic stage colors. Includes Python scripts for generating visual palette PDFs and a complete CSS variable system.

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python)
![CSS](https://img.shields.io/badge/CSS-Variables-1572B6?style=flat-square&logo=css3)
![reportlab](https://img.shields.io/badge/reportlab-PDF-red?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)

---

## Overview

Built for a mission-driven organization's multi-platform brand, this design system provides a single source of truth for colors, spacing, typography, and component tokens. The system supports dark theme as the primary context and uses rgba transparency patterns for layering instead of introducing new hues.

---

## Color Architecture

### Core Palette

| Token | Hex | Usage |
|-------|-----|-------|
| `--color-primary` | `#D4A853` | Main accent, buttons, highlights |
| `--color-primary-dark` | `#B8912E` | Darker gold, gradients |
| `--color-bg-base` | `#12141C` | Main background |
| `--color-bg-elevated` | `#1A1D26` | Cards, panels, overlays |

### Text & Neutrals

| Token | Hex | Usage |
|-------|-----|-------|
| `--color-text-header` | `#F5E6C8` | Headers, high contrast (warm cream) |
| `--color-text-primary` | `#E2E8F0` | Primary body text |
| `--color-text-secondary` | `#C5CDD9` | Secondary text |
| `--color-text-tertiary` | `#A8B2C1` | Tertiary text |
| `--color-text-muted` | `#7A8599` | Muted/labels |
| `--color-text-dim` | `#4A5568` | Dim/timestamps |

### Semantic Stage Colors

| Token | Hex | Stage |
|-------|-----|-------|
| `--color-stage-clarity` | `#93C5FD` | Clarity (blue) |
| `--color-stage-capability` | `#D4A853` | Capability (gold) |
| `--color-stage-contribution` | `#86EFAC` | Contribution (green) |

### Transparency Patterns

Gold overlays use `rgba(212, 168, 83, opacity)` with these standard stops:

```css
--gold-overlay-subtle:    rgba(212, 168, 83, 0.04);  /* hover backgrounds */
--gold-overlay-light:     rgba(212, 168, 83, 0.08);  /* active states */
--gold-overlay-medium:    rgba(212, 168, 83, 0.15);  /* selected states */
--gold-overlay-strong:    rgba(212, 168, 83, 0.25);  /* emphasis, borders */
```

---

## Programmatic Palette Generation

The `generate_palette.py` script produces a visual PDF reference sheet with all colors, organized by category:

```bash
python generate_palette.py --output palette.pdf
```

### How It Works

```python
from reportlab.lib.pagesizes import A4
from reportlab.pdfgen import canvas
from reportlab.lib.colors import HexColor

# Token definitions
PALETTE = {
    "Primary Brand": {
        "Main Accent": "#D4A853",
        "Dark Gold": "#B8912E",
    },
    "Dark Theme Base": {
        "Background": "#12141C",
        "Elevated": "#1A1D26",
    },
    # ... full palette
}
```

The script generates color swatches with hex codes, token names, and usage labels — ready for handoff to designers or documentation.

---

## CSS Token System

### Naming Convention

```css
:root {
  /* Pattern: --{category}-{property}-{variant} */
  --color-primary: #D4A853;
  --color-bg-base: #12141C;
  --color-text-primary: #E2E8F0;
  --color-stage-clarity: #93C5FD;

  /* Spacing scale (4px base) */
  --space-1: 0.25rem;   /* 4px */
  --space-2: 0.5rem;    /* 8px */
  --space-3: 0.75rem;   /* 12px */
  --space-4: 1rem;      /* 16px */
  --space-6: 1.5rem;    /* 24px */
  --space-8: 2rem;      /* 32px */
}
```

### JavaScript Constants

```javascript
// For use in React/JS contexts
export const C = {
  PRIMARY: '#D4A853',
  PRIMARY_DARK: '#B8912E',
  BG_BASE: '#12141C',
  BG_ELEVATED: '#1A1D26',
};

export const TINT = (color, opacity) =>
  `rgba(${parseInt(color.slice(1,3),16)}, ${parseInt(color.slice(3,5),16)}, ${parseInt(color.slice(5,7),16)}, ${opacity})`;
```

---

## Project Structure

```
├── tokens/
│   ├── colors.css          # CSS custom properties
│   ├── colors.json         # Machine-readable token definitions
│   ├── colors.js           # JS constants (const C, TINT helper)
│   └── spacing.css         # Spacing scale
├── scripts/
│   └── generate_palette.py # PDF palette generator
├── output/
│   └── palette.pdf         # Generated visual reference
└── README.md
```

---

## Usage

### In React / Tailwind projects

```jsx
// Import tokens
import { C, TINT } from './tokens/colors';

// Use in styled components or inline styles
<div style={{ backgroundColor: C.BG_BASE, color: C.PRIMARY }}>
  <span style={{ background: TINT(C.PRIMARY, 0.08) }}>Highlighted</span>
</div>
```

### In CSS

```css
@import './tokens/colors.css';

.card {
  background: var(--color-bg-elevated);
  border: 1px solid var(--gold-overlay-strong);
  color: var(--color-text-primary);
}
```

---

## What I Learned

- Building a token-based system that bridges design and development
- Using rgba transparency patterns for UI hierarchy without color explosion
- Programmatic PDF generation with Python's reportlab library
- Creating naming conventions that scale across CSS, JS, and JSON

---

## License

MIT — see [LICENSE](LICENSE) for details.
