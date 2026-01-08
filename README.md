# Documentation-First Development Framework

> A structured planning and execution framework for AI-assisted software development

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

---

## Overview

This template provides a complete documentation structure that guides you (and your AI coding partner) through every phase of software development—from initial vision to deployment.

**Why use this framework?**

- **Prevent scope creep** - Upfront planning catches issues before coding begins
- **Enable AI collaboration** - Context-preserving handoffs between sessions
- **Work for any stack** - Web, desktop, mobile, backend, CLI
- **Scale seamlessly** - Solo developer to team workflows

---

## Quick Start

### 1. Create Your Project

```bash
# Clone the template
git clone https://github.com/yourusername/doc-driven-dev.git my-project
cd my-project
rm -rf .git && git init
```

### 2. Replace Placeholders

Find and replace throughout the project:
- `[PROJECT_NAME]` → Your project name
- `[PROJECT_PATH]` → Full path to your project

### 3. Start Your First AI Session

```
I'm starting a new project using the documentation-first framework.

Location: [PROJECT_PATH]
Project: [PROJECT_NAME]

Read docs/planning/AGENT-GUIDE.md first, then help me complete Phase 1 Discovery.
```

---

## Framework Structure

```
your-project/
├── README.md
├── TEMPLATE-USAGE.md          # Detailed setup guide
├── docs/
│   ├── planning/              # 24 planning documents
│   │   ├── AGENT-GUIDE.md     # AI agent instructions (start here)
│   │   ├── DEPENDENCIES.md    # Document dependency graph
│   │   ├── 00-project-setup.md
│   │   ├── 01-vision-and-goals.md
│   │   ├── ...
│   │   └── 23-configuration-management.md
│   ├── roadmap/               # Sprint planning and tracking
│   │   ├── progress-tracker.md
│   │   ├── phase-gates.md
│   │   ├── sprint-overview.md
│   │   └── sprints/
│   └── reference/             # Living reference docs
│       ├── conventions.md
│       ├── glossary.md
│       ├── tech-decisions.md
│       └── troubleshooting.md
└── src/                       # Your code (create as needed)
```

---

## Development Phases

| Phase | Focus | Documents | Gate |
|-------|-------|-----------|------|
| **0** | Project Setup | 00 | Ready to discover |
| **1** | Discovery | 01-04 | Ready to design |
| **2A** | UI/UX Design | 05, 06, 13, 16 | - |
| **2B** | Technical Design | 07-09, 15 | - |
| **2C** | Code Standards | 17 | - |
| **2D** | Quality Planning | 10-14, 19-23 | Ready to plan sprints |
| **3** | Sprint Planning | roadmap/sprints/ | Ready to execute |
| **4+** | Execution | Per sprint docs | Per release |

Each phase has explicit **gate criteria** that must be met before proceeding. See `docs/roadmap/phase-gates.md`.

---

## Key Principles

| Principle | Why It Matters |
|-----------|----------------|
| **Plan before code** | Complete Phase 1-2 before production code |
| **Document decisions** | Use doc 18 (Decision Log) to prevent re-debates |
| **Preserve context** | Handoff messages enable seamless multi-session work |
| **Trust the graph** | Follow DEPENDENCIES.md to avoid blocked work |

---

## For AI Agents

If you're an AI agent reading this:

1. **Start here**: `docs/planning/AGENT-GUIDE.md` - Your operating instructions
2. **Check status**: `docs/roadmap/progress-tracker.md` - Current project state
3. **Follow order**: `docs/planning/DEPENDENCIES.md` - Document dependencies
4. **Use handoffs**: Generate handoff messages between sessions

---

## Supported Project Types

This framework works for any tech stack:

| Type | Example Stacks |
|------|----------------|
| **Web SPA** | React, Vue, Svelte, Angular |
| **Web SSR** | Next.js, Nuxt, SvelteKit, Remix |
| **Desktop** | Tauri, Electron, .NET MAUI |
| **Mobile** | React Native, Flutter, SwiftUI |
| **Backend** | Express, FastAPI, Gin, Actix |
| **CLI** | Commander, Cobra, Clap |

See `TEMPLATE-USAGE.md` for stack-specific guidance.

---

## Documentation

- **[TEMPLATE-USAGE.md](TEMPLATE-USAGE.md)** - Detailed setup and customization guide
- **[AGENT-GUIDE.md](docs/planning/AGENT-GUIDE.md)** - AI agent operating instructions
- **[DEPENDENCIES.md](docs/planning/DEPENDENCIES.md)** - Document dependency graph

---

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
