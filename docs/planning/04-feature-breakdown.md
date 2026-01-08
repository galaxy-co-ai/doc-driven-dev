# 04 - Feature Breakdown

<!-- AI: This document breaks requirements (doc 03) into implementable features. Complete after docs 01-03 and before design docs (05+). This bridges discovery and design phases. -->

## Feature Index

<!-- AI:
List all features with quick reference information. This table provides an at-a-glance view of the entire feature set.

Feature IDs should be stable - don't renumber. Use gaps if features are removed.
-->

| ID | Feature Name | Priority | Effort | Status | Sprint |
|----|--------------|----------|--------|--------|--------|
| F001 | <!-- AI: e.g., "User Authentication" --> | <!-- AI: P0/P1/P2 --> | <!-- AI: S/M/L/XL --> | <!-- AI: Planned/In Progress/Complete --> | <!-- AI: Sprint number or "Backlog" --> |
| F002 | <!-- AI: e.g., "Dashboard View" --> | <!-- AI: P0/P1/P2 --> | <!-- AI: S/M/L/XL --> | <!-- AI: Planned/In Progress/Complete --> | <!-- AI: Sprint number or "Backlog" --> |
| F003 | <!-- AI: e.g., "Data Export" --> | <!-- AI: P0/P1/P2 --> | <!-- AI: S/M/L/XL --> | <!-- AI: Planned/In Progress/Complete --> | <!-- AI: Sprint number or "Backlog" --> |

---

## Effort Estimation Guide

<!-- AI:
Use T-shirt sizes for initial estimation. Convert to time ranges during sprint planning.
Estimates are for a single developer. Adjust based on team size and experience.
-->

| Size | Typical Scope | Time Range | Example |
|------|---------------|------------|---------|
| **S** (Small) | Single component, no new patterns | 1-2 hours | Add a button, fix styling, simple bug fix |
| **M** (Medium) | Multiple components, follows existing patterns | 2-8 hours | New form, API integration, feature enhancement |
| **L** (Large) | New patterns, multiple files, needs design | 1-3 days | New page/view, complex component, new data model |
| **XL** (Extra Large) | Architectural changes, multiple systems | 3-5 days | Auth system, major refactor, new infrastructure |

**If larger than XL**: Break into smaller features. XL is the maximum for a single feature.

---

## Feature Details

<!-- AI:
Each feature gets its own section. Use the template below.

Feature naming: Use verb-noun format when possible.
- Good: "User Authentication", "Export Data", "Filter Search Results"
- Bad: "Auth", "Export Feature", "Filtering"
-->

### F001: [Feature Name]

<!-- AI: Copy this template for each feature. Delete the examples when filling in real content. -->

#### User Story

<!-- AI:
User story format: "As a [persona], I want to [action] so that [benefit]."

The persona should reference doc 02. The benefit should connect to a pain point or use case.

Examples:
- "As Alex (primary persona), I want to save my work automatically so that I never lose progress."
- "As a new user, I want to see a quick tutorial so that I can start using the app confidently."
-->

As a <!-- AI: persona name from doc 02 -->, I want to <!-- AI: specific action --> so that <!-- AI: specific benefit -->.

#### Priority & Effort

| Attribute | Value | Rationale |
|-----------|-------|-----------|
| Priority | <!-- AI: P0/P1/P2 --> | <!-- AI: Why this priority? Reference doc 03 requirement --> |
| Effort | <!-- AI: S/M/L/XL --> | <!-- AI: Brief justification for estimate --> |
| Risk | <!-- AI: Low/Medium/High --> | <!-- AI: What could go wrong? --> |

#### Acceptance Criteria

<!-- AI:
Acceptance criteria define when the feature is DONE. They should be:
- Testable: Can verify pass/fail
- Specific: No ambiguity
- Complete: Cover happy path AND edge cases

Format: Use "Given/When/Then" or simple checkboxes.

Given/When/Then example:
- Given I am logged in
- When I click the "Save" button
- Then my work is saved and I see a confirmation message

Checkbox example:
- [ ] User can perform action X
- [ ] System responds within Y seconds
- [ ] Error state shows message Z
-->

- [ ] <!-- AI: e.g., "User can complete [action] successfully" -->
- [ ] <!-- AI: e.g., "System validates [input] and shows error if invalid" -->
- [ ] <!-- AI: e.g., "Changes persist after page refresh" -->
- [ ] <!-- AI: e.g., "Feature works on all supported browsers (doc 03)" -->

#### Dependencies

<!-- AI:
List features or external dependencies that must be complete before this can start.
Also list features that depend on THIS feature (blocks).

Format: Feature ID or external dependency name
-->

| Type | Dependency | Notes |
|------|------------|-------|
| Requires | <!-- AI: e.g., "F003 (Data Model)" --> | <!-- AI: e.g., "Need data layer first" --> |
| Requires | <!-- AI: e.g., "Auth API configured" --> | <!-- AI: e.g., "External dependency" --> |
| Blocks | <!-- AI: e.g., "F005 (Sharing)" --> | <!-- AI: e.g., "Can't share until this exists" --> |

#### Technical Notes

<!-- AI:
Optional: Add implementation hints, technical decisions, or design considerations.
This helps during sprint planning and implementation.
-->

<!-- AI: e.g., "Consider using [library] for this. See doc 17 for component patterns." -->

#### Open Questions

<!-- AI:
Track unresolved questions specific to this feature.
-->

- <!-- AI: e.g., "Should we support [edge case]? Decision needed before implementation." -->

---

### F002: [Feature Name]

<!-- AI: Repeat the template above for each feature. -->

#### User Story

As a <!-- AI: persona name -->, I want to <!-- AI: action --> so that <!-- AI: benefit -->.

#### Priority & Effort

| Attribute | Value | Rationale |
|-----------|-------|-----------|
| Priority | <!-- AI: P0/P1/P2 --> | <!-- AI: Rationale --> |
| Effort | <!-- AI: S/M/L/XL --> | <!-- AI: Rationale --> |
| Risk | <!-- AI: Low/Medium/High --> | <!-- AI: Rationale --> |

#### Acceptance Criteria

- [ ] <!-- AI: Criterion 1 -->
- [ ] <!-- AI: Criterion 2 -->
- [ ] <!-- AI: Criterion 3 -->

#### Dependencies

| Type | Dependency | Notes |
|------|------------|-------|
| Requires | <!-- AI: Dependency --> | <!-- AI: Notes --> |
| Blocks | <!-- AI: Dependency --> | <!-- AI: Notes --> |

---

### F003: [Feature Name]

<!-- AI: Continue adding features as needed. -->

#### User Story

As a <!-- AI: persona name -->, I want to <!-- AI: action --> so that <!-- AI: benefit -->.

#### Priority & Effort

| Attribute | Value | Rationale |
|-----------|-------|-----------|
| Priority | <!-- AI: P0/P1/P2 --> | <!-- AI: Rationale --> |
| Effort | <!-- AI: S/M/L/XL --> | <!-- AI: Rationale --> |
| Risk | <!-- AI: Low/Medium/High --> | <!-- AI: Rationale --> |

#### Acceptance Criteria

- [ ] <!-- AI: Criterion 1 -->
- [ ] <!-- AI: Criterion 2 -->

#### Dependencies

| Type | Dependency | Notes |
|------|------------|-------|
| Requires | <!-- AI: Dependency --> | <!-- AI: Notes --> |

---

## Feature Dependency Graph

<!-- AI:
Visualize how features depend on each other. This helps with sprint planning.

Use ASCII art for simple graphs. For complex dependencies, reference an external diagram.

Arrow meaning: A ──► B means "A must be complete before B can start"

Example:
F001 (Auth) ──► F003 (User Profile) ──► F005 (Sharing)
                     │
                     └──► F004 (Settings)

F002 (Dashboard) ──► F006 (Analytics)
-->

```
<!-- AI: Draw the dependency graph here. Show critical path. -->

[Core Features]
F001 ──► F002 ──► F003
           │
           └──► F004

[Independent Features]
F005 (no dependencies)
```

### Critical Path

<!-- AI:
The critical path is the longest chain of dependent features. It determines minimum time to MVP.
-->

<!-- AI: e.g., "F001 → F002 → F003 → F006 is the critical path (4 features, ~X effort)" -->

---

## Priority Summary

| Priority | Count | Total Effort | Features |
|----------|-------|--------------|----------|
| P0 (Must Have) | <!-- AI: number --> | <!-- AI: e.g., "3M + 2L" --> | <!-- AI: e.g., "F001, F002, F003" --> |
| P1 (Should Have) | <!-- AI: number --> | <!-- AI: e.g., "1M + 1S" --> | <!-- AI: e.g., "F004, F005" --> |
| P2 (Nice to Have) | <!-- AI: number --> | <!-- AI: e.g., "2M" --> | <!-- AI: e.g., "F006, F007" --> |

---

## MVP Scope

<!-- AI:
Define exactly what's included in the Minimum Viable Product.
All P0 features should be here. Some P1 features may be included if time allows.
-->

### MVP Features (Must Ship)

- [ ] F001: <!-- AI: Feature name -->
- [ ] F002: <!-- AI: Feature name -->
- [ ] F003: <!-- AI: Feature name -->

### MVP Stretch Goals (If Time Allows)

- [ ] F004: <!-- AI: Feature name -->
- [ ] F005: <!-- AI: Feature name -->

### Post-MVP Backlog

<!-- AI: Features explicitly deferred to after MVP launch. -->

- F006: <!-- AI: Feature name --> - Reason: <!-- AI: Why deferred -->
- F007: <!-- AI: Feature name --> - Reason: <!-- AI: Why deferred -->

---

## Feature Changelog

<!-- AI:
Track significant changes to feature definitions. This provides history for decision-making.
-->

| Date | Feature | Change | Reason |
|------|---------|--------|--------|
| <!-- AI: YYYY-MM-DD --> | <!-- AI: Feature ID --> | <!-- AI: What changed --> | <!-- AI: Why --> |

---

## Related Documents

| Doc | Relationship |
|-----|--------------|
| [03-product-requirements.md](./03-product-requirements.md) | Requirements these features implement |
| [02-user-personas.md](./02-user-personas.md) | Personas referenced in user stories |
| [06-component-specs.md](./06-component-specs.md) | Component designs for features |
| [Sprint docs](../roadmap/sprints/) | Features assigned to sprints |
| [progress-tracker.md](../roadmap/progress-tracker.md) | Feature completion status |
| [18-decision-log.md](./18-decision-log.md) | Major feature decisions |
| [AGENT-GUIDE.md](./AGENT-GUIDE.md) | How to lead the process |

---

## AI Agent Instructions

### How to Complete This Document

1. **Start from doc 03 requirements** - Every P0 requirement should map to at least one feature here.

2. **Use consistent IDs** - Feature IDs are permanent. Don't renumber. Use gaps if needed.

3. **Write from user perspective** - User stories should use persona names and focus on value.

4. **Estimate conservatively** - When in doubt, estimate larger. It's better to finish early.

5. **Map dependencies carefully** - This drives sprint planning. Missing dependencies cause blockers.

### User Story Quality Checklist

| Component | Question | Example |
|-----------|----------|---------|
| Persona | Is it a specific person from doc 02? | "Alex" not "users" |
| Action | Is it a concrete action? | "save my work" not "have a good experience" |
| Benefit | Does it connect to a pain point? | "never lose progress" not "be happy" |

### Acceptance Criteria Patterns

**For data operations:**
- [ ] User can create [thing]
- [ ] User can read/view [thing]
- [ ] User can update [thing]
- [ ] User can delete [thing]
- [ ] Changes persist after refresh/restart

**For user actions:**
- [ ] Action completes within [X] seconds
- [ ] Success state is visually confirmed
- [ ] Error state shows actionable message
- [ ] Action can be undone (if applicable)

**For UI features:**
- [ ] Displays correctly on supported screen sizes
- [ ] Keyboard accessible
- [ ] Screen reader announces changes
- [ ] Loading states shown for operations > 500ms

### Questions to Ask the User

- "Walk me through using this feature step by step"
- "What's the most important thing this feature needs to do?"
- "What should happen if something goes wrong?"
- "How does this connect to other features you've described?"

### Document Completion Checklist

- [ ] All P0 requirements from doc 03 have corresponding features
- [ ] Every feature has user story, priority, effort, and acceptance criteria
- [ ] All feature dependencies are mapped
- [ ] Dependency graph shows critical path
- [ ] MVP scope is clearly defined
- [ ] No remaining [TBD] markers (or explicitly deferred with reason)
