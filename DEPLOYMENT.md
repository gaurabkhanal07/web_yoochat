# YooChat Deployment Guide

## 🚀 Deploying to Vercel

### Frontend (React App) Deployment

1. **Push your code to GitHub** (already done!)

2. **Deploy Frontend to Vercel:**
   - Go to [vercel.com](https://vercel.com)
   - Click "New Project"
   - Import your `web_yoochat` repository
   - Configure the project:
     - **Framework Preset:** Create React App
     - **Root Directory:** `yoochat`
     - **Build Command:** `npm run build`
     - **Output Directory:** `build`

3. **Add Environment Variables in Vercel:**
   - Go to Project Settings → Environment Variables
   - Add: `REACT_APP_API_URL` = `https://your-backend-url.vercel.app`
   - Save and redeploy

### Backend (Express API) Deployment

1. **Deploy Backend to Vercel:**
   - Create a new project in Vercel
   - Import your repository again
   - Configure the project:
     - **Framework Preset:** Other
     - **Root Directory:** `backend`
     - **Build Command:** (leave empty)
     - **Output Directory:** (leave empty)

2. **Add Environment Variables in Vercel:**
   - Go to Project Settings → Environment Variables
   - Add these variables:
     ```
     DATABASE_URL=your_neon_database_url
     secret_key=your_jwt_secret
     hill_key=GYBN
     FRONTEND_URL=https://your-frontend-url.vercel.app
     PORT=3000
     ```

3. **Update Frontend Environment Variable:**
   - Go back to your frontend project in Vercel
   - Update `REACT_APP_API_URL` with your backend URL
   - Redeploy the frontend

## 📝 Environment Variables Summary

### Frontend (.env.local)
```env
REACT_APP_API_URL=https://your-backend-url.vercel.app
```

### Backend (.env)
```env
PORT=3000
FRONTEND_URL=https://your-frontend-url.vercel.app
DATABASE_URL=postgresql://...your neon db url...
secret_key=your_secret_key_here
hill_key=GYBN
```

## ✅ Post-Deployment Checklist

- [ ] Backend deployed and accessible
- [ ] Database connected (check Vercel logs)
- [ ] Frontend deployed
- [ ] Environment variables configured on both
- [ ] CORS working (frontend can call backend)
- [ ] Test login functionality
- [ ] Test post creation
- [ ] Test image uploads (note: Vercel has file system limitations)

## ⚠️ Important Notes

### File Uploads
Vercel has a read-only file system. For production, you should:
1. Use a cloud storage service (AWS S3, Cloudinary, etc.)
2. Update the file upload logic to use cloud storage instead of local `/uploads`

### Current Setup
- ✅ URLs are now configurable via environment variables
- ✅ CORS configured for production
- ✅ Database migrations ready
- ⚠️ File uploads still save locally (needs cloud storage for production)

## 🔧 Alternative: Deploy Backend Elsewhere

If you prefer, you can deploy the backend to:
- **Railway.app** (better for file uploads)
- **Render.com** (has persistent storage)
- **Heroku** (with S3 addon)

Just update the `REACT_APP_API_URL` in your frontend to point to wherever you deploy the backend!

## 🧪 Testing Locally

After making these changes, test locally:

```bash
# Backend
cd backend
npm start

# Frontend (new terminal)
cd yoochat
npm start
```

Everything should work the same as before!
