# n8n Chatbot React App

A beautiful, responsive React chatbot that connects directly to n8n workflows via webhooks, deployed on GitHub Pages.

## 🚀 Features

- **Modern UI**: Clean, responsive chat interface with smooth animations
- **Direct n8n Integration**: Communicates directly with n8n webhooks (no backend required)
- **GitHub Pages Ready**: Optimized for static hosting on GitHub Pages
- **Error Handling**: Comprehensive error handling with user-friendly messages
- **Real-time Chat**: Instant messaging with typing indicators
- **Mobile Responsive**: Works perfectly on all device sizes

## 📋 Prerequisites

- Node.js 18+ installed
- n8n instance (cloud or self-hosted) with webhook configured
- GitHub account for deployment

## 🛠️ Setup Instructions

### 1. Clone and Install

```bash
git clone https://github.com/yourusername/dash10_webapp.git
cd dash10_webapp
npm install
```

### 2. Configure Environment Variables

Create a `.env.local` file in the root directory:

```bash
cp .env.example .env.local
```

Edit `.env.local` and add your n8n webhook URL:

```env
REACT_APP_N8N_WEBHOOK_URL=https://your-n8n-instance.com/webhook/your-webhook-id
```

### 3. Update package.json

Update the `homepage` field in `package.json`:

```json
{
  "homepage": "https://yourusername.github.io/your-repo-name"
}
```

### 4. Run Locally

```bash
npm start
```

The app will open at `http://localhost:3000`

## 🔧 n8n Workflow Configuration

### Required n8n Workflow Structure:

1. **Webhook Trigger Node**
   - Method: POST
   - Authentication: None (or configure as needed)
   - **IMPORTANT**: Enable CORS in webhook settings

2. **CORS Headers** (Add this to your webhook response):
   ```json
   {
     "Access-Control-Allow-Origin": "*",
     "Access-Control-Allow-Methods": "POST, OPTIONS",
     "Access-Control-Allow-Headers": "Content-Type"
   }
   ```

3. **Expected Request Format**:
   ```json
   {
     "message": "User's message text",
     "timestamp": "2024-01-01T12:00:00.000Z",
     "sessionId": "web-chat-1234567890"
   }
   ```

4. **Expected Response Format**:
   ```json
   {
     "message": "Bot's response text",
     "timestamp": "2024-01-01T12:00:00.000Z"
   }
   ```

### Sample n8n Workflow:

```
Webhook → Set CORS Headers → [Your AI Logic] → Response
```

**Webhook Node Settings:**
- HTTP Method: POST
- Path: `/webhook/chatbot` (or your chosen path)
- Response Mode: Respond to Webhook

**Set Headers Node** (HTTP Response):
```json
{
  "Access-Control-Allow-Origin": "*",
  "Access-Control-Allow-Methods": "POST, OPTIONS",
  "Access-Control-Allow-Headers": "Content-Type"
}
```

## 🚀 Deployment to GitHub Pages

### Automatic Deployment (Recommended)

1. **Enable GitHub Pages**:
   - Go to your repository settings
   - Navigate to "Pages" section
   - Source: "GitHub Actions"

2. **Set GitHub Secrets**:
   - Go to repository Settings → Secrets and variables → Actions
   - Add secret: `N8N_WEBHOOK_URL` with your webhook URL

3. **Push to main branch**:
   ```bash
   git add .
   git commit -m "Initial commit"
   git push origin main
   ```

The GitHub Action will automatically build and deploy your app!

### Manual Deployment

```bash
npm run build
npm run deploy
```

## 🔒 Security Considerations

### For Production:

1. **Webhook Authentication**: Configure authentication in your n8n webhook
2. **Rate Limiting**: Implement rate limiting in your n8n workflow
3. **Input Validation**: Validate and sanitize inputs in n8n
4. **HTTPS**: Ensure your n8n instance uses HTTPS
5. **Environment Variables**: Never commit webhook URLs to git

### CORS Configuration:

Since GitHub Pages serves static files, your n8n webhook must handle CORS. Add these headers to your n8n response:

```javascript
// In your n8n Function node
return {
  json: {
    message: "Your bot response"
  },
  headers: {
    "Access-Control-Allow-Origin": "*",
    "Access-Control-Allow-Methods": "POST, OPTIONS",
    "Access-Control-Allow-Headers": "Content-Type"
  }
};
```

## 🎨 Customization

### Styling
- Edit `src/components/ChatBot.css` for visual customization
- Modify colors, fonts, and layout as needed

### Functionality
- Update `src/components/ChatBot.js` for additional features
- Add message history persistence
- Implement user authentication
- Add file upload capabilities

## 🐛 Troubleshooting

### Common Issues:

1. **CORS Error**: Ensure CORS headers are set in your n8n webhook
2. **Webhook Not Found**: Verify your webhook URL is correct
3. **Build Fails**: Check Node.js version (requires 18+)
4. **GitHub Pages Not Updating**: Check GitHub Actions logs

### Debug Mode:

Enable debug logging by adding to `.env.local`:
```env
REACT_APP_DEBUG=true
```

## 📱 Browser Support

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📄 License

MIT License - see LICENSE file for details

## 🆘 Support

If you encounter issues:

1. Check the troubleshooting section
2. Review n8n workflow configuration
3. Check browser console for errors
4. Verify webhook URL and CORS settings

---

**Built with ❤️ using React and n8n**
