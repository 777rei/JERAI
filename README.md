# JERAI
AI FITNESS APP
JERAI AI Bodyweight Fitness App
Version 1.0
Created By Rei 
OVERVIEW
#JERAI is a complete bodyweight fitness web application with AI-powered 
automatic rep counting using your phone camera and MediaPipe Pose detection.

#FEATURES
- AI automatic rep counting (camera-based)
- Manual tap counting fallback
- 24 bodyweight exercises across 4 categories
- 8 workout plans (Beginner to Advanced)
- Time-based exercises (Plank, Wall Sit, Side Plank)
- Sound effects and haptic feedback
- Rest timer between sets with countdown
- Workout summary with stats
- Workout history and streak tracking
- Dark theme, mobile-first responsive design
- 100% client-side no backend required
- Works offline after first load

#SETUP
1. Upload all files to your web server
2. Ensure HTTPS is enabled (required for camera)
3. Open index.html in a modern browser
4. Done. No build step, no npm install, no database.

#REQUIREMENTS
- Modern browser (Chrome 90+, Safari 15+, Firefox 90+, Edge 90+)
- HTTPS enabled (for camera access)
- No server-side requirements
- No API keys needed

#CUSTOMIZATION
- Add exercises: Edit js/exercises.js — follow the existing format
- Modify plans: Edit js/workouts.js — follow the existing format
- Change colors: Edit CSS variables in css/style.css (:root section)
- Change app name: Edit index.html <title> and splash screen text

#CAMERA FEATURE NOTES
- Camera uses MediaPipe Pose (loaded from CDN)
- First load downloads ~10MB AI model (cached after that)
- Falls back to manual tap counting if camera unavailable
- Works best with good lighting and full-body visibility
- Camera feed is processed entirely on-device — nothing is uploaded

#BROWSER SUPPORT
- Chrome 90+ (recommended for best AI performance)
- Safari 15+ 
- Firefox 90+
- Edge 90+

#LICENSE
This code is sold as-is. You may use it for personal and commercial projects.
Redistribution of the source code is not permitted without authorization.

SUPPORT
For issues, please contact me
