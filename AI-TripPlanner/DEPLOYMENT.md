# Deployment Guide - Vercel (Frontend) & Render (Backend)

## Prerequisites
- GitHub account with your code repository
- Vercel account (https://vercel.com)
- Render account (https://render.com)
- MongoDB Atlas account for database

## Backend Deployment (Render)

### Step 1: Prepare the Backend
1. Ensure all dependencies are in `server/package.json`
2. Update `.env` with production values or use Render's environment variables

### Step 2: Deploy to Render
1. Go to [Render Dashboard](https://dashboard.render.com)
2. Click **New +** → **Web Service**
3. Connect your GitHub repository
4. Configure:
   - **Name**: ai-trip-planner-backend
   - **Runtime**: Node
   - **Build Command**: `npm install`
   - **Start Command**: `node server.js`
   - **Plan**: Free (or Paid for better performance)

### Step 3: Set Environment Variables on Render
Add these environment variables in Render dashboard:

```
NODE_ENV=production
PORT=10000
MONGODB_URI=your_mongodb_connection_string
CLIENT_URL=https://your-frontend-url.vercel.app
ALLOWED_ORIGINS=https://your-frontend-url.vercel.app
JWT_ACCESS_SECRET=generate_strong_random_secret
JWT_REFRESH_SECRET=generate_strong_random_secret
SESSION_SECRET=generate_strong_random_secret
GEMINI_API_KEY=your_gemini_api_key
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_SECURE=false
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_app_password
EMAIL_FROM=AI Trip Planner <noreply@yourdomain.com>
LOG_LEVEL=info
```

### Step 4: Deploy
- Click **Deploy**
- Get your backend URL (e.g., `https://ai-trip-planner-backend.onrender.com`)

---

## Frontend Deployment (Vercel)

### Step 1: Prepare the Frontend
1. Ensure `client/package.json` has correct build script
2. Test build locally: `cd client && npm run build`

### Step 2: Deploy to Vercel
1. Go to [Vercel Dashboard](https://vercel.com/dashboard)
2. Click **Add New** → **Project**
3. Import your GitHub repository
4. Select the `client` directory as root:
   - **Framework**: Create React App
   - **Root Directory**: `client`
   - **Build Command**: `npm run build`
   - **Output Directory**: `build`

### Step 3: Set Environment Variables on Vercel
Add these environment variables:

```
REACT_APP_API_URL=https://your-backend-url.onrender.com/api
REACT_APP_GOOGLE_MAPS_API_KEY=your_google_maps_api_key
```

Replace `https://your-backend-url.onrender.com` with your actual Render backend URL.

### Step 4: Deploy
- Click **Deploy**
- Get your frontend URL (e.g., `https://your-app.vercel.app`)

---

## Update Backend with Frontend URL

After deploying frontend to Vercel:
1. Go to Render dashboard
2. Update these environment variables with your Vercel URL:
   - `CLIENT_URL=https://your-app.vercel.app`
   - `ALLOWED_ORIGINS=https://your-app.vercel.app`
3. Redeploy the backend

---

## Important Configuration Files

### `vercel.json` (Frontend)
Located at `client/vercel.json` - Configures Vercel build and routing

### `render.yaml` (Backend)
Located at `render.yaml` - Configures Render deployment (optional, can use UI instead)

### `.env.example`
Template for environment variables - Copy and update with real values

---

## Troubleshooting

### CORS Errors
- Make sure `ALLOWED_ORIGINS` on backend matches your Vercel frontend URL
- Update `CLIENT_URL` environment variable

### Database Connection Issues
- Verify `MONGODB_URI` is correct
- Check MongoDB Atlas network access includes Render's IP
- Add `0.0.0.0/0` to IP whitelist if needed

### Socket.IO Connection Issues
- Ensure Socket.IO CORS is properly configured in `server.js`
- Update `CLIENT_URL` environment variable

### Build Failures
- Check logs in Render/Vercel dashboards
- Verify all dependencies are in `package.json`
- Ensure `.env` variables are set correctly

---

## Production Checklist

- [ ] Generate strong random secrets for JWT and SESSION
- [ ] Update MONGODB_URI with production database
- [ ] Configure email service credentials
- [ ] Set correct CLIENT_URL and ALLOWED_ORIGINS
- [ ] Test CORS and authentication
- [ ] Test Socket.IO connections
- [ ] Set NODE_ENV=production
- [ ] Enable HTTPS/SSL
- [ ] Monitor logs and errors
- [ ] Set up monitoring/uptime checks
- [ ] Backup database regularly

---

## Monitoring & Maintenance

### Render Dashboard
- Check application logs
- Monitor resource usage
- Set up alerts for failures

### Vercel Dashboard
- Monitor build times and deployments
- Check Web Analytics
- Review error reports

### Environment Variables
- Regularly rotate secrets
- Keep credentials secure in `.env` files
- Never commit real secrets to Git

---

## Local Development

To run locally during development:

```bash
# Install all dependencies
npm run install-all

# Run development mode (frontend + backend)
npm run dev
```

Frontend: http://localhost:3000
Backend: http://localhost:5000

---

## Additional Resources

- [Vercel Documentation](https://vercel.com/docs)
- [Render Documentation](https://render.com/docs)
- [MongoDB Atlas Guide](https://docs.atlas.mongodb.com/)
- [Create React App Deployment](https://create-react-app.dev/deployment/)
