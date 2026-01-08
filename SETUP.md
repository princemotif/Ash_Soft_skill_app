# Quick Setup Guide

## Prerequisites
- Node.js 18+ installed
- npm installed
- Modern browser (Chrome, Edge, or Safari recommended)
- Webcam and microphone access

## Installation Steps

1. **Install Dependencies**
```bash
npm install
```

2. **Environment Variables**
The `.env` file should already be configured with Supabase credentials. If not, copy from `.env.example`:
```bash
cp .env.example .env
```

Then update with your Supabase credentials:
```
VITE_SUPABASE_URL=your_supabase_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
```

3. **Start Development Server**
```bash
npm run dev
```

The app will be available at `http://localhost:5173`

## Demo Accounts

Use these accounts to explore different user roles:

### Student Account
- Email: `student@demo.com`
- Password: `password123`
- Access: Speaking, Writing, Quizzes, Tests, Profile

### Teacher Account
- Email: `teacher@demo.com`
- Password: `password123`
- Access: Monitoring Dashboard, View Submissions, Proctor Logs

### Admin Account
- Email: `admin@demo.com`
- Password: `password123`
- Access: User Management, Quiz Management, Full System Access

## Browser Permissions

When you first use the app, you'll need to grant permissions for:

1. **Microphone** - Required for speaking practice
2. **Camera** - Required for proctoring during tests

These are standard browser prompts. You can manage these permissions in your browser settings.

## Features to Try

### As a Student
1. **Dashboard** - View your progress and stats
2. **Speaking Practice** - Choose a topic and record yourself speaking
3. **Writing Practice** - Select a prompt and write an essay
4. **Quiz** - Take a 10-question grammar quiz
5. **Profile** - View your progress graph and activity timeline

### As a Teacher
1. **Live Monitoring** - See students currently taking tests
2. **Review Submissions** - Check speaking transcripts and essays
3. **Proctor Logs** - View violations and session details

### As an Admin
1. **Student Management** - View all registered students
2. **Activities** - Monitor all submissions
3. **Quiz Questions** - Add or remove quiz questions
4. **Proctor Logs** - Review all proctoring events

## Troubleshooting

### Camera/Microphone Not Working
- Check browser permissions in Settings
- Ensure no other app is using the camera/mic
- Try refreshing the page
- Use Chrome or Edge for best compatibility

### Speech Recognition Not Working
- Only works in Chrome, Edge, and Safari
- Requires HTTPS or localhost
- Check console for errors

### Database Connection Issues
- Verify `.env` file has correct Supabase credentials
- Check Supabase dashboard is accessible
- Ensure RLS policies are properly configured

## Building for Production

```bash
npm run build
```

This creates an optimized build in the `dist/` folder ready for deployment.

## Next Steps

1. Test all features with different user roles
2. Create your own student account via the signup page
3. Explore the proctoring features during tests
4. Review the comprehensive documentation in README.md

Enjoy using LinguaLearn!
