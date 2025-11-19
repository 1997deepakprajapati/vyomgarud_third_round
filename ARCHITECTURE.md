# Architecture Diagram

## System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                             │
│                    (User's Web Browser)                          │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             │ HTTP/HTTPS
                             │
┌────────────────────────────▼────────────────────────────────────┐
│                      FRONTEND LAYER                              │
│                    Next.js Application                          │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │                    Pages & Routes                        │  │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │  │
│  │  │   Home Page  │  │  Blog Posts  │  │  Single Post │  │  │
│  │  │   (/)        │  │  Listing     │  │  (/blog/:id) │  │  │
│  │  └──────────────┘  └──────────────┘  └──────────────┘  │  │
│  └──────────────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │              API Integration Layer                         │  │
│  │         (lib/api.ts - Strapi API Client)                  │  │
│  └───────────────────────────┬──────────────────────────────┘  │
└───────────────────────────────┼─────────────────────────────────┘
                                │
                                │ REST API Calls
                                │ (GET /api/blog-posts)
                                │
┌───────────────────────────────▼─────────────────────────────────┐
│                      BACKEND LAYER                               │
│                    Strapi CMS Server                            │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │              REST API Endpoints                           │  │
│  │  • GET /api/blog-posts                                   │  │
│  │  • GET /api/categories                                   │  │
│  │  • GET /api/tags                                         │  │
│  └──────────────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │              Content Type System                          │  │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │  │
│  │  │  Blog Post   │  │   Category   │  │     Tag      │  │  │
│  │  │              │  │              │  │              │  │  │
│  │  │ • title      │  │ • name       │  │ • name       │  │  │
│  │  │ • slug       │  │ • slug       │  │ • slug       │  │  │
│  │  │ • content    │  │ • description│  │              │  │  │
│  │  │ • excerpt    │  │              │  │              │  │  │
│  │  │ • image      │  │              │  │              │  │  │
│  │  │ • categories │  │              │  │              │  │  │
│  │  │ • tags       │  │              │  │              │  │  │
│  │  └──────────────┘  └──────────────┘  └──────────────┘  │  │
│  └──────────────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │              Admin Panel                                  │  │
│  │         (http://localhost:1337/admin)                    │  │
│  │  • Content Management Interface                          │  │
│  │  • Media Library                                         │  │
│  │  • User & Permission Management                          │  │
│  └───────────────────────────┬──────────────────────────────┘  │
└───────────────────────────────┼─────────────────────────────────┘
                                │
                                │ ORM/Query Layer
                                │
┌───────────────────────────────▼─────────────────────────────────┐
│                      DATA LAYER                                  │
│                    SQLite Database                               │
│              (backend/.tmp/data.db)                              │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │                    Tables                                │  │
│  │  • blog_posts                                            │  │
│  │  • categories                                            │  │
│  │  • tags                                                  │  │
│  │  • blog_posts_categories_links                            │  │
│  │  • blog_posts_tags_links                                 │  │
│  │  • files (for media uploads)                             │  │
│  └──────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

## Data Flow Sequence

### 1. Content Creation Flow
```
Admin User → Strapi Admin Panel → Content Type → Database
```

### 2. Content Retrieval Flow
```
User Browser → Next.js Frontend → API Call → Strapi REST API → Database → Response → Frontend Rendering
```

### 3. Image Upload Flow
```
Admin Panel → Strapi Media Library → File System (backend/public/uploads/) → Database Metadata
```

## Component Relationships

### Frontend Components
- **Layout**: Root layout with header and footer
- **Home Page**: Blog post listing with cards
- **Blog Post Page**: Individual post view with full content
- **API Client**: Centralized API communication layer

### Backend Components
- **Content Types**: Schema definitions for Blog Post, Category, Tag
- **REST API**: Auto-generated endpoints from content types
- **Admin Panel**: Content management interface
- **Media Library**: Image upload and management

## Technology Integration Points

1. **Strapi → Next.js**: REST API communication
2. **Next.js → Strapi**: Image optimization via Next.js Image component
3. **Strapi → SQLite**: ORM layer for data persistence
4. **Next.js → Browser**: Server-side rendering and client-side navigation

