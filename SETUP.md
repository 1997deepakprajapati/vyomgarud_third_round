# Quick Setup Guide

## Prerequisites
- Node.js v20+ and npm v6+

## Step-by-Step Setup

### 1. Install Backend Dependencies
```bash
cd backend
npm install
```

### 2. Start Strapi Backend
```bash
npm run develop
```
- Wait for server to start on `http://localhost:1337`
- Open `http://localhost:1337/admin` in browser
- **Create admin account** (first-time setup only)

### 3. Configure Strapi Permissions
After creating admin account:
1. Go to **Settings** → **Users & Permissions Plugin** → **Roles** → **Public**
2. Under **Permissions**, enable:
   - `blog-post`: `find` and `findOne`
   - `category`: `find` and `findOne`
   - `tag`: `find` and `findOne`
3. Click **Save**

### 4. Install Frontend Dependencies
Open a **new terminal window**:
```bash
cd frontend
npm install
```

### 5. Create Environment File
```bash
# In frontend directory
echo NEXT_PUBLIC_STRAPI_URL=http://localhost:1337 > .env.local
```

### 6. Start Next.js Frontend
```bash
npm run dev
```
- Frontend will start on `http://localhost:3000`

### 7. Create Your First Blog Post
1. Go to `http://localhost:1337/admin`
2. Navigate to **Content Manager** → **Blog Post**
3. Click **Create new entry**
4. Fill in the form:
   - **Title**: Your post title
   - **Content**: Your blog post content (rich text)
   - **Excerpt**: Short description (optional)
   - **Featured Image**: Upload an image (optional)
   - **Categories**: Create/select categories
   - **Tags**: Create/select tags
   - **Author**: Your name (optional)
5. Click **Save** then **Publish**

### 8. View Your Blog
- Visit `http://localhost:3000` to see your blog posts!

## Troubleshooting

**CORS Errors?**
- Make sure Strapi is running on port 1337
- Check `backend/config/middlewares.ts` includes `http://localhost:3000`

**Can't see posts?**
- Verify permissions are set in Strapi admin (Step 3)
- Make sure posts are **Published** (not just saved as draft)

**Images not loading?**
- Check `next.config.js` has correct image domain
- Verify Strapi is accessible

## Running Both Servers

You need **two terminal windows**:
- **Terminal 1**: `cd backend && npm run develop` (Strapi on :1337)
- **Terminal 2**: `cd frontend && npm run dev` (Next.js on :3000)

Both must be running simultaneously!

