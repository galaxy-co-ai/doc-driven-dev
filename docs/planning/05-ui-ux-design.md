# 05 - UI/UX Design

<!-- AI: This document captures the visual design and user experience decisions for projects with a user interface. Skip this document for CLI tools, background services, or pure APIs. -->

## Design Overview

<!-- AI: Provide a brief summary of the design direction. Include:
- Visual style (modern, minimal, playful, professional, etc.)
- Target platforms (web browser, desktop app, mobile app, etc.)
- Key design principles guiding decisions (e.g., "simplicity over features", "data density", "progressive disclosure")
-->

### Design Philosophy

<!-- AI: Describe the core principles driving UI decisions. Example prompts to answer:
- What feeling should users have when using this product?
- What existing products inspire this design? Why?
- What trade-offs are acceptable? (e.g., "beauty over speed", "density over whitespace")
-->

[Design philosophy and inspirations]

### Platform Targets

<!-- AI: List all platforms this UI will run on. For each platform, note specific considerations:
- **Web (Browser)**: Which browsers? Responsive or fixed width?
- **Desktop (Native)**: Window management? System tray? Menu bar?
- **Mobile (Native)**: iOS guidelines? Android Material Design? Both?
- **Progressive Web App**: Offline support? Install prompts?
-->

| Platform | Considerations |
|----------|----------------|
| [Platform 1] | [Specific considerations] |
| [Platform 2] | [Specific considerations] |

---

## Layout Structure

<!-- AI: Document the primary layout structure. Use ASCII wireframes for quick reference. Create separate wireframes for each major platform if layouts differ significantly. -->

### Primary Layout

<!-- AI: Draw the main application layout using ASCII art. Include:
- Major regions/zones (header, sidebar, main content, footer)
- Navigation elements
- Key interactive areas

Keep it abstract - use zone names, not specific component names.

Example format:
```
┌─────────────────────────────────────────────────────────┐
│  [Header Zone]                                          │
├──────────────┬──────────────────────────────────────────┤
│              │                                          │
│  [Nav Zone]  │         [Main Content Zone]              │
│              │                                          │
│              │                                          │
├──────────────┴──────────────────────────────────────────┤
│  [Footer Zone]                                          │
└─────────────────────────────────────────────────────────┘
```
-->

```
[ASCII layout diagram]
```

### Layout Variants

<!-- AI: If the layout changes significantly for different contexts (e.g., logged-in vs logged-out, mobile vs desktop), document each variant with its own diagram. -->

#### Variant: [Context Name]
```
[ASCII layout diagram for this variant]
```

---

## Wireframes

<!-- AI: Create wireframes for each major screen/view. Start with low-fidelity ASCII, then reference external tools for detailed mockups. -->

### Wireframing Approach

<!-- AI: Document your wireframing strategy:

**Fidelity Levels**:
- **Low-fidelity (Lo-fi)**: ASCII diagrams, paper sketches, or basic boxes. Use for initial exploration and stakeholder alignment.
- **Medium-fidelity (Mid-fi)**: Grayscale layouts with real text placeholders. Use for user flow validation.
- **High-fidelity (Hi-fi)**: Pixel-perfect mockups with colors, typography, and real content. Use for final approval and developer handoff.

**Recommended Tools**:
- Lo-fi: ASCII in docs, Excalidraw, Balsamiq, paper
- Mid-fi: Figma (free tier), Sketch, Adobe XD, Penpot
- Hi-fi: Figma, Sketch, Adobe XD

For this project, wireframes are stored in: [location, e.g., `/design` folder, Figma link]
-->

| Screen | Fidelity | Location |
|--------|----------|----------|
| [Screen Name] | [Lo-fi/Mid-fi/Hi-fi] | [Path or link] |

### Screen: [Main Screen Name]

<!-- AI: Document each major screen. Include:
1. ASCII wireframe showing element placement
2. Purpose: What does user accomplish here?
3. Key elements: List important interactive elements
4. Entry points: How does user get here?
5. Exit points: Where can user go from here?
-->

**Purpose**: [What user accomplishes on this screen]

**Wireframe**:
```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  [Use boxes and labels to show element placement]       │
│                                                         │
│  ┌─────────────┐  ┌──────────────────────────────┐     │
│  │   Element   │  │      Main Content Area       │     │
│  └─────────────┘  │                              │     │
│                   │                              │     │
│                   └──────────────────────────────┘     │
│                                                         │
│  [Action Button]                                        │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

**Key Elements**:
- [Element 1]: [Purpose]
- [Element 2]: [Purpose]

**Entry/Exit Points**:
- Entry: [How user arrives]
- Exit: [Where user can navigate to]

### Screen: [Secondary Screen Name]

<!-- AI: Repeat the structure above for each screen. Ensure every screen referenced in user flows has a wireframe. -->

[Repeat structure]

---

## User Flows

<!-- AI: Document the step-by-step paths users take to accomplish tasks. Focus on primary flows first, then edge cases. -->

### User Flow Diagram Guidance

<!-- AI:
User flows show the sequence of screens/actions for completing a task.

**Format options**:
1. **Text-based flowchart** (in this doc):
   ```
   [Start] → [Step 1] → [Decision?] → Yes → [Step 2a] → [End]
                              ↓
                             No → [Step 2b] → [End]
   ```

2. **ASCII flowchart** (more detailed):
   ```
   ┌─────────┐     ┌─────────┐     ◇─────────◇
   │  Start  │────▶│ Step 1  │────▶│Decision?│
   └─────────┘     └─────────┘     ◇─────────◇
                                    │Yes   │No
                                    ▼      ▼
                               ┌────────┐ ┌────────┐
                               │Step 2a │ │Step 2b │
                               └────────┘ └────────┘
   ```

3. **External tools**: Miro, FigJam, Whimsical, Lucidchart

For complex flows, include:
- Decision points (diamonds ◇)
- Error states
- Alternative paths
- Loops (for repeated actions)
-->

### Flow 1: [Primary User Goal]

<!-- AI: Document the most important user journey first. Example: "User completes first-time setup" or "User creates a new project". -->

**Goal**: [What user is trying to accomplish]

**Preconditions**: [What must be true before starting]

**Steps**:
```
[Start: User lands on X]
    ↓
[Step 1: User does Y]
    ↓
[Step 2: System shows Z]
    ↓
[Decision: Is condition met?]
    ├── Yes → [Step 3a: Continue flow]
    └── No → [Step 3b: Error handling]
    ↓
[End: User sees confirmation]
```

**Success Criteria**: [How do we know the flow succeeded?]

**Error States**:
- [Error condition 1]: [How it's handled]
- [Error condition 2]: [How it's handled]

### Flow 2: [Secondary User Goal]

<!-- AI: Continue documenting flows in priority order. Ensure every P0 feature has at least one user flow documented. -->

[Repeat structure]

---

## Navigation Structure

<!-- AI: Document how users move between screens/sections. Different patterns suit different applications. -->

### Navigation Pattern

<!-- AI: Choose and document the primary navigation pattern:

**Common Patterns**:
- **Top nav bar**: Horizontal tabs/links at top. Good for: Marketing sites, simple apps, web apps.
- **Side nav (persistent)**: Vertical menu on left. Good for: Dashboards, admin panels, complex apps.
- **Bottom nav**: Mobile tab bar at bottom. Good for: Mobile apps with 3-5 top-level sections.
- **Hamburger menu**: Hidden nav behind icon. Good for: Mobile web, secondary nav.
- **Command palette**: Keyboard-triggered search. Good for: Power users, developer tools.
- **Wizard/Stepper**: Sequential steps. Good for: Onboarding, multi-step forms.

For this project:
- Primary pattern: [Pattern name]
- Secondary pattern (if any): [Pattern name]
- Rationale: [Why these patterns fit]
-->

**Primary Navigation**:
| Item | Destination | Icon (if used) |
|------|-------------|----------------|
| [Nav Item 1] | [Screen/Section] | [Icon name or none] |
| [Nav Item 2] | [Screen/Section] | [Icon name or none] |

**Secondary Navigation** (if applicable):
[Breadcrumbs, tabs within pages, contextual menus, etc.]

### Information Architecture

<!-- AI: Show the hierarchy of content/screens. This helps ensure navigation matches content structure.

```
Home
├── Section A
│   ├── Page A1
│   └── Page A2
├── Section B
│   ├── Page B1
│   ├── Page B2
│   └── Page B3
└── Settings
    ├── Profile
    └── Preferences
```
-->

```
[Content hierarchy diagram]
```

---

## Interaction Patterns

<!-- AI: Document how users interact with the application beyond simple navigation. -->

### Input Methods

<!-- AI: Document supported input methods and their considerations:
- **Mouse/Pointer**: Hover states, click targets, drag and drop
- **Touch**: Tap targets (min 44x44px for mobile), gestures, swipe actions
- **Keyboard**: Tab order, shortcuts, focus management
- **Voice**: Voice commands (if applicable)
- **Gamepad/Remote**: D-pad navigation (if applicable)
-->

| Input Method | Supported | Key Considerations |
|--------------|-----------|-------------------|
| Mouse/Pointer | Yes/No | [Hover states, drag-drop, etc.] |
| Touch | Yes/No | [Tap targets, gestures, etc.] |
| Keyboard | Yes/No | [Tab order, shortcuts, etc.] |

### Keyboard Shortcuts

<!-- AI: List keyboard shortcuts if the application supports them. Group by function.
Consider:
- Standard shortcuts users expect (Ctrl+C, Ctrl+Z, Escape to close)
- Application-specific shortcuts
- Avoiding conflicts with browser/OS shortcuts
-->

| Category | Action | Shortcut |
|----------|--------|----------|
| General | [Action] | [Key combo] |
| Navigation | [Action] | [Key combo] |
| [Category] | [Action] | [Key combo] |

### Gestures (Mobile/Touch)

<!-- AI: Document touch gestures if targeting mobile or touch devices. -->

| Gesture | Action | Context |
|---------|--------|---------|
| Swipe left | [Action] | [Where this applies] |
| Swipe right | [Action] | [Where this applies] |
| Pull down | [Action] | [Where this applies] |
| Pinch | [Action] | [Where this applies] |

### Drag and Drop

<!-- AI: If drag-and-drop is supported, document:
- What elements are draggable
- Valid drop targets
- Visual feedback during drag
- What happens on drop
-->

| Draggable | Drop Target | Result |
|-----------|-------------|--------|
| [Item type] | [Target area] | [What happens] |

---

## Responsive Design

<!-- AI: Document how the UI adapts to different screen sizes. -->

### Breakpoint Strategy

<!-- AI: Define breakpoints and what changes at each. Common approaches:
- **Mobile-first**: Start with mobile, add complexity for larger screens
- **Desktop-first**: Start with desktop, simplify for smaller screens
- **Fluid**: No fixed breakpoints, everything scales

Standard breakpoints (adjust for your needs):
- Mobile: 0-639px
- Tablet: 640-1023px
- Desktop: 1024-1279px
- Large desktop: 1280px+
-->

| Breakpoint | Width Range | Layout Changes |
|------------|-------------|----------------|
| Mobile | 0-[X]px | [What changes: single column, hidden nav, etc.] |
| Tablet | [X]-[Y]px | [What changes] |
| Desktop | [Y]px+ | [What changes] |

### Responsive Behaviors

<!-- AI: Document specific responsive behaviors for key components. -->

**Navigation**:
- Mobile: [Behavior, e.g., "Collapses to hamburger menu"]
- Desktop: [Behavior, e.g., "Full horizontal nav bar"]

**Content Layout**:
- Mobile: [Behavior, e.g., "Single column, stacked"]
- Desktop: [Behavior, e.g., "Multi-column grid"]

**Images/Media**:
- [How images scale, art direction changes, etc.]

### Minimum Supported Dimensions

<!-- AI: Set minimum dimensions below which the UI may break or become unusable. -->

- **Minimum width**: [X]px
- **Minimum height**: [Y]px
- **Rationale**: [Why these minimums]

---

## Platform-Specific Guidance

<!-- AI: Document UI considerations specific to each target platform. -->

### Web Browser Considerations

<!-- AI: If targeting web browsers:
- Supported browsers and versions
- Progressive enhancement approach
- Handling of browser-specific features
- URL structure and deep linking
-->

| Browser | Minimum Version | Known Issues |
|---------|-----------------|--------------|
| Chrome | [Version] | [Issues or "None"] |
| Firefox | [Version] | [Issues or "None"] |
| Safari | [Version] | [Issues or "None"] |
| Edge | [Version] | [Issues or "None"] |

### Desktop Application Considerations

<!-- AI: If targeting desktop (Electron, Tauri, native):
- Window management (resizable, minimum size, multiple windows)
- Menu bar structure (File, Edit, View, Help menus)
- System tray integration
- Native file dialogs
- OS-specific styling (Windows title bar, macOS traffic lights)
-->

**Window Behavior**:
- Resizable: [Yes/No]
- Minimum size: [Width x Height]
- Multiple windows: [Yes/No]
- Remember position: [Yes/No]

**System Integration**:
- Menu bar: [Description or "Not applicable"]
- System tray: [Description or "Not applicable"]
- Notifications: [Native/Web/None]

### Mobile Application Considerations

<!-- AI: If targeting mobile (React Native, Flutter, native):
- Platform guidelines compliance (iOS HIG, Material Design)
- Safe areas (notch, home indicator)
- Status bar treatment
- Navigation gestures (back swipe on iOS)
- App icon and splash screen
-->

**iOS Specific**:
- Safe area handling: [Approach]
- Back gesture: [Supported/Not supported]
- Haptic feedback: [Where used]

**Android Specific**:
- Material Design version: [2/3]
- Back button handling: [Approach]
- Edge-to-edge display: [Yes/No]

---

## Visual Style

<!-- AI: Document the visual design direction. This bridges to design tokens (doc 16). -->

### Style Direction

<!-- AI: Describe the overall visual style:
- Aesthetic: Modern, minimal, playful, corporate, artistic, etc.
- Mood: Professional, friendly, serious, fun, calm, energetic
- Visual references: Similar products or design systems that inspire this
-->

**Aesthetic**: [Description]

**Mood Board / References**:
- [Reference 1]: [Why it's relevant]
- [Reference 2]: [Why it's relevant]

### Theme Support

<!-- AI: Document theme support:
- Light mode only
- Dark mode only
- Both (user toggle or system preference)
- Custom themes
-->

| Theme | Availability | Default |
|-------|--------------|---------|
| Light | [Yes/No] | [Yes/No] |
| Dark | [Yes/No] | [Yes/No] |
| System preference | [Supported/Not supported] | - |

### Iconography

<!-- AI: Document icon usage:
- Icon set/library (Heroicons, Lucide, Phosphor, custom)
- Icon style (outline, solid, duotone)
- Icon sizing scale
-->

**Icon Library**: [Name and link]

**Icon Style**: [Outline/Solid/Duotone]

**Icon Sizes**:
| Size Name | Dimensions | Usage |
|-----------|------------|-------|
| Small | [X]px | [Where used] |
| Medium | [X]px | [Where used] |
| Large | [X]px | [Where used] |

---

## Animation and Transitions

<!-- AI: Document motion design decisions. -->

### Animation Philosophy

<!-- AI: Describe the approach to animation:
- Subtle and functional vs. expressive and playful
- Performance considerations
- Reduced motion support (prefers-reduced-motion)
-->

**Approach**: [Description of animation philosophy]

**Reduced Motion**: [How the app respects prefers-reduced-motion]

### Transition Types

<!-- AI: Document standard transitions used throughout the app. -->

| Transition | Duration | Easing | Usage |
|------------|----------|--------|-------|
| Page transition | [X]ms | [ease/ease-in/ease-out/etc.] | [When used] |
| Modal open | [X]ms | [Easing] | [When used] |
| Hover state | [X]ms | [Easing] | [When used] |
| Loading | [X]ms | [Easing] | [When used] |

### Loading States

<!-- AI: Document how loading states are communicated:
- Skeleton screens
- Spinners
- Progress bars
- Shimmer effects
-->

| Context | Loading Pattern | Duration Threshold |
|---------|----------------|-------------------|
| Page load | [Pattern] | [Show after X ms] |
| Data fetch | [Pattern] | [Show after X ms] |
| Form submit | [Pattern] | [Show after X ms] |

---

## Related Documents

<!-- AI: Link to related documents. Ensure bidirectional linking. -->

| Document | Relationship |
|----------|--------------|
| [06 - Component Specs](./06-component-specs.md) | Component implementations of this design |
| [13 - Accessibility](./13-accessibility.md) | Accessibility requirements affecting design |
| [16 - Design Tokens](./16-design-tokens.md) | Visual design values (colors, typography, spacing) |
| [02 - User Personas](./02-user-personas.md) | Who we're designing for |
| [04 - Feature Breakdown](./04-feature-breakdown.md) | Features that need UI |

---

## AI Agent Instructions

<!-- AI: Instructions for AI agents working with this document. -->

### When Populating This Document

1. **Start with user flows**: Before wireframing, understand what users need to accomplish (reference doc 02 personas and doc 04 features)
2. **Keep wireframes low-fidelity initially**: ASCII diagrams are sufficient for planning. Don't over-invest before validation.
3. **Document decisions, not just outcomes**: Explain why a navigation pattern was chosen, not just what it is.
4. **Cross-reference constantly**: Every screen should trace back to a feature. Every interaction should have a user flow.
5. **Consider all platforms early**: If targeting multiple platforms, note differences from the start rather than retrofitting.

### When Implementing From This Document

1. **Check design tokens first**: Use values from doc 16, don't hard-code colors or spacing.
2. **Validate accessibility**: Cross-reference doc 13 for keyboard navigation and screen reader requirements.
3. **Follow component specs**: Reference doc 06 for detailed component behavior before implementing.
4. **Test responsive breakpoints**: Verify layouts at each documented breakpoint, not just arbitrary sizes.
5. **Implement reduced motion**: Always provide reduced motion alternatives for animations.

### Quality Checklist

Before marking this document complete:
- [ ] Every P0/P1 feature has an associated user flow
- [ ] Every screen in user flows has a wireframe
- [ ] Navigation structure covers all documented screens
- [ ] Responsive behavior is defined for all target platforms
- [ ] Animation philosophy is documented (even if "minimal")
- [ ] Related Documents section links are bidirectional
