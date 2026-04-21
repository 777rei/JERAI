<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  
  <h1>JERAI — AI Bodyweight Fitness App By Rei </h1>
  <p>Version 1.0 </p>

  <h2>Quick Start</h2>
  <ol>
    <li>Upload all files to your web server</li>
    <li>Make sure your server uses <strong>HTTPS</strong></li>
    <li>Open <code>index.html</code> in your browser</li>
    <li>That's it. No installation, no database, no build step.</li>
  </ol>

  <div class="note">
    <strong>HTTPS is required</strong> for camera access. Without HTTPS, the app still works perfectly in manual tap-counting mode.
  </div>

  <h2>File Structure</h2>
  <pre>jerai-fitness-app/
├── index.html          Main HTML file
├── css/
│   └── style.css       All styles
├── js/
│   ├── exercises.js    Exercise database
│   ├── workouts.js     Workout plan definitions
│   └── app.js          Application logic
├── assets/
│   └── favicon.svg     App icon
├── documentation/
│   └── index.html      This file
└── readme.txt          Setup overview</pre>

  <h2>Requirements</h2>
  <table>
    <tr><th>Requirement</th><th>Details</th></tr>
    <tr><td>Browser</td><td>Chrome 90+, Safari 15+, Firefox 90+, Edge 90+</td></tr>
    <tr><td>Server</td><td>Any static file server (Apache, Nginx, Caddy, etc.)</td></tr>
    <tr><td>HTTPS</td><td>Required for camera. Not required for manual mode.</td></tr>
    <tr><td>Backend</td><td>None needed. 100% client-side.</td></tr>
    <tr><td>Database</td><td>None needed. Uses localStorage.</td></tr>
    <tr><td>API Keys</td><td>None needed. MediaPipe loads from public CDN.</td></tr>
  </table>

  <h2>Camera / AI Feature</h2>
  <ul>
    <li>Uses <strong>MediaPipe Pose</strong> for body pose detection</li>
    <li>AI model is loaded from CDN (~10MB on first use, cached after)</li>
    <li>All processing happens <strong>on the user's device</strong></li>
    <li>No video is recorded, uploaded, or transmitted anywhere</li>
    <li>Automatically falls back to manual tap counting if camera unavailable</li>
    <li>Works best with good lighting and full-body visibility</li>
  </ul>

  <div class="warn">
    <strong>Privacy:</strong> The camera feed is processed entirely in the browser. No frames are stored, uploaded, or sent to any server. When the user closes the tab, camera access is fully revoked.
  </div>

  <h2>Customization</h2>

  <h3>Add a New Exercise</h3>
  <p>Edit <code>js/exercises.js</code> and add a new entry following this format:</p>
  <pre>{
  id: 'your-exercise-id',
  name: 'Exercise Name',
  icon: 'fa-icon-name',
  muscle: 'Target Muscles',
  cat: 'upper', // upper, lower, core, cardio
  diff: 'Beginner', // Beginner, Intermediate, Advanced
  cpr: 0.5, // calories per rep
  ai: true, // enable AI counting
  tb: false, // time-based exercise?
  gr: 'linear-gradient(135deg,#1a0f05,#2a1508)',
  ib: 'rgba(255,109,58,.12)',
  ic: '#ff6d3a',
  ins: ['Step 1.', 'Step 2.', 'Step 3.', 'Step 4.'],
  tips: ['Tip 1', 'Tip 2'],
  cnt: { m: 'angle', j: [[11,13,15],[12,14,16]], dTh: 105, uTh: 155, sp: 'up', mn: false }
  // For AI counting, use one of:
  // cnt: { m: 'angle', ... } — joint angle based
  // cnt: { m: 'dist', ... } — distance ratio based
  // cnt: { m: 'ht', ... } — height based
  // cnt: { m: 'time' } — time-based (plank)
}</pre>

  <h3>Add a New Workout Plan</h3>
  <p>Edit <code>js/workouts.js</code> and add a new entry:</p>
  <pre>{
  id: 'your-plan-id',
  name: 'Plan Name',
  desc: 'Short description',
  diff: 'Intermediate',
  dur: 15, // estimated minutes
  color: '#00e676',
  gr: 'linear-gradient(135deg,#0a2018,#0d1a14)',
  icon: 'fa-fire',
  ib: 'rgba(0,230,118,.12)',
  ic: '#00e676',
  ex: [
    { id: 'pushups', r: 15, s: 3, rst: 30 },
    { id: 'squats', r: 20, s: 3, rst: 30, t: false }
  ]
}</pre>

  <h3>Change Colors</h3>
  <p>Edit the CSS variables in <code>css/style.css</code> under <code>:root</code>:</p>
  <pre>:root {
  --accent: #00e676;    /* Main accent color */
  --bg: #08080e;         /* Background */
  --card: #13131f;       /* Card background */
  --border: #252538;     /* Border color */
  /* ... more variables */
}</pre>

  <h2>AI Counting Methods</h2>
  <table>
    <tr><th>Method</th><th>How It Works</th><th>Used For</th></tr>
    <tr><td><code>angle</code></td><td>Tracks joint angle (e.g., elbow or knee). Counts when angle goes below threshold then above threshold.</td><td>Push-ups, Squats, Lunges</td></tr>
    <tr><td><code>dist</code></td><td>Tracks distance ratio between two joints. Counts when distance crosses thresholds.</td><td>Jumping Jacks, Mountain Climbers</td></tr>
    <tr><td><code>ht</code></td><td>Tracks knee height relative to hip. Counts when knee rises above threshold.</td><td>High Knees</td></tr>
    <tr><td><code>time</code></td><td>No rep counting — just a timer. Counts down the target duration.</td><td>Plank, Wall Sit</td></tr>
  </table>

  <h2>MediaPipe Landmark Indices</h2>
  <p>Reference for custom AI counting configurations:</p>
  <table>
    <tr><th>Index</th><th>Landmark</th></tr>
    <tr><td>11</td><td>Left Shoulder</td></tr>
    <tr><td>12</td><td>Right Shoulder</td></tr>
    <tr><td>13</td><td>Left Elbow</td></tr>
    <tr><td>14</td><td>Right Elbow</td></tr>
    <tr><td>15</td><td>Left Wrist</td></tr>
    <tr><td>16</td><td>Right Wrist</td></tr>
    <tr><td>23</td><td>Left Hip</td></tr>
    <tr><td>24</td><td>Right Hip</td></tr>
    <tr><td>25</td><td>Left Knee</td></tr>
    <tr><td>26</td><td>Right Knee</td></tr>
    <tr><td>27</td><td>Left Ankle</td></tr>
    <tr><td>28</td><td>Right Ankle</td></tr>
  </table>

  <h2>Troubleshooting</h2>
  <table>
    <tr><th>Problem</th><th>Solution</th></tr>
    <tr><td>Camera not working</td><td>Ensure HTTPS. Don't use file:// protocol. Use Chrome (not in-app browser).</td></tr>
    <tr><td>AI model slow to load</td><td>First load downloads ~10MB. Subsequent loads use browser cache.</td></tr>
    <tr><td>Pose not detected</td><td>Ensure good lighting and full body visible in frame.</td></tr>
    <tr><td>Reps not counting</td><td>Perform full range of motion. Adjust thresholds in exercises.js if needed.</td></tr>
    <tr><td>Yellow warning appears</td><td>Camera unavailable — app falls back to manual tap counting mode.</td></tr>
    <tr><td>No sound</td><td>Check Profile > Sound Effects is toggled on. Some browsers require user interaction first.</td></tr>
  </table>

  <h2>License</h2>
  <p>Purchased source code may be used for personal and commercial projects. Redistribution of the source code files is not permitted without authorization.</p>

</body>
</html>1. Upload all files to your web server
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
