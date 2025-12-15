# NestJS Starter

A production-ready NestJS starter template with authentication, authorization, database integration, and Docker support.

## Overview

This is a TypeScript-based NestJS starter project that provides a solid foundation for building scalable server-side applications. It comes pre-configured with essential features commonly needed in modern web applications.

## Features

- **Authentication & Authorization**
  - JWT-based authentication (access + refresh tokens)
  - User registration and login
  - Role-based access control (USER, ADMIN)
  - Password hashing with Argon2
  - Protected routes with guards

- **Database**
  - PostgreSQL integration via Prisma ORM
  - User and RefreshToken models
  - Database migrations

- **Docker**
  - Multi-stage Dockerfile for optimized production images
  - Development setup with hot reload
  - Docker Compose for easy orchestration
  - Makefile shortcuts for common commands

- **Configuration**
  - Environment-based configuration
  - Schema validation with Zod
  - Type-safe configuration module

- **Code Quality**
  - TypeScript strict mode
  - ESLint + Prettier
  - Class validation and transformation
  - Jest for testing

## Tech Stack

- **Framework:** NestJS 11
- **Language:** TypeScript
- **Database:** PostgreSQL + Prisma
- **Authentication:** Passport.js + JWT
- **Validation:** class-validator, class-transformer, Zod
- **Containerization:** Docker + Docker Compose

## Quick Start with Docker

```bash
# Clone and enter the project
cd nestjs-starter

# Copy environment template
cp .env.example .env
# Edit .env with your JWT secrets

# Start everything (production mode)
make up-build

# Or start in development mode (with hot reload)
make dev
```

## Environment Variables

Create a `.env` file in the project root:

```env
# Application
NODE_ENV=development
PORT=3000

# Database
DATABASE_URL=postgresql://postgres:postgres@localhost:5433/nestjs_starter?schema=public

# JWT Secrets (generate secure random strings for production!)
JWT_ACCESS_TOKEN_SECRET=your-super-secret-access-token-key
JWT_REFRESH_TOKEN_SECRET=your-super-secret-refresh-token-key
JWT_ACCESS_TOKEN_EXPIRATION=15m
JWT_REFRESH_TOKEN_EXPIRATION=7d
```

## Development Options

### Option 1: Full Docker (Recommended for consistency)

```bash
make dev            # Start app + database with hot reload
make dev-logs       # View logs
make dev-down       # Stop everything
```

### Option 2: Local NestJS + Docker Database (Fastest hot reload)

```bash
make dev-local      # Start database + run NestJS locally
```

### Option 3: Fully Local

```bash
# Requires local PostgreSQL installation
npm install
npx prisma migrate dev
npm run start:dev
```

## Makefile Commands

| Command | Description |
|---------|-------------|
| `make up` | Start containers (production) |
| `make up-build` | Rebuild and start containers |
| `make down` | Stop containers |
| `make down-clean` | Stop containers and remove volumes |
| `make restart` | Restart containers |
| `make build` | Build containers |
| `make logs` | Follow all container logs |
| `make logs-app` | Follow app logs only |
| `make logs-db` | Follow database logs only |
| `make shell` | Open shell in app container |
| `make db-shell` | Open PostgreSQL CLI |
| `make migrate` | Run migrations in container |
| `make migrate-dev` | Run migrations locally |
| `make studio` | Open Prisma Studio |
| `make dev` | Start development environment (Docker) |
| `make dev-down` | Stop development environment |
| `make dev-rebuild` | Rebuild dev environment (no cache) |
| `make dev-logs` | Follow dev app logs |
| `make dev-local` | Local NestJS + Docker database |
| `make install` | Install dependencies (npm ci) |
| `make clean` | Remove containers, volumes, and node_modules |
| `make help` | Show all available commands |

## Project Setup (Without Docker)

```bash
# Install dependencies
npm install

# Set up environment variables
cp .env.example .env

# Run database migrations
npx prisma migrate dev

# Generate Prisma client
npx prisma generate
```

## Running the Application

```bash
# development
npm run start

# watch mode
npm run start:dev

# production mode
npm run start:prod
```

## Testing

```bash
# unit tests
npm run test

# e2e tests
npm run test:e2e

# test coverage
npm run test:cov
```

## Project Structure

```
├── prisma/
│   ├── schema.prisma       # Database schema
│   └── migrations/         # Database migrations
├── src/
│   ├── auth/               # Authentication module
│   │   ├── decorators/     # Custom decorators (@CurrentUser, @Public, @Roles)
│   │   ├── dto/            # Data transfer objects
│   │   ├── guards/         # Route guards (JWT, Roles)
│   │   └── strategies/     # Passport strategies
│   ├── config/             # Configuration management
│   ├── database/           # Prisma service and module
│   └── main.ts             # Application entry point
├── Dockerfile              # Production Docker image
├── Dockerfile.dev          # Development Docker image
├── docker-compose.yml      # Production compose config
├── docker-compose.dev.yml  # Development compose config
├── Makefile                # Command shortcuts
└── .env.example            # Environment template
```

## API Endpoints

### Authentication
- `POST /auth/register` - Register a new user
- `POST /auth/login` - Login with credentials
- `POST /auth/refresh` - Refresh access token
- `POST /auth/logout` - Logout user

## License

UNLICENSED
