# Where is the Bee?

Arcade-style hidden-object microgame: tap where you think the bee is hiding, get instant feedback, and enjoy juicy win effects (radiant petals, falling tiles, “found it” ring, and celebratory overlays) as you progress through levels.

## How it works
- `index.html` contains all game logic (no build step). Levels are sourced from `bee-locations.json`, mapping image filenames to bee coordinates.
- Level images live in `images/` and are loaded in order by filename (e.g., `level-0.png`, `level-1.png`, …). A downsampled offscreen canvas powers color sampling for immersive effects.
- Win flow: immediate “found it” ring → short pause → scene-colored petal burst → overlapping tile shatter to the next level.
- Miss flow: quick tap circle plus grass-clipping particles sampled from nearby pixels.
- Everything runs client-side; just open `index.html` in a modern browser.

## Adding or editing levels
1. Drop a new scene image into `images/` (match existing dimensions if possible).
2. Add a corresponding entry in `bee-locations.json`:
   ```json
   "level-15.png": { "x": 500, "y": 420 }
   ```
   Coordinates are pixel positions in the source image (not screen space).
3. Load `index.html` in the browser; the new level will appear in sorted order (filenames are sorted by number when present).

## Tweaking effects (quick pointers)
- Marker timing and delays: search for `showFoundMarker` and the hit flow in `handleTap`.
- Petal colors and motion: `playFloralFireworks` controls sampling and animation.
- Tile shatter: `playShatterToNextLevel` governs piece creation, outward drift, and fall curves.
- Miss particles: `spawnGrassClippings` sets speeds, gravity, and lifetimes.

## Running
Open `index.html` directly in a modern desktop or mobile browser. No dependencies or servers required.

## Dedication
For Maeve, 11 months old — with love and wonder. 👶🐝
