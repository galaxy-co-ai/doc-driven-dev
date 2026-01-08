# 16 - Design Tokens

<!-- AI: This document defines the design system's foundational values - colors, typography, spacing, etc. Use this for any project with visual UI. These tokens should be the single source of truth for all visual styling. -->

## Design Tokens Overview

<!-- AI: Design tokens are named values that represent design decisions. They bridge design and development by creating a shared vocabulary. Benefits:
- Consistency: Same values used everywhere
- Maintainability: Change in one place, updates everywhere
- Theming: Easy light/dark mode, brand variants
- Documentation: Self-documenting design system
-->

### Token Philosophy

<!-- AI: Document the approach to design tokens:
- Naming convention (semantic vs. literal)
- Abstraction levels (primitive vs. semantic)
- Implementation format (CSS variables, JS objects, design tool tokens)
-->

**Naming Convention**: [semantic/literal/hybrid]

**Abstraction Levels**:
- **Primitive tokens**: Raw values (e.g., `blue-500: #3B82F6`)
- **Semantic tokens**: Named by purpose (e.g., `color-primary: blue-500`)
- **Component tokens**: Component-specific (e.g., `button-bg: color-primary`)

**Implementation**: [CSS Custom Properties / JS Object / Tailwind Config / Style Dictionary]

### Token Customization Guide

<!-- AI: Help users customize tokens for their project -->

**Customizing Tokens**:
1. Start with primitive values that match your brand
2. Map semantic tokens to primitives
3. Override component tokens only when needed
4. Test in both light and dark modes
5. Verify accessibility (contrast ratios)

**Brand Customization Checklist**:
- [ ] Primary brand color defined
- [ ] Secondary/accent colors defined
- [ ] Typography matches brand guidelines
- [ ] Spacing feels appropriate for content density

---

## Colors

<!-- AI: Define the color system. Use a structured approach with primitives and semantic layers. -->

### Color Primitives

<!-- AI: Define raw color values. Use a consistent naming pattern.

Common patterns:
- Numbered scale: gray-100, gray-200, ..., gray-900
- Named scale: gray-lightest, gray-light, gray, gray-dark, gray-darkest

Include enough shades for flexibility (typically 9-11 per hue).
-->

#### Gray Scale
<!-- AI: Neutral colors for backgrounds, text, borders -->

```css
/* Gray Primitives - adjust hex values to match brand */
--gray-50:  #[hex];   /* Lightest - subtle backgrounds */
--gray-100: #[hex];   /* Very light backgrounds */
--gray-200: #[hex];   /* Light backgrounds, borders */
--gray-300: #[hex];   /* Borders, disabled text */
--gray-400: #[hex];   /* Placeholder text */
--gray-500: #[hex];   /* Secondary text */
--gray-600: #[hex];   /* Primary text (light mode) */
--gray-700: #[hex];   /* Darker text */
--gray-800: #[hex];   /* Dark backgrounds */
--gray-900: #[hex];   /* Darkest - deep backgrounds */
```

#### Brand Colors
<!-- AI: Primary and secondary brand colors with full scale -->

```css
/* Primary Brand Color Scale */
--primary-50:  #[hex];   /* Tinted backgrounds */
--primary-100: #[hex];
--primary-200: #[hex];
--primary-300: #[hex];
--primary-400: #[hex];
--primary-500: #[hex];   /* Main brand color */
--primary-600: #[hex];   /* Hover state */
--primary-700: #[hex];   /* Active state */
--primary-800: #[hex];
--primary-900: #[hex];

/* Secondary/Accent Color Scale - if applicable */
--accent-50:  #[hex];
--accent-500: #[hex];    /* Main accent */
--accent-600: #[hex];    /* Hover */
```

#### Semantic Colors
<!-- AI: Colors for status and feedback -->

```css
/* Status Colors */
--red-500:    #[hex];    /* Error/Danger */
--red-600:    #[hex];    /* Error hover */
--green-500:  #[hex];    /* Success */
--green-600:  #[hex];    /* Success hover */
--yellow-500: #[hex];    /* Warning */
--yellow-600: #[hex];    /* Warning hover */
--blue-500:   #[hex];    /* Info */
--blue-600:   #[hex];    /* Info hover */
```

### Semantic Color Tokens

<!-- AI: Map primitives to semantic meanings. These are what components should reference. -->

#### Light Theme

```css
/* Backgrounds */
--color-bg-primary:     var(--gray-50);     /* Main page background */
--color-bg-secondary:   var(--white);       /* Card/panel backgrounds */
--color-bg-tertiary:    var(--gray-100);    /* Subtle backgrounds */
--color-bg-inverse:     var(--gray-900);    /* Dark backgrounds */

/* Surfaces - interactive backgrounds */
--color-surface-default:  var(--white);
--color-surface-hover:    var(--gray-50);
--color-surface-active:   var(--gray-100);
--color-surface-selected: var(--primary-50);

/* Text */
--color-text-primary:   var(--gray-900);    /* Main text */
--color-text-secondary: var(--gray-600);    /* Supporting text */
--color-text-tertiary:  var(--gray-500);    /* Subtle text */
--color-text-disabled:  var(--gray-400);    /* Disabled text */
--color-text-inverse:   var(--white);       /* Text on dark */
--color-text-link:      var(--primary-600); /* Links */

/* Borders */
--color-border-default: var(--gray-200);    /* Default borders */
--color-border-strong:  var(--gray-300);    /* Emphasized borders */
--color-border-focus:   var(--primary-500); /* Focus rings */

/* Brand */
--color-primary:        var(--primary-500); /* Primary actions */
--color-primary-hover:  var(--primary-600);
--color-primary-active: var(--primary-700);

/* Status */
--color-success:        var(--green-500);
--color-error:          var(--red-500);
--color-warning:        var(--yellow-500);
--color-info:           var(--blue-500);
```

#### Dark Theme

<!-- AI: Define dark theme overrides. Only include tokens that change between themes. -->

```css
/* Dark theme overrides - applied when [data-theme="dark"] or .dark class */

/* Backgrounds - inverted */
--color-bg-primary:     var(--gray-900);
--color-bg-secondary:   var(--gray-800);
--color-bg-tertiary:    var(--gray-700);
--color-bg-inverse:     var(--gray-50);

/* Surfaces */
--color-surface-default:  var(--gray-800);
--color-surface-hover:    var(--gray-700);
--color-surface-active:   var(--gray-600);
--color-surface-selected: var(--primary-900);

/* Text - inverted */
--color-text-primary:   var(--gray-50);
--color-text-secondary: var(--gray-300);
--color-text-tertiary:  var(--gray-400);
--color-text-disabled:  var(--gray-500);
--color-text-inverse:   var(--gray-900);
--color-text-link:      var(--primary-400);

/* Borders - adjusted for dark */
--color-border-default: var(--gray-700);
--color-border-strong:  var(--gray-600);

/* Brand - may need adjustment for dark backgrounds */
--color-primary:        var(--primary-400);
--color-primary-hover:  var(--primary-300);
--color-primary-active: var(--primary-500);
```

### Theme Implementation Guide

<!-- AI: Document how to implement light/dark mode -->

**Implementation Options**:

1. **CSS Custom Properties with data attribute**:
```css
:root { /* light theme defaults */ }
[data-theme="dark"] { /* dark overrides */ }
```

2. **CSS Custom Properties with class**:
```css
:root { /* light theme defaults */ }
.dark { /* dark overrides */ }
```

3. **CSS Custom Properties with media query**:
```css
:root { /* light theme defaults */ }
@media (prefers-color-scheme: dark) { /* dark overrides */ }
```

4. **Combined (user preference + system fallback)**:
```css
:root { /* light defaults */ }
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) { /* dark overrides */ }
}
[data-theme="dark"] { /* dark overrides */ }
```

**Recommended Approach**: [Choose one and explain why]

**Theme Switching Code**:
```javascript
// Example implementation - adapt to your framework
function setTheme(theme) {
  document.documentElement.setAttribute('data-theme', theme);
  localStorage.setItem('theme', theme);
}

// Initialize from preference
const saved = localStorage.getItem('theme');
const system = window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light';
setTheme(saved || system);
```

---

## Typography

<!-- AI: Define typography tokens for consistent text styling -->

### Font Families

<!-- AI: Define font stacks. Include fallbacks for system fonts. -->

```css
/* Primary font - body text, UI */
--font-family-sans: '[Primary Font]', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;

/* Monospace - code, technical content */
--font-family-mono: '[Mono Font]', 'SF Mono', 'Fira Code', Consolas, monospace;

/* Display/Heading - optional, for distinctive headings */
--font-family-display: '[Display Font]', var(--font-family-sans);
```

**Font Loading**:
<!-- AI: Document how fonts are loaded -->
```
[Describe font loading strategy - self-hosted, Google Fonts, system fonts, etc.]
```

### Font Sizes

<!-- AI: Define a typographic scale. Common scales:
- Major Third (1.25): 12, 15, 19, 24, 30, 37, 47
- Minor Third (1.2): 12, 14, 17, 21, 25, 30, 36
- Perfect Fourth (1.333): 12, 16, 21, 28, 37, 50
-->

```css
/* Type Scale - using [scale name, e.g., "Major Third (1.25)"] */
--font-size-xs:   0.75rem;   /* 12px - small labels, captions */
--font-size-sm:   0.875rem;  /* 14px - secondary text */
--font-size-base: 1rem;      /* 16px - body text */
--font-size-lg:   1.125rem;  /* 18px - large body, intro text */
--font-size-xl:   1.25rem;   /* 20px - h4, card titles */
--font-size-2xl:  1.5rem;    /* 24px - h3 */
--font-size-3xl:  1.875rem;  /* 30px - h2 */
--font-size-4xl:  2.25rem;   /* 36px - h1 */
--font-size-5xl:  3rem;      /* 48px - display headings */
```

### Font Weights

```css
--font-weight-normal:   400;  /* Body text */
--font-weight-medium:   500;  /* Emphasis, labels */
--font-weight-semibold: 600;  /* Subheadings */
--font-weight-bold:     700;  /* Headings, strong emphasis */
```

### Line Heights

```css
--line-height-none:    1;      /* Single line elements */
--line-height-tight:   1.25;   /* Headings */
--line-height-snug:    1.375;  /* Subheadings */
--line-height-normal:  1.5;    /* Body text */
--line-height-relaxed: 1.625;  /* Comfortable reading */
--line-height-loose:   2;      /* Spacious text */
```

### Letter Spacing

```css
--letter-spacing-tighter: -0.05em;  /* Large headings */
--letter-spacing-tight:   -0.025em; /* Headings */
--letter-spacing-normal:  0;        /* Body */
--letter-spacing-wide:    0.025em;  /* All caps labels */
--letter-spacing-wider:   0.05em;   /* Small caps */
```

### Text Styles (Compositions)

<!-- AI: Pre-composed text styles for common use cases -->

| Style | Size | Weight | Line Height | Letter Spacing | Usage |
|-------|------|--------|-------------|----------------|-------|
| Display | 5xl | bold | tight | tighter | Hero headings |
| H1 | 4xl | bold | tight | tight | Page titles |
| H2 | 3xl | semibold | tight | tight | Section headings |
| H3 | 2xl | semibold | snug | normal | Subsection headings |
| H4 | xl | semibold | snug | normal | Card titles |
| Body | base | normal | normal | normal | Main content |
| Body Small | sm | normal | normal | normal | Secondary content |
| Caption | xs | normal | normal | normal | Labels, metadata |
| Code | sm (mono) | normal | normal | normal | Inline code |

---

## Spacing

<!-- AI: Define spacing scale for margins, padding, gaps -->

### Spacing Scale

<!-- AI: Use a consistent scale. Common approaches:
- 4px base: 4, 8, 12, 16, 20, 24, 32, 40, 48, 64
- 8px base: 8, 16, 24, 32, 48, 64, 80, 96
- Tailwind-style: 0, 1, 2, 3, 4, 5, 6, 8, 10, 12, 16...
-->

```css
/* Spacing Scale - base unit: [4px/8px] */
--space-0:  0;
--space-1:  0.25rem;  /* 4px */
--space-2:  0.5rem;   /* 8px */
--space-3:  0.75rem;  /* 12px */
--space-4:  1rem;     /* 16px */
--space-5:  1.25rem;  /* 20px */
--space-6:  1.5rem;   /* 24px */
--space-8:  2rem;     /* 32px */
--space-10: 2.5rem;   /* 40px */
--space-12: 3rem;     /* 48px */
--space-16: 4rem;     /* 64px */
--space-20: 5rem;     /* 80px */
--space-24: 6rem;     /* 96px */
```

### Semantic Spacing

<!-- AI: Map spacing to semantic uses -->

```css
/* Component internal spacing */
--space-component-xs: var(--space-1);   /* Tight grouping */
--space-component-sm: var(--space-2);   /* Default internal */
--space-component-md: var(--space-3);   /* Comfortable internal */
--space-component-lg: var(--space-4);   /* Spacious internal */

/* Layout spacing */
--space-layout-sm: var(--space-4);      /* Compact layouts */
--space-layout-md: var(--space-6);      /* Default layouts */
--space-layout-lg: var(--space-8);      /* Spacious layouts */
--space-layout-xl: var(--space-12);     /* Section spacing */

/* Page margins */
--space-page-x: var(--space-4);         /* Horizontal page padding */
--space-page-y: var(--space-6);         /* Vertical page padding */
```

---

## Border Radius

```css
--radius-none: 0;
--radius-sm:   0.125rem;  /* 2px - subtle rounding */
--radius-md:   0.25rem;   /* 4px - default for inputs */
--radius-lg:   0.5rem;    /* 8px - cards, panels */
--radius-xl:   0.75rem;   /* 12px - large cards */
--radius-2xl:  1rem;      /* 16px - modals */
--radius-full: 9999px;    /* Circular - avatars, pills */
```

---

## Shadows

<!-- AI: Define elevation system for depth -->

```css
/* Elevation scale - [describe shadow style: soft, crisp, colored] */
--shadow-xs:  0 1px 2px 0 rgb(0 0 0 / 0.05);                                    /* Subtle lift */
--shadow-sm:  0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);   /* Cards */
--shadow-md:  0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1); /* Dropdowns */
--shadow-lg:  0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1); /* Popovers */
--shadow-xl:  0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1); /* Modals */
--shadow-2xl: 0 25px 50px -12px rgb(0 0 0 / 0.25);                               /* Elevated modals */
--shadow-inner: inset 0 2px 4px 0 rgb(0 0 0 / 0.05);                            /* Inset elements */
```

**Dark Theme Shadows**:
```css
/* Shadows need adjustment for dark backgrounds */
--shadow-sm: 0 1px 3px 0 rgb(0 0 0 / 0.3), 0 1px 2px -1px rgb(0 0 0 / 0.3);
/* ... adjust other shadows similarly */
```

---

## Z-Index

<!-- AI: Define z-index scale to prevent conflicts -->

```css
/* Z-Index Scale - organized by layer type */
--z-negative:  -1;      /* Behind content */
--z-base:       0;      /* Default layer */
--z-raised:    10;      /* Slightly elevated */
--z-dropdown: 100;      /* Dropdowns, select menus */
--z-sticky:   200;      /* Sticky headers */
--z-overlay:  300;      /* Modal backdrops */
--z-modal:    400;      /* Modal content */
--z-popover:  500;      /* Popovers, tooltips */
--z-toast:    600;      /* Toast notifications */
--z-max:      999;      /* Maximum (use sparingly) */
```

---

## Transitions & Animation

<!-- AI: Define motion tokens for consistent animations -->

### Durations

```css
--duration-instant:  0ms;     /* No animation */
--duration-fast:     100ms;   /* Micro-interactions (hover, focus) */
--duration-normal:   200ms;   /* Standard transitions */
--duration-slow:     300ms;   /* Emphasis, reveals */
--duration-slower:   500ms;   /* Complex animations */
```

### Easings

```css
--ease-linear:    linear;
--ease-in:        cubic-bezier(0.4, 0, 1, 1);      /* Acceleration */
--ease-out:       cubic-bezier(0, 0, 0.2, 1);      /* Deceleration */
--ease-in-out:    cubic-bezier(0.4, 0, 0.2, 1);    /* Standard */
--ease-bounce:    cubic-bezier(0.68, -0.55, 0.265, 1.55); /* Playful */
```

### Composed Transitions

```css
--transition-fast:   var(--duration-fast) var(--ease-out);
--transition-normal: var(--duration-normal) var(--ease-out);
--transition-slow:   var(--duration-slow) var(--ease-in-out);

/* Common property transitions */
--transition-colors: color var(--transition-fast), background-color var(--transition-fast), border-color var(--transition-fast);
--transition-opacity: opacity var(--transition-normal);
--transition-transform: transform var(--transition-normal);
--transition-all: all var(--transition-normal);
```

### Reduced Motion

<!-- AI: Always respect prefers-reduced-motion -->

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## Breakpoints

<!-- AI: Define responsive breakpoints -->

```css
/* Breakpoints - mobile-first approach */
--breakpoint-sm:  640px;   /* Small tablets, large phones */
--breakpoint-md:  768px;   /* Tablets */
--breakpoint-lg:  1024px;  /* Laptops, small desktops */
--breakpoint-xl:  1280px;  /* Desktops */
--breakpoint-2xl: 1536px;  /* Large desktops */
```

**Media Query Usage**:
```css
/* Mobile-first: styles apply to all, then override at breakpoints */
.element { /* mobile styles */ }

@media (min-width: 768px) {
  .element { /* tablet+ styles */ }
}

@media (min-width: 1024px) {
  .element { /* desktop+ styles */ }
}
```

---

## Component Usage Guidelines

<!-- AI: Guide for how components should use tokens -->

### Token Selection Rules

| Element | Use Token |
|---------|-----------|
| Page background | `--color-bg-primary` |
| Card background | `--color-bg-secondary` |
| Primary text | `--color-text-primary` |
| Secondary text | `--color-text-secondary` |
| Primary button bg | `--color-primary` |
| Border | `--color-border-default` |
| Focus ring | `--color-border-focus` |
| Body text size | `--font-size-base` |
| Heading size | `--font-size-xl` to `--font-size-4xl` |
| Component padding | `--space-component-*` |
| Layout gaps | `--space-layout-*` |

### Anti-Patterns

<!-- AI: Document what NOT to do -->

**Avoid**:
- Hard-coded color values (`#FF0000`) - use tokens
- Hard-coded pixel values for spacing - use token scale
- Inconsistent font sizes - stick to the scale
- Magic numbers for z-index - use token scale
- Custom transitions per component - use token compositions

---

## Implementation Formats

<!-- AI: Show how to export tokens for different platforms -->

### CSS Custom Properties

```css
:root {
  /* All tokens as CSS custom properties */
}
```

### JavaScript/TypeScript Object

```typescript
export const tokens = {
  colors: {
    primary: '#[hex]',
    // ...
  },
  spacing: {
    1: '0.25rem',
    // ...
  },
  // ...
};
```

### Tailwind Config

```javascript
module.exports = {
  theme: {
    colors: {
      primary: 'var(--color-primary)',
      // ...
    },
    // ...
  },
};
```

### Design Tool Tokens (Figma, etc.)

[Link to design file or describe token sync approach]

---

## Related Documents

<!-- AI: Link to related documents. Ensure bidirectional linking. -->

| Document | Relationship |
|----------|--------------|
| [05 - UI/UX Design](./05-ui-ux-design.md) | Visual design using these tokens |
| [06 - Component Specs](./06-component-specs.md) | Components consuming these tokens |
| [13 - Accessibility](./13-accessibility.md) | Accessibility requirements (contrast, etc.) |
| [17 - Code Patterns](./17-code-patterns.md) | Patterns for using tokens in code |

---

## AI Agent Instructions

<!-- AI: Instructions for AI agents working with this document -->

### When Populating This Document

1. **Start with brand colors**: Get primary/secondary colors from design or stakeholder
2. **Build color scale**: Generate full scale (50-900) from brand colors
3. **Test contrast**: Verify text colors meet WCAG AA (4.5:1) on background colors
4. **Define light theme first**: Then derive dark theme by inverting/adjusting
5. **Use standard scales**: Don't invent custom spacing or type scales without reason

### When Implementing Tokens

1. **Use semantic tokens in components**: Don't reference primitives directly
2. **Apply tokens consistently**: Same token for same purpose everywhere
3. **Test both themes**: Verify all components look correct in light and dark
4. **Verify reduced motion**: Test with `prefers-reduced-motion` enabled
5. **Don't override with magic values**: If a token doesn't exist, add it to this doc first

### Quality Checklist

Before marking this document complete:
- [ ] All primitive color scales defined
- [ ] Semantic color mapping for light and dark themes
- [ ] Typography scale with all text styles
- [ ] Spacing scale documented
- [ ] Theme switching approach documented
- [ ] Reduced motion handling included
- [ ] Component usage guidelines provided
- [ ] Related Documents links are bidirectional
