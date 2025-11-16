# JavaScript/TypeScript Dependency Upgrade: [Package Name]

> **Template for upgrading npm/pnpm packages in JavaScript/TypeScript projects**

## Overview

**Upgrade ID:** DEP-[ID]
**Date:** [YYYY-MM-DD]
**Package Name:** [@scope/package-name or package-name]
**Package Manager:** pnpm (primary) / npm / yarn
**Current Version:** [X.Y.Z]
**Target Version:** [A.B.C]
**Upgrade Type:** [Major/Minor/Patch]
**Priority:** [Critical/High/Medium/Low]

## Motivation

### Why Upgrade?
- [ ] Security vulnerability (CVE-[ID] or GitHub Security Advisory)
- [ ] Bug fix needed
- [ ] New feature required
- [ ] Node.js version compatibility (e.g., Node 20 support)
- [ ] TypeScript compatibility (e.g., TS 5.x support)
- [ ] Performance improvement
- [ ] Deprecation warning
- [ ] Framework compatibility (Vue 3, React 18, etc.)
- [ ] Other: [Specify]

### Security Information
**CVE ID / GHSA ID:** [CVE-YYYY-XXXXX or GHSA-xxxx-xxxx-xxxx]
**Severity:** [Critical/High/Medium/Low]
**Advisory URL:** [Link to npm advisory or GitHub Security]

## Package Information

### Package Details
**npm Link:** https://www.npmjs.com/package/[package-name]
**Repository:** [GitHub/GitLab URL]
**Documentation:** [Link to docs]
**Changelog:** [Link to CHANGELOG.md or releases]
**License:** [MIT/Apache/BSD/etc.]

### Our Usage
**Where Used:**
- [Component/Feature 1]
- [Component/Feature 2]
- [Component/Feature 3]

**Usage Type:** [Direct dependency / Dev dependency / Peer dependency]
**Import Style:** [ESM / CommonJS / Both]

## Breaking Changes Analysis

### Official Release Notes
**Release Notes URL:** [Link]
**Migration Guide URL:** [Link]
**Breaking Changes:**

#### Change 1: [Description]
```typescript
// Before
import { oldMethod } from 'package-name'
oldMethod(param)

// After
import { newMethod } from 'package-name'
newMethod({ param, newOption: true })
```

**Impact:** [Description]
**Files Affected:** [Count or list]

#### Change 2: API Signature Changes
```typescript
// Old API
function fetch(url: string, options?: Options): Promise<Response>

// New API (TypeScript types changed)
function fetch(url: string | URL, options?: RequestInit): Promise<Response>
```

## Compatibility Check

### Node.js Version
**Current Node:** [e.g., 18.17.0]
**Required Node:** [e.g., >=18.0.0]
**Compatible:** [Yes/No]

### Package Manager Version
**pnpm:** [e.g., 8.x] (recommended)
**npm:** [e.g., 9.x]
**yarn:** [e.g., 3.x]

### TypeScript Compatibility
**Current TS:** [e.g., 5.3.0]
**Required TS:** [e.g., >=5.0.0]
**Compatible:** [Yes/No]

### Framework Compatibility
**Vue:** [Compatible versions]
**React:** [Compatible versions]
**Build Tool (Vite/Webpack):** [Compatible versions]

### Dependency Compatibility
```bash
# Check why package is installed
pnpm why package-name

# Check for conflicts
pnpm update package-name --dry-run

# Check all outdated packages
pnpm outdated
```

**Dependency Conflicts:**
| Package | Current | Peer Requires | Status |
|---------|---------|---------------|--------|
| [peer-dep-1] | [X.Y.Z] | [^A.B] | ✅/⚠️/❌ |

## Pre-Upgrade Checklist

- [ ] Review changelog and breaking changes
- [ ] Check TypeScript type definitions compatibility
- [ ] Check peer dependencies
- [ ] Review dependent packages (use `pnpm why`)
- [ ] Create feature branch
- [ ] Ensure all tests pass on current version
- [ ] Run type check (if TypeScript)
- [ ] Check for deprecation warnings

## Upgrade Execution

### Step 1: Update Package
```bash
# Using pnpm (recommended)
pnpm update package-name@^A.B.C

# Or specify exact version
pnpm add package-name@A.B.C

# Update with dependencies
pnpm up package-name --latest

# Dry run first
pnpm up package-name --latest --dry-run
```

### Step 2: Update Lock File
```bash
# pnpm
pnpm install

# npm
npm install

# yarn
yarn install
```

### Step 3: Type Check (TypeScript)
```bash
# Check types
pnpm run type-check

# Or directly
tsc --noEmit
```

### Step 4: Code Migration
**Files to Update:**
- [ ] [src/components/ComponentName.vue] - Update import/usage
- [ ] [src/utils/utilName.ts] - Update function calls
- [ ] [src/composables/useFeature.ts] - Update composable

**Code Changes:**
```typescript
// Example: ESLint config migration (v8 → v9)
// Old: .eslintrc.js
module.exports = {
  extends: ['eslint:recommended'],
  rules: {
    'no-console': 'warn'
  }
}

// New: eslint.config.js (flat config)
export default [
  {
    rules: {
      'no-console': 'warn'
    }
  }
]
```

## Testing

### Unit Tests
```bash
# Run all tests
pnpm test

# Run with coverage
pnpm test:coverage

# Run specific test
pnpm test ComponentName.spec.ts

# Watch mode
pnpm test:watch
```

### Type Testing
```bash
# Type check entire project
pnpm run type-check

# Check specific file
tsc --noEmit src/components/ComponentName.vue
```

### E2E Tests
```bash
# Run E2E tests
pnpm test:e2e

# Headed mode (see browser)
pnpm test:e2e --headed
```

### Build Testing
```bash
# Build for production
pnpm run build

# Preview build
pnpm run preview

# Check bundle size
pnpm run build --report
```

## Rollback Plan

### Rollback Steps
```bash
# Revert package.json and lock file
git checkout package.json pnpm-lock.yaml

# Reinstall old version
pnpm install

# Verify
pnpm test
pnpm run build
```

**Rollback Criteria:**
- Build fails
- Test failures > 5%
- TypeScript errors
- Runtime errors in critical paths
- Bundle size increase > 20%

## Performance Impact

### Bundle Size Analysis
```bash
# Before upgrade
pnpm run build
# Note bundle sizes

# After upgrade
pnpm run build
# Compare sizes

# Use bundle analyzer
pnpm add -D rollup-plugin-visualizer
```

**Metrics:**
| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Bundle size (gzip) | [X]KB | [Y]KB | [+/-Z]% |
| Chunks | [N] | [M] | [+/-P] |
| Dependencies | [N] | [M] | [+/-P] |

## Deployment

### Build for Production
```bash
# Install dependencies (production only)
pnpm install --prod

# Build
pnpm run build

# Test build locally
pnpm run preview
```

### CI/CD Updates
```yaml
# .github/workflows/ci.yml
- name: Install dependencies
  run: pnpm install --frozen-lockfile

- name: Type check
  run: pnpm run type-check

- name: Run tests
  run: pnpm test

- name: Build
  run: pnpm run build
```

## Post-Upgrade Monitoring

### Metrics to Watch
- [ ] Build time
- [ ] Bundle size
- [ ] Runtime errors (Sentry/error tracking)
- [ ] Page load time
- [ ] API response times
- [ ] Memory usage

### Browser Compatibility
- [ ] Chrome (latest)
- [ ] Firefox (latest)
- [ ] Safari (latest)
- [ ] Edge (latest)
- [ ] Mobile browsers

## Documentation Updates

- [ ] Update `docs/.claude/context/tech-stack.md`
- [ ] Update `package.json` version
- [ ] Update README.md if usage changed
- [ ] Update type definitions if custom types
- [ ] Update API documentation
- [ ] Update migration guide for team

## Framework-Specific Considerations

### Vue 3 Projects
```typescript
// Check for breaking changes in:
// - Composition API patterns
// - Component registration
// - Plugin usage
// - Reactivity APIs

// Example: Pinia update
import { defineStore } from 'pinia'

// Old pattern may still work, but new features available
export const useStore = defineStore('main', () => {
  // Setup stores pattern (new)
})
```

### React Projects
```typescript
// Check for breaking changes in:
// - Hooks usage
// - Component patterns
// - Context API
// - Concurrent features

// Example: React Query update (v4 → v5)
// Old
import { useQuery } from 'react-query'

// New
import { useQuery } from '@tanstack/react-query'
```

### Vite Projects
```typescript
// vite.config.ts changes
import { defineConfig } from 'vite'

export default defineConfig({
  // Check for plugin API changes
  plugins: [
    // Plugins may have new options
  ],
  // Check for new optimization options
  build: {
    // New features in newer Vite versions
  }
})
```

## Common Package Categories

### Build Tools
- **vite:** Build tool & dev server
- **@vitejs/plugin-vue:** Vue plugin for Vite
- **typescript:** TypeScript compiler

### Testing
- **vitest:** Unit testing
- **@vue/test-utils:** Vue component testing
- **playwright:** E2E testing

### State Management
- **pinia:** Vue state management
- **zustand:** React state management
- **@tanstack/query:** Async state management

### Utilities
- **axios:** HTTP client
- **@vueuse/core:** Vue composables
- **date-fns:** Date utilities

---
**Status:** [Planning/In Progress/Testing/Complete/Rolled Back]
**Last Updated:** [YYYY-MM-DD]
**Owner:** [Name/Team]

---

## Quick Reference

### pnpm Commands
```bash
# Show package info
pnpm list package-name

# Why is package installed
pnpm why package-name

# Check for security issues
pnpm audit

# Fix security issues
pnpm audit --fix

# Update interactive
pnpm up -i

# Check outdated
pnpm outdated
```

### npm Commands
```bash
# Equivalent npm commands
npm ls package-name
npm explain package-name
npm audit
npm audit fix
npm outdated
```

### Debug Commands
```bash
# Clear node_modules and reinstall
rm -rf node_modules pnpm-lock.yaml
pnpm install

# Verify package integrity
pnpm install --frozen-lockfile
```
