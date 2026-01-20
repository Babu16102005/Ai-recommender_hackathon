---
description: Deploy backend to Railway and frontend to Vercel
---

# Railway + Vercel Deployment Workflow

## Prerequisites
- GitHub account with code pushed
- Railway account (free at railway.app)
- Vercel account (free at vercel.com)

## Step 1: Push Latest Code to GitHub
```bash
git add -A
git commit -m "Add Docker configuration for deployment"
git push origin main
```

## Step 2: Deploy Backend to Railway

1. Go to https://railway.app
2. Click "Login" → Sign in with GitHub
3. Click "New Project" → "Deploy from GitHub repo"
4. Select your repository: `The_AI_recommender`
5. In "Configure your deployment":
   - Set **Root Directory**: `backend/learn`
6. Click "Add Variables" and add:
   - `GEMINI_API_KEY` = your_gemini_key
   - `YOUTUBE_API_KEY` = your_youtube_key
7. Click "Deploy"
8. Wait for build to complete
9. Click "Settings" → "Networking" → "Generate Domain"
10. Copy the generated URL (e.g., `https://xxx.railway.app`)

## Step 3: Deploy Frontend to Vercel

1. Go to https://vercel.com
2. Click "Login" → Sign in with GitHub
3. Click "Add New..." → "Project"
4. Import your repository: `The_AI_recommender`
5. Configure project:
   - **Root Directory**: Click "Edit" → select `frontend`
   - **Framework Preset**: Vite
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
6. Click "Environment Variables" and add:
   - `VITE_API_URL` = `https://xxx.railway.app` (your Railway URL from Step 2)
7. Click "Deploy"
8. Wait for deployment to complete
9. Your app is live at the Vercel URL!

## Step 4: Update CORS (if needed)

If you get CORS errors, update `backend/learn/app/main.py`:
```python
origins = [
    "http://localhost:5173",
    "https://your-app.vercel.app",  # Add your Vercel URL
]
```

Then redeploy the backend on Railway.
