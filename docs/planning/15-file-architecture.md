# 15 - File Architecture

<!-- AI: This document defines the folder structure, naming conventions, and organization patterns for your project. Select the appropriate template based on the project type from 00-project-setup.md. Adapt the structure to match your specific framework and team conventions. -->

---

## Stack-Variant Folder Structures

<!-- AI: Select ONE primary structure below based on your project type. Delete the others or adapt to create a hybrid. The structures shown are common conventions - adjust based on your framework's recommendations. -->

---

### Web SPA (React/Vue/Svelte/Angular)

<!-- AI: Use this structure for client-side single page applications. Adapt component folder names based on your UI framework conventions. -->

```
[project-name]/
├── docs/                          # Documentation
│   ├── planning/                  # Planning documents (this framework)
│   ├── roadmap/                   # Sprint planning
│   └── reference/                 # Reference docs
│
├── public/                        # Static assets (copied as-is to build)
│   ├── favicon.ico
│   └── robots.txt
│
├── src/                           # Application source
│   ├── assets/                    # Processed assets (images, fonts)
│   │
│   ├── components/                # UI components
│   │   ├── common/                # Shared/reusable components
│   │   │   ├── Button/
│   │   │   │   ├── Button.tsx     # (or .vue, .svelte)
│   │   │   │   ├── Button.test.ts
│   │   │   │   └── index.ts       # Re-export
│   │   │   └── ...
│   │   └── [feature]/             # Feature-specific components
│   │
│   ├── hooks/                     # Custom hooks (React) / composables (Vue)
│   ├── stores/                    # State management
│   ├── services/                  # API calls, external integrations
│   ├── utils/                     # Pure utility functions
│   ├── types/                     # TypeScript types/interfaces
│   ├── styles/                    # Global styles, design tokens
│   │
│   ├── pages/                     # Route pages (if using file-based routing)
│   │   └── ...                    # or routes/ depending on router
│   │
│   ├── App.tsx                    # Root component
│   ├── main.tsx                   # Entry point
│   └── router.ts                  # Route configuration (if centralized)
│
├── tests/                         # Test configuration and shared utilities
│   ├── setup.ts                   # Test setup file
│   └── mocks/                     # Shared mocks
│
├── .env.example                   # Environment template
├── package.json
├── tsconfig.json
├── vite.config.ts                 # (or webpack.config.js, etc.)
└── README.md
```

**Framework Variations:**
| Framework | Components | State | Hooks |
|-----------|------------|-------|-------|
| React | `.tsx` files | zustand/redux/jotai | `hooks/use-*.ts` |
| Vue | `.vue` SFCs | pinia | `composables/use*.ts` |
| Svelte | `.svelte` files | svelte/store | `lib/*.ts` |
| Angular | `.component.ts` | NgRx/services | services |

---

### Web SSR (Next.js/Nuxt/SvelteKit/Remix)

<!-- AI: Use this structure for server-side rendered applications. These frameworks have strong opinions about routing - follow their conventions. -->

```
[project-name]/
├── docs/                          # Documentation
│
├── public/                        # Static assets
│
├── src/                           # Application source (Next.js 13+ App Router)
│   ├── app/                       # App Router routes (Next.js 13+)
│   │   ├── layout.tsx             # Root layout
│   │   ├── page.tsx               # Home page
│   │   ├── loading.tsx            # Loading UI
│   │   ├── error.tsx              # Error boundary
│   │   ├── (auth)/                # Route group (no URL segment)
│   │   │   ├── login/
│   │   │   │   └── page.tsx
│   │   │   └── register/
│   │   │       └── page.tsx
│   │   └── dashboard/
│   │       ├── layout.tsx         # Nested layout
│   │       └── page.tsx
│   │
│   ├── components/                # Shared components
│   │   ├── ui/                    # Generic UI components
│   │   └── [feature]/             # Feature-specific components
│   │
│   ├── lib/                       # Shared utilities, server functions
│   │   ├── db.ts                  # Database client
│   │   ├── auth.ts                # Auth utilities
│   │   └── utils.ts               # General utilities
│   │
│   ├── hooks/                     # Client-side hooks
│   ├── types/                     # TypeScript types
│   └── styles/                    # Global styles
│
├── prisma/                        # Database schema (if using Prisma)
│   └── schema.prisma
│
├── .env.local                     # Local environment
├── next.config.js                 # Framework config
├── package.json
└── tsconfig.json
```

**Framework Variations:**
| Framework | Routes | Server Code | Config |
|-----------|--------|-------------|--------|
| Next.js (App) | `app/[route]/page.tsx` | `app/api/` or Server Actions | `next.config.js` |
| Next.js (Pages) | `pages/[route].tsx` | `pages/api/` | `next.config.js` |
| Nuxt | `pages/[route].vue` | `server/api/` | `nuxt.config.ts` |
| SvelteKit | `routes/[route]/+page.svelte` | `routes/api/+server.ts` | `svelte.config.js` |
| Remix | `routes/[route].tsx` | loaders/actions in same file | `remix.config.js` |

---

### Desktop (Tauri/Electron)

<!-- AI: Use this structure for desktop applications with web UI. The native backend code is separate from the web frontend. -->

```
[project-name]/
├── docs/                          # Documentation
│
├── src/                           # Frontend (web UI)
│   ├── components/
│   ├── hooks/
│   ├── stores/
│   ├── utils/
│   ├── types/
│   ├── styles/
│   ├── App.tsx
│   └── main.tsx
│
├── src-tauri/                     # Tauri backend (Rust)
│   ├── src/
│   │   ├── main.rs                # Entry point
│   │   ├── lib.rs                 # Library exports
│   │   ├── commands/              # IPC command handlers
│   │   │   ├── mod.rs
│   │   │   └── [feature].rs
│   │   ├── state/                 # Application state
│   │   └── utils/                 # Utilities
│   ├── icons/                     # Application icons
│   ├── Cargo.toml                 # Rust dependencies
│   └── tauri.conf.json            # Tauri configuration
│
├── src-electron/                  # Electron backend (if using Electron)
│   ├── main/
│   │   ├── index.ts               # Main process entry
│   │   ├── ipc/                   # IPC handlers
│   │   └── windows/               # Window management
│   ├── preload/
│   │   └── index.ts               # Preload scripts
│   └── electron-builder.json      # Build configuration
│
├── public/                        # Static assets
├── tests/
├── package.json
└── tsconfig.json
```

**Framework Variations:**
| Framework | Backend Location | Config | IPC Pattern |
|-----------|------------------|--------|-------------|
| Tauri | `src-tauri/` (Rust) | `tauri.conf.json` | `#[tauri::command]` |
| Electron | `src-electron/` (JS/TS) | `electron-builder.json` | `ipcMain/ipcRenderer` |
| Neutralino | `resources/` | `neutralino.config.json` | `Neutralino.os.*` |

---

### Backend API (Node.js - Express/Fastify/Hono)

<!-- AI: Use this structure for Node.js backend APIs. Follows layered architecture: routes → controllers → services → repositories. -->

```
[project-name]/
├── docs/                          # Documentation
│
├── src/
│   ├── config/                    # Configuration
│   │   ├── index.ts               # Config aggregation
│   │   ├── database.ts            # DB config
│   │   └── env.ts                 # Environment validation
│   │
│   ├── routes/                    # Route definitions
│   │   ├── index.ts               # Route aggregation
│   │   ├── users.routes.ts
│   │   └── [resource].routes.ts
│   │
│   ├── controllers/               # Request handlers
│   │   ├── users.controller.ts
│   │   └── [resource].controller.ts
│   │
│   ├── services/                  # Business logic
│   │   ├── users.service.ts
│   │   └── [resource].service.ts
│   │
│   ├── repositories/              # Data access (optional layer)
│   │   ├── users.repository.ts
│   │   └── [resource].repository.ts
│   │
│   ├── models/                    # Database models/schemas
│   │   ├── user.model.ts
│   │   └── [resource].model.ts
│   │
│   ├── middleware/                # Express/Fastify middleware
│   │   ├── auth.middleware.ts
│   │   ├── error.middleware.ts
│   │   └── validation.middleware.ts
│   │
│   ├── utils/                     # Utilities
│   │   ├── logger.ts
│   │   └── helpers.ts
│   │
│   ├── types/                     # TypeScript types
│   │   ├── index.ts
│   │   └── api.types.ts
│   │
│   ├── app.ts                     # Express/Fastify app setup
│   └── server.ts                  # Server entry point
│
├── prisma/                        # Prisma ORM (if used)
│   ├── schema.prisma
│   └── migrations/
│
├── tests/
│   ├── unit/
│   ├── integration/
│   └── fixtures/
│
├── .env.example
├── Dockerfile
├── docker-compose.yml
├── package.json
└── tsconfig.json
```

**Framework Variations:**
| Framework | App Setup | Route Pattern | Middleware |
|-----------|-----------|---------------|------------|
| Express | `app.use()` | `router.get()` | `(req, res, next)` |
| Fastify | `fastify.register()` | Plugins | `preHandler` hooks |
| Hono | `app.route()` | Chained methods | Middleware functions |
| Koa | `app.use()` | `router.get()` | `async (ctx, next)` |

---

### Backend API (Go)

<!-- AI: Use this structure for Go backend APIs. Follows standard Go project layout conventions. -->

```
[project-name]/
├── docs/                          # Documentation
│
├── cmd/                           # Application entry points
│   └── api/
│       └── main.go                # Main entry point
│
├── internal/                      # Private application code
│   ├── config/                    # Configuration
│   │   └── config.go
│   │
│   ├── handlers/                  # HTTP handlers (controllers)
│   │   ├── handlers.go            # Handler aggregation
│   │   ├── users.go
│   │   └── [resource].go
│   │
│   ├── services/                  # Business logic
│   │   ├── users.go
│   │   └── [resource].go
│   │
│   ├── repository/                # Data access
│   │   ├── repository.go          # Interface definitions
│   │   ├── postgres/              # PostgreSQL implementation
│   │   │   └── users.go
│   │   └── memory/                # In-memory (for testing)
│   │       └── users.go
│   │
│   ├── models/                    # Domain models
│   │   └── user.go
│   │
│   └── middleware/                # HTTP middleware
│       ├── auth.go
│       └── logging.go
│
├── pkg/                           # Public, reusable packages
│   └── validator/
│       └── validator.go
│
├── migrations/                    # Database migrations
│   └── 001_initial.sql
│
├── tests/                         # Integration tests
│   └── api_test.go
│
├── .env.example
├── Dockerfile
├── go.mod
├── go.sum
└── Makefile
```

---

### Backend API (Rust)

<!-- AI: Use this structure for Rust backend APIs using Axum, Actix-web, or similar. -->

```
[project-name]/
├── docs/                          # Documentation
│
├── src/
│   ├── main.rs                    # Entry point
│   ├── lib.rs                     # Library exports
│   │
│   ├── config/
│   │   └── mod.rs                 # Configuration
│   │
│   ├── routes/                    # Route definitions
│   │   ├── mod.rs
│   │   ├── users.rs
│   │   └── [resource].rs
│   │
│   ├── handlers/                  # Request handlers
│   │   ├── mod.rs
│   │   ├── users.rs
│   │   └── [resource].rs
│   │
│   ├── services/                  # Business logic
│   │   ├── mod.rs
│   │   └── users.rs
│   │
│   ├── models/                    # Domain models
│   │   ├── mod.rs
│   │   └── user.rs
│   │
│   ├── db/                        # Database
│   │   ├── mod.rs
│   │   └── queries.rs
│   │
│   ├── middleware/                # Middleware
│   │   ├── mod.rs
│   │   └── auth.rs
│   │
│   └── error.rs                   # Error types
│
├── migrations/                    # SQLx migrations
│
├── tests/
│   └── integration_tests.rs
│
├── .env.example
├── Cargo.toml
├── Dockerfile
└── sqlx-data.json                 # SQLx offline data
```

---

### CLI Tool

<!-- AI: Use this structure for command-line applications. Works for Node.js, Go, or Rust CLIs. -->

```
[project-name]/
├── docs/                          # Documentation
│
├── src/                           # Source code
│   ├── commands/                  # Subcommand implementations
│   │   ├── init.ts                # (or .go, .rs)
│   │   ├── build.ts
│   │   └── [command].ts
│   │
│   ├── lib/                       # Core library code
│   │   ├── config.ts              # Config file loading
│   │   ├── logger.ts              # Output formatting
│   │   └── [feature].ts
│   │
│   ├── utils/                     # Utilities
│   │   ├── fs.ts                  # File system helpers
│   │   └── prompts.ts             # Interactive prompts
│   │
│   ├── types/                     # Type definitions
│   │
│   ├── cli.ts                     # CLI definition (args, help)
│   └── index.ts                   # Entry point
│
├── templates/                     # Templates (if CLI generates files)
│   └── [template-name]/
│
├── tests/
│   ├── unit/
│   └── integration/
│
├── bin/                           # Binary entry points
│   └── cli.js                     # Shebang entry (#!/usr/bin/env node)
│
├── package.json                   # With "bin" field
└── tsconfig.json
```

**Language Variations:**
| Language | Entry Point | Arg Parsing | Config |
|----------|-------------|-------------|--------|
| Node.js | `src/index.ts` | commander/yargs/cac | `package.json` bin |
| Go | `cmd/[name]/main.go` | cobra/urfave/cli | `go.mod` |
| Rust | `src/main.rs` | clap | `Cargo.toml` |

---

## Naming Conventions

<!-- AI: Select naming conventions that match your ecosystem. Consistency is more important than any specific choice. -->

### File Naming by Ecosystem

| Ecosystem | Components | Functions/Utils | Types | Tests |
|-----------|------------|-----------------|-------|-------|
| React/TS | `PascalCase.tsx` | `kebab-case.ts` | `kebab-case.types.ts` | `*.test.ts(x)` |
| Vue | `PascalCase.vue` | `kebab-case.ts` | `*.d.ts` | `*.spec.ts` |
| Angular | `kebab-case.component.ts` | `kebab-case.ts` | `*.interface.ts` | `*.spec.ts` |
| Node.js | N/A | `kebab-case.ts` | `*.types.ts` | `*.test.ts` |
| Go | `snake_case.go` | `snake_case.go` | same file | `*_test.go` |
| Rust | `snake_case.rs` | `snake_case.rs` | same file | `mod tests` |
| Python | `snake_case.py` | `snake_case.py` | type hints | `test_*.py` |

### Folder Naming

<!-- AI: Folder names should be lowercase. Use kebab-case for multi-word names in JS/TS ecosystems, snake_case for Go/Rust/Python. -->

| Convention | Example | When to Use |
|------------|---------|-------------|
| lowercase | `components/` | Always preferred for folders |
| kebab-case | `user-settings/` | Multi-word in JS/TS projects |
| snake_case | `user_settings/` | Multi-word in Go/Rust/Python |

### Special Files

| File | Purpose | Location |
|------|---------|----------|
| `index.ts` / `mod.rs` | Barrel exports | Folder root |
| `types.ts` / `*.d.ts` | Type definitions | With related code or `types/` |
| `constants.ts` | Constants | `utils/` or relevant folder |
| `README.md` | Documentation | Project root |

---

## Import Patterns

<!-- AI: Import order and style varies by ecosystem. Choose one pattern and enforce it with linting. -->

### JavaScript/TypeScript Import Order

```typescript
// 1. Node.js built-ins (with 'node:' prefix in modern code)
import path from 'node:path';
import fs from 'node:fs';

// 2. External packages (from node_modules)
import express from 'express';
import { z } from 'zod';

// 3. Internal absolute imports (using path aliases)
import { db } from '@/lib/db';
import { Button } from '@/components/ui';

// 4. Relative imports (same feature/module)
import { UserCard } from './UserCard';
import { formatUser } from './utils';

// 5. Type imports (always last, use 'import type')
import type { User } from '@/types';
import type { UserCardProps } from './UserCard.types';
```

### Path Aliases

<!-- AI: Configure path aliases in tsconfig.json or your bundler config. Common patterns: -->

```json
{
  "compilerOptions": {
    "paths": {
      "@/*": ["./src/*"],
      "@components/*": ["./src/components/*"],
      "@lib/*": ["./src/lib/*"],
      "@utils/*": ["./src/utils/*"],
      "@types/*": ["./src/types/*"]
    }
  }
}
```

### Go Import Order

```go
import (
    // Standard library
    "context"
    "fmt"

    // External packages
    "github.com/gin-gonic/gin"

    // Internal packages
    "myproject/internal/handlers"
    "myproject/internal/services"
)
```

### Rust Import Order

```rust
// Standard library
use std::collections::HashMap;

// External crates
use axum::{Router, routing::get};
use serde::{Deserialize, Serialize};

// Internal modules
use crate::handlers::users;
use crate::models::User;
```

---

## Barrel Exports (Index Files)

<!-- AI: Barrel exports simplify imports but can cause issues with tree-shaking. Use them judiciously. -->

### When to Use

| Use Case | Example |
|----------|---------|
| Shared component library | `components/ui/index.ts` exports all UI components |
| Public API of a package | `src/index.ts` exports public types and functions |
| Type re-exports | `types/index.ts` aggregates shared types |

### When NOT to Use

| Avoid When | Reason |
|------------|--------|
| Feature-specific components | Importing from index pulls unnecessary code |
| Large modules | Tree-shaking may not eliminate unused exports |
| Circular dependency risk | Index files can create import cycles |

### Example Pattern

```typescript
// src/components/ui/index.ts
export { Button } from './Button';
export { Input } from './Input';
export { Card } from './Card';

// Usage: import { Button, Input } from '@/components/ui';
```

---

## Co-location Rules

<!-- AI: Co-location keeps related files together. Define rules for what stays together vs what goes in shared folders. -->

### Co-locate (Keep Together)

| Files | Location | Rationale |
|-------|----------|-----------|
| Component + its tests | `Button/Button.test.tsx` | Tests are tightly coupled |
| Component + its types | `Button/Button.types.ts` | Types are implementation detail |
| Component + its styles | `Button/Button.module.css` | Styles are component-specific |
| Component + its stories | `Button/Button.stories.tsx` | Stories document the component |

### Separate (Shared Folders)

| Files | Location | Rationale |
|-------|----------|-----------|
| Global styles | `src/styles/` | Apply across all components |
| Shared types | `src/types/` | Used by multiple modules |
| API types | `src/types/api.types.ts` | Contract with backend |
| Test utilities | `tests/utils/` | Shared test helpers |
| Test fixtures | `tests/fixtures/` | Shared test data |

---

## File Templates

<!-- AI: Provide templates that match your project's conventions. Adjust based on your framework. -->

### Component Template (React)

```typescript
// src/components/[category]/[ComponentName].tsx
import type { [ComponentName]Props } from './[ComponentName].types';

export function [ComponentName]({ /* props */ }: [ComponentName]Props) {
  return (
    <div>
      {/* Component content */}
    </div>
  );
}
```

### Component Template (Vue)

```vue
<!-- src/components/[category]/[ComponentName].vue -->
<script setup lang="ts">
interface Props {
  // Define props
}

const props = defineProps<Props>();
</script>

<template>
  <div>
    <!-- Component content -->
  </div>
</template>

<style scoped>
/* Component styles */
</style>
```

### Service Template (Node.js)

```typescript
// src/services/[resource].service.ts
import { db } from '@/lib/db';
import type { CreateResourceInput, Resource } from '@/types';

export class ResourceService {
  async findAll(): Promise<Resource[]> {
    return db.resource.findMany();
  }

  async findById(id: string): Promise<Resource | null> {
    return db.resource.findUnique({ where: { id } });
  }

  async create(input: CreateResourceInput): Promise<Resource> {
    return db.resource.create({ data: input });
  }
}
```

### Handler Template (Go)

```go
// internal/handlers/[resource].go
package handlers

import (
    "net/http"
    "github.com/gin-gonic/gin"
)

type ResourceHandler struct {
    service *services.ResourceService
}

func NewResourceHandler(s *services.ResourceService) *ResourceHandler {
    return &ResourceHandler{service: s}
}

func (h *ResourceHandler) GetAll(c *gin.Context) {
    resources, err := h.service.FindAll(c.Request.Context())
    if err != nil {
        c.JSON(http.StatusInternalServerError, gin.H{"error": err.Error()})
        return
    }
    c.JSON(http.StatusOK, resources)
}
```

---

## Related Documents

| Document | Relationship |
|----------|--------------|
| [00-project-setup.md](./00-project-setup.md) | Project type determines base structure |
| [07-technical-architecture.md](./07-technical-architecture.md) | Architecture informs folder organization |
| [17-code-patterns.md](./17-code-patterns.md) | Patterns implemented within this structure |
| [conventions.md](../reference/conventions.md) | Naming conventions reference |

---

## AI Agent Instructions

### When to Update This Document
- After initial project setup (select base structure)
- When adding new major features (add feature folders)
- When establishing new conventions (document them here)
- When onboarding new team members (ensure accuracy)

### How to Use This Document

1. **Select Base Structure**: Choose the template matching your project type
2. **Customize for Project**: Add/remove folders based on actual needs
3. **Document Naming Rules**: Ensure team alignment on conventions
4. **Configure Path Aliases**: Set up import aliases early
5. **Define Co-location Rules**: Clarify what goes where

### Quality Checks

Before considering this document complete:
- [ ] Folder structure matches actual project
- [ ] All naming conventions documented
- [ ] Import patterns established with examples
- [ ] Path aliases configured and documented
- [ ] Co-location rules defined
- [ ] File templates provided for common patterns

### Common Issues

| Issue | Solution |
|-------|----------|
| Inconsistent naming | Enforce with ESLint/Prettier rules |
| Circular imports | Review dependency graph, restructure if needed |
| Deep nesting | Flatten structure, use path aliases |
| Missing index files | Add barrel exports for shared code |
| Unclear ownership | Each folder should have clear purpose |
