# 13 - Accessibility (A11y)

<!-- AI: This document defines accessibility requirements and implementation guidelines. Accessibility ensures the application is usable by people with disabilities. Applicable to all applications with user interfaces. -->

## Accessibility Philosophy

<!-- AI: Establish accessibility principles for the project:

**Why Accessibility Matters**:
- Ethical: Everyone deserves equal access
- Legal: Many jurisdictions require accessibility (ADA, EAA, Section 508)
- Business: Expands potential user base
- Quality: Accessible code is often better code

**Key Questions**:
- What's the target compliance level?
- Who are the users with accessibility needs?
- What assistive technologies should be supported?
-->

**Philosophy**: [Describe the accessibility commitment for this project]

**Target Compliance**: WCAG 2.1 Level [AA / AAA]

**Supported Assistive Technologies**:
- [ ] Screen readers (NVDA, VoiceOver, JAWS)
- [ ] Keyboard-only navigation
- [ ] Screen magnifiers
- [ ] Voice control
- [ ] Switch devices

---

## WCAG Guidelines Overview

<!-- AI: Reference the Web Content Accessibility Guidelines. WCAG is organized around four principles: POUR.

**Perceivable**: Information must be presentable in ways users can perceive
**Operable**: Interface components must be operable
**Understandable**: Information and operation must be understandable
**Robust**: Content must be robust enough for assistive technologies
-->

### Compliance Levels

| Level | Description | Target? |
|-------|-------------|---------|
| A | Minimum accessibility | Required baseline |
| AA | Addresses major barriers | [Recommended target] |
| AAA | Highest accessibility | May be impractical for all content |

### Key Requirements by Level

<!-- AI: Highlight the most relevant requirements -->

**Level A (Must Have)**:
- [ ] All non-text content has text alternatives
- [ ] Color is not the only means of conveying information
- [ ] All functionality available from keyboard
- [ ] Content does not cause seizures (no flashing > 3 times/sec)
- [ ] Bypass blocks available (skip navigation)

**Level AA (Should Have)**:
- [ ] Captions for live audio
- [ ] Sufficient color contrast (4.5:1 for text)
- [ ] Text resizable to 200% without loss
- [ ] Multiple ways to find pages
- [ ] Visible focus indicators
- [ ] Consistent navigation

**Level AAA (Nice to Have)**:
- [ ] Sign language interpretation
- [ ] Extended audio description
- [ ] Higher contrast (7:1)
- [ ] No timing limits
- [ ] Reading level guidance

---

## Keyboard Navigation

<!-- AI: Keyboard accessibility is critical - many users cannot use a mouse -->

### Keyboard Navigation Principles

**Essential Rules**:
1. All interactive elements must be reachable via keyboard
2. Focus order must be logical (usually top-to-bottom, left-to-right)
3. Focus must be visible at all times
4. Users should be able to escape any component
5. Custom components must implement expected keyboard patterns

### Focus Management

<!-- AI: How focus moves through the interface -->

**Focus Order**:
<!-- AI: Document the logical focus order for the main page/views -->

1. Skip link (if present)
2. [Primary navigation]
3. [Main content]
4. [Secondary content/sidebar]
5. [Footer]

**Focus Trapping** (for modals/dialogs):
- Focus must stay within modal while open
- First focusable element receives focus on open
- Focus returns to trigger element on close
- Escape key closes the modal

**Programmatic Focus**:
- Move focus to new content when navigating (SPA)
- Move focus to error messages when validation fails
- Announce dynamic content changes

### Focus Indicators

<!-- AI: How focus is visually indicated -->

**Requirements**:
- Focus indicator must be visible on all interactive elements
- Must have minimum 3:1 contrast against adjacent colors
- Must not rely on color alone (shape/outline recommended)

**Implementation**:
```css
/* Example focus style */
:focus-visible {
  outline: 2px solid [focus-color];
  outline-offset: 2px;
}

/* Remove default only if custom style provided */
:focus:not(:focus-visible) {
  outline: none;
}
```

**Focus Indicator Design**:
| Element Type | Focus Style | Notes |
|--------------|-------------|-------|
| Buttons | [Outline style] | Clear, high contrast |
| Links | [Outline style] | Match or complement button style |
| Inputs | [Border/ring style] | Distinguishable from focus |
| Cards | [Border/shadow] | Visible on entire element |

### Keyboard Shortcuts

<!-- AI: Document application keyboard shortcuts.

**Best Practices**:
- Don't override browser shortcuts
- Make shortcuts discoverable (help menu)
- Provide single-key shortcuts cautiously (can conflict with screen readers)
- Support standard shortcuts (Ctrl+S for save, etc.)
-->

#### Global Shortcuts

| Action | Shortcut | Notes |
|--------|----------|-------|
| Open keyboard shortcut help | `?` or `F1` | Show all shortcuts |
| [Primary action] | [Shortcut] | [Notes] |
| [Secondary action] | [Shortcut] | [Notes] |

#### Navigation Shortcuts

| Action | Shortcut | Notes |
|--------|----------|-------|
| Skip to main content | `Alt+1` / Skip link | Bypass navigation |
| [Navigation action] | [Shortcut] | [Notes] |

#### Common Patterns

| Context | Action | Key(s) |
|---------|--------|--------|
| Dialogs | Close | `Escape` |
| Menus | Close | `Escape` |
| Menus | Navigate | Arrow keys |
| Menus | Select | `Enter` / `Space` |
| Tabs | Switch tab | Arrow keys |
| Trees | Expand/collapse | Arrow keys |
| Grids | Navigate cells | Arrow keys |

---

## Screen Reader Support

<!-- AI: Ensure content is accessible to screen reader users -->

### Semantic HTML

<!-- AI: Use native HTML elements correctly - they have built-in accessibility -->

**Use Native Elements**:
| Purpose | Correct | Avoid |
|---------|---------|-------|
| Button | `<button>` | `<div onclick>` |
| Link | `<a href>` | `<span onclick>` |
| Heading | `<h1>`-`<h6>` | `<div class="heading">` |
| List | `<ul>`, `<ol>`, `<li>` | `<div>` with bullets |
| Table | `<table>`, `<th>`, `<td>` | CSS grid for data |
| Form field | `<input>`, `<select>` | Custom divs |

**Document Structure**:
- One `<main>` element per page
- Use `<nav>` for navigation regions
- Use `<header>` and `<footer>` for page regions
- Use `<aside>` for complementary content
- Use `<section>` or `<article>` for content regions

**Heading Hierarchy**:
- Start with `<h1>` (one per page)
- Don't skip levels (h1 -> h2 -> h3, not h1 -> h3)
- Headings should describe content below them

### ARIA (Accessible Rich Internet Applications)

<!-- AI: ARIA adds accessibility to custom components, but use sparingly.

**First Rule of ARIA**: Don't use ARIA if native HTML will do the job.
ARIA doesn't add functionality, only accessibility information.
-->

#### ARIA Roles

<!-- AI: Roles define what an element is -->

**Common Widget Roles**:
| Role | Use For | Notes |
|------|---------|-------|
| `button` | Clickable elements | Prefer `<button>` element |
| `link` | Navigation elements | Prefer `<a>` element |
| `dialog` | Modal dialogs | Use with `aria-modal="true"` |
| `alertdialog` | Dialogs requiring response | Use for important messages |
| `menu` | Dropdown menus | With `menuitem` children |
| `tablist` / `tab` / `tabpanel` | Tab interfaces | Manage with arrow keys |
| `tree` / `treeitem` | Hierarchical lists | Expandable/collapsible |

**Landmark Roles** (use HTML5 elements when possible):
| Role | HTML5 Equivalent | Purpose |
|------|------------------|---------|
| `banner` | `<header>` | Page header |
| `navigation` | `<nav>` | Navigation links |
| `main` | `<main>` | Main content |
| `complementary` | `<aside>` | Supporting content |
| `contentinfo` | `<footer>` | Page footer |
| `search` | `<search>` | Search functionality |

#### ARIA Properties

<!-- AI: Properties describe element characteristics -->

**Essential Properties**:
| Property | Purpose | Example |
|----------|---------|---------|
| `aria-label` | Invisible label | `aria-label="Close dialog"` |
| `aria-labelledby` | Reference visible label | `aria-labelledby="title-id"` |
| `aria-describedby` | Additional description | `aria-describedby="help-text-id"` |
| `aria-required` | Mark required fields | `aria-required="true"` |
| `aria-invalid` | Mark invalid fields | `aria-invalid="true"` |
| `aria-hidden` | Hide from screen readers | `aria-hidden="true"` |

#### ARIA States

<!-- AI: States change based on user interaction -->

| State | Purpose | Values |
|-------|---------|--------|
| `aria-expanded` | Expandable elements | `true` / `false` |
| `aria-selected` | Selected state | `true` / `false` |
| `aria-pressed` | Toggle button state | `true` / `false` / `mixed` |
| `aria-checked` | Checkbox/radio state | `true` / `false` / `mixed` |
| `aria-disabled` | Disabled state | `true` / `false` |
| `aria-current` | Current item | `page` / `step` / `true` |

### Live Regions

<!-- AI: Announce dynamic content changes to screen readers -->

**Live Region Types**:
| Type | Attribute | Use For |
|------|-----------|---------|
| Polite | `aria-live="polite"` | Non-urgent updates (wait for pause) |
| Assertive | `aria-live="assertive"` | Urgent updates (interrupt) |
| Alert | `role="alert"` | Error messages (assertive by default) |
| Status | `role="status"` | Status updates (polite by default) |
| Log | `role="log"` | Chat messages, activity logs |

**Best Practices**:
- Use `polite` by default, `assertive` sparingly
- Don't announce too frequently (overwhelming)
- Keep announcements concise
- Live region must exist in DOM before content changes

**Implementation Examples**:
```html
<!-- Status message area -->
<div role="status" aria-live="polite" class="sr-only">
  <!-- Content updated dynamically -->
</div>

<!-- Error announcement -->
<div role="alert" aria-live="assertive">
  Error: Please fix the form errors below.
</div>
```

### Screen Reader Testing

<!-- AI: How to test with screen readers -->

**Primary Screen Readers**:
| Platform | Screen Reader | Browser | Notes |
|----------|---------------|---------|-------|
| Windows | NVDA | Firefox/Chrome | Free, widely used |
| Windows | JAWS | Chrome/IE | Paid, enterprise standard |
| macOS | VoiceOver | Safari | Built-in |
| iOS | VoiceOver | Safari | Built-in |
| Android | TalkBack | Chrome | Built-in |

**Testing Checklist**:
- [ ] All content is announced
- [ ] Focus order matches visual order
- [ ] Interactive elements are operable
- [ ] Form labels are announced
- [ ] Error messages are announced
- [ ] Dynamic content changes are announced
- [ ] Images have alt text (or are hidden)

---

## Color and Contrast

<!-- AI: Ensure visual content is perceivable by users with low vision or color blindness -->

### Contrast Requirements

| Content Type | WCAG AA | WCAG AAA |
|--------------|---------|----------|
| Normal text (<18px or <14px bold) | 4.5:1 | 7:1 |
| Large text (>=18px or >=14px bold) | 3:1 | 4.5:1 |
| UI components and graphics | 3:1 | Not defined |
| Focus indicators | 3:1 | Not defined |

### Color Combinations

<!-- AI: Document and verify color combinations used in the app -->

| Usage | Foreground | Background | Ratio | Pass? |
|-------|------------|------------|-------|-------|
| Body text | [Color] | [Color] | [X]:1 | [AA/AAA] |
| Headings | [Color] | [Color] | [X]:1 | [AA/AAA] |
| Links | [Color] | [Color] | [X]:1 | [AA/AAA] |
| Buttons | [Color] | [Color] | [X]:1 | [AA/AAA] |
| Error text | [Color] | [Color] | [X]:1 | [AA/AAA] |

### Color Contrast Tools

<!-- AI: Tools for checking and ensuring color contrast -->

**Online Tools**:
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [Colorable](https://colorable.jxnblk.com/)
- [Contrast Ratio](https://contrast-ratio.com/)

**Browser Extensions**:
- axe DevTools
- WAVE
- Lighthouse

**Design Tools**:
- Figma: Stark, Contrast plugins
- Sketch: Stark plugin
- Adobe: Built-in contrast checker

### Color Independence

<!-- AI: Don't rely on color alone to convey information -->

**Requirements**:
- Color must not be the only indicator of:
  - Errors (add icon + text)
  - Required fields (add asterisk + text)
  - Status (add icon + label)
  - Links (underline or other indicator)
  - Selection state (border/icon)

**Examples**:
| Bad | Good |
|-----|------|
| Red border only for errors | Red border + error icon + error text |
| Green/red status dots | Dots + "Active"/"Inactive" labels |
| Blue links with no underline | Underlined links or icon indicator |

### Color Blindness Considerations

<!-- AI: Design for common color vision deficiencies -->

**Avoid Problematic Combinations**:
- Red/Green (most common deficiency)
- Blue/Yellow
- Blue/Purple

**Testing**:
- Use simulators (Chrome DevTools, Figma plugins)
- Test with grayscale view
- Ensure icons/patterns supplement color

---

## Motion and Animation

<!-- AI: Animations can cause problems for users with vestibular disorders or cognitive disabilities -->

### Reduced Motion

<!-- AI: Respect user preference for reduced motion -->

**Implementation**:
```css
/* Default: animate */
.element {
  transition: transform 0.3s ease;
}

/* Reduced motion preference */
@media (prefers-reduced-motion: reduce) {
  .element {
    transition: none;
  }

  /* Or provide alternative */
  .element {
    transition: opacity 0.1s;
  }
}
```

**JavaScript Detection**:
```javascript
const prefersReducedMotion = window.matchMedia(
  '(prefers-reduced-motion: reduce)'
).matches;
```

### Animation Guidelines

**Safe Animations**:
- Opacity changes
- Color transitions
- Small movements (< 100px)
- Short duration (< 0.3s)

**Potentially Problematic**:
- Parallax effects
- Large movements
- Spinning/rotating
- Infinite animations
- Auto-playing video

**Best Practices**:
- Provide controls to pause/stop animations
- Avoid content that flashes > 3 times per second
- Keep animations brief and purposeful
- Offer reduced motion alternative

---

## Forms and Inputs

<!-- AI: Forms have specific accessibility requirements -->

### Form Labels

**Requirements**:
- Every input must have a label
- Labels must be programmatically associated
- Placeholder text is not a substitute for labels

**Association Methods**:
```html
<!-- Method 1: for/id (recommended) -->
<label for="email">Email</label>
<input type="email" id="email">

<!-- Method 2: Wrapping -->
<label>
  Email
  <input type="email">
</label>

<!-- Method 3: aria-labelledby -->
<span id="email-label">Email</span>
<input type="email" aria-labelledby="email-label">

<!-- Method 4: aria-label (invisible label) -->
<input type="search" aria-label="Search">
```

### Error Messages

**Requirements**:
- Errors must be announced to screen readers
- Error must be associated with the field
- Error must be visible and clear

**Implementation**:
```html
<label for="email">Email</label>
<input
  type="email"
  id="email"
  aria-invalid="true"
  aria-describedby="email-error"
>
<span id="email-error" role="alert">
  Please enter a valid email address.
</span>
```

### Required Fields

**Indication Methods**:
- Visual indicator (asterisk *)
- Text indication (include "required" in label or helper text)
- `aria-required="true"` for programmatic indication
- Native `required` attribute when using HTML5 validation

### Input Instructions

- Provide format hints (e.g., "YYYY-MM-DD")
- Use `aria-describedby` to associate instructions
- Keep instructions visible, not just in placeholders

---

## Images and Media

<!-- AI: Non-text content needs text alternatives -->

### Image Alt Text

**Guidelines**:
| Image Type | Alt Text |
|------------|----------|
| Informative | Describe the information conveyed |
| Decorative | Empty alt (`alt=""`) or CSS background |
| Functional (links/buttons) | Describe the action |
| Complex (charts/graphs) | Brief summary + long description |

**Examples**:
```html
<!-- Informative -->
<img src="chart.png" alt="Sales increased 50% from Q1 to Q2">

<!-- Decorative -->
<img src="divider.png" alt="">

<!-- Functional -->
<a href="home.html">
  <img src="logo.png" alt="Return to homepage">
</a>

<!-- Complex -->
<figure>
  <img src="data-chart.png" alt="Quarterly sales chart" aria-describedby="chart-desc">
  <figcaption id="chart-desc">
    Sales data showing Q1: $100K, Q2: $150K, Q3: $175K, Q4: $200K.
    <a href="sales-data.html">View full data table</a>
  </figcaption>
</figure>
```

### Video and Audio

**Requirements**:
- Captions for video with audio
- Transcript for audio-only content
- Audio description for important visual content
- No autoplay (or provide pause control)
- Volume control accessible by keyboard

---

## Accessibility by Platform

<!-- AI: Platform-specific accessibility considerations -->

### Web Applications

- Use semantic HTML
- Ensure SPA announcements for navigation
- Test with multiple browsers/screen readers
- Implement skip links for navigation

### Desktop Applications

- Follow platform accessibility APIs (Windows, macOS)
- Support system high contrast modes
- Respect system font size settings
- Support keyboard shortcuts

### Mobile Applications

- Follow platform guidelines (iOS, Android)
- Ensure touch targets are large enough (44x44px minimum)
- Support system accessibility settings
- Test with platform screen readers

### CLI Applications

- Provide clear, parseable output
- Support screen reader-friendly output modes
- Use exit codes for status
- Avoid color as only indicator

---

## Testing and Validation

<!-- AI: How to test accessibility -->

### Automated Testing

**Tools**:
| Tool | Type | Notes |
|------|------|-------|
| axe DevTools | Browser extension | Comprehensive, actionable |
| WAVE | Browser extension | Visual feedback |
| Lighthouse | Browser DevTools | Built into Chrome |
| eslint-plugin-jsx-a11y | Linter | Catch issues in code |
| @axe-core/react | Runtime | Test in development |

**Limitations**:
- Automated tests catch ~30-50% of issues
- Cannot assess usability or quality of alt text
- May miss context-dependent issues
- Must be combined with manual testing

### Manual Testing

**Keyboard Testing Checklist**:
- [ ] Tab through entire page - all interactive elements reachable
- [ ] Focus order logical
- [ ] Focus visible at all times
- [ ] Can escape any component (modals, menus)
- [ ] Enter/Space activate buttons
- [ ] Arrow keys work in menus, tabs, etc.

**Screen Reader Testing Checklist**:
- [ ] Page title announced
- [ ] Headings announced with correct levels
- [ ] Images have appropriate alt text
- [ ] Form fields have labels
- [ ] Error messages announced
- [ ] Dynamic content changes announced
- [ ] Tables announced correctly

**Visual Testing Checklist**:
- [ ] Works at 200% zoom
- [ ] Works with system high contrast
- [ ] Color contrast sufficient
- [ ] Focus indicators visible
- [ ] No information lost without color

### Testing Schedule

| Type | Frequency | By Whom |
|------|-----------|---------|
| Automated (CI) | Every build | Automated |
| Manual keyboard | Every feature | Developer |
| Screen reader | Before release | QA/Developer |
| User testing | Quarterly | Accessibility specialist |

---

## Implementation Checklist

<!-- AI: Pre-release accessibility checklist -->

### Development
- [ ] Semantic HTML used throughout
- [ ] All images have appropriate alt text
- [ ] All forms have labels
- [ ] Focus order is logical
- [ ] Focus indicators visible
- [ ] Color contrast meets requirements
- [ ] Reduced motion respected

### Testing
- [ ] Automated accessibility tests pass
- [ ] Keyboard navigation tested
- [ ] Screen reader tested
- [ ] Zoom to 200% tested
- [ ] High contrast mode tested

### Documentation
- [ ] Keyboard shortcuts documented
- [ ] Accessibility statement published (if required)
- [ ] Known issues documented

---

## Related Documents

<!-- AI: Link to related documents. Ensure bidirectional linking. -->

| Document | Relationship |
|----------|--------------|
| [05 - UI/UX Design](./05-ui-ux-design.md) | User interface design |
| [16 - Design Tokens](./16-design-tokens.md) | Color and spacing tokens |
| [06 - Component Specs](./06-component-specs.md) | Component accessibility requirements |
| [10 - Error Handling](./10-error-handling.md) | Accessible error presentation |
| [12 - Testing Strategy](./12-testing-strategy.md) | Accessibility testing approach |

---

## AI Agent Instructions

<!-- AI: Instructions for AI agents working with this document -->

### When Populating This Document

1. **Start from UI design**: Reference doc 05 to understand interface structure
2. **Identify interactive elements**: List all buttons, links, forms, custom widgets
3. **Define keyboard patterns**: Document how each component is keyboard accessible
4. **Check color usage**: Audit color combinations from doc 16 for contrast
5. **Plan screen reader support**: Document ARIA usage for custom components

### When Implementing Accessibility

1. **Use semantic HTML first**: Don't reach for ARIA until native HTML is exhausted
2. **Test as you build**: Run axe DevTools frequently during development
3. **Keyboard test every component**: Tab through, escape out, verify focus
4. **Write meaningful alt text**: Describe information, not appearance
5. **Announce dynamic content**: Add live regions for async updates

### Common Mistakes to Avoid

- **Div soup**: Using `<div>` for everything instead of semantic elements
- **Unlabeled inputs**: Inputs without associated `<label>` elements
- **Mouse-only interactions**: Hover states without keyboard equivalent
- **Color-only information**: Using red/green without icons or text
- **Hidden focus**: Removing focus outlines without replacement
- **Autoplaying media**: Unexpected audio without controls
- **ARIA overuse**: Adding ARIA to native elements that don't need it

### Quality Checklist

Before marking this document complete:
- [ ] Target WCAG level defined
- [ ] Keyboard navigation documented
- [ ] Focus management rules established
- [ ] ARIA patterns documented for custom components
- [ ] Color contrast verified
- [ ] Motion/animation guidelines set
- [ ] Testing approach defined
- [ ] Related Documents links are bidirectional
