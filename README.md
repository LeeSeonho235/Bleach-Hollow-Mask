# Face Tracking AR Mask

Real-time AR web app that overlays a mask on your face using webcam input. Hand gesture controls activate and deactivate the effect — swipe down over your face to apply, swipe up to remove. Built entirely in the browser with MediaPipe.

## Demo

https://github.com/user-attachments/assets/d7b1f5c3-9b8e-45d4-95b7-435a4662934d


## How It Works

The app runs two MediaPipe models simultaneously in the browser:

- **Face Mesh** — tracks 468+ facial landmarks in real time to position and scale the mask
- **Hands** — tracks the index finger to detect vertical swipe gestures over the face area

The mask aligns to both eyes using landmark points 468 and 473 (iris centers), and scales proportionally based on the distance between them. A video overlay effect is composited using Canvas `screen` blend mode to simulate an energy aura.

## Gesture Detection

The gesture system uses a simple state machine:

```
idle → swipe_down_start → mask ON  (hand above face → swipes down past face)
idle → swipe_up_start   → mask OFF (hand below face → swipes up past face)
```

- Only triggers when the hand is within the face's horizontal bounds
- Requires a minimum vertical movement of 0.25 (normalized coordinates)
- 1-second cooldown prevents duplicate triggers

## Tech Stack

- **Face Tracking:** MediaPipe Face Mesh (468 landmarks, iris refinement)
- **Hand Tracking:** MediaPipe Hands (21 landmarks per hand)
- **Rendering:** Canvas 2D API with composite blending
- **Video Effect:** Screen blend mode for transparent overlay
- **Frontend:** Single HTML file, no build tools, no frameworks

## Running Locally

Open `index.html` in Chrome or Edge and allow camera access. No server or installation needed.

## Things I Learned Building This

- Running multiple MediaPipe models (Face Mesh + Hands) simultaneously in the browser
- Aligning 2D overlays to 3D face landmarks with proper scaling and positioning
- Implementing a state machine for gesture detection with cooldown logic
- Using Canvas composite operations (`screen` blend mode) to make black-background videos appear transparent
- The demo video matters as much as the code — I used Canva to create a polished walkthrough since a static screenshot can't show real-time AR properly

## License

MIT
