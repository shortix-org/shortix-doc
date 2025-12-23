# Change: Fix Shadcn UI Loading

## Why
Shadcn UI components are currently not loading their styles because the project is using Tailwind CSS v4, but the configuration (directives in `index.css` and missing Vite plugin) follows v3 conventions. This prevents Tailwind from processing the CSS and applying styles to the components.

## What Changes
- Install `@tailwindcss/vite` dev dependency.
- Update `vite.config.ts` to include the `@tailwindcss/vite` plugin.
- Migrate `src/index.css` to Tailwind v4 syntax (`@import "tailwindcss";`).
- Move custom theme configurations (colors, radius) from `tailwind.config.js` into `src/index.css` using the `@theme` directive.
- Remove legacy `tailwind.config.js` and `postcss.config.js` (if present and unused).

## Impact
- Affected specs: `frontend`
- Affected code: `shortix-web/src/index.css`, `shortix-web/vite.config.ts`, `shortix-web/package.json`
