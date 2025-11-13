<div align="center">

# 🎬 Opus

### Professional Live Streaming & Recording Studio

[![Next.js](https://img.shields.io/badge/Next.js-15-black?style=flat-square&logo=next.js)](https://nextjs.org/)
[![React](https://img.shields.io/badge/React-19-61dafb?style=flat-square&logo=react)](https://reactjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.7-blue?style=flat-square&logo=typescript)](https://www.typescriptlang.org/)
[![GraphQL](https://img.shields.io/badge/GraphQL-API-e10098?style=flat-square&logo=graphql)](https://graphql.org/)
[![WebRTC](https://img.shields.io/badge/WebRTC-Enabled-orange?style=flat-square)](https://webrtc.org/)

**A full-featured video production platform with studio-grade audio processing, multi-track recording, and real-time collaboration.**

[Features](#-features) • [Demo](#-demo) • [Tech Stack](#-tech-stack) • [Getting Started](#-getting-started) • [Architecture](#-architecture)

</div>

---

## 📺 Demo

![Opus Demo](demo.gif)

> A comprehensive video production studio right in your browser

---

## ✨ Features

### 🎙️ Professional Audio Processing
- **Studio-Grade Mixer** - Individual audio controls for each participant/source
- **3-Band Equalizer** - Fine-tune Low (200Hz), Mid (1kHz), and High (3kHz) frequencies
- **Dynamic Compressor** - Threshold, Ratio, Attack, and Release controls with real-time visualization
- **Limiter** - Prevent audio clipping with adjustable threshold
- **Effects Suite** - Reverb and Echo with mix controls
- **Real-time Meters** - Visual feedback with waveform displays that respond to all processing parameters

### 🎥 Video Production
- **Multi-Source Recording** - Record video, audio, screen shares, and webcams independently
- **Multi-Track Timeline** - Professional video editor with separate tracks for each source
- **Live Preview** - Real-time video composition with customizable layouts
- **Screen Sharing** - Share your screen with participants
- **Background Removal** - AI-powered background segmentation for professional look

### 🎬 Studio Features
- **Teleprompter** - Built-in scrolling script editor for hosts
- **Live Chat** - Real-time messaging with participants
- **Emoji Reactions** - Animated floating reactions during sessions
- **Role Management** - Host and guest roles with different permissions
- **Session Controls** - Start/stop recording, manage participants, control layouts

### 🤖 AI Capabilities
- **AI Voice Generation** - 5 free TTS voices powered by Coqui (no API keys needed)
- **Live Transcription** - Real-time speech-to-text
- **Translation Service** - Multi-language support
- **Background Segmentation** - MediaPipe/TensorFlow.js integration

### 🔧 Technical Features
- **WebRTC Streaming** - Low-latency peer-to-peer video/audio
- **RTMP Output** - Stream directly to YouTube, Twitch, etc. via MediaMTX
- **Multi-Track Export** - Export individual tracks or compose final video
- **GraphQL API** - Type-safe, efficient data fetching
- **Real-time Sync** - Socket.io for instant updates
- **Responsive Design** - Works on desktop and tablet devices

---

## 🛠️ Tech Stack

### Frontend
- **Framework:** Next.js 15 (React 19, App Router)
- **Language:** TypeScript 5.7
- **Styling:** TailwindCSS with custom Opus theme
- **Animations:** Framer Motion
- **State Management:** Zustand
- **GraphQL Client:** Apollo Client 4
- **Real-time:** Socket.io Client
- **Video Processing:** FFmpeg.wasm, MediaPipe, TensorFlow.js
- **WebRTC:** SimplePeer

### Backend
- **Runtime:** Node.js + TypeScript
- **Framework:** Express.js
- **API:** Apollo Server 4 (GraphQL)
- **Database:** MongoDB + Mongoose
- **Authentication:** JWT
- **Real-time:** Socket.io
- **File Upload:** Apollo Upload Server

### Microservices
- **TTS Service:** Python Flask + Coqui TTS
- **Transcription Service:** Speech-to-text processing
- **Translation Service:** Multi-language translation
- **Media Processor:** Video/audio processing pipeline
- **AI Service:** ML model inference

### Infrastructure
- **Streaming:** MediaMTX (RTMP/WebRTC gateway)
- **Cache:** Redis (session management)
- **Storage:** File system (with planned S3 integration)

---

## 🚀 Getting Started

### Prerequisites

```bash
Node.js >= 18.0.0
Python >= 3.11
MongoDB
Redis
MediaMTX
```

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/bchikara/opus.git
cd opus
```

2. **Install all dependencies**
```bash
npm run install:all
```

3. **Set up environment variables**

Create `.env` files in `frontend/` and `backend/` directories:

**Frontend (.env.local):**
```env
NEXT_PUBLIC_API_URL=https://localhost:8000
NEXT_PUBLIC_GRAPHQL_URL=https://localhost:8000/graphql
NEXT_PUBLIC_MEDIAMTX_URL=https://localhost:8000/api/mediamtx
NEXT_PUBLIC_MEDIAMTX_ENABLED=true
```

**Backend (.env):**
```env
MONGODB_URI=mongodb://localhost:27017/opus
JWT_SECRET=your-secret-key
REDIS_URL=redis://localhost:6379
PORT=8000
```

4. **Generate SSL certificates** (for HTTPS development)
```bash
./generate-cert.sh
```

5. **Start all services**
```bash
npm run dev
```

This starts:
- 🟣 **Frontend:** https://localhost:3000
- 🔵 **Backend:** https://localhost:8000
- 🟢 **TTS Service:** http://localhost:5001
- 🔴 **MediaMTX:** rtmp://localhost:1935

### Development Commands

```bash
npm run dev              # Run all services
npm run dev:frontend     # Frontend only
npm run dev:backend      # Backend only
npm run dev:tts          # TTS service only
npm run build            # Build all services
npm run start            # Production mode
```

---

## 🏗️ Architecture

```
Opus/
├── frontend/              # Next.js application
│   ├── app/              # App router pages
│   ├── components/       # React components
│   │   └── studio/       # Studio-specific components
│   ├── hooks/            # Custom React hooks
│   ├── lib/              # Utilities and GraphQL
│   └── contexts/         # React contexts
│
├── backend/              # Node.js GraphQL server
│   ├── src/
│   │   ├── models/       # MongoDB schemas
│   │   ├── resolvers/    # GraphQL resolvers
│   │   ├── typeDefs/     # GraphQL schema
│   │   └── services/     # Business logic
│   └── uploads/          # File storage
│
├── tts-service/          # AI voice generation
│   ├── app.py            # Flask server
│   └── models/           # TTS models
│
├── transcription-service/ # Speech-to-text
├── translation-service/   # Multi-language
├── ai-service/           # ML inference
├── media-processor/      # Video/audio processing
│
└── scripts/              # Utility scripts
```

### Key Components

**Studio View (`components/studio/`):**
- `HostView.tsx` - Main studio interface for hosts
- `ExpandableParticipantCard.tsx` - Audio mixer with professional controls
- `VideoPlayer.tsx` - WebRTC video rendering
- `Teleprompter.tsx` - Scrolling script display
- `ChatSidebar.tsx` - Real-time messaging
- `FloatingEmoji.tsx` - Animated reactions

**Editor View (`app/editor/`):**
- `VideoPlayer.tsx` - Playback with timeline sync
- `Timeline.tsx` - Multi-track timeline editor
- `TrackList.tsx` - Source management
- `ExportModal.tsx` - Export configuration

---

## 📖 Usage

### Creating a Session

1. **Start a new project** from the dashboard
2. **Configure session settings** (name, privacy, layout)
3. **Share invite link** with guests
4. **Open studio** and start recording

### Audio Mixing

1. **Click on any participant card** to expand audio controls
2. **Adjust volume, gain, and pan** using the rotary knobs
3. **Enable EQ** and adjust Low/Mid/High frequencies
4. **Add compression** for consistent audio levels
5. **Apply reverb/echo** for creative effects
6. **Monitor levels** in real-time with visual meters

### Recording & Editing

1. **Start recording** from studio controls
2. **Individual tracks** are recorded separately
3. **Open editor** after session ends
4. **Trim, arrange, and compose** your final video
5. **Export** in your preferred format

### AI Voice Generation

1. Click **Create → AI Voice** in any project
2. Enter your script text
3. Select from 5 professional voices
4. Watch progress and get instant results
5. Audio automatically added as a recording track

---

## 🎨 Screenshots

<details>
<summary>View Screenshots</summary>

### Studio Interface
![Studio View](docs/screenshots/studio.png)

### Audio Mixer
![Audio Mixer](docs/screenshots/mixer.png)

### Video Editor
![Video Editor](docs/screenshots/editor.png)

### Teleprompter
![Teleprompter](docs/screenshots/teleprompter.png)

</details>

---

## 🔐 Security

- JWT-based authentication
- HTTPS/WSS for all connections
- Secure WebRTC with STUN/TURN
- Input validation with Zod
- Rate limiting on API endpoints
- CORS configuration
- Session management with Redis

---

## 🗺️ Roadmap

- [ ] Cloud storage (S3/R2) integration
- [ ] Advanced background effects
- [ ] More AI voices and languages
- [ ] Live streaming to multiple platforms
- [ ] Collaborative editing
- [ ] Mobile app (React Native)
- [ ] Video effects and filters
- [ ] Automated highlight generation
- [ ] Analytics dashboard

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- [Coqui TTS](https://github.com/coqui-ai/TTS) - Open source text-to-speech
- [MediaMTX](https://github.com/bluenviron/mediamtx) - RTMP/WebRTC server
- [SimplePeer](https://github.com/feross/simple-peer) - WebRTC wrapper
- [FFmpeg.wasm](https://github.com/ffmpegwasm/ffmpeg.wasm) - Browser video processing
- [MediaPipe](https://mediapipe.dev/) - ML solutions for media

---

<div align="center">

**Built with ❤️ using TypeScript, React, and WebRTC**

[⬆ Back to Top](#-opus)

</div>
