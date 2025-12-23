# Design: Tailwind v4 Migration for Shadcn UI

## Context
Shortix-web uses Shadcn UI components which depend on Tailwind CSS for styling. The project currently has `tailwindcss v4` in its dependencies but uses `v3` configuration files and CSS directives. This mismatch results in unstyled components.

## Goals
- Restore component styling by correctly implementing Tailwind v4.
- Simplify configuration by leveraging v4's "CSS-first" approach.

## Decisions

### 1. Vite Plugin Integration
- **Decision**: Use `@tailwindcss/vite`.
- **Rationale**: This is the official and recommended way to integrate Tailwind v4 with Vite, replacing the need for a separate PostCSS step in most cases.

### 2. Configuration Migration
- **Decision**: Move `tailwind.config.js` contents to `@theme` blocks in `index.css`.
- **Rationale**: Tailwind v4 prioritizes CSS configuration. Keeping it in `index.css` is the idiomatic v4 way and allows for better variable discovery.

### 3. CSS Syntax Update
- **Decision**: Replace `@tailwind` directives with `@import "tailwindcss";`.
- **Rationale**: Required for Tailwind v4.

## Migration Details

### Modified `vite.config.ts`
```typescript
import tailwindcss from '@tailwindcss/vite'
// ...
export default defineConfig({
  plugins: [
    react(),
    tailwindcss(),
  ],
  // ...
})
```

### Modified `src/index.css`
```css
@import "tailwindcss";

@theme {
  --color-border: hsl(var(--border));
  --color-input: hsl(var(--input));
  /* ... mapping hsl variables to tailwind theme ... */
}
```

## Risks / Trade-offs
- **Breaking Changes**: Moving from `v3` to `v4` might have subtle rendering differences, but since current styling is 0%, it is a safe progression.
- **Dependency Update**: Adding `@tailwindcss/vite` is a new dependency but aligns with the existing `tailwindcss@v4`.
