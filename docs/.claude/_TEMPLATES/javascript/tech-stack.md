# JavaScript/TypeScript Technology Stack

## Core Technologies

### Runtime
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Node.js | 18+ | JavaScript runtime | https://nodejs.org/ |
| npm | Latest | Package manager | https://docs.npmjs.com/ |

### Language
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| TypeScript | 5.x | Type-safe JavaScript | https://www.typescriptlang.org/ |
| JavaScript | ES2022+ | Programming language | https://developer.mozilla.org/en-US/docs/Web/JavaScript |

## Development Tools

### Build Tools
| Technology | Purpose | Documentation |
|------------|---------|---------------|
| Vite | Fast build tool | https://vitejs.dev/ |
| esbuild | JavaScript bundler | https://esbuild.github.io/ |
| Rollup | Module bundler | https://rollupjs.org/ |

### Code Quality
| Technology | Purpose | Documentation |
|------------|---------|---------------|
| ESLint | Linting | https://eslint.org/ |
| Prettier | Code formatting | https://prettier.io/ |
| TypeScript | Type checking | https://www.typescriptlang.org/ |

### Testing
| Technology | Purpose | Documentation |
|------------|---------|---------------|
| Vitest | Unit testing | https://vitest.dev/ |
| Jest | Testing framework | https://jestjs.io/ |
| Playwright | E2E testing | https://playwright.dev/ |

## Package Management

### Primary Package Manager
- **Tool:** npm (default) / yarn / pnpm
- **Lock File:** package-lock.json / yarn.lock / pnpm-lock.yaml
- **Registry:** npmjs.com

### Common Commands
```bash
# Install dependencies
npm install

# Add package
npm install package-name

# Add dev dependency
npm install --save-dev package-name

# Update packages
npm update

# Run scripts
npm run dev
npm run build
npm test
```

### Package.json Structure
```json
{
  "name": "project-name",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "test": "vitest",
    "lint": "eslint .",
    "format": "prettier --write ."
  },
  "dependencies": {},
  "devDependencies": {}
}
```

## Configuration Files

### TypeScript (tsconfig.json)
```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "moduleResolution": "node",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  }
}
```

### ESLint (.eslintrc.js)
```javascript
module.exports = {
  root: true,
  parser: '@typescript-eslint/parser',
  plugins: ['@typescript-eslint'],
  extends: [
    'eslint:recommended',
    'plugin:@typescript-eslint/recommended',
    'prettier'
  ]
}
```

### Prettier (.prettierrc)
```json
{
  "semi": false,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5"
}
```

## Common Dependencies

### Utilities
| Package | Purpose |
|---------|---------|
| lodash | Utility functions |
| date-fns | Date manipulation |
| zod | Schema validation |
| axios | HTTP client |

### Development
| Package | Purpose |
|---------|---------|
| @types/node | Node.js types |
| typescript | TypeScript compiler |
| ts-node | TypeScript execution |

---
*Node Version: 18+*
*TypeScript Version: 5.x*
*Package Manager: npm/yarn/pnpm*
