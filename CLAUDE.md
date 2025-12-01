# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

PlanDev Gateway is the API gateway for [PlanDev](https://github.com/NASA-AMMOS/plandev), NASA-AMMOS's mission planning and sequencing system. It provides authentication, file handling, GraphQL playground, and various API endpoints that interface with the PlanDev backend services.

## Tech Stack

- **Runtime**: Node.js 20+ with ES modules
- **Language**: TypeScript (strict mode)
- **Framework**: Express.js
- **Database**: PostgreSQL (via `pg` client)
- **Auth**: JWT-based authentication with pluggable adapters (CAM, NoAuth)
- **Testing**: Vitest
- **Linting**: ESLint
- **Formatting**: Prettier

## Common Commands

```bash
# Install dependencies
npm install

# Development (watch mode with auto-restart)
npm run dev

# Build TypeScript to dist/
npm run build

# Run production server
npm start

# Run tests
npm test

# Lint code
npm run lint

# Format code
npm run format

# Check formatting without making changes
npm run format:check

# Clean build artifacts
npm run clean
```

## Project Structure

```
src/
├── main.ts                 # Application entry point, Express setup
├── env.ts                  # Environment variable configuration
├── logger.ts               # Winston logging setup
├── packages/               # Feature modules
│   ├── api-playground/     # GraphQL Altair playground
│   ├── auth/               # Authentication (adapters, middleware, routes)
│   ├── db/                 # Database connection and queries
│   ├── expansion/          # Expansion logic endpoints
│   ├── external-source/    # External data source handling
│   ├── files/              # File upload/download endpoints
│   ├── hasura/             # Hasura event handlers
│   ├── health/             # Health check endpoints
│   ├── plan/               # Plan management endpoints
│   └── swagger/            # OpenAPI/Swagger documentation
├── schemas/                # JSON validation schemas
├── types/                  # TypeScript type definitions
└── util/                   # Utility functions
```

## Architecture Notes

- **Authentication Adapters**: The gateway supports pluggable auth via adapters in `src/packages/auth/adapters/`. Set `AUTH_TYPE` env var to `none` or `cam`.
- **Route Initialization**: Each package exports an `init*Routes(app)` function called from `main.ts`.
- **Environment Config**: All env vars are accessed through `getEnv()` from `src/env.ts`. See `docs/ENVIRONMENT.md` for full list.
- **GraphQL**: The gateway proxies requests to Hasura and provides a GraphQL playground at `/api-playground`.

## Development Setup

1. Copy `.env.template` to `.env`
2. Set required environment variables:
   - `GATEWAY_DB_USER`
   - `GATEWAY_DB_PASSWORD`
   - `HASURA_GRAPHQL_JWT_SECRET`
   - `HASURA_API_URL` (if not using default localhost:8080)
3. Run `npm install && npm run dev`

## Testing

Tests use Vitest and are located in:
- `test/` directory for integration tests
- `src/**/*.test.ts` for unit tests (co-located with source)

Run with `npm test`.

## Code Style

- Use ES module imports (with `.js` extension for local imports)
- Follow existing patterns for new routes/packages
- Types are defined in `src/types/` directory
- Prefer async/await over callbacks
