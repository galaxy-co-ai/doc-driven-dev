# 17 - Code Patterns

<!-- AI: This document defines code patterns and conventions for your project. The patterns are explained conceptually first, then shown with framework-specific examples. Adapt examples to match your tech stack. -->

---

## How to Use This Document

<!-- AI: This document contains two types of content:
1. **Conceptual explanations** - Framework-agnostic descriptions of patterns
2. **Code examples** - Labeled by framework (React, Vue, Go, etc.)

When implementing for your project:
- Read the conceptual explanation to understand the "why"
- Find examples matching your stack, or adapt similar examples
- If your framework isn't shown, use the concept to create your own implementation
-->

---

## Component Patterns

### Concept: Component Structure

A well-structured component:
- Has a single responsibility
- Separates concerns (logic vs presentation)
- Uses clear interfaces (props/inputs)
- Handles its own error states
- Is testable in isolation

### Example: Reference Component (React)

```typescript
// src/components/feature/UserCard.tsx
import { memo } from 'react';
import { formatDate } from '@/utils/format-date';
import type { UserCardProps } from './UserCard.types';

/**
 * Displays a user's profile card with avatar and basic info.
 *
 * @example
 * <UserCard user={user} onSelect={handleSelect} />
 */
export const UserCard = memo(function UserCard({
  user,
  isSelected = false,
  onSelect,
}: UserCardProps) {
  const handleClick = () => {
    onSelect?.(user.id);
  };

  return (
    <div
      className={`user-card ${isSelected ? 'user-card--selected' : ''}`}
      onClick={handleClick}
      data-testid="user-card"
    >
      <img
        src={user.avatarUrl}
        alt={`${user.name}'s avatar`}
        className="user-card__avatar"
      />
      <div className="user-card__info">
        <h3 className="user-card__name">{user.name}</h3>
        <span className="user-card__joined">
          Joined {formatDate(user.createdAt)}
        </span>
      </div>
    </div>
  );
});
```

```typescript
// src/components/feature/UserCard.types.ts
import type { User } from '@/types';

export interface UserCardProps {
  user: User;
  isSelected?: boolean;
  onSelect?: (userId: string) => void;
}
```

### Example: Reference Component (Vue)

```vue
<!-- src/components/feature/UserCard.vue -->
<script setup lang="ts">
import { computed } from 'vue';
import { formatDate } from '@/utils/format-date';
import type { User } from '@/types';

interface Props {
  user: User;
  isSelected?: boolean;
}

const props = withDefaults(defineProps<Props>(), {
  isSelected: false,
});

const emit = defineEmits<{
  select: [userId: string];
}>();

const handleClick = () => {
  emit('select', props.user.id);
};

const cardClass = computed(() => ({
  'user-card': true,
  'user-card--selected': props.isSelected,
}));
</script>

<template>
  <div :class="cardClass" @click="handleClick" data-testid="user-card">
    <img
      :src="user.avatarUrl"
      :alt="`${user.name}'s avatar`"
      class="user-card__avatar"
    />
    <div class="user-card__info">
      <h3 class="user-card__name">{{ user.name }}</h3>
      <span class="user-card__joined">
        Joined {{ formatDate(user.createdAt) }}
      </span>
    </div>
  </div>
</template>
```

---

## State Management Patterns

### Concept: State Management

State management approaches vary by complexity:

| Complexity | Approach | When to Use |
|------------|----------|-------------|
| Simple | Component state | Single component needs |
| Medium | Context/Providers | Shared state across component tree |
| Complex | Global store | App-wide state, multiple consumers |
| Server | Query libraries | Remote data with caching needs |

**Key principles:**
- Keep state as local as possible
- Derive computed values, don't duplicate
- Separate UI state from server state
- Make state updates predictable

### Example: Store Pattern (React + Zustand)

```typescript
// src/stores/user.store.ts
import { create } from 'zustand';
import { persist } from 'zustand/middleware';
import type { User } from '@/types';

interface UserState {
  // State
  currentUser: User | null;
  isAuthenticated: boolean;

  // Actions
  setUser: (user: User) => void;
  clearUser: () => void;
}

export const useUserStore = create<UserState>()(
  persist(
    (set) => ({
      currentUser: null,
      isAuthenticated: false,

      setUser: (user) => set({
        currentUser: user,
        isAuthenticated: true
      }),

      clearUser: () => set({
        currentUser: null,
        isAuthenticated: false
      }),
    }),
    {
      name: 'user-storage',
      partialize: (state) => ({ currentUser: state.currentUser }),
    }
  )
);
```

### Example: Store Pattern (Vue + Pinia)

```typescript
// src/stores/user.ts
import { defineStore } from 'pinia';
import type { User } from '@/types';

export const useUserStore = defineStore('user', {
  state: () => ({
    currentUser: null as User | null,
  }),

  getters: {
    isAuthenticated: (state) => state.currentUser !== null,
  },

  actions: {
    setUser(user: User) {
      this.currentUser = user;
    },

    clearUser() {
      this.currentUser = null;
    },
  },

  persist: {
    paths: ['currentUser'],
  },
});
```

---

## Data Fetching Patterns

### Concept: Data Fetching

Modern data fetching handles:
- Loading states
- Error states
- Caching and revalidation
- Optimistic updates
- Request deduplication

**Key principles:**
- Separate data fetching from UI components
- Handle all states (loading, error, success, empty)
- Cache server data appropriately
- Show meaningful loading indicators

### Example: Data Fetching Hook (React + TanStack Query)

```typescript
// src/hooks/use-users.ts
import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query';
import { userService } from '@/services/user.service';
import type { User, CreateUserInput } from '@/types';

export function useUsers() {
  return useQuery({
    queryKey: ['users'],
    queryFn: () => userService.getAll(),
  });
}

export function useUser(userId: string | null) {
  return useQuery({
    queryKey: ['users', userId],
    queryFn: () => userService.getById(userId!),
    enabled: !!userId,
  });
}

export function useCreateUser() {
  const queryClient = useQueryClient();

  return useMutation({
    mutationFn: (input: CreateUserInput) => userService.create(input),
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['users'] });
    },
  });
}
```

### Example: Data Fetching (Vue Composable)

```typescript
// src/composables/useUsers.ts
import { ref, computed, watchEffect } from 'vue';
import { userService } from '@/services/user.service';
import type { User } from '@/types';

export function useUsers() {
  const users = ref<User[]>([]);
  const isLoading = ref(false);
  const error = ref<Error | null>(null);

  async function fetchUsers() {
    isLoading.value = true;
    error.value = null;
    try {
      users.value = await userService.getAll();
    } catch (e) {
      error.value = e as Error;
    } finally {
      isLoading.value = false;
    }
  }

  return {
    users: computed(() => users.value),
    isLoading: computed(() => isLoading.value),
    error: computed(() => error.value),
    fetchUsers,
  };
}
```

### Example: Data Fetching (SSR - Next.js)

```typescript
// src/app/users/page.tsx (Next.js App Router)
import { userService } from '@/lib/user.service';
import { UserList } from '@/components/UserList';

// Server Component - fetches on server
export default async function UsersPage() {
  const users = await userService.getAll();

  return (
    <div>
      <h1>Users</h1>
      <UserList users={users} />
    </div>
  );
}
```

---

## Form Handling Patterns

### Concept: Form Handling

Form handling involves:
- Controlled inputs (form state)
- Validation (sync and async)
- Error display
- Submission handling
- Loading states

**Key principles:**
- Validate on blur for immediate feedback
- Show errors near the relevant field
- Disable submit during loading
- Handle server validation errors

### Example: Form Pattern (React + React Hook Form)

```typescript
// src/components/forms/UserForm.tsx
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { z } from 'zod';

const userSchema = z.object({
  name: z.string().min(2, 'Name must be at least 2 characters'),
  email: z.string().email('Invalid email address'),
  role: z.enum(['admin', 'user', 'guest']),
});

type UserFormData = z.infer<typeof userSchema>;

interface UserFormProps {
  onSubmit: (data: UserFormData) => Promise<void>;
  defaultValues?: Partial<UserFormData>;
}

export function UserForm({ onSubmit, defaultValues }: UserFormProps) {
  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
  } = useForm<UserFormData>({
    resolver: zodResolver(userSchema),
    defaultValues,
  });

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <div>
        <label htmlFor="name">Name</label>
        <input id="name" {...register('name')} />
        {errors.name && (
          <span className="error">{errors.name.message}</span>
        )}
      </div>

      <div>
        <label htmlFor="email">Email</label>
        <input id="email" type="email" {...register('email')} />
        {errors.email && (
          <span className="error">{errors.email.message}</span>
        )}
      </div>

      <div>
        <label htmlFor="role">Role</label>
        <select id="role" {...register('role')}>
          <option value="user">User</option>
          <option value="admin">Admin</option>
          <option value="guest">Guest</option>
        </select>
        {errors.role && (
          <span className="error">{errors.role.message}</span>
        )}
      </div>

      <button type="submit" disabled={isSubmitting}>
        {isSubmitting ? 'Saving...' : 'Save'}
      </button>
    </form>
  );
}
```

### Example: Form Pattern (Vue + VeeValidate)

```vue
<!-- src/components/forms/UserForm.vue -->
<script setup lang="ts">
import { useForm } from 'vee-validate';
import { toTypedSchema } from '@vee-validate/zod';
import { z } from 'zod';

const userSchema = toTypedSchema(
  z.object({
    name: z.string().min(2, 'Name must be at least 2 characters'),
    email: z.string().email('Invalid email address'),
    role: z.enum(['admin', 'user', 'guest']),
  })
);

const { handleSubmit, errors, isSubmitting, defineField } = useForm({
  validationSchema: userSchema,
});

const [name, nameAttrs] = defineField('name');
const [email, emailAttrs] = defineField('email');
const [role, roleAttrs] = defineField('role');

const emit = defineEmits<{
  submit: [data: { name: string; email: string; role: string }];
}>();

const onSubmit = handleSubmit((values) => {
  emit('submit', values);
});
</script>

<template>
  <form @submit="onSubmit">
    <div>
      <label for="name">Name</label>
      <input id="name" v-model="name" v-bind="nameAttrs" />
      <span v-if="errors.name" class="error">{{ errors.name }}</span>
    </div>

    <div>
      <label for="email">Email</label>
      <input id="email" type="email" v-model="email" v-bind="emailAttrs" />
      <span v-if="errors.email" class="error">{{ errors.email }}</span>
    </div>

    <div>
      <label for="role">Role</label>
      <select id="role" v-model="role" v-bind="roleAttrs">
        <option value="user">User</option>
        <option value="admin">Admin</option>
        <option value="guest">Guest</option>
      </select>
      <span v-if="errors.role" class="error">{{ errors.role }}</span>
    </div>

    <button type="submit" :disabled="isSubmitting">
      {{ isSubmitting ? 'Saving...' : 'Save' }}
    </button>
  </form>
</template>
```

---

## Authentication Patterns

### Concept: Authentication

Authentication typically involves:
- Login/logout flows
- Token storage (secure)
- Protected routes/pages
- Session refresh
- Role-based access

**Key principles:**
- Store tokens securely (httpOnly cookies preferred)
- Check auth state on app load
- Handle token expiration gracefully
- Redirect unauthenticated users appropriately

### Example: Auth Context (React)

```typescript
// src/contexts/auth.context.tsx
import { createContext, useContext, useState, useEffect, ReactNode } from 'react';
import { authService } from '@/services/auth.service';
import type { User } from '@/types';

interface AuthContextValue {
  user: User | null;
  isLoading: boolean;
  isAuthenticated: boolean;
  login: (email: string, password: string) => Promise<void>;
  logout: () => Promise<void>;
}

const AuthContext = createContext<AuthContextValue | null>(null);

export function AuthProvider({ children }: { children: ReactNode }) {
  const [user, setUser] = useState<User | null>(null);
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    // Check for existing session on mount
    authService.getCurrentUser()
      .then(setUser)
      .catch(() => setUser(null))
      .finally(() => setIsLoading(false));
  }, []);

  const login = async (email: string, password: string) => {
    const user = await authService.login(email, password);
    setUser(user);
  };

  const logout = async () => {
    await authService.logout();
    setUser(null);
  };

  return (
    <AuthContext.Provider
      value={{
        user,
        isLoading,
        isAuthenticated: !!user,
        login,
        logout
      }}
    >
      {children}
    </AuthContext.Provider>
  );
}

export function useAuth() {
  const context = useContext(AuthContext);
  if (!context) {
    throw new Error('useAuth must be used within AuthProvider');
  }
  return context;
}
```

### Example: Protected Route (React)

```typescript
// src/components/auth/ProtectedRoute.tsx
import { Navigate, useLocation } from 'react-router-dom';
import { useAuth } from '@/contexts/auth.context';

interface ProtectedRouteProps {
  children: React.ReactNode;
  requiredRole?: string;
}

export function ProtectedRoute({ children, requiredRole }: ProtectedRouteProps) {
  const { isAuthenticated, isLoading, user } = useAuth();
  const location = useLocation();

  if (isLoading) {
    return <div>Loading...</div>;
  }

  if (!isAuthenticated) {
    return <Navigate to="/login" state={{ from: location }} replace />;
  }

  if (requiredRole && user?.role !== requiredRole) {
    return <Navigate to="/unauthorized" replace />;
  }

  return <>{children}</>;
}
```

### Example: Auth Middleware (Node.js/Express)

```typescript
// src/middleware/auth.middleware.ts
import { Request, Response, NextFunction } from 'express';
import { verifyToken } from '@/lib/jwt';
import { userService } from '@/services/user.service';

export async function authenticate(
  req: Request,
  res: Response,
  next: NextFunction
) {
  const token = req.headers.authorization?.replace('Bearer ', '');

  if (!token) {
    return res.status(401).json({ error: 'Authentication required' });
  }

  try {
    const payload = verifyToken(token);
    const user = await userService.findById(payload.userId);

    if (!user) {
      return res.status(401).json({ error: 'User not found' });
    }

    req.user = user;
    next();
  } catch (error) {
    return res.status(401).json({ error: 'Invalid token' });
  }
}

export function requireRole(...roles: string[]) {
  return (req: Request, res: Response, next: NextFunction) => {
    if (!req.user) {
      return res.status(401).json({ error: 'Authentication required' });
    }

    if (!roles.includes(req.user.role)) {
      return res.status(403).json({ error: 'Insufficient permissions' });
    }

    next();
  };
}
```

---

## Testing Patterns

### Concept: Testing Strategy

Testing levels and their purposes:

| Level | What It Tests | Tools (JS) |
|-------|--------------|------------|
| Unit | Individual functions, utilities | Vitest, Jest |
| Component | UI components in isolation | Testing Library |
| Integration | Multiple units working together | Testing Library, Supertest |
| E2E | Full user flows | Playwright, Cypress |

**Key principles:**
- Test behavior, not implementation
- Prefer integration tests for confidence
- Mock external dependencies, not internal code
- Keep tests fast and reliable

### Example: Unit Test (Vitest)

```typescript
// src/utils/format-date.test.ts
import { describe, it, expect, beforeEach, vi } from 'vitest';
import { formatDate, formatRelativeTime } from './format-date';

describe('formatDate', () => {
  beforeEach(() => {
    // Mock current date for consistent tests
    vi.useFakeTimers();
    vi.setSystemTime(new Date('2024-01-15T12:00:00Z'));
  });

  it('formats today\'s date as time only', () => {
    const today = new Date('2024-01-15T09:30:00Z');
    expect(formatDate(today)).toBe('9:30 AM');
  });

  it('formats older dates with month and day', () => {
    const older = new Date('2024-01-10T09:30:00Z');
    expect(formatDate(older)).toBe('Jan 10');
  });

  it('handles string input', () => {
    expect(formatDate('2024-01-15T09:30:00Z')).toBe('9:30 AM');
  });
});

describe('formatRelativeTime', () => {
  it('returns "just now" for recent times', () => {
    const recent = new Date(Date.now() - 30000); // 30 seconds ago
    expect(formatRelativeTime(recent)).toBe('just now');
  });

  it('returns minutes ago', () => {
    const minutes = new Date(Date.now() - 5 * 60 * 1000);
    expect(formatRelativeTime(minutes)).toBe('5 minutes ago');
  });
});
```

### Example: Component Test (React + Testing Library)

```typescript
// src/components/feature/UserCard.test.tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { describe, it, expect, vi } from 'vitest';
import { UserCard } from './UserCard';

const mockUser = {
  id: '1',
  name: 'John Doe',
  avatarUrl: 'https://example.com/avatar.jpg',
  createdAt: new Date('2024-01-01'),
};

describe('UserCard', () => {
  it('renders user information', () => {
    render(<UserCard user={mockUser} />);

    expect(screen.getByText('John Doe')).toBeInTheDocument();
    expect(screen.getByAltText("John Doe's avatar")).toBeInTheDocument();
  });

  it('calls onSelect when clicked', () => {
    const onSelect = vi.fn();
    render(<UserCard user={mockUser} onSelect={onSelect} />);

    fireEvent.click(screen.getByTestId('user-card'));

    expect(onSelect).toHaveBeenCalledWith('1');
  });

  it('applies selected class when isSelected is true', () => {
    render(<UserCard user={mockUser} isSelected />);

    expect(screen.getByTestId('user-card')).toHaveClass('user-card--selected');
  });

  it('does not call onSelect when not provided', () => {
    render(<UserCard user={mockUser} />);

    // Should not throw
    fireEvent.click(screen.getByTestId('user-card'));
  });
});
```

### Example: API Integration Test (Node.js + Supertest)

```typescript
// tests/integration/users.test.ts
import { describe, it, expect, beforeAll, afterAll } from 'vitest';
import request from 'supertest';
import { app } from '@/app';
import { db } from '@/lib/db';

describe('Users API', () => {
  beforeAll(async () => {
    // Setup: seed test data
    await db.user.create({
      data: { id: 'test-1', name: 'Test User', email: 'test@example.com' },
    });
  });

  afterAll(async () => {
    // Cleanup
    await db.user.deleteMany({ where: { id: { startsWith: 'test-' } } });
  });

  describe('GET /api/users', () => {
    it('returns list of users', async () => {
      const response = await request(app)
        .get('/api/users')
        .expect(200);

      expect(response.body).toBeInstanceOf(Array);
      expect(response.body.length).toBeGreaterThan(0);
    });
  });

  describe('POST /api/users', () => {
    it('creates a new user', async () => {
      const newUser = { name: 'New User', email: 'new@example.com' };

      const response = await request(app)
        .post('/api/users')
        .send(newUser)
        .expect(201);

      expect(response.body).toMatchObject(newUser);
      expect(response.body.id).toBeDefined();
    });

    it('returns 400 for invalid input', async () => {
      const response = await request(app)
        .post('/api/users')
        .send({ name: '' }) // Missing email, empty name
        .expect(400);

      expect(response.body.error).toBeDefined();
    });
  });
});
```

---

## Error Handling Patterns

### Concept: Error Handling

Errors should be:
- Caught at appropriate boundaries
- Logged with context
- Presented helpfully to users
- Recoverable when possible

### Example: Error Boundary (React)

```typescript
// src/components/shared/ErrorBoundary.tsx
import { Component, ErrorInfo, ReactNode } from 'react';

interface Props {
  children: ReactNode;
  fallback?: ReactNode | ((error: Error) => ReactNode);
  onError?: (error: Error, errorInfo: ErrorInfo) => void;
}

interface State {
  hasError: boolean;
  error: Error | null;
}

export class ErrorBoundary extends Component<Props, State> {
  state: State = { hasError: false, error: null };

  static getDerivedStateFromError(error: Error): State {
    return { hasError: true, error };
  }

  componentDidCatch(error: Error, errorInfo: ErrorInfo) {
    console.error('Error caught by boundary:', error, errorInfo);
    this.props.onError?.(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      if (typeof this.props.fallback === 'function') {
        return this.props.fallback(this.state.error!);
      }
      return this.props.fallback || (
        <div className="error-fallback">
          <h2>Something went wrong</h2>
          <button onClick={() => this.setState({ hasError: false, error: null })}>
            Try again
          </button>
        </div>
      );
    }
    return this.props.children;
  }
}
```

### Example: Service Error Handling (TypeScript)

```typescript
// src/lib/errors.ts
export class AppError extends Error {
  constructor(
    message: string,
    public code: string,
    public statusCode: number = 500,
    public isOperational: boolean = true
  ) {
    super(message);
    this.name = 'AppError';
    Error.captureStackTrace(this, this.constructor);
  }
}

export class NotFoundError extends AppError {
  constructor(resource: string, id: string) {
    super(`${resource} with id ${id} not found`, 'NOT_FOUND', 404);
  }
}

export class ValidationError extends AppError {
  constructor(message: string, public fields?: Record<string, string>) {
    super(message, 'VALIDATION_ERROR', 400);
  }
}

export class UnauthorizedError extends AppError {
  constructor(message = 'Authentication required') {
    super(message, 'UNAUTHORIZED', 401);
  }
}
```

---

## Loading State Patterns

### Concept: Loading States

UI should communicate:
- When data is being fetched
- Progress (if determinable)
- Empty states
- Error states

### Example: Loading States (React)

```typescript
// src/components/shared/AsyncContent.tsx
import type { ReactNode } from 'react';

interface AsyncContentProps<T> {
  isLoading: boolean;
  error: Error | null;
  data: T | null;
  loadingFallback?: ReactNode;
  errorFallback?: ReactNode | ((error: Error) => ReactNode);
  emptyFallback?: ReactNode;
  children: (data: T) => ReactNode;
}

export function AsyncContent<T>({
  isLoading,
  error,
  data,
  loadingFallback = <LoadingSkeleton />,
  errorFallback,
  emptyFallback = <EmptyState />,
  children,
}: AsyncContentProps<T>) {
  if (isLoading) {
    return <>{loadingFallback}</>;
  }

  if (error) {
    if (typeof errorFallback === 'function') {
      return <>{errorFallback(error)}</>;
    }
    return <>{errorFallback || <ErrorDisplay error={error} />}</>;
  }

  if (!data || (Array.isArray(data) && data.length === 0)) {
    return <>{emptyFallback}</>;
  }

  return <>{children(data)}</>;
}

// Usage:
// <AsyncContent
//   isLoading={isLoading}
//   error={error}
//   data={users}
// >
//   {(users) => <UserList users={users} />}
// </AsyncContent>
```

---

## Anti-Patterns (Avoid These)

### Do Not: Inline Complex Logic in Templates

```typescript
// Bad - hard to read and test
<div>
  {items.filter(i => i.active && i.createdAt > cutoffDate)
    .sort((a, b) => b.priority - a.priority)
    .map(i => <Item key={i.id} {...i} />)}
</div>

// Good - extract to variable or hook
const sortedActiveItems = useMemo(() =>
  items
    .filter(i => i.active && i.createdAt > cutoffDate)
    .sort((a, b) => b.priority - a.priority),
  [items, cutoffDate]
);

<div>
  {sortedActiveItems.map(i => <Item key={i.id} {...i} />)}
</div>
```

### Do Not: Direct DOM Manipulation (in Declarative Frameworks)

```typescript
// Bad - breaks React's model
function handleClick() {
  document.getElementById('my-element')!.style.color = 'red';
}

// Good - use state
const [color, setColor] = useState('black');
const handleClick = () => setColor('red');
<div style={{ color }}>...</div>
```

### Do Not: Forget Cleanup in Effects

```typescript
// Bad - memory leak
useEffect(() => {
  const interval = setInterval(tick, 1000);
  // Missing cleanup!
}, []);

// Good - always cleanup
useEffect(() => {
  const interval = setInterval(tick, 1000);
  return () => clearInterval(interval);
}, []);
```

### Do Not: Mutate State Directly

```typescript
// Bad - mutation doesn't trigger re-render
function addItem(item: Item) {
  items.push(item); // DON'T DO THIS
  setItems(items);
}

// Good - create new reference
function addItem(item: Item) {
  setItems([...items, item]);
}
```

### Do Not: Ignore Error States

```typescript
// Bad - fails silently
async function fetchData() {
  const data = await api.getData();
  setData(data);
}

// Good - handle errors
async function fetchData() {
  setIsLoading(true);
  setError(null);
  try {
    const data = await api.getData();
    setData(data);
  } catch (error) {
    setError(error as Error);
  } finally {
    setIsLoading(false);
  }
}
```

---

## Related Documents

| Document | Relationship |
|----------|--------------|
| [10-error-handling.md](./10-error-handling.md) | Error handling strategy details |
| [12-testing-strategy.md](./12-testing-strategy.md) | Testing approach and coverage goals |
| [15-file-architecture.md](./15-file-architecture.md) | Where to put pattern implementations |
| [16-design-tokens.md](./16-design-tokens.md) | Styling patterns and tokens |
| [conventions.md](../reference/conventions.md) | Code style conventions |

---

## AI Agent Instructions

### When to Update This Document
- When establishing new patterns for the project
- When adding examples for additional frameworks
- When discovering anti-patterns during code review
- When onboarding highlights missing pattern documentation

### How to Use This Document

1. **Understand Concepts First**: Read the concept section before copying code
2. **Find Your Framework**: Look for examples matching your stack
3. **Adapt as Needed**: Examples are starting points, not rigid templates
4. **Document New Patterns**: Add patterns discovered during development
5. **Reference in Code Review**: Use as shared vocabulary for discussions

### Quality Checks

Before considering this document complete:
- [ ] All major patterns have conceptual explanations
- [ ] Examples provided for primary project framework
- [ ] Anti-patterns documented with correct alternatives
- [ ] Testing patterns cover all test levels used in project
- [ ] Error handling patterns align with 10-error-handling.md

### Adding New Patterns

When adding a new pattern:
1. Start with the concept (framework-agnostic)
2. Explain when and why to use it
3. Provide at least one code example
4. Label examples by framework clearly
5. Include any gotchas or common mistakes
