# Daily Question - AI Agent Instructions

## Project Overview

This is a monorepo containing a **Nuxt 4** application (Vue 3) for a daily question feature. The project is in early stages with minimal implementation.

## Architecture

- **Root**: Minimal project scaffold with a `vue/` subdirectory
- **Vue App** (`vue/`): Standard Nuxt 4 application using the minimal starter template
  - Currently displays only the `NuxtWelcome` component in `app/app.vue`
  - No custom pages, components, composables, or server routes yet implemented
  - Uses Nuxt's app directory structure (not pages directory)

## Package Management & Dependencies

- **Package Manager**: `pnpm` (required - not npm or yarn)
- **Adding Packages**: Always use `pnpm add --save-exact <package>` to install with exact versions (no `^` or `~`)
- **Nuxt Version**: 4.2.0 (latest major version)
- **Vue Version**: 3.5.22
- **Firebase**: 12.5.0 with nuxt-vuefire 1.1.0 for Firebase integration
- **VueFire**: 3.2.2 for Vue Firebase bindings
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
pnpm generate # Static site generation
pnpm preview  # Preview production build locally
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

- **TypeScript**: Project uses TypeScript with Nuxt's split tsconfig setup (`.nuxt/tsconfig.*.json` references)
- **Nuxt Auto-imports**: Components, composables, and utilities are auto-imported (no explicit imports needed)
- **Nuxt DevTools**: Enabled in `nuxt.config.ts`
- **Compatibility Date**: Set to `2025-07-15` in config
- **Firebase Integration**: nuxt-vuefire module configured with authentication enabled
- **SSR Mode**: Disabled - client-side rendering only
- **Environment Variables**: Use `.env` file locally (not committed), secrets in Firebase App Hosting for production

## Current State & Next Steps

The codebase is a fresh Nuxt 4 starter with:

- ✅ Basic Nuxt configuration
- ✅ Development tooling setup (TypeScript, devtools)
- ✅ Firebase integration configured (nuxt-vuefire module)
- ✅ Firebase App Hosting deployment configuration
- ✅ Environment variables setup for Firebase config
- ❌ No custom components or pages
- ❌ No API routes or server middleware
- ❌ No styling framework or design system

When adding features, follow Nuxt 4 conventions:

- Place components in `vue/components/` for auto-import
- Use `vue/app/pages/` if file-based routing is needed (requires removing `app.vue` approach)
- Add composables to `vue/composables/` for shared logic
- Server routes go in `vue/server/api/` or `vue/server/routes/`
