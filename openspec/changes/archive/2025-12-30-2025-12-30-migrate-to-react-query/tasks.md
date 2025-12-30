# Tasks: Migrate to TanStack Query

- [x] Core Setup [x]
    - [x] Install `@tanstack/react-query`
    - [x] Configure `QueryClientProvider` in `App.tsx`
- [x] Refactor URL Listing [x]
    - [x] Create `useUrls` hook (optional but recommended) or implement `useQuery` in `UrlList.tsx`
    - [x] Remove `useEffect` and manual loading/error states from `UrlList.tsx`
- [x] Refactor URL Creation [x]
    - [x] Implement `useMutation` in `CreateUrlForm.tsx`
    - [x] Handle cache invalidation for `['urls']` on success
    - [x] Remove manual `loading` state from `CreateUrlForm.tsx`
- [x] Verification [x]
    - [x] Verify background refetching
    - [x] Verify UI updates immediately after creation
    - [x] Run `npm run build`
