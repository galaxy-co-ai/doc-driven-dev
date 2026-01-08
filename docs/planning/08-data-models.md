# 08 - Data Models

<!-- AI: This document defines the data structures, entities, and persistence strategy for the application. Applicable to all project types that manage data. -->

## Data Modeling Overview

<!-- AI: Provide context for the data architecture:
- Primary data types being managed
- Data ownership and boundaries
- Key relationships between entities
- Read vs write patterns (read-heavy, write-heavy, balanced)
-->

### Domain Context

<!-- AI: Describe the business domain in terms of data:
- What real-world concepts does this application model?
- What are the core entities that define the domain?
- What actions/events transform data?
-->

**Domain Description**: [Brief description of what the application manages]

**Core Entities**: [List primary entities/concepts]

**Key Operations**: [List main data operations - create, transform, query]

### Data Architecture Style

<!-- AI: Document the architectural approach to data:

**Common Patterns**:
- **CRUD-centric**: Simple create/read/update/delete operations
- **Event-sourced**: Store events, derive state
- **Document-oriented**: Flexible schemas, nested data
- **Relational**: Normalized tables with foreign keys
- **Graph**: Nodes and relationships
- **Hybrid**: Combination based on use case

Choose based on:
- Query patterns (complex queries = relational, flexible = document)
- Consistency needs (strict = relational, eventual = document/event)
- Scale requirements (horizontal = document/event, vertical = relational)
-->

**Pattern**: [CRUD/Event-sourced/Document/Relational/Graph/Hybrid]

**Rationale**: [Why this pattern fits]

---

## Entity Definitions

<!-- AI: Define each entity/model in the system. Use language-agnostic notation that can be translated to any implementation.

For each entity, document:
1. Purpose: What real-world concept this represents
2. Fields: All attributes with types and constraints
3. Relationships: How it connects to other entities
4. Lifecycle: How instances are created, modified, deleted
-->

### Entity: [EntityName]

<!-- AI: Template for entity definition. Repeat for each entity.

Use generic type notation:
- string, text (short vs long)
- integer, float, decimal
- boolean
- datetime, date, timestamp
- enum(value1, value2, ...)
- uuid, id
- reference(OtherEntity)
- array(type)
- map/object
- optional(type) for nullable fields
-->

**Purpose**: [What this entity represents in the domain]

**Fields**:
| Field | Type | Required | Constraints | Description |
|-------|------|----------|-------------|-------------|
| id | uuid | Yes | Primary key | Unique identifier |
| [field_name] | [type] | [Yes/No] | [constraints] | [description] |
| created_at | timestamp | Yes | Auto-set | Creation time |
| updated_at | timestamp | Yes | Auto-update | Last modification time |

**Relationships**:
| Relationship | Target | Cardinality | Description |
|--------------|--------|-------------|-------------|
| [relationship_name] | [TargetEntity] | [1:1, 1:N, N:M] | [description] |

**Indexes** (if applicable):
| Index | Fields | Type | Purpose |
|-------|--------|------|---------|
| [index_name] | [field(s)] | [unique/btree/hash/text] | [why needed] |

**Lifecycle**:
- **Created**: [When/how instances are created]
- **Modified**: [What operations update instances]
- **Deleted**: [Soft delete? Hard delete? Cascade rules?]

**Example Instance**:
```json
{
  "id": "[example_id]",
  "[field]": "[example_value]"
}
```

### Entity: [NextEntity]

<!-- AI: Repeat structure for each entity -->

---

## Entity Relationship Diagram

<!-- AI: Visualize relationships between entities. Use ASCII or reference external diagram.

Format:
```
┌─────────────┐       1:N       ┌─────────────┐
│   Entity A  │─────────────────│   Entity B  │
└─────────────┘                 └─────────────┘
      │                               │
      │ 1:1                           │ N:M
      ▼                               ▼
┌─────────────┐                 ┌─────────────┐
│   Entity C  │                 │   Entity D  │
└─────────────┘                 └─────────────┘
```

Notation:
- 1:1 = One to one
- 1:N = One to many
- N:M = Many to many
-->

```
[Entity relationship diagram]
```

---

## Data Types and Enums

<!-- AI: Define reusable types and enumerations used across entities -->

### Custom Types

<!-- AI: Define any custom/composite types -->

**Type: [TypeName]**
```
{
  [field]: [type]
}
```

### Enumerations

<!-- AI: Define all enum types used in entities -->

**Enum: [EnumName]**
| Value | Description |
|-------|-------------|
| [value1] | [what this value means] |
| [value2] | [what this value means] |

---

## Validation Rules

<!-- AI: Document validation rules beyond simple type constraints. These ensure data integrity at the application level. -->

### Field-Level Validation

<!-- AI: Rules that apply to individual fields -->

| Entity | Field | Rule | Error Message |
|--------|-------|------|---------------|
| [Entity] | [field] | [rule description] | [user-facing message] |

**Common Rule Types**:
- Required: Must have a value
- Length: min/max characters
- Range: min/max numeric value
- Pattern: regex match (email, phone, etc.)
- Enum: must be one of allowed values
- Unique: no duplicates allowed
- Custom: business logic validation

### Entity-Level Validation

<!-- AI: Rules that span multiple fields or require context -->

| Entity | Rule | Description |
|--------|------|-------------|
| [Entity] | [rule_name] | [description of cross-field validation] |

### Business Rules

<!-- AI: Validation that depends on business logic or external state -->

| Rule | Entities Involved | Description |
|------|-------------------|-------------|
| [rule_name] | [Entity1, Entity2] | [business constraint] |

---

## Persistence Strategy

<!-- AI: Document how and where data is stored. Choose based on project requirements. -->

### Storage Comparison

<!-- AI: Help choose the right storage solution:

**SQL Databases** (PostgreSQL, MySQL, SQLite):
- Best for: Structured data, complex queries, transactions, data integrity
- Avoid when: Highly variable schemas, massive horizontal scale needs

**NoSQL Document** (MongoDB, CouchDB, Firestore):
- Best for: Flexible schemas, rapid iteration, hierarchical data
- Avoid when: Complex joins needed, strict consistency required

**Key-Value** (Redis, DynamoDB):
- Best for: Simple lookups, caching, session storage, high throughput
- Avoid when: Complex queries, relationships needed

**File-based** (JSON files, SQLite, embedded):
- Best for: Desktop apps, single-user, offline-first, simple data
- Avoid when: Concurrent access, large datasets, complex queries

**In-Memory** (application state only):
- Best for: Temporary data, computed values, performance-critical
- Avoid when: Data must survive restarts
-->

### Chosen Strategy

<!-- AI: Document the chosen persistence approach for each data category -->

| Data Category | Storage Type | Technology | Rationale |
|---------------|--------------|------------|-----------|
| [Category 1] | [SQL/NoSQL/File/Memory] | [Specific tech] | [Why] |
| [Category 2] | [SQL/NoSQL/File/Memory] | [Specific tech] | [Why] |

### Storage Location Mapping

<!-- AI: Map entities to their storage locations -->

| Entity | Storage | Table/Collection/File | Notes |
|--------|---------|----------------------|-------|
| [Entity1] | [Storage name] | [table/collection name] | [notes] |

### Sensitive Data Handling

<!-- AI: Identify and document handling for sensitive data -->

| Data | Sensitivity Level | Storage Approach | Encryption |
|------|-------------------|------------------|------------|
| [field/entity] | [PII/Secret/Confidential] | [how stored] | [Yes/No, method] |

---

## State Management (UI Applications)

<!-- AI: For applications with UI, document how data flows through the application state. Skip for pure backends/CLIs. -->

### Global State Structure

<!-- AI: Define the shape of application-wide state -->

```
AppState {
  [domain1]: {
    [slice of state]
  },
  [domain2]: {
    [slice of state]
  },
  ui: {
    [UI-specific state]
  }
}
```

### State Domains

<!-- AI: Break down each state domain -->

**Domain: [DomainName]**
| Key | Type | Source | Description |
|-----|------|--------|-------------|
| [key] | [type] | [API/local/computed] | [what this represents] |

### State Synchronization

<!-- AI: How local state syncs with persistent storage -->

| State | Sync Strategy | Trigger | Conflict Resolution |
|-------|---------------|---------|---------------------|
| [state key] | [push/pull/realtime] | [on change/on interval/manual] | [last-write-wins/merge/manual] |

---

## Data Flow Diagrams

<!-- AI: Visualize how data moves through the system for key operations -->

### Flow: [Operation Name]

<!-- AI: Document data flow for key operations. Example: "User creates a new item"

Format:
```
[Source] → [Transform/Validate] → [Store] → [Notify] → [Update UI]
```
-->

**Trigger**: [What initiates this flow]

```
[Step-by-step flow diagram]
```

**Side Effects**: [What else happens as a result]

---

## Migration Strategy

<!-- AI: Document how data schema changes are handled over time -->

### Migration Approach

<!-- AI: Choose migration strategy:

**For SQL databases**:
- Migration files (up/down scripts)
- Tools: Prisma, TypeORM, Knex, Alembic, Flyway

**For NoSQL**:
- Application-level migration
- Dual-write during transition
- Lazy migration on read

**For file-based**:
- Version field in data
- Migration on app startup

**For mobile/desktop**:
- Similar to file-based, with version checks
-->

**Strategy**: [Migration approach]

**Tool/Process**: [Migration tool or manual process]

### Migration Guidelines

<!-- AI: Document guidelines for writing migrations -->

1. **Forward-only**: [Do you support rollback?]
2. **Zero-downtime**: [Required? If so, approach?]
3. **Data preservation**: [How to handle data transformation?]
4. **Testing**: [How are migrations tested?]

### Version History

<!-- AI: Track schema versions and major changes -->

| Version | Date | Changes | Migration Notes |
|---------|------|---------|-----------------|
| [v1] | [date] | Initial schema | - |
| [v2] | [date] | [changes] | [notes] |

---

## Query Patterns

<!-- AI: Document common query patterns for performance optimization -->

### Read Patterns

<!-- AI: Document common read operations -->

| Query | Frequency | Entities | Indexes Needed |
|-------|-----------|----------|----------------|
| [query description] | [High/Medium/Low] | [entities involved] | [index requirements] |

### Write Patterns

<!-- AI: Document common write operations -->

| Operation | Frequency | Entities | Transaction Required |
|-----------|-----------|----------|---------------------|
| [operation description] | [High/Medium/Low] | [entities involved] | [Yes/No] |

### Performance Considerations

<!-- AI: Note any performance-critical queries or patterns -->

| Concern | Pattern | Mitigation |
|---------|---------|------------|
| [concern, e.g., N+1 queries] | [where it occurs] | [solution] |

---

## Related Documents

<!-- AI: Link to related documents. Ensure bidirectional linking. -->

| Document | Relationship |
|----------|--------------|
| [09 - API Contracts](./09-api-contracts.md) | API endpoints that expose this data |
| [07 - Technical Architecture](./07-technical-architecture.md) | System architecture containing data layer |
| [11 - Security Considerations](./11-security-considerations.md) | Security requirements for data |
| [10 - Error Handling](./10-error-handling.md) | Error handling for data operations |
| [03 - Product Requirements](./03-product-requirements.md) | Business requirements driving data needs |

---

## AI Agent Instructions

<!-- AI: Instructions for AI agents working with this document -->

### When Populating This Document

1. **Start from requirements**: Reference doc 03 to understand what data the product needs
2. **Identify entities from features**: Each feature in doc 04 likely has associated data
3. **Define relationships early**: Entity relationships drive schema design
4. **Be explicit about constraints**: Document all validation rules, not just "obvious" ones
5. **Choose persistence based on requirements**: Don't default to SQL or NoSQL - evaluate

### When Implementing Data Layer

1. **Generate from this doc**: Use entity definitions to generate models/schemas
2. **Implement validation first**: Validation rules should be enforced at the data layer
3. **Create migrations incrementally**: One migration per logical change
4. **Index early**: Add indexes documented here from the start
5. **Handle sensitive data carefully**: Follow the encryption/storage guidelines

### Quality Checklist

Before marking this document complete:
- [ ] All entities from features (doc 04) are defined
- [ ] All relationships have cardinality documented
- [ ] Validation rules cover all constraints
- [ ] Persistence strategy chosen and justified
- [ ] Sensitive data handling documented
- [ ] Migration approach defined
- [ ] Related Documents links are bidirectional
