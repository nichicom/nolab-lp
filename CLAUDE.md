# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

脳活ラボ (Nolab) - Landing page for a cognitive health and dementia prevention application. Built with Astro.js and deployed to Firebase Hosting at https://www.nolab.tokyo.

## Development Commands

### Setup
```bash
# Bootstrap project (install dependencies, configure git hooks)
mise run bootstrap

# Check development environment
mise run doctor
```

### Development
```bash
# Start dev server on http://localhost:4321
bun run dev

# Build for production
bun run build

# Preview production build
bun run preview

# Deploy to Firebase Hosting
bun run deploy

# Clean node_modules
mise run clean
```

## Architecture

### Tech Stack
- **Framework**: Astro.js v5.7.13 (static site generator)
- **Package Manager**: Bun 1.2.13
- **Runtime**: Node.js 22.15.1 (managed by mise)
- **Deployment**: Firebase Hosting (target: "lp", dist: "./dist")
- **Git Hooks**: lefthook with commitlint

### Component Architecture

The site follows a modular component structure in `/src/components/`:
- **Page Sections**: Hero, Prevention, Problem, Solution, Features, Benefits, HowToUse, Download, FAQ, Contact
- **Layout Components**: Header, Footer, SEO
- **Utility Components**: key.astro (reusable feature highlights)

All sections are imported and composed in `/src/pages/index.astro`.

### Styling System
- Global CSS with CSS custom properties (`/src/styles/global.css`)
- Design tokens:
  - `--color-indigo: #004299` (primary)
  - `--color-gold: #218d49` (secondary)
  - `--color-sumi: #2F2F2F` (text)
- Font: Noto Sans JP (400, 700)
- Mobile-first responsive design

### Development Workflow

1. **Git Hooks**: Commit messages are validated against conventional commits format
2. **Version Management**: All tools strictly pinned in `mise.toml`
3. **Build Process**: 
   - Development: Files in `/src/` are processed by Astro
   - Production: Static files generated to `/dist/`
   - Sitemap automatically generated at build time

### Key Configuration Files

- `astro.config.mjs` - Astro configuration with sitemap integration
- `mise.toml` - Tool versions and custom tasks (bootstrap, doctor, clean)
- `lefthook.yml` - Git hooks for commit message linting
- `commitlint.config.ts` - Conventional commits rules (subject-case disabled)
- `firebase.json` - Firebase Hosting configuration