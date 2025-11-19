# Blogging Website - Strapi CMS + Next.js

A modern, full-stack blogging platform built with Strapi (headless CMS) and Next.js (React framework). This project demonstrates the integration between a backend CMS and a modern frontend framework for dynamic content management.

## 📋 Table of Contents

- [Architecture Overview](#architecture-overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Setup Instructions](#setup-instructions)
- [Project Structure](#project-structure)
- [Usage](#usage)
- [API Endpoints](#api-endpoints)
- [Deployment](#deployment)

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                         User Browser                         │
└───────────────────────────┬─────────────────────────────────┘
                            │
                            │ HTTP Requests
                            │
┌───────────────────────────▼─────────────────────────────────┐
│                    Next.js Frontend                          │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   Home Page  │  │  Blog Posts  │  │  Single Post │      │
│  │   (Listing)  │  │   (Dynamic)  │  │   (Dynamic)  │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└───────────────────────────┬─────────────────────────────────┘
                            │
                            │ REST API Calls
                            │ (GET /api/blog-posts)
                            │
┌───────────────────────────▼─────────────────────────────────┐
│                    Strapi Backend                           │
│  ┌─────────────────────────────────────────────────────┐   │
│  │              Content Types                          │   │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐         │   │
│  │  │Blog Post │  │ Category │  │   Tag    │         │   │
│  │  └──────────┘  └──────────┘  └──────────┘         │   │
│  └─────────────────────────────────────────────────────┘   │
│  ┌─────────────────────────────────────────────────────┐   │
│  │           Admin Panel (Port 1337/admin)             │   │
│  │  • Create/Edit/Delete Posts                         │   │
│  │  • Upload Images                                    │   │
│  │  • Manage Categories & Tags                        │   │
│  └─────────────────────────────────────────────────────┘   │
└───────────────────────────┬─────────────────────────────────┘
                            │
                            │ Data Persistence
                            │
┌───────────────────────────▼─────────────────────────────────┐
│                    SQLite Database                          │
│              (Stored in backend/.tmp/data.db)               │
└─────────────────────────────────────────────────────────────┘
```

### Data Flow

1. **Content Creation**: Admin users create blog posts, categories, and tags through the Strapi admin panel
2. **Content Storage**: Data is stored in SQLite database via Strapi
3. **API Exposure**: Strapi automatically generates REST API endpoints
4. **Frontend Consumption**: Next.js frontend fetches data from Strapi API
5. **User Display**: Blog posts are rendered on the public-facing website

## ✨ Features

- ✅ **Content Management**: Create, edit, and delete blog posts through Strapi admin panel
- ✅ **Image Upload**: Support for featured images with automatic optimization
- ✅ **Categorization**: Organize posts with categories and tags
- ✅ **Rich Content**: Rich text editor for blog post content
- ✅ **SEO-Friendly**: Automatic slug generation and metadata support
- ✅ **Responsive Design**: Modern, mobile-friendly UI built with Tailwind CSS
- ✅ **Real-time Updates**: Dynamic content fetching from Strapi API

## 🛠️ Tech Stack

### Backend
- **Strapi 5.31.0**: Headless CMS built on Node.js
- **SQLite**: Database (via better-sqlite3)
- **TypeScript**: Type-safe development

### Frontend
- **Next.js 14**: React framework with App Router
- **TypeScript**: Type-safe development
- **Tailwind CSS**: Utility-first CSS framework
- **React**: UI library

## 📦 Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v20.0.0 or higher)
- **npm** (v6.0.0 or higher)
- A modern web browser

## 🚀 Setup Instructions

### Step 1: Clone the Repository

```bash
git clone <repository-url>
cd roundthree
```

### Step 2: Install Backend Dependencies

```bash
cd backend
npm install
```

### Step 3: Start Strapi Backend

```bash
npm run develop
```

The Strapi server will start on `http://localhost:1337`

**First-time setup:**
1. Navigate to `http://localhost:1337/admin`
2. Create an admin account (first user)
3. After logging in, configure permissions:
   - Go to **Settings** → **Users & Permissions Plugin** → **Roles** → **Public**
   - Enable permissions for:
     - `blog-post`: `find` and `findOne`
     - `category`: `find` and `findOne`
     - `tag`: `find` and `findOne`
   - Save the permissions

### Step 4: Install Frontend Dependencies

Open a new terminal window:

```bash
cd frontend
npm install
```

### Step 5: Configure Environment Variables

Create a `.env.local` file in the `frontend` directory:

```bash
cd frontend
echo "NEXT_PUBLIC_STRAPI_URL=http://localhost:1337" > .env.local
```

### Step 6: Start Next.js Frontend

```bash
npm run dev
```

The frontend will start on `http://localhost:3000`

### Step 7: Create Your First Blog Post

1. Go to `http://localhost:1337/admin`
2. Navigate to **Content Manager** → **Blog Post**
3. Click **Create new entry**
4. Fill in:
   - Title
   - Content (rich text)
   - Excerpt (optional)
   - Featured Image (optional - upload an image)
   - Categories (create categories first if needed)
   - Tags (create tags first if needed)
   - Author (optional)
5. Click **Save** and then **Publish**

6. Visit `http://localhost:3000` to see your blog post!

## 📁 Project Structure

```
roundthree/
├── backend/                 # Strapi CMS Backend
│   ├── config/             # Strapi configuration files
│   │   ├── database.ts     # Database configuration (SQLite)
│   │   ├── middlewares.ts  # CORS and middleware setup
│   │   └── ...
│   ├── src/
│   │   └── api/            # Content type definitions
│   │       ├── blog-post/  # Blog post content type
│   │       ├── category/   # Category content type
│   │       └── tag/        # Tag content type
│   ├── .tmp/               # SQLite database storage
│   └── package.json
│
├── frontend/               # Next.js Frontend
│   ├── app/                # Next.js App Router
│   │   ├── page.tsx        # Home page (blog listing)
│   │   ├── blog/
│   │   │   └── [slug]/     # Dynamic blog post page
│   │   ├── layout.tsx      # Root layout
│   │   └── globals.css     # Global styles
│   ├── lib/
│   │   └── api.ts          # Strapi API integration
│   └── package.json
│
└── README.md               # This file
```

## 💻 Usage

### Creating Content Types (Already Done)

The content types (Blog Post, Category, Tag) are already defined in:
- `backend/src/api/blog-post/content-types/blog-post/schema.json`
- `backend/src/api/category/content-types/category/schema.json`
- `backend/src/api/tag/content-types/tag/schema.json`

### Managing Content

1. **Create Categories**: Go to Content Manager → Category → Create new entry
2. **Create Tags**: Go to Content Manager → Tag → Create new entry
3. **Create Blog Posts**: Go to Content Manager → Blog Post → Create new entry

### Viewing Content

- **Blog Listing**: `http://localhost:3000`
- **Individual Post**: `http://localhost:3000/blog/[post-slug]`

## 🔌 API Endpoints

Strapi automatically generates REST API endpoints:

- `GET /api/blog-posts` - Get all blog posts
- `GET /api/blog-posts/:id` - Get a single blog post
- `GET /api/categories` - Get all categories
- `GET /api/tags` - Get all tags

The frontend uses these endpoints via the API utility functions in `frontend/lib/api.ts`.

## 🚢 Deployment

### Local Development

Both servers should be running:
- Backend: `http://localhost:1337`
- Frontend: `http://localhost:3000`

### Optional: Production Deployment

#### Frontend (Vercel)
1. Push code to GitHub
2. Import project to Vercel
3. Set environment variable: `NEXT_PUBLIC_STRAPI_URL=<your-strapi-url>`
4. Deploy

#### Backend (Render/Heroku)
1. Push code to GitHub
2. Create new service on Render/Heroku
3. Set build command: `cd backend && npm install && npm run build`
4. Set start command: `cd backend && npm start`
5. Configure environment variables as needed

**Note**: For production, consider switching from SQLite to PostgreSQL for better scalability.

## 🐛 Troubleshooting

### CORS Errors
- Ensure `backend/config/middlewares.ts` includes the frontend URL in CORS origins

### Images Not Loading
- Check that `next.config.js` includes the correct image domain configuration
- Verify Strapi is running and accessible

### API Connection Issues
- Verify Strapi is running on port 1337
- Check `.env.local` has correct `NEXT_PUBLIC_STRAPI_URL`
- Ensure permissions are set in Strapi admin panel

## 📝 Notes

- The project uses SQLite for simplicity in local development
- All content types support draft/publish workflow
- Images are stored in `backend/public/uploads/`
- The frontend uses Next.js App Router for modern React patterns

## 📄 License

This project is created for Round 3 technical assessment.

---

**Made with ❤️ for Round 3**

