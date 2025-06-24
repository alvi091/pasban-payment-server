# Pasban Payment Server - Railway Deployment

Express.js server for handling Razorpay payment processing securely, deployed on Railway.

## Railway Deployment Steps

### 1. Prepare Repository
```bash
# Make sure your server code is in a Git repository
cd server
git init
git add .
git commit -m "Initial commit for payment server"
```

### 2. Deploy to Railway
1. Go to [Railway Dashboard](https://railway.app/)
2. Click "New Project" → "Deploy from GitHub repo"
3. Connect your GitHub repository
4. Select the repository containing your server code
5. Railway will automatically detect it's a Node.js project

### 3. Environment Variables
Add these environment variables in Railway dashboard:
```
NODE_ENV=production
FRONTEND_URL=https://pasban.in
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
PORT=5000
```

### 4. Custom Start Command (if needed)
Railway should automatically detect your start command from package.json, but you can override it in the Railway dashboard:
- Start Command: `npm start`

### 5. Update Frontend
Update your frontend environment variables:
```
VITE_PAYMENT_SERVER_URL=https://your-railway-app-name.railway.app
```

## API Endpoints

### POST /api/create-order
Creates a new Razorpay order.

**Request Body:**
```json
{
  "amount": 1000,
  "receipt": "order_receipt_123",
  "currency": "INR"
}
```

**Response:**
```json
{
  "success": true,
  "order": {
    "id": "order_xyz123",
    "amount": 100000,
    "currency": "INR",
    "receipt": "order_receipt_123",
    "status": "created"
  }
}
```

### GET /health
Health check endpoint for monitoring.

## Security Features

- Helmet.js for security headers
- Rate limiting (100 requests per 15 minutes)
- CORS configuration for production domain
- Input validation
- Error handling

## Production Considerations

1. **Environment Variables**: Never commit sensitive keys to Git
2. **CORS**: Configured for https://pasban.in
3. **Rate Limiting**: Prevents abuse
4. **Error Handling**: Comprehensive error responses
5. **Health Checks**: For monitoring and uptime

## Monitoring

- Health check endpoint: `/health`
- Logs available in Railway dashboard
- Set up monitoring alerts in Railway

## Troubleshooting

1. **CORS Issues**: Ensure frontend domain is in allowedOrigins
2. **Environment Variables**: Check all required vars are set in Railway
3. **Razorpay Keys**: Verify keys are correct and active
4. **Rate Limiting**: Check if requests are being rate limited

## Local Development

```bash
npm install
npm run dev
```

Server runs on http://localhost:5000

## Railway vs Render Differences

### Advantages of Railway:
- Faster cold starts
- Better developer experience
- More generous free tier
- Automatic HTTPS
- Built-in monitoring
- Easier environment variable management

### Migration Benefits:
- Improved performance
- Better uptime
- More reliable deployments
- Enhanced monitoring capabilities