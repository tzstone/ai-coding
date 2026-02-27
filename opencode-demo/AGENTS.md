# AGENTS.md

This file provides guidance to AI coding agents working in this Vue 3 TypeScript repository.

## Development Commands

```sh
pnpm install              # Install dependencies
pnpm run dev              # Start dev server with hot reload
pnpm run build            # Type-check, compile, and minify for production
pnpm run type-check       # Run vue-tsc for type checking
pnpm run lint             # Run oxlint (primary) + eslint (secondary) with auto-fix
pnpm run format           # Format code with Prettier (targets src/)
pnpm run test:unit        # Run all unit tests with Vitest
pnpm run test:unit HelloWorld  # Run specific test file by name pattern
```

## Project Stack

- **Vue 3** with Composition API and `<script setup>` syntax
- **TypeScript** for type safety throughout
- **Vite** for build tooling and dev server
- **Vue Router** for routing (`src/router/index.ts`)
- **Pinia** for state management (`src/stores/`)
- **Vitest** with jsdom for testing
- **@vue/test-utils** for component testing

## Code Style Guidelines

### Imports

- Use `@` alias for `src/` imports: `import Component from '@/components/Component.vue'`
- Use named imports where appropriate: `import { ref, computed } from 'vue'`
- Group imports in order: Vue APIs, third-party libraries, local components

### TypeScript

- All `.vue` files use `<script setup lang="ts">`
- Define props with type syntax: `defineProps<{ msg: string }>()`
- Return types inferred where possible, explicit for complex types

### Naming Conventions

- **Component files**: PascalCase (`HelloWorld.vue`, `HomeView.vue`)
- **Component tags**: PascalCase in templates (`<HelloWorld />`)
- **Store functions**: `useXStore` pattern (`useCounterStore`, `useUserStore`)
- **Variables/functions**: camelCase (`const userName = ''`, `function getData()`)
- **Routes**: lowercase (`'home'`, `'about'`)

### Formatting

- No semicolons
- Single quotes
- 100 character line width
- 2 space indentation
- Trailing newlines required
- Trim trailing whitespace

### Vue Components

- Use `<script setup lang="ts">` for all components
- Define props and emits with TypeScript syntax
- Use `defineEmits` for events with types
- Keep styles scoped to component: `<style scoped>`
- Prefer composition functions over Options API

### State Management (Pinia)

- Use setup stores: `defineStore('name', () => { ... })`
- Export with `useXStore` naming convention
- Use `ref()` for reactive state, `computed()` for derived state

### Testing

- Place tests in `__tests__` directories alongside code: `src/components/__tests__/`
- Use `@vue/test-utils` for component testing
- Test files: `*.spec.ts` or `*.test.ts`
- Use Vitest globals (`describe`, `it`, `expect`)
- Run single test: `pnpm run test:unit <testName>`

### Styling

- Use scoped styles for components
- Leverage CSS variables defined in `src/assets/base.css`
- Follow mobile-first responsive design
- Use semantic HTML elements

## Type Checking

Run `vue-tsc` before committing for `.vue` files. The project uses project references with separate configs:

- `tsconfig.app.json` - App code
- `tsconfig.vitest.json` - Test code
- `tsconfig.node.json` - Node/build tooling

## Linting Priority

1. **oxlint** runs first (fast, primary linter)
2. **eslint** runs second with Vue/TypeScript rules
3. Both run with `--fix` flag for auto-correction
4. Fix all lint errors before pushing

## File Structure

- `src/views/` - Page components (HomeView, AboutView)
- `src/components/` - Reusable Vue components
- `src/components/icons/` - Icon components
- `src/router/` - Vue Router configuration
- `src/stores/` - Pinia stores
- `src/assets/` - Static assets (CSS, images)
- `src/**/__tests__/` - Test files next to source code

## Build Requirements

- Node version: ^20.19.0 || >=22.12.0
- Run `pnpm run type-check` before `pnpm run build`
- Build fails on type errors

## Error Handling

- Don't silently catch errors without handling
- Use Vue's error boundaries where appropriate
- Prefer explicit error messages over generic ones
- Log errors to console during development
