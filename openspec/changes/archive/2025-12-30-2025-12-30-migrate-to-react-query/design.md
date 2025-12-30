# Design: React Query Migration

## Architecture
We will use `@tanstack/react-query` (v5) to manage all server-side state in `shortix-web`.

### 1. Provider Setup
`QueryClient` will be initialized in `App.tsx` and wrapped around the application using `QueryClientProvider`.

### 2. Data Fetching Pattern
- **Fetching:** Use `useQuery` for GET requests (listing URLs).
- **Mutations:** Use `useMutation` for POST/PUT/DELETE requests (creating a URL).

### 3. Cache Invalidation
Instead of using `keyProp` to force a re-render of `UrlList`, we will use `queryClient.invalidateQueries({ queryKey: ['urls'] })` inside the `onSuccess` callback of the `createUrl` mutation.

### 4. Dependencies
- `@tanstack/react-query`
- `@tanstack/react-query-devtools` (for development)
