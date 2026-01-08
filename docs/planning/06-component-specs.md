# 06 - Component Specs

<!-- AI: This document defines the UI components that make up the application. Use this for any project with a graphical user interface. Skip for CLI tools, background services, or pure APIs without UI. -->

## Component Architecture Overview

<!-- AI: Provide context for the component architecture:
- What component model/library is being used (React, Vue, Svelte, Web Components, SwiftUI, Jetpack Compose, etc.)
- Component organization strategy (atomic design, feature-based, domain-driven)
- Shared component philosophy (design system, UI library, custom components)
-->

### Component Model

<!-- AI: Document the component technology and paradigm:

**Framework Examples**:
- React: Function components with hooks, JSX
- Vue: Single File Components (.vue), Composition API or Options API
- Svelte: .svelte files with reactive declarations
- Angular: TypeScript classes with decorators
- SwiftUI: View protocol, declarative Swift
- Jetpack Compose: @Composable functions, Kotlin

**Paradigm**:
- Declarative (React, Vue, Svelte, SwiftUI)
- Component-based (all modern frameworks)
- Reactive (Vue, Svelte, Solid)
-->

**Framework**: [Framework name and version]

**Component Format**: [File format and conventions, e.g., ".tsx files with named exports"]

**State Management**: [How components manage state - props drilling, context, external store]

### Component Organization

<!-- AI: Document how components are organized in the codebase:

**Common Strategies**:
- **Atomic Design**: atoms → molecules → organisms → templates → pages
- **Feature-based**: Group by feature/domain, each feature has its own components
- **Type-based**: components/buttons, components/forms, components/layout
- **Flat**: All components in one folder (small projects only)

Choose based on project size:
- Small (<20 components): Flat or simple type-based
- Medium (20-100 components): Feature-based or atomic
- Large (100+ components): Atomic design or domain-driven
-->

**Strategy**: [Organization strategy name]

**Folder Structure**:
```
[Describe component folder structure, e.g.:]
src/components/
├── shared/           # Reusable across features
├── features/         # Feature-specific components
│   ├── auth/
│   └── dashboard/
└── layout/           # Layout components
```

---

## Component Hierarchy

<!-- AI: Document the component tree showing parent-child relationships. This provides a map of how components compose together.

Keep abstract - use descriptive names, not implementation details.

Format:
```
AppRoot
├── LayoutShell
│   ├── Header
│   │   ├── Logo
│   │   ├── Navigation
│   │   └── UserMenu
│   ├── MainContent
│   │   └── [Page-specific content]
│   └── Footer
├── ModalContainer
│   └── [Dynamic modals]
└── ToastContainer
    └── [Dynamic toasts]
```
-->

```
[Component hierarchy diagram]
```

### Hierarchy Notes

<!-- AI: Add notes explaining:
- Why certain components are siblings vs nested
- Which components are rendered conditionally
- Which components are instantiated dynamically (lists, modals)
-->

- [Note about hierarchy decisions]

---

## Component Categories

<!-- AI: Group components by purpose. This helps developers find the right component and understand where new components should go.

**Standard Categories**:
- **Layout**: Page structure, grids, containers, spacing
- **Navigation**: Menus, tabs, breadcrumbs, pagination
- **Forms**: Inputs, selects, checkboxes, form groups, validation
- **Feedback**: Alerts, toasts, modals, loading states
- **Data Display**: Tables, lists, cards, badges, avatars
- **Actions**: Buttons, links, icon buttons, FABs
- **Overlays**: Modals, drawers, popovers, tooltips
-->

| Category | Components | Description |
|----------|------------|-------------|
| Layout | [Component list] | [Category purpose] |
| Navigation | [Component list] | [Category purpose] |
| Forms | [Component list] | [Category purpose] |
| Feedback | [Component list] | [Category purpose] |
| Data Display | [Component list] | [Category purpose] |
| Actions | [Component list] | [Category purpose] |
| Overlays | [Component list] | [Category purpose] |
| [Custom Category] | [Component list] | [Category purpose] |

---

## Shared/Base Components

<!-- AI: Document reusable base components that appear throughout the application. These form the building blocks for feature-specific components. -->

### Button

<!-- AI: Document button component with all variants. This is an example template - repeat similar structure for other shared components. -->

**Purpose**: Trigger actions when clicked/pressed

**Variants**:
| Variant | Usage |
|---------|-------|
| Primary | Main call-to-action, one per screen section |
| Secondary | Supporting actions |
| Ghost/Text | Low-emphasis actions, inline actions |
| Danger | Destructive actions (delete, remove) |
| Icon-only | Toolbar actions, compact UI |

**Sizes**:
| Size | Height | Use Case |
|------|--------|----------|
| Small (sm) | [X]px | Dense UI, tables, inline |
| Medium (md) | [X]px | Default, most contexts |
| Large (lg) | [X]px | Primary CTAs, mobile touch targets |

**States**:
- Default, Hover, Focus, Active, Disabled, Loading

**Props** (Example - React):
<!-- AI: Adapt prop table format to your framework:
- React: Props interface with types
- Vue: defineProps with types
- Svelte: export let declarations
- Angular: @Input() decorators
-->

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| variant | 'primary' \| 'secondary' \| 'ghost' \| 'danger' | No | 'primary' | Visual style |
| size | 'sm' \| 'md' \| 'lg' | No | 'md' | Button size |
| disabled | boolean | No | false | Disable interaction |
| loading | boolean | No | false | Show loading spinner |
| onClick | () => void | No | - | Click handler |
| children | ReactNode | Yes | - | Button content |

### Input

<!-- AI: Document input component. -->

**Purpose**: Accept text input from users

**Types**:
| Type | Usage |
|------|-------|
| Text | General text input |
| Password | Masked input for secrets |
| Email | Email with validation hints |
| Number | Numeric input with increment/decrement |
| Search | Search with clear button |
| Textarea | Multi-line text |

**States**:
- Default, Focus, Filled, Error, Disabled, Read-only

**Props**:
| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| type | 'text' \| 'password' \| 'email' \| 'number' \| 'search' | No | 'text' | Input type |
| value | string | Yes | - | Current value |
| onChange | (value: string) => void | Yes | - | Value change handler |
| placeholder | string | No | - | Placeholder text |
| error | string | No | - | Error message to display |
| disabled | boolean | No | false | Disable input |

### [Additional Shared Components]

<!-- AI: Document other shared components using the same structure:
- Select/Dropdown
- Checkbox
- Radio
- Toggle/Switch
- Modal
- Toast/Notification
- Card
- Badge
- Avatar
- Tooltip
- Tabs
- Accordion
- Table (if applicable)

For each, include: Purpose, Variants, States, Props
-->

---

## Feature Components

<!-- AI: Document components specific to application features. These are composed from shared components and implement business logic. -->

### Feature: [Feature Name]

<!-- AI: Group components by the feature they belong to. Reference doc 04 Feature Breakdown for feature definitions. -->

#### [FeatureComponent Name]

**Purpose**: [What this component does in the context of the feature]

**Location**: `[Path in codebase]`

**Composition**:
<!-- AI: List which shared/other components this uses -->
- Uses: [SharedComponent1], [SharedComponent2]

**Props**:
| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| [prop] | [type] | [Yes/No] | [default] | [description] |

**Internal State**:
<!-- AI: Document state managed within this component -->
| State | Type | Purpose |
|-------|------|---------|
| [state] | [type] | [what it tracks] |

**Events Emitted**:
<!-- AI: Document callbacks/events this component can trigger -->
| Event | Payload | When Triggered |
|-------|---------|----------------|
| [onEvent] | [payload type] | [trigger condition] |

**Behavior**:
<!-- AI: Describe key behaviors, interactions, and side effects -->
- [Behavior 1]
- [Behavior 2]

**Example Usage**:
```[language]
[Code example showing typical usage]
```

### Feature: [Next Feature]

<!-- AI: Repeat structure for each feature area -->

---

## Component Documentation Standards

<!-- AI: Define how components should be documented in code. Consistent documentation helps both humans and AI agents understand components. -->

### Code Documentation Format

<!-- AI: Choose documentation format based on framework:
- JSDoc (JavaScript/TypeScript)
- TSDoc (TypeScript)
- Vue component comments
- SwiftUI documentation comments
- KDoc (Kotlin/Compose)
-->

**Format**: [JSDoc/TSDoc/Other]

**Required Documentation**:
```[language]
/**
 * [Component description - what it does, when to use it]
 *
 * @example
 * [Usage example]
 *
 * @param props - Component props
 * @param props.[propName] - [Prop description]
 */
```

### Prop Documentation Requirements

<!-- AI: Define what must be documented for each prop -->

Every prop must have:
- [ ] Type annotation (in code)
- [ ] Description (in JSDoc/comments)
- [ ] Default value documented (if optional)
- [ ] Validation constraints noted (min/max, patterns)

### Storybook/Documentation Site

<!-- AI: If using component documentation tools like Storybook, Docz, or Histoire, document the approach -->

**Tool**: [Storybook/Histoire/Docz/None]

**Story Requirements**:
- [ ] Default state story
- [ ] All variant stories
- [ ] Interactive controls
- [ ] Accessibility annotations

---

## Component Reusability Guidelines

<!-- AI: Document principles for creating reusable components -->

### When to Create a New Component

<!-- AI: Help developers decide when to extract a new component -->

Create a new component when:
- [ ] **Used 3+ times**: Same UI pattern appears in multiple places
- [ ] **Standalone concept**: Has clear, single responsibility
- [ ] **Complex logic**: Contains significant state or effects
- [ ] **Testing boundary**: Needs isolated testing

Do NOT create a new component when:
- [ ] Only used once and simple
- [ ] Would require many configuration props for different uses
- [ ] Just to reduce file length (use sections/comments instead)

### Component API Design Principles

<!-- AI: Document principles for designing component interfaces -->

1. **Prop Naming**:
   - Use camelCase for all props
   - Boolean props: `isX`, `hasX`, `canX`, `shouldX`
   - Event handlers: `onX` (onClick, onChange, onSubmit)
   - Render props: `renderX` (renderHeader, renderItem)

2. **Composition over Configuration**:
   - Prefer children/slots over many configuration props
   - Use compound components for complex widgets (e.g., Tabs + Tab + TabPanel)

3. **Sensible Defaults**:
   - Every optional prop should have a sensible default
   - Components should work with minimal props

4. **Escape Hatches**:
   - Allow className/style overrides for customization
   - Spread remaining props to root element

### Accessibility Requirements

<!-- AI: Document accessibility requirements for components. Reference doc 13 for full details. -->

All interactive components must:
- [ ] Be keyboard accessible (focusable, operable with keyboard)
- [ ] Have appropriate ARIA attributes
- [ ] Maintain visible focus indicators
- [ ] Support screen reader announcements
- [ ] Meet color contrast requirements (4.5:1 for text)

---

## Component State Patterns

<!-- AI: Document patterns for managing state within and across components -->

### Local State

<!-- AI: When and how to use component-local state -->

**Use local state for**:
- UI-only state (open/closed, hover, focus)
- Form input values before submission
- Transient state that doesn't affect other components

**Example** (React):
```jsx
const [isOpen, setIsOpen] = useState(false);
```

### Shared State

<!-- AI: Patterns for sharing state between components -->

**Prop Drilling**: Pass through 1-2 levels max
- Good for: Simple parent-child relationships
- Avoid when: Props pass through components that don't use them

**Context/Provider** (React Context, Vue provide/inject):
- Good for: Theme, auth, localization, deeply nested shared state
- Avoid when: State changes frequently (performance)

**External Store** (Redux, Zustand, Pinia, Vuex):
- Good for: Complex app state, time-travel debugging needed
- Avoid when: Simple apps, prototype stage

### Derived State

<!-- AI: How to handle computed/derived values -->

- Compute in render when cheap
- Use memoization (useMemo, computed) when expensive
- Never store derived state in state (source of bugs)

---

## Related Documents

<!-- AI: Link to related documents. Ensure bidirectional linking. -->

| Document | Relationship |
|----------|--------------|
| [05 - UI/UX Design](./05-ui-ux-design.md) | Visual designs these components implement |
| [16 - Design Tokens](./16-design-tokens.md) | Design values components consume |
| [17 - Code Patterns](./17-code-patterns.md) | Implementation patterns for components |
| [15 - File Architecture](./15-file-architecture.md) | Where component files live |
| [13 - Accessibility](./13-accessibility.md) | Accessibility requirements for components |

---

## AI Agent Instructions

<!-- AI: Instructions for AI agents working with this document -->

### When Populating This Document

1. **Start from UI/UX Design**: Reference doc 05 to understand what components are needed
2. **Identify shared components first**: Look for patterns that repeat across screens
3. **Use consistent prop naming**: Follow the naming conventions defined in this doc
4. **Document behavior, not implementation**: Describe what a component does, not how it's coded
5. **Keep hierarchy updated**: As you add components, update the hierarchy diagram

### When Implementing Components

1. **Check for existing components**: Search this doc before creating new components
2. **Follow the documented API**: Implement props and events as specified
3. **Match the variants**: Ensure all documented variants are implemented
4. **Test accessibility**: Every component should meet the accessibility requirements listed
5. **Update this doc**: If implementation requires API changes, update this doc first

### Quality Checklist

Before marking this document complete:
- [ ] Component hierarchy covers all screens from doc 05
- [ ] All shared components have complete prop documentation
- [ ] All feature components are linked to features in doc 04
- [ ] Reusability guidelines are clear and actionable
- [ ] State patterns are documented with examples
- [ ] Related Documents links are bidirectional
