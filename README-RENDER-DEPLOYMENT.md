# URL Shortener Backend - Render Deployment Guide

## Overview
This backend is now configured to deploy on Render with the following optimizations:
- Dynamic port configuration
- Production environment variable handling
- CORS configuration for cross-origin requests
- Health check endpoints
- Proper cookie settings for HTTPS

## Environment Variables Required on Render

Set these environment variables in your Render dashboard:

### Required Variables:
- `MONGO_URI`: Your MongoDB connection string (use MongoDB Atlas for production)
  - Example: `mongodb+srv://username:password@cluster.mongodb.net/url-shortener`
- `JWT_SECRET`: A secure random string for JWT token signing
  - Example: `your_super_secure_jwt_secret_here_make_it_long_and_random`
- `APP_URL`: Your deployed backend URL (Render will provide this)
  - Example: `https://your-app-name.onrender.com/`
- `NODE_ENV`: Set to `production`

### Optional Variables:
- `FRONTEND_URL`: Additional frontend URL if different from the hardcoded one
- `PORT`: Render sets this automatically, but you can override if needed

## Deployment Steps

1. **Push your code to GitHub** (if not already done)

2. **Create a new Web Service on Render:**
   - Connect your GitHub repository
   - Select the branch you want to deploy
   - Set the following build settings:
     - **Build Command**: `cd BACKEND && npm install`
     - **Start Command**: `cd BACKEND && npm start`

3. **Set Environment Variables:**
   - Go to your service's Environment tab
   - Add all the required environment variables listed above

4. **Deploy:**
   - Render will automatically build and deploy your service
   - The health check endpoint `/health` will help Render verify the service is running

## Important Notes

- **MongoDB**: Make sure to use MongoDB Atlas or another cloud MongoDB service for production
- **CORS**: The app is configured to accept requests from your Vercel frontend
- **Cookies**: Configured for HTTPS with proper SameSite settings for cross-origin requests
- **Health Check**: Available at `/health` endpoint for monitoring

## Testing the Deployment

Once deployed, you can test these endpoints:
- `GET /health` - Health check
- `GET /` - Root endpoint with API info
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `POST /api/create` - Create short URL

## Troubleshooting

1. **Database Connection Issues**: Verify your MONGO_URI is correct and MongoDB Atlas allows connections from anywhere (0.0.0.0/0)
2. **CORS Issues**: Check that your frontend URL is properly configured in the CORS settings
3. **Environment Variables**: Ensure all required environment variables are set in Render dashboard
