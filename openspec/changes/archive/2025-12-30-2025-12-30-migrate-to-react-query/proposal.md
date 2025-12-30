# Proposal: Migrate to TanStack Query

This proposal aims to align the `shortix-web` implementation with the project specifications by replacing the current `useState`/`useEffect` data fetching pattern with TanStack Query (React Query).

## Problem
The current implementation in `shortix-web` relies on manual state management (`useState`, `useEffect`) and Axios for data fetching. This leads to:
- Boilerplate code for loading/error states.
- Lack of caching and background synchronization.
- Manual cache invalidation (e.g., using `keyProp` in `Dashboard.tsx`).

## Proposed Solution
Introduce `@tanstack/react-query` to manage server state.
- Set up `QueryClient` and `QueryClientProvider` in `App.tsx`.
- Refactor `UrlList.tsx` to use `useQuery`.
- Refactor `CreateUrlForm.tsx` to use `useMutation`.
- Remove manual `loading`/`error` states and `useEffect` hooks for fetching.

## Goals
- Reduced boilerplate in components.
- Improved UX with automatic background refetching and caching.
- Synchronized UI after mutations (creating a URL).
