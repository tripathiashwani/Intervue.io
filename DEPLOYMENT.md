# Live Polling System - Deployment Guide

## Prerequisites

- Node.js (v16 or higher)
- npm or yarn
- Git

## Local Development

### Backend Setup

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create `.env` file with the following variables:
   ```
   PORT=5000
   CLIENT_URL=http://localhost:3000
   NODE_ENV=development
   ```

4. Start the development server:
   ```bash
   npm start
   ```

   For development with auto-restart:
   ```bash
   npm run dev
   ```

### Frontend Setup

1. Navigate to the frontend directory:
   ```bash
   cd frontend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create `.env` file with:
   ```
   REACT_APP_SERVER_URL=http://localhost:5000
   ```

4. Start the development server:
   ```bash
   npm start
   ```

## Production Deployment

### Backend Deployment (Heroku)

1. Install Heroku CLI and login:
   ```bash
   heroku login
   ```

2. Create a new Heroku app:
   ```bash
   heroku create your-polling-backend
   ```

3. Set environment variables:
   ```bash
   heroku config:set NODE_ENV=production
   heroku config:set CLIENT_URL=https://your-frontend-url.vercel.app
   ```

4. Deploy:
   ```bash
   git subtree push --prefix backend heroku main
   ```

### Frontend Deployment (Vercel)

1. Install Vercel CLI:
   ```bash
   npm i -g vercel
   ```

2. Navigate to frontend directory and deploy:
   ```bash
   cd frontend
   vercel
   ```

3. Set environment variables in Vercel dashboard:
   ```
   REACT_APP_SERVER_URL=https://your-backend-app.herokuapp.com
   ```

### Alternative Deployment Options

#### Railway (Backend)
- Connect your GitHub repository
- Set build command: `cd backend && npm install`
- Set start command: `cd backend && npm start`
- Add environment variables in Railway dashboard

#### Netlify (Frontend)
- Connect your GitHub repository
- Set build command: `cd frontend && npm run build`
- Set publish directory: `frontend/build`
- Add environment variables in Netlify dashboard

## Environment Variables

### Backend (.env)
```
PORT=5000
CLIENT_URL=http://localhost:3000
NODE_ENV=development
```

### Frontend (.env)
```
REACT_APP_SERVER_URL=http://localhost:5000
GENERATE_SOURCEMAP=false
```

## Features Implemented

### Core Features ✅
- [x] Teacher can create polls
- [x] Students can join with unique names
- [x] Real-time answer submission
- [x] Live results viewing
- [x] 60-second timer per question
- [x] Question flow control
- [x] Socket.io real-time communication

### Bonus Features ✅
- [x] Chat popup for teacher-student interaction
- [x] Past poll results storage and viewing
- [x] Configurable poll time limits
- [x] Teacher can remove students
- [x] Responsive design
- [x] Professional UI/UX

## Architecture

### Backend (Express.js + Socket.io)
- RESTful API endpoints
- Real-time WebSocket communication
- In-memory data storage (can be extended to use databases)
- CORS configuration for cross-origin requests

### Frontend (React + Redux + TypeScript)
- Component-based architecture
- Redux for state management
- TypeScript for type safety
- Socket.io client for real-time features
- Responsive CSS design

## API Endpoints

### REST API
- `GET /api/health` - Server health check
- `GET /api/poll/current` - Get current poll status
- `GET /api/poll/history` - Get poll history

### Socket Events

#### Client to Server
- `teacher-join` - Teacher joins the session
- `student-join` - Student joins with name
- `create-poll` - Teacher creates a new poll
- `submit-answer` - Student submits answer
- `send-message` - Send chat message
- `remove-student` - Teacher removes student

#### Server to Client
- `teacher-joined` - Teacher join confirmation
- `student-joined` - Student join confirmation
- `new-poll` - New poll created
- `results-updated` - Live results update
- `timer-update` - Timer countdown update
- `poll-ended` - Poll completion
- `new-message` - New chat message
- `removed-by-teacher` - Student removal notification

## Troubleshooting

### Common Issues

1. **CORS errors**: Ensure CLIENT_URL is correctly set in backend .env
2. **Socket connection issues**: Check if both servers are running and ports are correct
3. **Build errors**: Clear node_modules and reinstall dependencies
4. **TypeScript errors**: Check import paths and type definitions

### Debug Mode

Enable debug logging by setting:
```bash
DEBUG=socket.io:* npm start
```

## Performance Considerations

- In-memory storage is suitable for demo/small scale
- For production, consider using Redis for session storage
- Implement rate limiting for API endpoints
- Add connection limits for Socket.io
- Use a CDN for frontend assets

## Security Considerations

- Input validation on all user inputs
- XSS protection with proper escaping
- Rate limiting on poll creation and messaging
- Session management for user authentication
- HTTPS in production

## License

MIT License - Feel free to use this project for educational or commercial purposes.
