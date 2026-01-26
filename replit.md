# NYPD Punishment Logger

## Overview

This is a full-stack web application for NYPD roleplay server administrators to log and generate punishment messages for rule violations. The app allows HR personnel to select offenses from a predefined list, input officer details, and generate formatted punishment or revoke messages that can be copied to clipboard.

The application serves a React frontend from an Express backend, uses PostgreSQL for data persistence, and includes AI integration capabilities for enhanced message generation.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight alternative to React Router)
- **State Management**: TanStack React Query for server state
- **Styling**: Tailwind CSS with shadcn/ui component library
- **Animations**: Framer Motion for UI transitions
- **Build Tool**: Vite with hot module replacement

The frontend follows a component-based architecture with:
- Pages in `client/src/pages/`
- Reusable components in `client/src/components/`
- Custom hooks in `client/src/hooks/`
- UI primitives from shadcn/ui in `client/src/components/ui/`

### Backend Architecture
- **Runtime**: Node.js with Express 5
- **Language**: TypeScript compiled with tsx
- **API Pattern**: RESTful endpoints defined in `shared/routes.ts`
- **Database ORM**: Drizzle ORM with PostgreSQL
- **Validation**: Zod schemas for request/response validation

Key backend files:
- `server/index.ts` - Express app setup and middleware
- `server/routes.ts` - API route registration
- `server/storage.ts` - Database operations layer
- `server/db.ts` - Database connection pool

### Shared Code
The `shared/` directory contains code used by both frontend and backend:
- `schema.ts` - Drizzle table definitions and Zod schemas
- `routes.ts` - API contract definitions with type-safe endpoints
- `models/chat.ts` - Chat/conversation schemas for AI features

### Data Model
Two primary tables:
1. **offenses** - Predefined violation codes with descriptions and punishments
2. **logs** - Records of punishment/revoke actions taken by HR

### AI Integrations
Located in `server/replit_integrations/`:
- **chat** - Conversation-based AI interactions
- **audio** - Voice chat with speech-to-text/text-to-speech
- **image** - Image generation capabilities
- **batch** - Rate-limited batch processing utilities

## External Dependencies

### Database
- **PostgreSQL** - Primary data store via `DATABASE_URL` environment variable
- **Drizzle ORM** - Type-safe database queries and migrations
- **connect-pg-simple** - Session storage (available but not currently used)

### AI Services
- **OpenAI API** - Via Replit AI Integrations
  - Environment variables: `AI_INTEGRATIONS_OPENAI_API_KEY`, `AI_INTEGRATIONS_OPENAI_BASE_URL`
  - Used for chat completions, image generation, and voice features

### Frontend Libraries
- **@tanstack/react-query** - Async state management
- **@radix-ui/** - Accessible UI primitives (30+ components)
- **framer-motion** - Animation library
- **date-fns** - Date manipulation utilities
- **wouter** - Client-side routing

### Development Tools
- **Vite** - Frontend build and dev server
- **esbuild** - Production server bundling
- **drizzle-kit** - Database migration tooling

### Build Configuration
- Development: `npm run dev` - Runs tsx with Vite middleware
- Production: `npm run build` - Bundles client with Vite, server with esbuild
- Database: `npm run db:push` - Push schema changes to PostgreSQL