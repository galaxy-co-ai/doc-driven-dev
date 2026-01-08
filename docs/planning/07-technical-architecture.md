# 07 - Technical Architecture

<!-- AI: This document defines the system architecture for your project. Select the appropriate architecture pattern based on the project type identified in 00-project-setup.md. Remove architecture patterns that don't apply. -->

---

## Architecture Pattern Selection

<!-- AI: Based on the project type from 00-project-setup.md, select ONE primary architecture pattern below. Delete the others or mark them as secondary if you have a hybrid architecture (e.g., SPA frontend + Backend API). -->

| Project Type | Primary Pattern | When to Use |
|--------------|-----------------|-------------|
| Web SPA | Client-Side Architecture | Interactive apps, dashboards, tools |
| Web SSR | Server-Rendered Architecture | Content sites, SEO-critical apps, e-commerce |
| Desktop | Desktop App Architecture | Native apps with system access |
| Mobile | Mobile App Architecture | iOS/Android native or cross-platform |
| Backend API | Server Architecture | APIs, microservices, data processing |
| CLI Tool | CLI Architecture | Command-line utilities, developer tools |

---

## System Architecture Diagrams

### Template: How to Draw Architecture Diagrams

<!-- AI: Use ASCII diagrams for portability. Include:
- All major layers/components
- Data flow direction (arrows)
- External integrations
- Persistence layer if applicable
-->

```
Key symbols:
┌─────────┐     Box: Component/Layer
│         │
└─────────┘

    │
    ▼           Arrow: Data flow direction

    ─────       Line: Connection

[  Name  ]      External system

{  Name  }      Data store
```

---

### SPA (Single Page Application) Architecture

<!-- AI: Use this pattern for React, Vue, Svelte, Angular apps that run primarily in the browser. -->

```
┌─────────────────────────────────────────────────────────────┐
│                    Browser (Client)                         │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────────────────────────────────────────────┐    │
│  │                  UI Framework                        │    │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────────────┐   │    │
│  │  │Components│  │  State   │  │    Routing       │   │    │
│  │  └──────────┘  └──────────┘  └──────────────────┘   │    │
│  └─────────────────────┬───────────────────────────────┘    │
│                        │ HTTP/WebSocket                     │
└────────────────────────┼────────────────────────────────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │   Backend API       │
              │   (REST/GraphQL)    │
              └─────────────────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │   External Services │
              │   (Auth, Storage)   │
              └─────────────────────┘
```

**Characteristics:**
- Single HTML page, JavaScript handles all rendering
- Client-side routing (no full page reloads)
- State managed in browser (memory, localStorage)
- Communicates with backend via API calls

---

### SSR (Server-Side Rendering) Architecture

<!-- AI: Use this pattern for Next.js, Nuxt, SvelteKit, Remix apps with server rendering. -->

```
┌─────────────────────────────────────────────────────────────┐
│                       Browser                               │
│  ┌─────────────────────────────────────────────────────┐    │
│  │              Hydrated UI Framework                   │    │
│  │  (Interactive after initial server-rendered HTML)    │    │
│  └─────────────────────┬───────────────────────────────┘    │
└────────────────────────┼────────────────────────────────────┘
                         │ HTTP (HTML + JSON)
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                    Application Server                       │
├─────────────────────────────────────────────────────────────┤
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐    │
│  │  Routes  │  │ Loaders  │  │ Actions  │  │  SSR     │    │
│  │          │  │ (data)   │  │ (forms)  │  │ Renderer │    │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘    │
└─────────────────────┬───────────────────────────────────────┘
                      │
          ┌───────────┴───────────┐
          ▼                       ▼
   { Database }          [ External APIs ]
```

**Characteristics:**
- Initial HTML rendered on server
- Hydration enables interactivity after load
- Built-in data fetching at route level
- Better SEO, faster initial paint

---

### Desktop Application Architecture

<!-- AI: Use this pattern for Tauri, Electron, or native desktop applications. -->

```
┌─────────────────────────────────────────────────────────────┐
│                    Desktop Application                      │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────────────────────────────────────────────┐    │
│  │                   UI Layer                           │    │
│  │  (Web: HTML/CSS/JS  OR  Native: Qt/GTK/SwiftUI)     │    │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────────────┐   │    │
│  │  │  Views   │  │  State   │  │   Event Handlers │   │    │
│  │  └──────────┘  └──────────┘  └──────────────────┘   │    │
│  └─────────────────────┬───────────────────────────────┘    │
│                        │ IPC / Bridge / Direct call         │
│  ┌─────────────────────┴───────────────────────────────┐    │
│  │               Native Backend                         │    │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────────────┐   │    │
│  │  │ Commands │  │  State   │  │  System Access   │   │    │
│  │  │          │  │ Manager  │  │  (FS, Network)   │   │    │
│  │  └──────────┘  └──────────┘  └──────────────────┘   │    │
│  └─────────────────────────────────────────────────────┘    │
└───────────────────────────┬─────────────────────────────────┘
                            │
            ┌───────────────┼───────────────┐
            ▼               ▼               ▼
      { Local DB }   [ External API ]  { File System }
```

**Characteristics:**
- Native shell provides system access
- UI can be web-based (Electron/Tauri) or native
- IPC bridges UI and native code
- Full filesystem and OS access

---

### Mobile Application Architecture

<!-- AI: Use this pattern for React Native, Flutter, or native iOS/Android apps. -->

```
┌─────────────────────────────────────────────────────────────┐
│                    Mobile Application                       │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────────────────────────────────────────────┐    │
│  │                  UI Layer                            │    │
│  │  (React Native / Flutter / SwiftUI / Jetpack)       │    │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────────────┐   │    │
│  │  │ Screens  │  │Navigation│  │    Components    │   │    │
│  │  └──────────┘  └──────────┘  └──────────────────┘   │    │
│  └─────────────────────┬───────────────────────────────┘    │
│                        │                                    │
│  ┌─────────────────────┴───────────────────────────────┐    │
│  │              State & Business Logic                  │    │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────────────┐   │    │
│  │  │  State   │  │ Services │  │  Native Modules  │   │    │
│  │  │ Manager  │  │          │  │  (Camera, GPS)   │   │    │
│  │  └──────────┘  └──────────┘  └──────────────────┘   │    │
│  └─────────────────────────────────────────────────────┘    │
└───────────────────────────┬─────────────────────────────────┘
                            │
            ┌───────────────┼───────────────┐
            ▼               ▼               ▼
      { Local DB }   [ Backend API ]  { Secure Storage }
       (SQLite)       (REST/GraphQL)    (Keychain)
```

**Characteristics:**
- Platform-specific UI rendering
- Bridge for native device features
- Offline-first with local database
- Push notifications via platform services

---

### Backend API Architecture

<!-- AI: Use this pattern for REST/GraphQL APIs, microservices, or data processing backends. -->

```
┌─────────────────────────────────────────────────────────────┐
│                 API Gateway / Load Balancer                 │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                   Application Server                        │
├─────────────────────────────────────────────────────────────┤
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐    │
│  │  Routes  │  │Middleware│  │Controllers│  │ Services │    │
│  │          │  │ (Auth,   │  │           │  │ (Business│    │
│  │          │  │  Logging)│  │           │  │  Logic)  │    │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘    │
│                                                             │
│  ┌──────────┐  ┌──────────┐  ┌──────────────────────────┐  │
│  │   ORM/   │  │  Cache   │  │     External Service     │  │
│  │  Query   │  │  Layer   │  │      Integrations        │  │
│  └──────────┘  └──────────┘  └──────────────────────────┘  │
└───────────────────────────┬─────────────────────────────────┘
                            │
            ┌───────────────┼───────────────┐
            ▼               ▼               ▼
      { Database }    { Cache }      [ External APIs ]
       (SQL/NoSQL)    (Redis)         (Payment, Email)
```

**Characteristics:**
- Stateless request handling
- Layered architecture (routes → controllers → services)
- Database abstraction via ORM or query builder
- Horizontal scaling possible

---

### CLI Tool Architecture

<!-- AI: Use this pattern for command-line tools and developer utilities. -->

```
┌─────────────────────────────────────────────────────────────┐
│                      CLI Application                        │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────────────────────────────────────────────┐    │
│  │                  Entry Point                         │    │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────────────┐   │    │
│  │  │  Arg     │  │ Command  │  │     Help /       │   │    │
│  │  │  Parser  │  │ Router   │  │   Version Info   │   │    │
│  │  └──────────┘  └──────────┘  └──────────────────┘   │    │
│  └─────────────────────┬───────────────────────────────┘    │
│                        │                                    │
│  ┌─────────────────────┴───────────────────────────────┐    │
│  │                   Commands                           │    │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────────────┐   │    │
│  │  │  init    │  │   run    │  │     build        │   │    │
│  │  │          │  │          │  │                  │   │    │
│  │  └──────────┘  └──────────┘  └──────────────────┘   │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐    │
│  │                Core Utilities                        │    │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────────────┐   │    │
│  │  │   I/O    │  │  Config  │  │     Logging      │   │    │
│  │  │  Helpers │  │  Loader  │  │                  │   │    │
│  │  └──────────┘  └──────────┘  └──────────────────┘   │    │
│  └─────────────────────────────────────────────────────┘    │
└───────────────────────────┬─────────────────────────────────┘
                            │
            ┌───────────────┼───────────────┐
            ▼               ▼               ▼
      { Config File }  { File System }  [ stdout/stderr ]
```

**Characteristics:**
- Single entry point with argument parsing
- Subcommand pattern for complex tools
- Configuration from files and environment
- Exit codes for scripting integration

---

## Tech Stack

<!-- AI: Fill in this table based on the project requirements. Use specific versions when known, or version ranges (e.g., "v18.x+") when flexible. Mark decisions as [TBD] only if genuinely undecided. -->

### Stack Selection Guidance

| Layer | Questions to Answer |
|-------|---------------------|
| Runtime/Framework | What platform constraints exist? What team experience? |
| Language | Type safety needs? Performance requirements? Ecosystem? |
| UI Framework | SSR needs? Component library availability? Bundle size? |
| State Management | Complexity level? Server state vs client state? |
| Database | Relational vs document? Scale requirements? Hosted vs self-managed? |
| Build Tool | Monorepo? Build speed priority? Plugin ecosystem needs? |

### Tech Stack Table

<!-- AI: Copy and fill this template. Add/remove rows as needed for your stack. -->

| Layer | Technology | Version | Rationale |
|-------|------------|---------|-----------|
<!-- AI: Add row for each technology choice. Example rows: -->
<!-- | Runtime | Node.js | 20.x LTS | Team familiarity, ecosystem | -->
<!-- | Framework | Next.js | 14.x | SSR needs, file-based routing | -->
<!-- | Language | TypeScript | 5.x | Type safety, IDE support | -->
<!-- | Database | PostgreSQL | 16.x | Relational needs, JSON support | -->
<!-- | ORM | Prisma | 5.x | Type-safe queries, migrations | -->
<!-- | Testing | Vitest | 1.x | Fast, Vite-compatible | -->

---

## Data Flow

<!-- AI: Document how data moves through your application. Adapt based on your architecture pattern. -->

### Request/Response Flow

<!-- AI: Describe the typical request lifecycle. Example: -->

```
<!-- AI: Replace with your actual data flow. Examples below for different architectures: -->

[SPA Example]
User Action → Component Event → State Update → API Call → Backend Processing
                                                                    │
                                                                    ▼
Component Update ← State Update ← Response Parsing ← API Response ←─┘

[SSR Example]
Browser Request → Server Route → Data Loader → Database Query
                                                      │
                                                      ▼
Browser Render ← Hydration ← HTML Response ← Server Render ←─┘

[API Example]
HTTP Request → Middleware → Route Handler → Service → Repository → Database
                                                                       │
                                                                       ▼
HTTP Response ← Serialization ← Service Response ← Query Result ←──────┘
```

### State Flow

<!-- AI: Document how state is managed and synchronized. Consider:
- Where is the source of truth?
- How do components/modules get notified of changes?
- What persistence strategy is used?
-->

---

## Key Architectural Decisions

<!-- AI: Document significant architectural choices using this format. These should be non-trivial decisions that affect the overall system. For full decision records, use 18-decision-log.md. -->

### Decision Template

```
### Decision: [Short title]
- **Context**: What situation or problem prompted this decision?
- **Options Considered**: What alternatives were evaluated?
- **Choice**: What was decided?
- **Rationale**: Why was this chosen over alternatives?
- **Trade-offs**: What are the downsides of this choice?
- **Consequences**: What does this mean for implementation?
```

### Guidance: What Warrants an Architectural Decision?

Document decisions about:
- Framework/library selection (especially if multiple viable options exist)
- Data storage approach (SQL vs NoSQL, local vs cloud)
- Authentication/authorization strategy
- API design (REST vs GraphQL vs gRPC)
- Deployment architecture (serverless vs containers vs VMs)
- State management approach
- Caching strategy
- Error handling philosophy

### Example Decisions (Delete after reading)

<!-- AI: Here are example decisions showing the format. Delete these and add your actual decisions. -->

```
### Decision: Server-Side Rendering Framework
- **Context**: Need SEO for marketing pages while maintaining SPA-like interactivity
- **Options Considered**: Next.js, Remix, SvelteKit, Astro
- **Choice**: Next.js 14 with App Router
- **Rationale**: Team TypeScript experience, large ecosystem, Vercel deployment simplicity
- **Trade-offs**: Larger bundle than Astro, vendor lock-in risk with Vercel features
- **Consequences**: Use Server Components by default, Client Components only when needed
```

```
### Decision: Database Selection
- **Context**: Application needs relational data with complex queries
- **Options Considered**: PostgreSQL, MySQL, SQLite, MongoDB
- **Choice**: PostgreSQL via Supabase
- **Rationale**: JSON support for flexible fields, excellent query performance, managed hosting
- **Trade-offs**: More complex than SQLite for simple apps, hosting cost
- **Consequences**: Use Prisma ORM, leverage Postgres-specific features (arrays, JSONB)
```

---

## Build & Development

<!-- AI: Document commands for each stage of development. Adapt based on your package manager and tooling. -->

### Command Reference

| Stage | Command | Description |
|-------|---------|-------------|
| Install | `<!-- AI: e.g., npm install, pnpm install, cargo build -->` | Install dependencies |
| Dev | `<!-- AI: e.g., npm run dev, cargo run -->` | Start development server |
| Build | `<!-- AI: e.g., npm run build, cargo build --release -->` | Production build |
| Test | `<!-- AI: e.g., npm test, cargo test -->` | Run tests |
| Lint | `<!-- AI: e.g., npm run lint, cargo clippy -->` | Run linters |
| Format | `<!-- AI: e.g., npm run format, cargo fmt -->` | Format code |

### Environment Configuration

<!-- AI: Document environment variables needed for development. Do not include actual secrets. -->

| Variable | Required | Description | Example |
|----------|----------|-------------|---------|
<!-- AI: Add environment variables your app needs. Example: -->
<!-- | DATABASE_URL | Yes | Database connection string | postgres://... | -->
<!-- | API_KEY | Yes | External API authentication | (from provider) | -->
<!-- | NODE_ENV | No | Environment mode | development | -->

### Build Outputs

<!-- AI: Document what the build produces and where it goes. -->

| Platform/Target | Output Location | Format |
|-----------------|-----------------|--------|
<!-- AI: Add build outputs. Examples: -->
<!-- | Web | dist/ | Static files (HTML, JS, CSS) | -->
<!-- | Desktop (Windows) | target/release/ | .exe, .msi | -->
<!-- | Desktop (macOS) | target/release/ | .app, .dmg | -->
<!-- | Docker | - | Container image | -->

---

## Deployment Architecture

<!-- AI: Document how the application is deployed and hosted. -->

### Deployment Strategy

<!-- AI: Select and document your deployment approach. Options include:
- Static hosting (Vercel, Netlify, S3+CloudFront)
- Container orchestration (Docker, Kubernetes)
- Serverless functions (AWS Lambda, Vercel Functions)
- Traditional server (VPS, dedicated)
- App stores (iOS App Store, Google Play, Steam)
- Package registries (npm, crates.io, PyPI)
-->

### Infrastructure Diagram

```
<!-- AI: Draw deployment architecture. Example: -->

[Users] → [CDN] → [Load Balancer] → [App Servers] → [Database]
                                  ↘ [Background Jobs] ↗
```

### Scaling Considerations

<!-- AI: Document how the system scales. Consider:
- What are the bottlenecks?
- What scales horizontally vs vertically?
- What caching strategies are used?
-->

---

## Related Documents

| Document | Relationship |
|----------|--------------|
| [00-project-setup.md](./00-project-setup.md) | Project type determines architecture pattern |
| [03-product-requirements.md](./03-product-requirements.md) | Requirements inform architectural constraints |
| [08-data-models.md](./08-data-models.md) | Data layer implementation details |
| [09-api-contracts.md](./09-api-contracts.md) | API design and contracts |
| [15-file-architecture.md](./15-file-architecture.md) | Folder structure implementation |
| [18-decision-log.md](./18-decision-log.md) | Full architectural decision records |
| [19-cicd-pipeline.md](./19-cicd-pipeline.md) | Build and deployment automation |

---

## AI Agent Instructions

### When to Update This Document
- After initial project setup (select architecture pattern)
- When making significant technology choices
- When adding major new components or integrations
- Before starting implementation phase

### How to Use This Document

1. **Start with Architecture Selection**: Choose the primary pattern based on project type
2. **Fill Tech Stack**: Document all technology choices with rationale
3. **Document Data Flow**: Show how information moves through the system
4. **Record Decisions**: Add architectural decisions as they're made
5. **Define Commands**: Ensure all build/dev/test commands are documented

### Quality Checks

Before considering this document complete:
- [ ] Single architecture pattern selected (or hybrid clearly explained)
- [ ] All tech stack layers documented with versions
- [ ] Data flow diagram matches actual implementation plan
- [ ] At least 2-3 key architectural decisions documented
- [ ] All build commands tested and working
- [ ] Deployment target identified
- [ ] Related documents cross-referenced

### Common Issues

| Issue | Solution |
|-------|----------|
| Architecture too complex | Start simple, add complexity only when needed |
| Missing rationale | Every tech choice should explain "why" |
| Outdated versions | Update versions before implementation starts |
| No deployment plan | Define target environment early to avoid surprises |
