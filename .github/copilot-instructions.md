# Daily Question - AI Agent Instructions

## Project Overview

This is a monorepo containing a **Nuxt 4** application (Vue 3) for a daily question feature. The project includes Firebase authentication and uses Nuxt UI for components.

## Architecture

- **Root**: Minimal project scaffold with a `vue/` subdirectory
- **Vue App** (`vue/`): Nuxt 4 application with Nuxt UI and Firebase integration
  - Uses `app/` directory structure with file-based routing via `app/pages/`
  - Main app layout in `app/app.vue` with authentication guard
  - Custom components in `app/components/`: `AuthForm.vue`, `AppLogo.vue`, `TemplateMenu.vue`
  - Landing page at `app/pages/index.vue` (Nuxt UI starter template content)
  - Custom CSS theme in `app/assets/css/main.css` with Nuxt UI and Tailwind CSS

## Package Management & Dependencies

- **Package Manager**: `pnpm@10.19.0` (required - not npm or yarn)
- **Adding Packages**: Always use `pnpm add --save-exact <package>` to install with exact versions (no `^` or `~`)
- **Nuxt Version**: 4.2.0 (latest major version)
- **Vue Version**: 3.5.22
- **Vue Router**: 4.6.3
- **Nuxt UI**: 4.1.0 (UI component library)
- **Firebase**: 12.5.0 with nuxt-vuefire 1.1.0 for Firebase integration
- **VueFire**: 3.2.2 for Vue Firebase bindings
- **Icons**: @iconify-json/lucide 1.2.71, @iconify-json/simple-icons 1.2.55
- All package management commands must be run from the `vue/` directory

## Development Workflow

### Running the Development Server

```bash
cd vue
pnpm install  # First time only
pnpm dev      # Starts on http://localhost:3000
```

### Building for Production

```bash
cd vue
pnpm build    # Standard build
pnpm generate # Static site generation (not applicable with SSR disabled)
pnpm preview  # Preview production build locally
```

### Type Checking

```bash
cd vue
pnpm typecheck  # Run TypeScript type checking
```

## Deployment

- **Target Platform**: Firebase App Hosting (configured via `apphosting.yaml`)
- **Configuration**: Firebase App Hosting config exists at root level
- **Environment Variables**: Configured as secrets in `apphosting.yaml`:
  - `NUXT_PUBLIC_FIREBASE_API_KEY`
  - `NUXT_PUBLIC_FIREBASE_AUTH_DOMAIN`
  - `NUXT_PUBLIC_FIREBASE_PROJECT_ID`
  - `NUXT_PUBLIC_FIREBASE_APP_ID`
  - `NUXT_PUBLIC_FIREBASE_STORAGE_BUCKET`
  - `NUXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID`
- **SSR**: Disabled (`ssr: false` in `nuxt.config.ts`) for client-side only rendering
- **Scaling**: Min 0, Max 1 instance configured

## Key Conventions

- **TypeScript**: This is a TypeScript project. ALL new code (components, composables, utilities, server routes) must be written in TypeScript
  - Uses Nuxt's split tsconfig setup (`.nuxt/tsconfig.*.json` references)
  - Use proper type annotations for function parameters, return types, and variables
  - Leverage TypeScript's type inference where appropriate
  - Run `pnpm typecheck` to verify types before committing
- **Nuxt Auto-imports**: Components, composables, and utilities are auto-imported (no explicit imports needed)
- **Nuxt DevTools**: Enabled in `nuxt.config.ts`
- **Compatibility Date**: Set to `2025-07-15` in config
- **Firebase Integration**: nuxt-vuefire module configured with authentication enabled
- **SSR Mode**: Disabled - client-side rendering only
- **Environment Variables**: Use `.env` file locally (not committed), secrets in Firebase App Hosting for production
- **Styling**: Custom theme using Tailwind CSS with Nuxt UI's @theme directive
- **Authentication**: Firebase Auth with email/password, auth guard in `app.vue`

## Next Steps & Development Guidelines

When adding features, follow Nuxt 4 conventions:

- **TypeScript Required**: All new files must use TypeScript (.ts for scripts, .vue with `<script setup lang="ts">` for components)
- **Components**: Place in `vue/app/components/` for auto-import (already set up)
- **Pages**: Add to `vue/app/pages/` for file-based routing (already configured)
- **Composables**: Add to `vue/composables/` for shared logic (use .ts extension)
- **Server Routes**: Create in `vue/server/api/` or `vue/server/routes/` with .ts extension (directory doesn't exist yet)
- **Utilities**: Add to `vue/utils/` for helper functions (use .ts extension)

### Planned Features

- Implement daily question creation and display functionality
- Add Firestore integration for storing questions and responses
- Create admin interface for managing questions
- Add user profile and history features
- Implement question scheduling system
