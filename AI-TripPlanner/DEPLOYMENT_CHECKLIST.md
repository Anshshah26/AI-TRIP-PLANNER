# AI Trip Planner - Deployment Checklist

## Pre-Deployment Checklist

### Backend (Render)
- [ ] Review server configuration in `server/server.js`
- [ ] Verify all API routes are working locally
- [ ] Check MongoDB connection string format
- [ ] Test with `npm run dev` locally
- [ ] Ensure error handling is working
- [ ] Verify Socket.IO configuration

### Frontend (Vercel)
- [ ] Test build: `cd client && npm run build`
- [ ] Verify no build warnings/errors
- [ ] Check API endpoint configuration in `src/services/api.js`
- [ ] Test API calls with local backend
- [ ] Verify environment variables are used correctly

### Code Repository
- [ ] Push all code to GitHub
- [ ] Create `.env.example` files (DONE ✓)
- [ ] Add `render.yaml` and `vercel.json` (DONE ✓)
- [ ] Ensure no hardcoded URLs (check for localhost)
- [ ] No sensitive data in Git (only in .env files)

### Configuration Files Created
- [x] `client/vercel.json` - Vercel frontend config
- [x] `render.yaml` - Render backend config  
- [x] `server/.env.example` - Backend environment template
- [x] `client/.env.example` - Frontend environment template
- [x] `DEPLOYMENT.md` - Complete deployment guide

---

## Deployment Steps

### 1. Backend Deployment on Render

```bash
# Ensure you have the latest code pushed to GitHub
git add .
git commit -m "Prepare for deployment"
git push origin main
```

1. Go to https://render.com/dashboard
2. Click "New +" → "Web Service"
3. Connect GitHub repository
4. Select "ai-trip-planner" (or your repo name)
5. Configure:
   - **Name**: ai-trip-planner-backend
   - **Environment**: Node
   - **Build Command**: `npm install`
   - **Start Command**: `node server.js`
   - **Plan**: Free/Starter (select based on needs)
6. Add Environment Variables (copy from `server/.env.example`):
   - `NODE_ENV`: production
   - `PORT`: 10000
   - `MONGODB_URI`: [your MongoDB connection string]
   - All JWT secrets, API keys, etc.
7. Click "Create Web Service"
8. **Note the Render URL** (e.g., https://ai-trip-planner-backend.onrender.com)

### 2. Frontend Deployment on Vercel

1. Go to https://vercel.com/dashboard
2. Click "Add New" → "Project"
3. Import GitHub repository
4. **Root Directory**: Set to `client`
5. **Framework**: Create React App
6. Configure:
   - **Build Command**: `npm run build`
   - **Output Directory**: `build`
7. Add Environment Variables:
   - `REACT_APP_API_URL`: https://ai-trip-planner-backend.onrender.com/api (use your Render URL)
   - `REACT_APP_GOOGLE_MAPS_API_KEY`: [your Google Maps API key]
8. Click "Deploy"
9. **Note the Vercel URL** (e.g., https://your-app.vercel.app)

### 3. Update Backend with Frontend URL

After frontend is deployed:
1. Go back to Render dashboard
2. Select your backend service
3. Go to "Environment"
4. Update variables:
   - `CLIENT_URL`: https://your-app.vercel.app
   - `ALLOWED_ORIGINS`: https://your-app.vercel.app
5. Click "Save" - Backend will automatically redeploy

---

## Post-Deployment Testing

### Test Backend
```bash
curl https://ai-trip-planner-backend.onrender.com/api/health
```

### Test Frontend
- Visit https://your-app.vercel.app
- Try logging in
- Check browser console for errors
- Check Vercel logs: https://vercel.com/dashboard

### Monitor Deployments
- **Render Logs**: Dashboard → Service → Logs
- **Vercel Logs**: Dashboard → Select Project → Deployments → View logs
- **MongoDB**: Check connection in Atlas console

---

## Troubleshooting Common Issues

### 502 Bad Gateway on Render
- Check server is listening on PORT 10000
- Verify MongoDB connection string
- Check build logs for errors
- Ensure dependencies are installed

### CORS Errors
- Verify `ALLOWED_ORIGINS` includes your Vercel URL
- Check CORS headers in `server/middleware/security.js`
- Ensure Socket.IO CORS is configured

### API Connection Failed
- Verify `REACT_APP_API_URL` is correct in Vercel env vars
- Check backend is running on Render
- Test endpoint directly: `curl <backend-url>/api/endpoint`

### Socket.IO Connection Issues
- Update `CLIENT_URL` in backend env vars
- Restart backend after updating env vars
- Check WebSocket is enabled in Vercel (it is by default)

### Database Connection Issues
- Verify MongoDB connection string format
- Check MongoDB Atlas IP whitelist (add 0.0.0.0/0 for testing)
- Ensure database name is correct
- Check user credentials

---

## Maintenance

### Regular Tasks
- Monitor error logs
- Check storage/bandwidth usage
- Update dependencies: `npm update`
- Rotate JWT secrets periodically
- Backup MongoDB regularly

### Scaling
- If Render free tier is insufficient, upgrade plan
- Consider Vercel Pro for better performance
- Use CDN for static assets
- Optimize database queries

### Updates
- Test changes locally first
- Push to separate branch
- Create PR for review
- Merge to main only when ready
- Deployments happen automatically on main branch

---

## Environment Variables Reference

### Backend (Render)
- **NODE_ENV**: Set to "production"
- **PORT**: Must be 10000 for Render
- **MONGODB_URI**: MongoDB connection string
- **CLIENT_URL**: Your Vercel frontend URL
- **ALLOWED_ORIGINS**: CORS allowed origins (can be same as CLIENT_URL)
- **JWT secrets**: Generate strong random values
- **GEMINI_API_KEY**: Google Gemini API key
- **EMAIL credentials**: Gmail app-specific password recommended

### Frontend (Vercel)
- **REACT_APP_API_URL**: Your Render backend URL with /api suffix
- **REACT_APP_GOOGLE_MAPS_API_KEY**: Google Maps API key

---

## Useful Commands

### Generate strong secrets
```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

### Test backend locally
```bash
cd server
npm install
npm run dev
```

### Test frontend build locally
```bash
cd client
npm install
npm run build
npm start
```

### Check if backend is running
```bash
curl -I https://your-backend-url.onrender.com
```

---

## Support & Resources

- Render Documentation: https://render.com/docs
- Vercel Documentation: https://vercel.com/docs
- MongoDB Atlas: https://docs.atlas.mongodb.com/
- Express.js: https://expressjs.com/
- React Documentation: https://react.dev/

---

Last updated: 2026
Project: AI Trip Planner
