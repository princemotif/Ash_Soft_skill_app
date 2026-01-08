# LinguaLearn - English Learning Platform

A comprehensive full-stack English learning web application with real-time proctoring, speech recognition, and advanced assessment features.

## Overview

LinguaLearn is a complete English learning platform designed for students, teachers, and administrators. It provides interactive speaking practice, writing assessments, grammar quizzes, and comprehensive testing with built-in proctoring capabilities.

## Features

### Core Learning Modules

#### 1. Speaking Practice
- Multiple difficulty-level topics (beginner, intermediate, advanced)
- Real-time speech-to-text transcription using Web Speech API
- Live word count and transcript display
- Grammar and fluency analysis
- Automated feedback and mistake detection
- Audio recording with MediaRecorder API
- 2-minute timed sessions

#### 2. Writing Practice
- Curated writing prompts by difficulty level
- Real-time word count tracking
- Grammar correction and analysis
- Vocabulary and coherence scoring
- Detailed feedback on writing quality
- Minimum word count recommendations

#### 3. Grammar Quizzes
- 10-question multiple-choice assessments
- Randomized question selection
- 10-minute timer with auto-submit
- Progress tracking with question navigator
- Instant scoring and detailed explanations
- Answer review with correct/incorrect highlighting

#### 4. Full Tests
- Comprehensive assessment combining all modules
- Integrated proctoring system
- Timed sections
- Overall score calculation
- Complete test history tracking

### User Roles

#### Students
- Access to all learning modules
- Personal dashboard with statistics
- Progress tracking and history
- Profile with performance graphs
- Activity timeline
- Score analytics

#### Teachers
- Real-time monitoring dashboard
- Live session tracking with heartbeat monitoring
- View active students and their progress
- Review submissions (speaking transcripts, essays, quiz scores)
- Access to proctoring logs and violations
- Recent submissions overview

#### Admins
- Complete system management
- Student management and viewing
- Activity monitoring across all users
- Quiz question management (add/remove)
- Proctoring log review
- System-wide analytics

### Proctoring System

#### Real-time Monitoring
- Webcam feed in corner display
- Face presence detection
- 5-second snapshot intervals
- Active session heartbeat tracking
- Live session status updates

#### Violation Detection
- Tab switch detection and logging
- Face not detected warnings
- Multiple faces detection
- Timestamp recording for all events
- Real-time alerts to students

#### Teacher Monitoring
- Live view of active test sessions
- Per-student violation logs
- Session duration tracking
- Snapshot review capability
- Event timeline per attempt

## Tech Stack

### Frontend
- **React 18** - UI framework
- **Vite** - Build tool and dev server
- **TypeScript** - Type safety
- **TailwindCSS** - Styling
- **React Router** - Client-side routing
- **Recharts** - Data visualization
- **Lucide React** - Icon library

### Backend & Database
- **Supabase** - PostgreSQL database
- **Row Level Security (RLS)** - Database security
- **Real-time subscriptions** - Live updates

### APIs & Browser Features
- **Web Speech API** - Speech recognition
- **MediaRecorder API** - Audio recording
- **WebRTC** - Webcam access
- **Visibility API** - Tab switch detection

## Project Structure

```
lingualearn/
├── src/
│   ├── components/          # Reusable components
│   │   ├── Navbar.tsx
│   │   ├── ProtectedRoute.tsx
│   │   └── ProctoringMonitor.tsx
│   ├── contexts/           # React contexts
│   │   └── AuthContext.tsx
│   ├── lib/               # Utilities and configs
│   │   ├── supabase.ts
│   │   └── auth.ts
│   ├── pages/             # Main application pages
│   │   ├── Login.tsx
│   │   ├── Signup.tsx
│   │   ├── Dashboard.tsx
│   │   ├── Speaking.tsx
│   │   ├── Writing.tsx
│   │   ├── Quiz.tsx
│   │   ├── Test.tsx
│   │   ├── Profile.tsx
│   │   ├── Admin.tsx
│   │   └── Teacher.tsx
│   ├── App.tsx            # Main app with routing
│   ├── main.tsx           # App entry point
│   └── index.css          # Global styles
├── public/                # Static assets
├── supabase/             # Database migrations
└── package.json          # Dependencies
```

## Database Schema

### Tables

1. **users** - User authentication and profiles
2. **speaking_topics** - Speaking practice topics
3. **speaking_attempts** - Student speaking submissions
4. **writing_prompts** - Writing practice prompts
5. **writing_attempts** - Student writing submissions
6. **quiz_questions** - Quiz question bank
7. **quiz_attempts** - Quiz submissions and scores
8. **test_attempts** - Full test submissions
9. **proctoring_logs** - Proctoring events and violations
10. **live_sessions** - Active session tracking

### Security
- Row Level Security (RLS) enabled on all tables
- Students can only view/modify their own data
- Teachers can view all student data (read-only)
- Admins have full access to all data

## Setup Instructions

### Prerequisites
- Node.js 18+ and npm
- Modern web browser with webcam and microphone
- Supabase account (provided)

### Installation

1. **Clone and install dependencies:**
```bash
npm install
```

2. **Environment Variables:**
The `.env` file should already contain:
```env
VITE_SUPABASE_URL=your_supabase_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
```

3. **Start Development Server:**
```bash
npm run dev
```

The application will open at `http://localhost:5173`

### Demo Accounts

Three demo accounts are pre-configured:

- **Student:** student@demo.com / password123
- **Teacher:** teacher@demo.com / password123
- **Admin:** admin@demo.com / password123

## How Proctoring Works

### Architecture

1. **Session Initiation**
   - When a proctored activity starts, webcam access is requested
   - A live session record is created in the database
   - ProctoringMonitor component mounts and starts tracking

2. **Real-time Monitoring**
   - Webcam feed displays in top-right corner
   - Snapshots captured every 5 seconds
   - Heartbeat sent every 3 seconds to update session status
   - Tab visibility changes are immediately detected

3. **Violation Logging**
   - All events logged to `proctoring_logs` table
   - Event types: tab_switch, face_not_detected, started, completed, heartbeat
   - Timestamps and event data stored for review
   - Student receives real-time warnings

4. **Teacher View**
   - Teachers see all active sessions in real-time
   - Session list updates every 3 seconds
   - Click any session to view detailed logs
   - Review violations and timestamps

5. **Session Cleanup**
   - On component unmount, session marked inactive
   - Final "completed" event logged
   - Camera stream stopped and released

### Privacy & Security
- Camera feed never leaves the student's browser
- Only metadata and event logs stored in database
- Students fully aware of monitoring (visible camera feed)
- All proctoring data secured with RLS policies

## Features in Detail

### Speech Recognition
- Uses browser's built-in Web Speech API
- Continuous recognition with interim results
- Real-time transcript updates
- Supports 120-second recording sessions

### Grammar Analysis
- Pattern-based error detection
- Common mistake identification
- Automated feedback generation
- Correction suggestions

### Scoring System
- Speaking: Grammar (50%) + Fluency (50%)
- Writing: Grammar (33%) + Vocabulary (33%) + Coherence (33%)
- Quiz: Percentage of correct answers
- All scores normalized to 0-100 scale

### Progress Tracking
- Activity timeline with all attempts
- Performance graphs using Recharts
- Average score calculations
- Per-module statistics

## Building for Production

```bash
npm run build
```

This creates an optimized production build in the `dist/` folder.

### Deployment Options

1. **Vercel/Netlify** (Recommended)
   - Connect your Git repository
   - Set environment variables in platform dashboard
   - Auto-deploys on git push

2. **Traditional Hosting**
   - Upload `dist/` folder contents
   - Configure environment variables on server
   - Ensure SPA routing works (redirect all to index.html)

### Environment Variables for Production
Ensure these are set in your hosting platform:
- `VITE_SUPABASE_URL`
- `VITE_SUPABASE_ANON_KEY`

## Browser Compatibility

### Required Features
- Web Speech API (Chrome, Edge, Safari)
- MediaRecorder API (All modern browsers)
- getUserMedia (WebRTC) (All modern browsers)
- Visibility API (All modern browsers)

### Recommended Browsers
- Chrome 80+
- Edge 80+
- Safari 14+
- Firefox 90+ (limited speech recognition)

## Known Limitations

1. **Speech Recognition**
   - Best supported in Chrome/Edge
   - Firefox has limited support
   - Requires stable internet connection

2. **Proctoring**
   - Requires camera/microphone permissions
   - Face detection is basic (presence check only)
   - Cannot prevent screenshot tools

3. **Mobile Support**
   - Interface is responsive
   - Camera features may vary by device
   - Speech recognition less reliable on mobile

## Development Notes

### Running Tests
```bash
npm run typecheck
```

### Linting
```bash
npm run lint
```

### Code Organization
- Each page is self-contained
- Components are reusable across modules
- Contexts manage global state
- Database queries use Supabase client

## Troubleshooting

### Camera Not Working
- Ensure browser has camera permissions
- Check if camera is already in use
- Try refreshing the page

### Speech Recognition Not Starting
- Only works in HTTPS or localhost
- Check browser console for errors
- Verify microphone permissions

### Authentication Issues
- Clear browser localStorage
- Check Supabase connection
- Verify environment variables

## Future Enhancements

- AI-powered feedback using GPT models
- Advanced face recognition with ML
- Voice analysis for pronunciation
- Peer review system
- Certificate generation
- Email notifications
- Mobile apps (React Native)
- Offline mode support

## License

This project is for educational purposes.

## Support

For issues or questions, please check:
1. Browser console for errors
2. Network tab for API failures
3. Supabase dashboard for database issues

---

Built with React, TypeScript, Vite, and Supabase
