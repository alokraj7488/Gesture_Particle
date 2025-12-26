# Gesture Particles (No Spin)

An interactive, real-time web art installation that transforms your hand gestures into mesmerizing 3D particle sculptures using **MediaPipe Hands** for hand tracking and **Three.js** for GPU-accelerated visuals.

---

## ✨ Features

- **Real-time gesture recognition**: Uses on-device ML to detect 5 distinct hand poses
- **Dynamic particle morphing**: 15,000 particles fluidly transition between geometric and symbolic forms
- **Fully interactive**:
  - Move your hand to rotate the particle field
  - Pinch thumb and index finger to scale up and add color intensity
- **Gesture-to-shape mapping**:
  - ✊ **Fist** → Glowing cube  
  - ✋ **Open palm** → Expanding sphere  
  - ✌️ **Peace sign** → Twisting DNA helix  
  - 🤘 **Rock on** → Animated starburst  
  - 🤟 **"I Love You" sign** → Floating "I Love U" text with a pulsing 3D heart
- **No auto-spin**: Unlike typical demos, rotation is *only* driven by your hand—creating a more intuitive, embodied experience
- **Responsive design**: Works on desktop and mobile (with camera support)

---

## 🛠️ Tech Stack

- **Frontend**: HTML5, JavaScript (ES Modules)
- **3D Engine**: [Three.js](https://threejs.org/) (r160)
- **Hand Tracking**: [MediaPipe Hands](https://developers.google.com/mediapipe/solutions/vision/hand_landmarker) (via `@mediapipe/tasks-vision`)
- **Utilities**: `@mediapipe/camera_utils`, `drawing_utils`
- **Hosting**: Zero dependencies—runs directly from static files

---

## ▶️ How to Use

1. **Launch the demo**:
   - For best results, serve over **HTTPS** (required for camera access)
   - Local development? Use a simple server:
     ```bash
     # Python
     python -m http.server 8000

     # Node.js
     npx serve

     # Live Server (VS Code extension)
     ```
2. Open `index.html` in your browser (Chrome or Edge recommended for best MediaPipe performance)
3. Allow camera permissions when prompted
4. Position your hand in view and try the gestures!

> 💡 **Tip**: Use a well-lit room and keep your hand centered for optimal tracking.

---

## 🎨 Customization

Want to add your own shape?
1. Edit the `Templates` object in the script
2. Define a new function that returns an array of `[x, y, z]` positions (length = `particleCount * 3`)
3. Add gesture logic in `detectGesture()`
4. Assign a color in the animation loop

Example:
Templates.MY_SHAPE = () => {
  const arr = [];
  for (let i = 0; i < particleCount; i++) {
    arr.push(
      Math.sin(i * 0.1) * 20,  // x
      (i / particleCount) * 40 - 20, // y
      Math.cos(i * 0.1) * 20   // z
    );
  }
  return arr;
};

