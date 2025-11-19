# Quick Start Guide

## How to Run the Project

### Step 1: Install Dependencies

**Backend (Strapi):**
```bash
cd backend
npm install
```

**Frontend (Next.js):**
```bash
cd frontend
npm install
```

### Step 2: Start Strapi Backend

Open **Terminal 1**:
```bash
cd backend
npm run develop
```

Wait for the server to start. You should see:
```
Server started on http://localhost:1337
```

**First Time Setup:**
1. Open browser: `http://localhost:1337/admin`
2. Create your admin account (email, password, etc.)
3. After logging in, configure permissions:
   - Go to **Settings** → **Users & Permissions Plugin** → **Roles** → **Public**
   - Enable these permissions:
     - `blog-post`: Check `find` and `findOne`
     - `category`: Check `find` and `findOne`
     - `tag`: Check `find` and `findOne`
   - Click **Save**

### Step 3: Create Environment File for Frontend

Open **Terminal 2** (new terminal):
```bash
cd frontend
```

Create `.env.local` file:
```bash
# Windows PowerShell
echo "NEXT_PUBLIC_STRAPI_URL=http://localhost:1337" > .env.local

# Or create manually: create a file named .env.local with this content:
# NEXT_PUBLIC_STRAPI_URL=http://localhost:1337
```

### Step 4: Start Next.js Frontend

In **Terminal 2** (still in frontend directory):
```bash
npm run dev
```

Wait for the server to start. You should see:
```
Ready on http://localhost:3000
```

### Step 5: View Your Blog

Open browser: `http://localhost:3000`

## Creating Your First Blog Post

1. Go to `http://localhost:1337/admin` (Strapi admin panel)
2. Click **Content Manager** in the left sidebar
3. Click **Blog Post** → **Create new entry**
4. Fill in:
   - **Title**: Your blog post title
   - **Content**: Write your blog post (rich text editor)
   - **Excerpt**: Short description (optional)
   - **Featured Image**: Click to upload an image (optional)
   - **Categories**: Click to create/select categories
   - **Tags**: Click to create/select tags
   - **Author**: Your name (optional)
5. Click **Save** (top right)
6. Click **Publish** (to make it visible on the frontend)
7. Visit `http://localhost:3000` to see your post!

## Important Notes

- **Keep both terminals running**: You need both Strapi (Terminal 1) and Next.js (Terminal 2) running simultaneously
- **Backend must be running first**: Start Strapi before starting Next.js
- **Permissions are required**: Don't skip Step 2 permissions setup, or posts won't be visible

## Troubleshooting

**Port already in use?**
- Strapi uses port 1337, Next.js uses port 3000
- Make sure nothing else is using these ports

**Can't see posts?**
- Check permissions in Strapi admin (Step 2)
- Make sure posts are **Published**, not just saved as draft

**CORS errors?**
- Verify Strapi is running on port 1337
- Check `.env.local` has correct URL

