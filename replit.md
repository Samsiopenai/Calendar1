# CAMERA TOON - Creative Studio Work Schedule Management

## Overview

CAMERA TOON is a comprehensive web application designed for managing work schedules at a creative studio. The system allows for planning employee shifts, tracking work schedules, and managing team assignments through an intuitive drag-and-drop calendar interface. The application supports multiple user roles with different permission levels and provides a modern, responsive user experience.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Build Tool**: Vite with custom configuration
- **UI Library**: Radix UI components with shadcn/ui design system
- **Styling**: Tailwind CSS with custom color variables and gradient themes
- **State Management**: TanStack Query (React Query) for server state management
- **Routing**: Wouter for lightweight client-side routing
- **Drag & Drop**: react-dnd with HTML5 backend for intuitive shift assignment

### Backend Architecture
- **Runtime**: Node.js with Express.js server
- **Language**: TypeScript with ES modules
- **Database**: SQLite with Drizzle ORM for type-safe database operations
- **Authentication**: Session-based authentication with bearer tokens
- **Storage**: In-memory storage implementation with predefined user accounts

### Data Storage Solutions
- **Primary Database**: SQLite configured for PostgreSQL compatibility (ready for production upgrade)
- **ORM**: Drizzle ORM with schema validation using Zod
- **Session Management**: In-memory session storage with automatic cleanup
- **Development Storage**: MemStorage class implementing IStorage interface

## Key Components

### Authentication System
- **User Roles**: Three-tier role system (admin, worker, guest)
- **Predefined Accounts**: 
  - vladshain (Admin) - Full system access
  - kostyamolokov (Worker) - Can create/modify shifts
  - andreykosting (Worker) - Can create/modify shifts
  - liya (Guest) - Read-only access
- **Session Management**: Bearer token authentication with expiration
- **Role-Based Access Control**: Middleware-based permission checking

### Calendar Management
- **Monthly View**: Interactive calendar with navigation between months
- **Dual Shift System**: Day and night shifts for each calendar date
- **Drag & Drop Interface**: Intuitive employee assignment via sidebar
- **Visual Feedback**: Color-coded employee avatars and shift indicators
- **Real-time Updates**: Optimistic updates with TanStack Query

### Employee Management
- **Employee Cards**: Compact and full view variants with color coding
- **Avatar System**: Initial-based avatars with customizable colors
- **Role Display**: Localized role names and permissions
- **Sidebar Integration**: Draggable employee cards for shift assignment

### UI Components
- **Design System**: Comprehensive shadcn/ui component library
- **Theming**: Dark mode with custom purple/pink gradient scheme
- **Responsive Design**: Mobile-first approach with adaptive layouts
- **Animations**: Smooth transitions and hover effects
- **Toast Notifications**: User feedback for actions and errors

## Data Flow

### Authentication Flow
1. User submits login credentials
2. Server validates against predefined accounts
3. Session created with unique token
4. Token stored in localStorage
5. Subsequent requests include Bearer token
6. Middleware validates token and attaches user context

### Shift Management Flow
1. User drags employee from sidebar to calendar slot
2. Frontend optimistically updates UI
3. API request sent with shift data
4. Backend validates permissions and creates shift
5. Database updated with new shift record
6. UI refreshed with server response

### Data Synchronization
- **Optimistic Updates**: Immediate UI feedback before server confirmation
- **Cache Management**: TanStack Query handles caching and invalidation
- **Error Handling**: Automatic retry and rollback on failures
- **Real-time Sync**: Queries automatically refetch on window focus

## External Dependencies

### Core Dependencies
- **@neondatabase/serverless**: Database connectivity (prepared for Neon PostgreSQL)
- **@tanstack/react-query**: Server state management
- **@radix-ui/***: Comprehensive UI component primitives
- **drizzle-orm**: Type-safe database operations
- **react-dnd**: Drag and drop functionality
- **wouter**: Lightweight routing
- **zod**: Schema validation

### Development Dependencies
- **@replit/vite-plugin-***: Replit-specific development tools
- **@types/***: TypeScript type definitions
- **tailwindcss**: Utility-first CSS framework
- **tsx**: TypeScript execution for development

## Deployment Strategy

### Development Environment
- **Hot Module Replacement**: Vite HMR for fast development iterations
- **TypeScript Compilation**: Real-time type checking and compilation
- **Asset Handling**: Vite handles static assets and imports
- **Error Overlay**: Runtime error reporting and debugging

### Production Build
- **Frontend**: Vite builds optimized React application to dist/public
- **Backend**: esbuild compiles TypeScript server to dist/index.js
- **Static Assets**: Served from dist/public directory
- **Environment Variables**: DATABASE_URL required for production

### Database Strategy
- **Development**: In-memory SQLite with predefined data
- **Production Ready**: Configured for PostgreSQL with Drizzle migrations
- **Schema Management**: Drizzle Kit for database migrations
- **Connection**: Environment-based database URL configuration

## User Preferences

Preferred communication style: Simple, everyday language.

## Telegram Integration

### Bot Configuration
- **Bot Name**: @CAMERA_TOON_BOT
- **Token**: 7679093791:AAEljqJ8kDjE1m3dLgLq8dBcmi2qejpC5ww
- **Features**: Automatic shift notifications, test messaging, broadcast messages

### Configured Telegram IDs
- **Влад Шайн** (Admin): 1120409420
- **Андрей Костин** (Worker): 1007433194  
- **Костя Молоков** (Worker): 535994249
- **Лия** (Guest): No Telegram (read-only user)

### Admin Panel Features
- Bot status monitoring and testing
- Team Telegram ID management display
- Test message sending to admin
- Broadcast messaging to all team members
- Automatic shift assignment notifications

### API Endpoints
- `POST /api/telegram/test` - Test bot functionality
- `POST /api/telegram/broadcast` - Send message to all team members
- Enhanced `POST /api/shifts` - Now includes automatic Telegram notifications

## Changelog

- July 05, 2025: Initial setup
- July 05, 2025: Added Telegram bot integration with admin panel and automatic notifications