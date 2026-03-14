# Tools

## Runtime
- **OpenCode** is your runtime.

## Paperclip API
- `GET /api/agents/me` — identity.
- `GET /api/companies/{companyId}/issues?assigneeAgentId={agentId}&status=todo,in_progress,blocked` — inbox.
- `PATCH /api/issues/{issueId}` — status updates. Include `X-Paperclip-Run-Id`.

---

## Test Stack

| Package | Purpose |
|---------|---------|
| `vitest` | Test runner |
| `@testing-library/react` | Component testing |
| `@testing-library/jest-dom` | Custom matchers |
| `@testing-library/user-event` | User interaction simulation |
| `msw` | API mocking (Mock Service Worker) |

```bash
npx vitest run                                    # All tests
npx vitest run --coverage                         # With coverage
npx vitest run components/Button/Button.test.tsx  # Specific file
```

---

## Skills

### 1. TDD — test-driven-development (obra/superpowers, 23K)

**IRON LAW: NO CODE WITHOUT A FAILING TEST FIRST.**

| Phase | Action | Verify |
|-------|--------|--------|
| 🔴 RED | Write ONE failing test (one behavior, clear name) | Run → MUST FAIL |
| 🟢 GREEN | Write MINIMAL code to pass (no extras) | Run ALL → ALL PASS |
| 🔵 REFACTOR | Remove duplication, improve names | Run ALL → STILL PASS |

Write code before test? **Delete it.** No "reference," no "adapting." Delete means delete.

### 2. Web App Testing — webapp-testing (anthropics, 22K)
- `render()` to mount · `screen.getByRole()` for queries · `userEvent` for interactions
- `waitFor()` for async · MSW for API mocking (never mock fetch directly)

### 3. Systematic Debugging — systematic-debugging (obra/superpowers, 28K)
When tests fail: Root Cause → Pattern Analysis → Hypothesis (SINGLE change) → Fix at root cause

### 4. Verification — verification-before-completion (obra, 16K)
Run `npx vitest run`, read FULL output, only report PASS if exit code 0 + all tests pass.

---

## Testing Patterns (Minimal Reference)

### Component Test
```tsx
render(<Button>Click me</Button>)
expect(screen.getByRole('button', { name: 'Click me' })).toBeInTheDocument()
expect(screen.getByRole('button')).toBeDisabled()
```

### User Interaction
```tsx
await userEvent.type(screen.getByLabelText('Email'), 'test@example.com')
await userEvent.click(screen.getByRole('button', { name: 'Sign in' }))
expect(onSubmit).toHaveBeenCalledWith({ email: 'test@example.com' })
```

### API Mock (MSW)
```tsx
const server = setupServer(
  http.get('/api/users', () => HttpResponse.json([{ id: 1, name: 'Alice' }]))
)
beforeAll(() => server.listen())
afterEach(() => server.resetHandlers())
afterAll(() => server.close())

// Error case:
server.use(http.get('/api/users', () => HttpResponse.error()))
```

### Zustand Store
```tsx
const { result } = renderHook(() => useAuthStore())
act(() => result.current.login({ id: 1, name: 'Alice' }))
expect(result.current.isAuthenticated).toBe(true)
```

### Custom Hook
```tsx
const { result, rerender } = renderHook(
  ({ value }) => useDebounce(value, 500),
  { initialProps: { value: 'initial' } }
)
rerender({ value: 'updated' })
await waitFor(() => expect(result.current).toBe('updated'), { timeout: 600 })
```

---

## File Naming
```
components/feature-name/
├── FeatureName.tsx           → FeatureName.test.tsx
├── useFeatureName.ts         → useFeatureName.test.ts
stores/featureStore.ts        → featureStore.test.ts
```

## Rules
- DO NOT test shadcn/ui components (tested upstream)
- `getByRole()` + `getByLabelText()` over `getByTestId()`
- `userEvent` over `fireEvent`
- MSW for API mocking, never mock `fetch`
- One test file per source file
- Run ALL tests before reporting
