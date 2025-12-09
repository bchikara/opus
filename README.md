# StreamOpus - Professional Studio Recording Platform

A production-ready platform for recording, editing, and streaming multi-participant video sessions with distributed recording, live transcription, AI translation, and professional editing tools.

## Features

### Studio & Recording
- **Multi-participant recording** with WebRTC streaming via MediaMTX
- **Distributed recording architecture** - Each participant records locally, uploads chunks in background
- **Real-time audio waveforms** with Redis caching
- **Multi-source recording** - Camera, screen share, and audio tracks
- **Recording controls** - Pause/resume, quality settings, storage estimation
- **Auto-reconnection** with state persistence on network failures

### Live Features
- **Real-time chat** with link previews and emoji reactions
- **Live transcription** using OpenAI Whisper
- **Multi-language translation** with 14+ languages
- **Teleprompter** with script editor and auto-scroll
- **Live streaming** to RTMP destinations
- **Audio mixer** with EQ, compressor, effects, and pan controls

### Post-Production
- **Timeline editor** with drag-drop editing
- **AI-powered features** - Auto-captions, voice translation, scene detection
- **Multi-track editing** with waveform visualization
- **Export** to multiple formats and resolutions
- **Cloud storage** with Cloudflare R2 integration

## Demo

🎥 **Watch the full demo and walkthrough:**

[![StreamOpus Demo](https://img.youtube.com/vi/wJMe9czLsXo/maxresdefault.jpg)](https://youtu.be/wJMe9czLsXo)

**[Watch on YouTube →](https://youtu.be/wJMe9czLsXo)**

See StreamOpus in action with:
- Real-time multi-participant recording
- WebRTC streaming and distributed recording
- AI-powered transcription and translation
- Live chat and collaboration features
- Advanced recording controls and settings
- Post-production editing tools

## Architecture

```
Opus/
├── frontend/          # Next.js 15 + React + TypeScript
├── backend/           # Node.js + Express + GraphQL + MongoDB
├── tts-service/       # Python Flask - Free AI voice generation (Coqui TTS)
├── translation-service/  # Python Flask - Multi-language translation
├── transcription-service/  # Python Flask - Whisper transcription
└── scripts/           # Utility scripts
```

## Tech Stack

**Frontend:**
- Next.js 15 (App Router)
- React 18 with TypeScript
- Apollo Client (GraphQL)
- Tailwind CSS
- Framer Motion
- WebRTC for streaming

**Backend:**
- Node.js + Express
- GraphQL (Apollo Server)
- MongoDB with Mongoose
- Redis (caching, Bull queues)
- Socket.io (real-time)
- BullMQ (job processing)

**Storage:**
- Cloudflare R2 (object storage)
- MongoDB (metadata, users, sessions)
- Redis (cache, queues, waveforms)

**Media:**
- MediaMTX (WebRTC/WHIP server)
- FFmpeg (video processing)
- OpenAI Whisper (transcription)
- Coqui TTS (voice generation)

## Prerequisites

- Node.js 18+
- MongoDB 6+
- Redis 7+
- Python 3.11+ (for AI services)
- FFmpeg
- MediaMTX

## Quick Start

### 1. Clone the Repository

```bash
git clone <repository-url>
cd Opus
```

### 2. Setup Backend

```bash
cd backend
npm install
```

Create `.env` file:
```env
# MongoDB
MONGODB_URI=mongodb://localhost:27017/opus

# Redis
REDIS_HOST=localhost
REDIS_PORT=6379

# JWT
JWT_SECRET=your-secret-key-here
JWT_REFRESH_SECRET=your-refresh-secret-here

# Cloudflare R2
R2_ACCOUNT_ID=your-account-id
R2_ACCESS_KEY_ID=your-access-key
R2_SECRET_ACCESS_KEY=your-secret-key
R2_BUCKET_NAME=opus-recordings
R2_PUBLIC_URL=https://your-bucket.r2.cloudflarestorage.com

# Services
TRANSCRIPTION_SERVICE_URL=http://localhost:5002
TTS_SERVICE_URL=http://localhost:5001
TRANSLATION_SERVICE_URL=http://localhost:5003

# OAuth (optional)
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
GITHUB_CLIENT_ID=your-github-client-id
GITHUB_CLIENT_SECRET=your-github-client-secret
```

Start backend:
```bash
npm run dev
```

### 3. Setup Frontend

```bash
cd frontend
npm install
```

Create `.env.local`:
```env
NEXT_PUBLIC_GRAPHQL_URL=http://localhost:8000/graphql
NEXT_PUBLIC_SOCKET_URL=http://localhost:8000
NEXT_PUBLIC_MEDIAMTX_WHIP_URL=http://localhost:8889
NEXT_PUBLIC_GOOGLE_CLIENT_ID=your-google-client-id
```

Start frontend:
```bash
npm run dev
```

### 4. Setup MediaMTX

Download MediaMTX from https://github.com/bluenviron/mediamtx/releases

```bash
# Extract and run
./mediamtx
```

Or use the provided script:
```bash
chmod +x start-mediamtx.sh
./start-mediamtx.sh
```

### 5. Setup AI Services

#### Transcription Service (Whisper)

```bash
cd transcription-service
chmod +x setup.sh
./setup.sh

chmod +x start.sh
./start.sh
```

Service runs on `http://localhost:5002`

#### TTS Service (Voice Generation)

```bash
cd tts-service
chmod +x setup.sh
./setup.sh

chmod +x start.sh
./start.sh
```

Service runs on `http://localhost:5001`

#### Translation Service

```bash
cd translation-service
chmod +x setup.sh
./setup.sh

chmod +x start.sh
./start.sh
```

Service runs on `http://localhost:5003`

### 6. Start All Services

Use the convenience script to start everything:

```bash
chmod +x start-all.sh
./start-all.sh
```

## Development

### Frontend Development

```bash
cd frontend
npm run dev        # Start dev server
npm run build      # Production build
npm run lint       # Lint code
```

### Backend Development

```bash
cd backend
npm run dev        # Start with nodemon
npm run build      # Build TypeScript
npm start          # Production start
```

### Database

MongoDB must be running on `localhost:27017` (or configured URL)

```bash
# Start MongoDB (macOS)
brew services start mongodb-community

# Start MongoDB (Linux)
sudo systemctl start mongod
```

### Redis

Redis must be running on `localhost:6379` (or configured URL)

```bash
# Start Redis (macOS)
brew services start redis

# Start Redis (Linux)
sudo systemctl start redis
```

## Project Structure

### Frontend
```
frontend/
├── app/                    # Next.js app routes
│   ├── dashboard/         # Dashboard pages
│   ├── studio/            # Recording studio
│   ├── editor/            # Video editor
│   └── signin/            # Authentication
├── components/            # React components
│   ├── studio/           # Studio components
│   ├── dashboard/        # Dashboard components
│   └── modals/           # Modal dialogs
├── contexts/             # React contexts
├── hooks/                # Custom React hooks
├── lib/                  # Utilities & services
│   ├── graphql/         # GraphQL queries/mutations
│   ├── streaming/       # WebRTC streaming
│   ├── recording/       # Recording logic
│   └── upload/          # Upload management
└── public/              # Static assets
```

### Backend
```
backend/
├── src/
│   ├── graphql/         # GraphQL schema & resolvers
│   ├── models/          # Mongoose models
│   ├── routes/          # REST API routes
│   ├── services/        # Business logic
│   ├── queues/          # BullMQ job queues
│   ├── socket/          # Socket.io handlers
│   └── server.ts        # Express server
```

## Key Features Documentation

### Distributed Recording

Each participant records locally and uploads chunks in the background. This ensures:
- No data loss on network failures
- Better quality (no stream compression)
- Resilient to disconnections
- Scalable to many participants

See implementation in:
- Frontend: `frontend/lib/recording/LocalRecorder.ts`
- Backend: `backend/src/queues/recordingProcessingQueue.ts`

### Real-time Audio Waveforms

Waveforms are generated during recording and cached in Redis for instant playback.

- Generation: `backend/src/services/waveformCache.ts`
- Display: `frontend/components/audio/SimpleAudioWaveform.tsx`

### WebRTC Streaming

Uses MediaMTX for WHIP/WHEP protocol:
- Publish: `frontend/lib/streaming/WebRTCStreamManager.ts`
- Subscribe: `frontend/lib/streaming/MultiStreamManager.ts`
- Reconnection: `frontend/lib/streaming/WebRTCReconnectionManager.ts`

## Environment Variables Reference

### Backend (.env)

| Variable | Description | Required |
|----------|-------------|----------|
| `MONGODB_URI` | MongoDB connection string | Yes |
| `REDIS_HOST` | Redis host | Yes |
| `REDIS_PORT` | Redis port | Yes |
| `JWT_SECRET` | JWT signing secret | Yes |
| `R2_ACCOUNT_ID` | Cloudflare R2 account ID | Yes |
| `R2_ACCESS_KEY_ID` | R2 access key | Yes |
| `R2_SECRET_ACCESS_KEY` | R2 secret key | Yes |
| `R2_BUCKET_NAME` | R2 bucket name | Yes |
| `TRANSCRIPTION_SERVICE_URL` | Whisper service URL | Yes |
| `TTS_SERVICE_URL` | TTS service URL | Optional |
| `TRANSLATION_SERVICE_URL` | Translation service URL | Optional |

### Frontend (.env.local)

| Variable | Description | Required |
|----------|-------------|----------|
| `NEXT_PUBLIC_GRAPHQL_URL` | GraphQL endpoint | Yes |
| `NEXT_PUBLIC_SOCKET_URL` | Socket.io endpoint | Yes |
| `NEXT_PUBLIC_MEDIAMTX_WHIP_URL` | MediaMTX WHIP URL | Yes |
| `NEXT_PUBLIC_GOOGLE_CLIENT_ID` | Google OAuth client ID | Optional |

## Testing

```bash
# Frontend tests
cd frontend
npm test

# Backend tests
cd backend
npm test
```

## Production Deployment

### Frontend (Vercel/Netlify)

1. Connect GitHub repository
2. Set environment variables
3. Deploy automatically on push

### Backend (Railway/Render/AWS)

1. Set up MongoDB Atlas
2. Set up Redis Cloud
3. Configure environment variables
4. Deploy backend service

### AI Services (Docker recommended)

Each service has a Dockerfile for containerized deployment.

```bash
# Build images
docker build -t opus-transcription ./transcription-service
docker build -t opus-tts ./tts-service
docker build -t opus-translation ./translation-service

# Run containers
docker run -p 5002:5002 opus-transcription
docker run -p 5001:5001 opus-tts
docker run -p 5003:5003 opus-translation
```

## Performance Optimization

- **Redis caching** for waveforms and frequently accessed data
- **BullMQ queues** for background job processing
- **Cloudflare R2** for distributed object storage
- **IndexedDB** for client-side chunk storage
- **Progressive chunk upload** during recording

## Troubleshooting

### Common Issues

**WebRTC not connecting:**
- Check MediaMTX is running on port 8889
- Verify firewall allows WebRTC ports
- Check WHIP URL is correct

**Uploads failing:**
- Verify R2 credentials
- Check bucket permissions
- Ensure network connectivity

**MongoDB connection error:**
- Start MongoDB service
- Check connection string
- Verify database exists

**Redis connection error:**
- Start Redis service
- Check Redis is on port 6379
- Verify Redis configuration

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests
5. Submit a pull request

## License

MIT License - see LICENSE file for details

## Support

For issues and questions:
- GitHub Issues: [repository-url]/issues
- Documentation: [docs-url]

## Credits

Built with:
- OpenAI Whisper for transcription
- Coqui TTS for voice generation
- MediaMTX for WebRTC streaming
- Cloudflare R2 for storage
- And many other open-source projects

## Author

**Built by Chikara**

🌐 Portfolio: [https://www.builtbychikara.dev/](https://www.builtbychikara.dev/)

🎥 Demo Video: [https://youtu.be/wJMe9czLsXo](https://youtu.be/wJMe9czLsXo)
