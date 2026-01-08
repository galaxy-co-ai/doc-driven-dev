# Template Usage Guide

This template provides a documentation-first framework for AI-assisted software development. Follow this guide to bootstrap a new project.

---

## Quick Start

### 1. Clone or Copy the Template

```bash
# Option A: Clone the template
git clone <template-repo-url> your-project-name
cd your-project-name
rm -rf .git
git init

# Option B: Copy the folder
cp -r "Project Template" your-project-name
cd your-project-name
git init
```

### 2. Find and Replace Placeholders

Replace these placeholders throughout the project:

| Placeholder | Replace With | Example |
|-------------|--------------|---------|
| `[PROJECT_NAME]` | Your project name | `TaskManager` |
| `[PROJECT_PATH]` | Full path to project | `C:\Users\You\projects\task-manager` |

**Files to update:**
- `docs/planning/AGENT-GUIDE.md` - Project context and description
- `docs/roadmap/sprints/sprint-template.md` - Handoff message template

**Quick replacement commands:**

```bash
# PowerShell
Get-ChildItem -Recurse -File | ForEach-Object {
    (Get-Content $_.FullName) -replace '\[PROJECT_NAME\]', 'YourProjectName' |
    Set-Content $_.FullName
}

# Bash/Unix
find . -type f -exec sed -i 's/\[PROJECT_NAME\]/YourProjectName/g' {} +
find . -type f -exec sed -i 's|\[PROJECT_PATH\]|/your/project/path|g' {} +
```

### 3. Initialize Your Project

```bash
# Copy environment template
cp .env.example .env

# Initialize your tech stack (examples)
npm init                    # Node.js
cargo init                  # Rust
pnpm create tauri-app       # Tauri
```

### 4. Fill in AGENT-GUIDE.md

Open `docs/planning/AGENT-GUIDE.md` and complete these sections:

- **What is [PROJECT_NAME]?** - Brief project description
- **Core Concept** - Main components and goals
- **Tech Stack** - Will be filled via docs 07, 08, 09, 16

---

## Document Completion Order

Follow the dependency graph in `docs/planning/DEPENDENCIES.md`. Here's the recommended order:

### Phase 0: Foundation
1. **00-project-setup.md** - Initialize project, record versions

### Phase 1: Discovery (Complete in Order)
2. **01-vision-and-goals.md** - Why this project exists
3. **02-user-personas.md** - Who will use it
4. **03-product-requirements.md** - What it must do
5. **04-feature-breakdown.md** - Features and priorities

### Phase 2A: UI/UX Design (After 04)
- **05-ui-ux-design.md** - Layouts and flows
- **06-component-specs.md** - UI component details
- **16-design-tokens.md** - Colors, spacing, typography
- **13-accessibility.md** - A11y requirements

### Phase 2B: Technical Design (After 04, Parallel with 2A)
- **07-technical-architecture.md** - System design
- **08-data-models.md** - Data structures
- **09-api-contracts.md** - API definitions
- **15-file-architecture.md** - Project structure

### Phase 2C: Code Patterns (After 2A and 2B)
- **17-code-patterns.md** - Coding standards and examples

### Phase 2D: Quality (After 17)
- **10-error-handling.md** - Error strategy
- **11-security-considerations.md** - Security measures
- **12-testing-strategy.md** - Test approach
- **14-performance-goals.md** - Performance targets
- **19-cicd-pipeline.md** - Build and deploy automation

### Ongoing
- **18-decision-log.md** - Record decisions as you go

---

## Customizing for Different Tech Stacks

### Web Application (React/Vue/Angular)

Update these docs:
- **07-technical-architecture.md** - Framework choice, state management
- **08-data-models.md** - Frontend state shape, API response types
- **09-api-contracts.md** - REST/GraphQL endpoints
- **16-design-tokens.md** - CSS variables or design system

### Desktop Application (Tauri/Electron)

Additional considerations:
- **07-technical-architecture.md** - IPC communication, native APIs
- **11-security-considerations.md** - File system access, permissions
- **19-cicd-pipeline.md** - Multi-platform builds

### Backend/API Service

Focus areas:
- **08-data-models.md** - Database schemas
- **09-api-contracts.md** - API documentation (OpenAPI)
- **11-security-considerations.md** - Auth, rate limiting
- **12-testing-strategy.md** - Integration tests, load tests

### CLI Tool

Focus areas:
- **05-ui-ux-design.md** - Command structure, help text
- **10-error-handling.md** - Exit codes, error messages
- **13-accessibility.md** - Screen reader compatibility

---

## Working with AI Agents

This template is designed for AI-assisted development. Key features:

### AGENT-GUIDE.md
The central document that AI agents read first. It contains:
- Project context and goals
- Session protocols
- Communication guidelines
- Handoff procedures

### Progress Tracking
- **progress-tracker.md** - Overall project status
- **sprint-XX.md** files - Detailed sprint tasks

### Handoff System
Each session should end with a handoff message (template in sprint docs) that allows the next session to continue seamlessly.

---

## Sprint Workflow

### Creating a New Sprint

1. Copy `docs/roadmap/sprints/sprint-template.md` to `sprint-01.md`
2. Fill in sprint goal and tasks
3. Update `docs/roadmap/sprint-overview.md`
4. Update `docs/roadmap/progress-tracker.md`

### During a Sprint

1. Agent reads AGENT-GUIDE.md and progress-tracker.md
2. Agent works through sprint tasks
3. Tasks are checked off as completed
4. Decisions are logged in doc 18

### Completing a Sprint

1. Verify all acceptance criteria met
2. Update progress-tracker.md
3. Generate handoff message
4. Create next sprint file if needed

---

## File Structure Reference

```
your-project/
├── .env.example              # Environment template
├── TEMPLATE-USAGE.md         # This file
├── docs/
│   ├── planning/
│   │   ├── AGENT-GUIDE.md    # AI agent instructions
│   │   ├── DEPENDENCIES.md   # Doc dependency graph
│   │   ├── 00-project-setup.md
│   │   ├── 01-vision-and-goals.md
│   │   ├── ... (02-19)
│   │   └── 18-decision-log.md
│   ├── roadmap/
│   │   ├── sprint-overview.md
│   │   ├── progress-tracker.md
│   │   └── sprints/
│   │       └── sprint-template.md
│   └── reference/
│       ├── tech-decisions.md
│       ├── conventions.md
│       ├── glossary.md
│       └── troubleshooting.md
└── src/                      # Your code (create as needed)
```

---

## Tips for Success

1. **Complete docs in order** - The dependency graph exists for a reason
2. **Don't skip Phase 1** - Discovery docs inform all technical decisions
3. **Update progress-tracker.md** - Every session should update this
4. **Use the handoff system** - Enables seamless multi-session work
5. **Log decisions** - Doc 18 prevents revisiting settled questions
6. **Keep sprints small** - 3-5 tasks per sprint works well

---

## Getting Help

- Review `docs/planning/DEPENDENCIES.md` for document relationships
- Check `docs/reference/troubleshooting.md` for common issues
- Update `docs/reference/glossary.md` with project-specific terms
