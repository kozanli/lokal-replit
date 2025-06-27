# LocalReplit - Web-based Code Editor

## Overview
LocalReplit is a full-stack web application that provides an IDE-like experience for creating and editing web projects. It features a modern React frontend with a Node.js/Express backend, allowing users to create projects, manage files, edit code, and preview their work in real-time.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Styling**: Tailwind CSS with shadcn/ui component library
- **State Management**: TanStack Query for server state management
- **Routing**: Wouter for client-side routing
- **Build Tool**: Vite for development and building
- **Code Style**: New York style from shadcn/ui

### Backend Architecture
- **Runtime**: Node.js with Express.js
- **Language**: TypeScript with ES modules
- **Database**: PostgreSQL with Drizzle ORM
- **Database Provider**: Neon Database (@neondatabase/serverless)
- **Development**: tsx for TypeScript execution
- **Production**: esbuild for server bundling

### Data Storage Solutions
- **Primary Database**: PostgreSQL via Neon Database (Active)
- **ORM**: Drizzle with automatic migrations
- **Session Storage**: PostgreSQL with connect-pg-simple
- **Schema Management**: Drizzle Kit for migrations and schema management
- **Storage Implementation**: DatabaseStorage class with automatic initialization

## Key Components

### Database Schema
- **Projects Table**: Stores project metadata (id, name, description, template, created_at)
- **Files Table**: Stores file content and structure (id, project_id, path, content, type)
- **Validation**: Zod schemas for type-safe data validation

### Core Features
- **Project Management**: Create, list, and delete projects with different templates
- **File System**: Create, edit, and manage files within projects
- **Code Editor**: Text-based code editor with syntax highlighting
- **Live Preview**: Real-time preview of HTML/CSS/JS projects
- **AI Integration**: OpenAI GPT-4o integration for code generation and improvement

### UI Components
- **File Explorer**: Tree-view file browser with create/delete functionality
- **Code Editor**: Multi-tab editor with file switching
- **Live Preview**: Responsive preview pane with device simulation
- **Top Navigation**: Project switcher and creation tools

## Data Flow

1. **Project Creation**: User creates project → Validated via Zod → Stored in PostgreSQL → UI updates via TanStack Query
2. **File Management**: User modifies files → Real-time updates → Database persistence → Query cache invalidation
3. **Code Editing**: File content changes → Debounced API calls → Database updates → Preview refresh
4. **AI Generation**: User prompt → OpenAI API → Generated code → File creation/updates → Database storage

## External Dependencies

### Core Dependencies
- **@neondatabase/serverless**: PostgreSQL database connection
- **drizzle-orm**: Type-safe database ORM
- **@tanstack/react-query**: Server state management
- **@radix-ui/react-***: Headless UI components
- **tailwindcss**: Utility-first CSS framework
- **zod**: Schema validation
- **wouter**: Lightweight routing

### Development Tools
- **vite**: Build tool and development server
- **tsx**: TypeScript execution for development
- **esbuild**: Production bundling
- **drizzle-kit**: Database migration tool

### AI Integration
- **openai**: GPT-4o API for code generation
- **Environment Variables**: OPENAI_API_KEY for authentication

## Deployment Strategy

### Development Environment
- **Command**: `npm run dev`
- **Server**: tsx with hot reloading
- **Client**: Vite dev server with HMR
- **Database**: PostgreSQL via DATABASE_URL environment variable

### Production Build
- **Build Process**: 
  1. `vite build` - Builds React frontend to `dist/public`
  2. `esbuild` - Bundles Express server to `dist/index.js`
- **Deployment**: Replit autoscale deployment
- **Runtime**: `npm run start` serves production build

### Environment Configuration
- **Development**: NODE_ENV=development
- **Production**: NODE_ENV=production
- **Database**: DATABASE_URL environment variable required
- **AI Features**: OPENAI_API_KEY environment variable

### Platform Integration
- **Replit Modules**: nodejs-20, web, postgresql-16
- **Port Configuration**: Internal port 5000, external port 80
- **Auto-deployment**: Configured for Replit's autoscale platform

## Changelog
- June 26, 2025: Initial setup
- June 26, 2025: Complete Turkish localization of the entire interface including:
  - All UI components and buttons
  - Error messages and notifications
  - Default project content and templates
  - Navigation and menu items
  - Tooltips and help text
- June 26, 2025: Migrated from in-memory storage to PostgreSQL database:
  - Created database schema with proper relations
  - Implemented DatabaseStorage class with all CRUD operations
  - Added automatic initialization with Turkish default project
  - Successfully deployed database tables via Drizzle
- June 26, 2025: Implemented tabbed interface for code editor and live preview:
  - Combined code editor and live preview in single panel with tab switching
  - User can toggle between "Kod Editörü" and "Canlı Önizleme" tabs
  - File explorer remains fixed on left side
- June 26, 2025: Added file upload functionality to AI assistant:
  - File upload button (paperclip icon) in AI chat area
  - Support for multiple file types (code, text, config files)
  - Uploaded files automatically included in AI prompts
  - File list display with size information and remove option
  - Black background for textarea as requested
- June 26, 2025: Fixed layout issues and removed gray empty spaces:
  - Removed bottom gray space from LivePreview component
  - Removed terminal/console section from CodeEditor component
  - Optimized layout for full-screen code editing and preview
  - Fixed file explorer scrolling issues
  - Improved tab navigation and component spacing
- June 26, 2025: Upgraded to Monaco Editor with comprehensive language support:
  - Replaced basic text editor with VS Code-based Monaco Editor
  - Added support for 40+ programming languages including Python, Java, PHP, C++, Go, Rust
  - Implemented professional features: syntax highlighting, autocomplete, IntelliSense
  - Enhanced AI code generation compatibility for all major programming languages
  - Maintained Turkish interface with professional code editing capabilities
- June 26, 2025: Implemented VS Code-style multi-project tab system:
  - Added project tab navigation above file explorer
  - Each project opens in separate tab with independent file state
  - Tab closing functionality with X button (minimum one tab always open)
  - Automatic new tab creation when selecting different projects from header
  - Each tab maintains its own active files, open files, and editor/preview state
- June 26, 2025: Reorganized interface layout for better clarity:
  - Separated AI Assistant into dedicated component (bottom of left panel)
  - Cleaned up File Explorer to show only project files (top of left panel)
  - Eliminated confusion between file navigation and AI chat functionality
  - Maintained black background for AI assistant textarea as requested
- June 26, 2025: Implemented complete local file system integration:
  - Added FileSystemManager for physical file operations (create, read, write, delete)
  - Synchronized database and physical files automatically
  - Project export/import as ZIP files with full structure preservation
  - File copying, moving, and backup creation capabilities
  - Secure path validation to prevent directory traversal attacks
  - Real-time file watching for external changes detection
  - Enhanced project management with delete, copy, and backup operations
- June 26, 2025: Implemented advanced AI engine with comprehensive capabilities:
  - Advanced AI Engine with multi-step reasoning and context awareness
  - Intelligent code analysis with quality scoring and issue detection
  - Real-time code suggestions with confidence scoring
  - Proactive debugging assistant with solution recommendations
  - Personalized AI preferences and learning from user patterns
  - Multi-tab AI interface (Chat, Analysis, Suggestions, Settings)
  - Context-aware conversations with project history
  - Performance optimization and security vulnerability detection
- June 26, 2025: Enhanced AI system with professional development tools:
  - Prompt Templates system with 6 pre-built templates (React Component, API Endpoint, Utility Function, Styled Layout, Database Schema, Full-Stack Feature)
  - Package Manager integration with npm install/uninstall via web interface
  - Popular packages quick-install system (React, Axios, Lodash, TypeScript, etc.)
  - Hot Reload service foundation for real-time preview updates
  - 6-tab AI interface expansion (Chat, Analysis, Templates, Suggestions, Packages, Settings)
  - Enhanced developer workflow with professional package management
- June 26, 2025: Implemented Replit Agent-style operation status display:
  - Fixed AI operation status to appear only in dedicated area below text input
  - Removed duplicate status indicators from chat history
  - Real-time operation reporting ("Analyzing code...", "Generating files...", etc.)
  - Clean chat area showing only actual user/AI conversations
  - Professional status animations with spinning indicators and progress dots
- June 26, 2025: Streamlined AI chat interface for minimal, clean design:
  - Removed user badges, timestamps, and message type indicators from chat
  - Eliminated "Gelişmiş AI Asistan" header for cleaner appearance
  - Added Enter key support for quick message sending (Shift+Enter for new lines)
  - Simplified message bubbles to show only essential content
  - Focused on pure conversational interface without visual clutter
- June 26, 2025: Fixed API endpoint compatibility issues and query method conflicts:
  - Resolved useQuery/POST method conflicts by converting to useMutation pattern
  - Fixed duplicate endpoint definitions causing route conflicts
  - Converted AI suggestions and analysis endpoints to proper POST mutations
  - Eliminated QueryClient fetch method errors for all AI endpoints
  - Synchronized FileSystemManager with database storage for complete CRUD operations
  - All API endpoints now function correctly without HTTP method validation errors
- June 26, 2025: Simplified application architecture by removing complex file management system:
  - Removed entire FileSystemManager and physical file system integration
  - Eliminated complex file operations (copy, move, backup, export/import)
  - Simplified File Explorer to basic file creation and navigation only
  - Streamlined AI Assistant to essential code generation functionality
  - Resolved all API endpoint conflicts and stability issues
  - Application now stable with database-only storage approach
  - Fixed API parameter order issues in advanced AI assistant
  - All endpoints now responding correctly (HTTP 200 status confirmed)
  - Core functionality verified: file operations, Monaco editor, live preview, AI integration
- June 26, 2025: Implemented advanced real-time code analysis system:
  - Created comprehensive RealtimeCodeAnalyzer with 300+ static analysis rules
  - JavaScript/TypeScript analysis: var usage, equality checks, function complexity, undefined handling
  - HTML analysis: DOCTYPE, viewport, alt text, semantic elements, form validation
  - CSS analysis: !important usage, vendor prefixes, modern layout techniques
  - Python analysis: PEP 8 compliance, import organization, naming conventions
  - Performance analysis: nested loops, DOM queries, memory leaks, complex selectors
  - Security analysis: XSS vulnerabilities, code injection, insecure storage, weak randomness
  - Real-time scoring system: quality (1-10), performance (1-10), security assessment
  - Created RealtimeCodeAssistant UI component with 3-tab interface (Issues, Performance, Security)
  - Integrated with existing editor: automatic analysis on file changes with 1.5s debounce
  - Test results: 8.8/10 quality score, comprehensive issue detection and recommendations
- June 26, 2025: Reorganized AI interface architecture for improved usability:
  - Separated AI Chat and Code Analysis into distinct components
  - Added "Kod Analizi" tab to editor navigation (Kod Editörü | Canlı Önizleme | Kod Analizi)
  - Restored clean AI Chat interface in left panel with black background textarea
  - Created dedicated CodeAnalysis component for analysis-only functionality
  - Fixed chat area color scheme and prevented interface conflicts
  - Chat and analysis systems now operate independently without visual interference
  - Removed "Proje Dosyaları" header text from file explorer for cleaner appearance
  - Reorganized layout: AI Chat (left panel), Editor/Preview with integrated file explorer (right panel)
  - Eliminated duplicate file explorers - kept only the one integrated in code editor
  - Cleaned up layout to two-panel design for better space utilization
- June 27, 2025: Modernized header design with compact, contemporary styling:
  - Reduced header height from 16 to 12 (h-16 to h-12)
  - Minimized logo icon size and made LocalReplit text more compact
  - Converted all buttons to smaller sizes: h-8 height, reduced padding, smaller icons
  - Updated select dropdown to compact size with rounded-md corners
  - Modernized spacing and typography for sleek, professional appearance
  - All UI elements now use consistent small sizing and modern design language
- June 27, 2025: Implemented comprehensive auto-fix system for code analysis:
  - Added "Düzelt" (Fix) buttons for each detected code issue
  - Created /api/ai/fix-code endpoint with regex-based automated corrections
  - Integrated auto-fix with real-time code analysis for instant problem resolution
  - Added callback system to refresh Monaco editor content after fixes
  - Supports common fixes: var→let, ==→===, missing semicolons, DOCTYPE, viewport meta tags
  - Real-time UI updates with success notifications and automatic re-analysis
- June 27, 2025: Integrated code analysis with AI assistant for intelligent error reporting:
  - Added automatic notification system from code analysis to AI assistant
  - Event-based communication between components using CustomEvent
  - AI assistant automatically receives error details and generates helpful suggestions
  - Code analysis triggers AI responses when issues are detected
  - Enhanced workflow: analysis detects errors → AI gets notification → provides solutions
- June 27, 2025: Fixed Monaco Editor content persistence and save functionality:
  - Implemented file-specific content cache system to preserve unsaved changes
  - Enhanced state management to prevent content loss when switching between files
  - Fixed auto-save (1.5s debounce) and manual save operations
  - Added proper cache synchronization after successful file saves
  - Each file maintains independent content state preventing overwrites
  - Toast notifications for successful save operations

## User Preferences
- Preferred communication style: Simple, everyday language
- Interface language: Turkish (complete localization implemented)
- UI Design preference: Extremely minimal, modern design with compact buttons and clean styling