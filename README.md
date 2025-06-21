# Pasban Payment Server - Render Deployment

Express.js server for handling Razorpay payment processing securely, deployed on Render.

## Render Deployment Steps

### 1. Prepare Repository
```bash
# Make sure your server code is in a Git repository
cd server
git init
git add .
git commit -m "Initial commit for payment server"
```

### 2. Deploy to Render
1. Go to [Render Dashboard](https://dashboard.render.com/)
2. Click "New +" → "Web Service"
3. Connect your GitHub repository
4. Configure the service:
   - **Name**: `pasban-payment-server`
   - **Environment**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Plan**: Free (or paid for better performance)

### 3. Environment Variables
Add these environment variables in Render dashboard:
```
NODE_ENV=production
FRONTEND_URL=https://pasban.in
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
PORT=5000
```

### 4. Update Frontend
Update your frontend `.env` file:
```
VITE_PAYMENT_SERVER_URL=https://your-render-app-name.onrender.com
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
- Logs available in Render dashboard
- Set up monitoring alerts in Render

## Troubleshooting

1. **CORS Issues**: Ensure frontend domain is in allowedOrigins
2. **Environment Variables**: Check all required vars are set in Render
3. **Razorpay Keys**: Verify keys are correct and active
4. **Rate Limiting**: Check if requests are being rate limited

## Local Development

```bash
npm install
npm run dev
```

Server runs on http://localhost:5000