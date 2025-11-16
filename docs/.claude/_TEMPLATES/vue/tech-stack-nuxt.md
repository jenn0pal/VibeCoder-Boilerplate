# Nuxt 3 Technology Stack

## Core Technologies

### Framework
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Nuxt | 3.x | Meta-framework for Vue | https://nuxt.com/ |
| Vue | 3.x | UI framework | https://vuejs.org/ |
| Nitro | Latest | Server engine | https://nitro.unjs.io/ |

### State Management
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Pinia | 2.x | State management | https://pinia.vuejs.org/ |
| useState | Built-in | Nuxt state composable | https://nuxt.com/docs/api/composables/use-state |

### Routing
- **File-based routing:** Automatic from `pages/` directory
- **Dynamic routes:** `[id].vue` syntax
- **Middleware:** Built-in route guards

## Development Tools

### Build & Dev
| Technology | Purpose | Documentation |
|------------|---------|---------------|
| Vite | Build tool & dev server | https://vitejs.dev/ |
| Nitro | Server-side rendering | https://nitro.unjs.io/ |
| h3 | HTTP framework | https://github.com/unjs/h3 |

### Code Quality
| Technology | Purpose |
|------------|---------|
| ESLint | Linting (Nuxt module) |
| Prettier | Formatting |
| TypeScript | Type checking |

### Testing
| Technology | Purpose |
|------------|---------|
| Vitest | Unit testing |
| @vue/test-utils | Component testing |
| Playwright | E2E testing |

## Common Nuxt Modules

### Official Modules
```bash
# UI Framework
@nuxtjs/tailwindcss

# State Management
@pinia/nuxt

# Image Optimization
@nuxt/image

# Internationalization
@nuxtjs/i18n

# Content Management
@nuxt/content
```

### Community Modules
```bash
# Auth
@sidebase/nuxt-auth

# Security
nuxt-security

# SEO
@nuxtjs/seo

# Analytics
@nuxtjs/google-analytics
```

## Package Management

### Primary Package Manager
- **Tool:** npm / pnpm / yarn
- **Lock File:** package-lock.json / pnpm-lock.yaml / yarn.lock

### Common Commands
```bash
# Development
npm run dev

# Build
npm run build

# Production preview
npm run preview

# Type check
npm run type-check

# Generate static site
npm run generate
```

## Server API Routes

### Nitro Server
- **API Routes:** `server/api/`
- **Middleware:** `server/middleware/`
- **Plugins:** `server/plugins/`
- **Utils:** `server/utils/`

### Example Structure
```
server/
├── api/
│   ├── users.get.ts       # GET /api/users
│   ├── users.post.ts      # POST /api/users
│   └── users/
│       └── [id].get.ts    # GET /api/users/:id
├── middleware/
│   └── auth.ts
└── utils/
    └── db.ts
```

## Deployment

### SSR Deployment
- **Node.js server:** Required
- **Port:** Configurable (default: 3000)
- **Output:** `.output/` directory

### Static Deployment (SSG)
```bash
npm run generate
# Outputs to .output/public/
```

### Edge Deployment
- Vercel
- Netlify
- Cloudflare Pages
- AWS Amplify

---
*Nuxt Version: 3.x*
*Vue Version: 3.x*
*Node Version: 18+*
