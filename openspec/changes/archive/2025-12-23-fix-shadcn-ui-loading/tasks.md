## 1. Environment Preparation
- [x] 1.1 Install `@tailwindcss/vite` as a dev dependency in `shortix-web`
- [x] 1.2 Verify `tailwindcss` version is `^4.0.0` or higher in `package.json`

## 2. Configuration & Styling
- [x] 2.1 Update `shortix-web/vite.config.ts` to include the `@tailwindcss/vite` plugin
- [x] 2.2 Migrate `shortix-web/src/index.css` to Tailwind v4 syntax:
    - Replace `@tailwind` directives with `@import "tailwindcss";`
    - Add `@theme` block and map CSS variables to Tailwind theme properties
- [x] 2.3 Remove legacy `tailwind.config.js` from `shortix-web`

## 3. Verification
- [x] 3.1 Run `npm run dev` and verify no build errors
- [x] 3.2 Verify Shadcn component styling in the browser (e.g., primary buttons are correctly colored)
- [x] 3.3 Verify Tailwind animations are working (if used)
