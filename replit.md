# Lua Obfuscator

## Overview

A web-based Lua code obfuscator that provides developers with tools to protect their Lua scripts through variable renaming, function obfuscation, string encoding, comment removal, and whitespace minification. Built as a utility-focused developer tool with a code-first interface inspired by VS Code and GitHub's design principles.

The application is a full-stack TypeScript solution using React on the frontend and Express on the backend, with Lua parsing capabilities powered by luaparse. The interface prioritizes code readability and developer ergonomics with a dark-optimized theme and clear input-to-output workflow.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework & Tooling**
- React 18 with TypeScript for type-safe component development
- Vite as the build tool and development server for fast HMR and optimized production builds
- Wouter for lightweight client-side routing (single-page application with home and 404 routes)

**UI Component System**
- Shadcn/ui component library (New York style variant) built on Radix UI primitives
- Tailwind CSS for utility-first styling with custom design tokens
- Class Variance Authority (CVA) for type-safe component variants
- Dark mode support via theme provider with localStorage persistence

**State Management**
- TanStack Query (React Query) for server state management and API interactions
- Local React state for UI controls (code input, options, settings panel visibility)
- Custom hooks for mobile detection and toast notifications

**Design System**
- Typography: JetBrains Mono/Fira Code for code, Inter for UI text
- Color system: HSL-based custom properties with comprehensive theme variables
- Spacing: Tailwind units (2, 4, 6, 8) for consistent layout
- Component structure: Header bar + two-panel code editor layout

### Backend Architecture

**Server Framework**
- Express.js for HTTP server and API routing
- TypeScript throughout the server codebase
- ESM module system (type: "module" in package.json)

**Code Processing**
- Luaparse library for parsing Lua code into AST (Abstract Syntax Tree)
- Custom obfuscation engine (`server/obfuscator.ts`) that:
  - Generates random identifiers for variable/function renaming
  - Encodes strings using byte-based conversion with `string.char()`
  - Removes comments (single-line and multi-line)
  - Preserves Lua reserved keywords and common globals
  - Handles AST traversal and transformation

**API Design**
- Single POST endpoint `/api/obfuscate` accepting code and options
- Request/response validation using Zod schemas from shared directory
- Structured error handling with detailed error messages

**Development Features**
- Request/response logging middleware with timing metrics
- Vite middleware integration for development with HMR
- Raw body capture for request validation

### Data Storage Solutions

**Current Implementation**
- In-memory storage class (`MemStorage`) with user CRUD operations
- User schema defined but not actively used in obfuscation workflow
- No persistent database currently connected

**Database Configuration**
- Drizzle ORM configured with PostgreSQL dialect
- Neon serverless PostgreSQL driver ready for integration
- Schema location: `shared/schema.ts`
- Migrations directory: `./migrations`
- Database URL expected via `DATABASE_URL` environment variable

**Session Management**
- `connect-pg-simple` package included for PostgreSQL-backed sessions
- Session infrastructure available but not currently implemented

### External Dependencies

**Core Libraries**
- `luaparse`: Lua code parsing and AST generation
- `@neondatabase/serverless`: PostgreSQL database driver for serverless environments
- `drizzle-orm`: Type-safe ORM for database operations
- `drizzle-zod`: Schema validation integration

**UI Component Libraries**
- `@radix-ui/*`: 20+ unstyled, accessible component primitives (accordion, dialog, dropdown, select, etc.)
- `cmdk`: Command menu component
- `embla-carousel-react`: Carousel/slider functionality
- `vaul`: Drawer component
- `input-otp`: OTP input component
- `react-day-picker`: Calendar/date picker

**Styling & Utilities**
- `tailwindcss`: Utility-first CSS framework
- `class-variance-authority`: Type-safe variant API
- `clsx` & `tailwind-merge`: Conditional class name utilities
- `lucide-react`: Icon library
- `date-fns`: Date manipulation utilities

**Form Handling**
- `react-hook-form`: Form state management
- `@hookform/resolvers`: Validation resolver integration
- `zod`: Runtime type validation and schema definition

**Development Tools**
- `@replit/vite-plugin-*`: Replit-specific development plugins (cartographer, dev banner, runtime error overlay)
- Google Fonts integration: JetBrains Mono, Fira Code, Inter, Geist Mono, DM Sans, Architects Daughter

**Build & Runtime**
- `esbuild`: Backend bundling for production
- `tsx`: TypeScript execution for development server
- Path aliases configured: `@/` for client source, `@shared/` for shared code, `@assets/` for static assets