# 09 - API Contracts

<!-- AI: This document defines all interfaces between components of the system, including external APIs consumed, APIs exposed, and internal communication protocols. Applicable to any project that communicates across boundaries (network, process, module). -->

## API Architecture Overview

<!-- AI: Provide context for the API landscape:
- What APIs does this application consume (external)?
- What APIs does this application expose (if any)?
- What internal communication patterns exist (IPC, events, messages)?
-->

### API Landscape

<!-- AI: Map all API boundaries in the system -->

| Boundary | Type | Protocol | Direction |
|----------|------|----------|-----------|
| [API Name] | [External/Exposed/Internal] | [REST/GraphQL/gRPC/WebSocket/IPC] | [Consume/Expose/Bidirectional] |

### Communication Protocols Comparison

<!-- AI: Help choose appropriate protocols. Reference this when adding new APIs.

**REST (HTTP/JSON)**:
- Best for: Public APIs, CRUD operations, caching, wide client support
- Avoid when: Real-time needs, complex queries, bandwidth constraints

**GraphQL**:
- Best for: Complex data needs, client-driven queries, avoiding over/under-fetching
- Avoid when: Simple CRUD, caching is critical, small team

**gRPC (Protocol Buffers)**:
- Best for: Microservices, high performance, streaming, type safety
- Avoid when: Browser clients, simple APIs, wide language support needed

**WebSocket**:
- Best for: Real-time updates, bidirectional communication, live data
- Avoid when: Simple request/response, SEO concerns, stateless needs

**IPC (Inter-Process Communication)**:
- Best for: Desktop apps (Electron/Tauri), native-web bridges, local services
- Frameworks: Tauri commands, Electron IPC, Unix sockets, Windows named pipes

**Message Queues** (RabbitMQ, Kafka):
- Best for: Async processing, decoupling, reliability, high throughput
- Avoid when: Synchronous needs, simple architectures
-->

---

## External APIs Consumed

<!-- AI: Document all external/third-party APIs the application uses -->

### API: [Service Name]

<!-- AI: Template for external API documentation. Repeat for each external service.

Include:
1. Purpose: Why we use this API
2. Authentication: How we authenticate
3. Key endpoints: Most-used endpoints
4. Rate limits: Known limits and how we handle them
5. Error handling: How we handle API errors
-->

**Purpose**: [What this API provides to our application]

**Base URL**: `[base_url]`

**Documentation**: [Link to official docs]

**Authentication**:
| Method | Location | Format |
|--------|----------|--------|
| [API Key/OAuth/JWT] | [Header/Query/Body] | [Format details] |

**Environment Variables**:
```
[ENV_VAR_NAME]=[description, not actual value]
```

#### Endpoint: [Endpoint Name]

<!-- AI: Document each endpoint we use. Focus on our usage, not full API docs. -->

**Request**:
```
[METHOD] [path]
```

**Headers**:
| Header | Value | Required |
|--------|-------|----------|
| [header] | [value/description] | [Yes/No] |

**Request Body** (if applicable):
```json
{
  "[field]": "[type] - [description]"
}
```

**Response**:
```json
{
  "[field]": "[type] - [description]"
}
```

**Error Codes**:
| Code | Meaning | Our Handling |
|------|---------|--------------|
| [status] | [meaning] | [how we handle it] |

**Rate Limits**:
- Limit: [X requests per Y time]
- Our approach: [How we stay within limits]

#### Endpoint: [Next Endpoint]

<!-- AI: Repeat for each endpoint used -->

---

### API: [Next External Service]

<!-- AI: Repeat structure for each external API -->

---

## APIs Exposed

<!-- AI: Document APIs this application exposes for external/internal consumers. Skip if this is a client-only application. -->

### API Design Decisions

<!-- AI: Document API design choices -->

**Protocol**: [REST/GraphQL/gRPC]

**Rationale**: [Why this protocol]

**Conventions**:
- Naming: [snake_case/camelCase/kebab-case]
- Versioning: [URL path/Header/Query param]
- Pagination: [Cursor/Offset/Keyset]
- Filtering: [Query params/Request body]

### Base Configuration

**Base URL**: `[scheme]://[host]/[base_path]`

**Versioning**: `[strategy]` (e.g., `/api/v1/...`)

**Content Type**: `application/json` (or other)

### Authentication

<!-- AI: Document authentication for exposed APIs -->

**Method**: [JWT/API Key/OAuth 2.0/Session/None]

**Flow**:
```
[Step-by-step authentication flow]
```

**Token Format** (if applicable):
```json
{
  "[claim]": "[description]"
}
```

**Authorization**: [How permissions are enforced - RBAC, ABAC, etc.]

### Standard Response Format

<!-- AI: Define consistent response structure -->

**Success Response**:
```json
{
  "data": "[response payload]",
  "meta": {
    "timestamp": "[ISO 8601 datetime]",
    "requestId": "[request tracking ID]"
  }
}
```

**Error Response**:
```json
{
  "error": {
    "code": "[error_code]",
    "message": "[human-readable message]",
    "details": "[additional context, optional]"
  },
  "meta": {
    "timestamp": "[ISO 8601 datetime]",
    "requestId": "[request tracking ID]"
  }
}
```

### Standard Error Codes

| HTTP Status | Error Code | Description |
|-------------|------------|-------------|
| 400 | validation_error | Request validation failed |
| 401 | unauthorized | Authentication required |
| 403 | forbidden | Insufficient permissions |
| 404 | not_found | Resource not found |
| 409 | conflict | Resource conflict (duplicate, version mismatch) |
| 422 | unprocessable | Business logic validation failed |
| 429 | rate_limited | Too many requests |
| 500 | internal_error | Unexpected server error |

### Endpoints

#### Resource: [ResourceName]

<!-- AI: Group endpoints by resource/domain. Document each endpoint. -->

##### List [Resources]

**Endpoint**: `GET /[resources]`

**Description**: [What this endpoint does]

**Authentication**: [Required/Optional/None]

**Authorization**: [Permission required]

**Query Parameters**:
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| page | integer | No | 1 | Page number |
| limit | integer | No | 20 | Items per page (max 100) |
| [param] | [type] | [Yes/No] | [default] | [description] |

**Response** (200 OK):
```json
{
  "data": [
    {
      "[field]": "[type]"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 100,
    "totalPages": 5
  }
}
```

##### Get [Resource]

**Endpoint**: `GET /[resources]/{id}`

**Description**: [What this endpoint does]

**Path Parameters**:
| Parameter | Type | Description |
|-----------|------|-------------|
| id | uuid | Resource identifier |

**Response** (200 OK):
```json
{
  "data": {
    "[field]": "[type]"
  }
}
```

##### Create [Resource]

**Endpoint**: `POST /[resources]`

**Description**: [What this endpoint does]

**Request Body**:
```json
{
  "[field]": "[type] - [description]"
}
```

**Response** (201 Created):
```json
{
  "data": {
    "id": "[uuid]",
    "[field]": "[value]"
  }
}
```

##### Update [Resource]

**Endpoint**: `PUT /[resources]/{id}` or `PATCH /[resources]/{id}`

**Description**: [Full update (PUT) or partial update (PATCH)]

**Request Body**:
```json
{
  "[field]": "[type] - [description]"
}
```

**Response** (200 OK):
```json
{
  "data": {
    "[updated resource]"
  }
}
```

##### Delete [Resource]

**Endpoint**: `DELETE /[resources]/{id}`

**Description**: [What happens on delete - soft delete, cascade, etc.]

**Response** (204 No Content): Empty body

#### Resource: [Next Resource]

<!-- AI: Repeat for each resource -->

---

## Internal Communication (IPC/Events)

<!-- AI: Document internal communication patterns. Applicable to:
- Desktop apps (Electron, Tauri) with frontend-backend communication
- Microservices with message passing
- Event-driven architectures
-->

### IPC Pattern Selection

<!-- AI: Choose and document IPC pattern:

**Desktop App IPC (Tauri, Electron)**:
- Tauri: Commands (invoke) and Events (emit/listen)
- Electron: ipcMain/ipcRenderer

**Microservices**:
- Sync: REST/gRPC between services
- Async: Message queues (RabbitMQ, Kafka, SQS)

**Event-Driven**:
- In-process: Event emitters, pub/sub
- Cross-process: Message brokers, webhooks
-->

**Pattern**: [Commands + Events / Request-Reply / Pub-Sub / etc.]

**Framework/Technology**: [Tauri IPC / Electron IPC / RabbitMQ / Kafka / Custom]

### Commands/Invocations

<!-- AI: Document synchronous command-style communication (request-response) -->

#### Command: [command_name]

**Direction**: [Frontend → Backend / Service A → Service B]

**Purpose**: [What this command does]

**Request**:
```[language]
// Request type/structure
{
  [parameter]: [type]
}
```

**Response**:
```[language]
// Response type/structure
{
  [field]: [type]
}
```

**Errors**:
| Error | Condition | Handling |
|-------|-----------|----------|
| [error_type] | [when it occurs] | [how caller handles it] |

**Example**:
```[language]
// How to invoke this command
[invocation example]
```

### Events/Messages

<!-- AI: Document asynchronous event-based communication -->

#### Event: [event_name]

**Direction**: [Backend → Frontend / Publisher → Subscribers]

**Purpose**: [What triggers this event and why]

**Payload**:
```[language]
{
  [field]: [type]
}
```

**Subscribers**: [Who listens for this event]

**Delivery Guarantee**: [At-most-once / At-least-once / Exactly-once]

**Example**:
```[language]
// How to emit and listen for this event
[example code]
```

---

## WebSocket Contracts (Real-time)

<!-- AI: Document WebSocket communication if applicable. Skip if not using real-time. -->

### Connection

**URL**: `ws[s]://[host]/[path]`

**Authentication**: [How connection is authenticated]

**Connection Lifecycle**:
1. Client connects to [URL]
2. [Authentication handshake if any]
3. Server sends [initial message type]
4. Bidirectional communication begins

### Message Types

<!-- AI: Document each message type -->

#### Message: [message_type]

**Direction**: [Client → Server / Server → Client / Bidirectional]

**Purpose**: [What this message accomplishes]

**Payload**:
```json
{
  "type": "[message_type]",
  "data": {
    "[field]": "[type]"
  }
}
```

**Response** (if applicable):
```json
{
  "type": "[response_type]",
  "data": {
    "[field]": "[type]"
  }
}
```

### Error Handling

**Error Message Format**:
```json
{
  "type": "error",
  "error": {
    "code": "[error_code]",
    "message": "[description]"
  }
}
```

**Reconnection Strategy**:
- Retry delay: [initial delay]
- Backoff: [exponential/linear/fixed]
- Max retries: [number or infinite]

---

## API Versioning Strategy

<!-- AI: Document how API changes are managed -->

### Versioning Approach

<!-- AI: Choose versioning strategy:

**URL Path Versioning** (`/api/v1/...`):
- Pros: Clear, cacheable, easy routing
- Cons: URL changes, client updates required

**Header Versioning** (`Accept: application/vnd.api.v1+json`):
- Pros: Clean URLs, resource-centric
- Cons: Less visible, harder to test

**Query Parameter** (`?version=1`):
- Pros: Easy to add, visible
- Cons: Not RESTful, caching issues
-->

**Strategy**: [URL Path / Header / Query Parameter]

**Current Version**: [v1]

**Deprecation Policy**:
- Old versions supported for: [time period]
- Deprecation notice: [How communicated - header, docs, etc.]
- Migration guides: [Where provided]

### Breaking vs Non-Breaking Changes

**Non-Breaking (safe)**:
- Adding new optional fields
- Adding new endpoints
- Adding new query parameters

**Breaking (requires new version)**:
- Removing/renaming fields
- Changing field types
- Changing authentication
- Removing endpoints

---

## Rate Limiting

<!-- AI: Document rate limiting for exposed APIs. Skip if not applicable. -->

### Limits

| Endpoint Pattern | Limit | Window | Scope |
|------------------|-------|--------|-------|
| [pattern or *] | [requests] | [per second/minute/hour] | [per user/per IP/global] |

### Response Headers

```
X-RateLimit-Limit: [max requests]
X-RateLimit-Remaining: [remaining requests]
X-RateLimit-Reset: [unix timestamp when limit resets]
```

### Exceeded Response

**Status**: 429 Too Many Requests

```json
{
  "error": {
    "code": "rate_limited",
    "message": "Too many requests",
    "retryAfter": [seconds until reset]
  }
}
```

---

## Related Documents

<!-- AI: Link to related documents. Ensure bidirectional linking. -->

| Document | Relationship |
|----------|--------------|
| [08 - Data Models](./08-data-models.md) | Data structures these APIs transfer |
| [07 - Technical Architecture](./07-technical-architecture.md) | System architecture showing API boundaries |
| [10 - Error Handling](./10-error-handling.md) | Error handling patterns for API calls |
| [11 - Security Considerations](./11-security-considerations.md) | Security requirements for APIs |
| [12 - Testing Strategy](./12-testing-strategy.md) | API testing approach |

---

## AI Agent Instructions

<!-- AI: Instructions for AI agents working with this document -->

### When Populating This Document

1. **Start from architecture**: Reference doc 07 to identify all API boundaries
2. **Use data models**: Reference doc 08 for request/response shapes
3. **Be specific about types**: Don't use "any" or "object" - define structures
4. **Document all error cases**: Every endpoint should have error documentation
5. **Include examples**: Real-looking example requests/responses help understanding

### When Implementing APIs

1. **Generate types from contracts**: Use this doc to generate TypeScript/OpenAPI/Proto definitions
2. **Implement validation**: All documented constraints should be enforced
3. **Match error codes exactly**: Use the documented error codes and formats
4. **Test against contracts**: Verify implementation matches documentation
5. **Update doc on changes**: If implementation requires changes, update this doc first

### Quality Checklist

Before marking this document complete:
- [ ] All external APIs consumed are documented
- [ ] All exposed APIs have complete endpoint documentation
- [ ] All IPC/internal communication is documented
- [ ] Authentication/authorization is clear for each API
- [ ] Error handling is documented for each endpoint
- [ ] Rate limiting is defined (if applicable)
- [ ] Versioning strategy is documented
- [ ] Related Documents links are bidirectional
