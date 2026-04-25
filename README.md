# ✋ GestureDraw

> A real-time gesture-controlled drawing canvas — draw, erase, zoom, and pan using only your hand in front of a webcam. No mouse. No touch. Just gestures.

![GestureDraw Banner](https://img.shields.io/badge/Built%20With-MediaPipe-blue?style=for-the-badge) ![HTML](https://img.shields.io/badge/HTML-Single%20File-orange?style=for-the-badge) ![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

---

## 🎥 Demo

Open `gesture-draw.html` in Chrome or Edge, allow camera access, and start drawing with your finger.

---

## ✨ Features

- ☝️ **Draw** with just your index finger — point and move
- ✌️ **Erase** with two fingers (index + middle)
- 🖐️🖐️ **Zoom In/Out** using both open palms — spread apart or bring together
- ✊ **Pan the canvas** — make a fist to grab, move your hand, open palm to release
- 🎨 **10 colors** to choose from
- 🖊️ **4 brush sizes**
- 🤲 **Both hands supported** — switch between left and right hand freely
- 🧠 Powered by **MediaPipe Hands** — no model training, no API, runs 100% in browser

---

## 🖐️ Gesture Guide

| Gesture | Hand Shape | Action |
|---|---|---|
| ☝️ Index finger only | One finger pointing up | **Draw** |
| ✌️ Two fingers | Index + middle up, rest curled | **Erase** |
| 🖐️🖐️ Both open palms apart | All 5 fingers spread, both hands moving away | **Zoom In** |
| 🖐️🖐️ Both open palms close | All 5 fingers spread, both hands moving together | **Zoom Out** |
| ✊ Fist | Close all fingers into a fist | **Grab canvas (start pan)** |
| 🖐️ Open palm | Open all fingers while fisting | **Release pan** |

---

## 🚀 Getting Started

### No install needed

1. Download `gesture-draw.html`
2. Open it in **Google Chrome** or **Microsoft Edge**
3. Click **Enable Camera** and allow webcam access
4. Wait ~3 seconds for MediaPipe to load
5. Show your hand and start drawing!

> ⚠️ **Requires Chrome or Edge** — Firefox does not fully support the MediaPipe camera utils used in this project.

---

## 🛠️ How It Works

This is a **single HTML file** with no build step, no dependencies to install, and no backend.

| Technology | Role |
|---|---|
| [MediaPipe Hands](https://google.github.io/mediapipe/solutions/hands) | Real-time 21-point hand landmark detection |
| HTML5 Canvas (Offscreen) | All strokes stored on a 4000×3000 offscreen canvas |
| Vanilla JavaScript | Gesture classification + canvas rendering |
| CSS | UI styling, cursor states, layout |

### Architecture

```
Webcam Feed (640×480)
      ↓
MediaPipe Hands (2 hands, 21 landmarks each, ~30fps)
      ↓
Gesture Classifier (per hand)
   ├── Index only        → Draw on offscreen canvas
   ├── Index + Middle    → Erase on offscreen canvas
   ├── Both open palms   → Zoom (update scale factor)
   └── Fist / Open palm  → Pan (update offset)
      ↓
renderOffscreen() → drawImage(offCanvas, panX, panY, W*zoom, H*zoom)
      ↓
Visible Canvas (browser window)
```

### Why Offscreen Canvas?

Pan and zoom are **instant** because strokes are stored on a large offscreen canvas (`4000×3000px`). The visible canvas simply blits the offscreen canvas with the current pan offset and zoom scale — no re-rendering of strokes needed.

---

## 📁 File Structure

```
gesture-draw/
└── gesture-draw.html      # The entire app — open this in Chrome
└── README.md              # This file
```

---

## 💡 Tips for Best Results

- Use in **good lighting** — MediaPipe works best when your hand is clearly visible
- Keep your hand **40–60cm from the camera**
- **Curl unused fingers fully** when drawing — a half-curled middle finger can confuse draw vs erase
- For zoom, hold **both open palms** facing the camera and move them slowly
- The small **webcam preview** in the bottom-right corner shows your hand landmarks live — use it to check if your hand is being detected

---

## 🔧 Customization

You can easily tweak these constants at the top of the `<script>` tag:

```js
// Colors available in the palette
const COLORS = ['#e8e8f0', '#7c6dfa', '#fa6d8f', ...];

// Brush sizes (in pixels)
const SIZES = [3, 6, 12, 20];

// Offscreen canvas size (drawing area)
const OFF_W = 4000, OFF_H = 3000;
```

---

## 🌐 Deploy for Free

You can host this for free and share it as a link:

### GitHub Pages
1. Create a new GitHub repository
2. Upload `gesture-draw.html` and rename it to `index.html`
3. Go to **Settings → Pages → Source → main branch**
4. Your app is live at `https://yourusername.github.io/repo-name`

### Netlify (drag & drop)
1. Go to [netlify.com](https://netlify.com)
2. Drag your `gesture-draw.html` file onto the deploy area
3. Get a live link instantly

---

## 🤝 Contributing

Pull requests are welcome! Some ideas for contributions:

- [ ] Undo / Redo support
- [ ] Save drawing as PNG
- [ ] More brush shapes (spray, marker, pencil texture)
- [ ] Custom gesture sensitivity settings
- [ ] Mobile support via touch fallback

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

## 🙏 Credits

- [MediaPipe](https://google.github.io/mediapipe/) by Google — hand landmark detection
- Built with ❤️ using vanilla HTML, CSS, and JavaScript — no frameworks needed
