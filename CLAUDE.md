# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Kyudo Simulation (弓道射法模擬) is a web-based Japanese archery (Kyudo) simulator built with vanilla HTML, CSS, and JavaScript. The project simulates the **Hassetsu** (射法八節 - Eight Stages of Shooting) process with real-time physics and visual feedback.

**Key Characteristics:**
- Pure client-side web application (no build tools, no dependencies)
- Two main files: `index.html` (main simulator) and `animation_prototype.html` (vector animation prototype)
- Bilingual interface (Traditional Chinese with Japanese terminology)

## Architecture

### Core Components

**1. SVG Animation Engine (`SvgArcherEngine`)**
- Located in: `index.html:662-816`
- Manages the eight-stage (Hassetsu) shooting form animation cycle
- Uses keyframe-based pose interpolation with 8 predefined poses
- Controls: arm rotations (la, lf, ra, rf), bow tilt (bt), bow bend (bb), head position (hx)
- Kinematics system calculates bow string and arrow positions from bone transformations
- States: INIT → ANIMATING → KAI (ready to shoot) → ZANSHIN

**2. Physics Simulation**
- Located in: `index.html:818-1001`
- Constants: `PX_TO_CM = 2.5`, `DIST_M = 28`, `G = 9.81`
- Energy formula: `e = 0.5 * f * 0.85 * 0.75` (bow force × efficiency factors)
- Arrow trajectory uses parabolic motion with drop calculation
- Breathing/tremor effects: sine-wave breathing + jitter + cumulative noise

**3. Replay System**
- Two modes:
  - **Target Face View**: Circular zoom for hits within 18cm (scaled 3.5x)
  - **Hawk-Eye View**: Rectangular side-view for misses within 5m (0.4 scale)
- Canvas coordinates: `x * 2` for face view, `x * 0.4` for hawk-eye
- Impact visualization uses separate static dots + animated pulse effects

**4. Sound Engine (`SoundEngine`)**
- Located in: `index.html:660`
- Web Audio API synthesis (no external audio files)
- Hit sound: white noise burst + triangle wave oscillator
- Auto-resume for mobile browser audio policy compliance

### SVG Mannequin Rig (ANKF Standard Style)

**Hierarchy:**
```
archer-rig (translate)
├── legs (static: hakama + tabi)
├── torso-bones (translate)
│   ├── head-grp (translate, animated hx offset)
│   ├── arm-l-grp (rotate la)
│   │   └── fore-l-grp (rotate lf)
│   │       └── bow-grp (rotate bt, contains bow path)
│   ├── arm-r-grp (rotate ra)
│   │   └── fore-r-grp (rotate rf, yugake/glove)
│   └── dynamic-visuals (string + arrow line)
```

**Critical Transform Chain:**
- Shoulder pivots: Left (18, -68), Right (-18, -68) relative to torso
- Bone lengths: Upper arm = 32px, Forearm = 29px
- Bow tips: Top (-130), Bottom (80) relative to bow-grp
- String attachment requires forward kinematics from all transforms

## Common Development Tasks

### Running the Application
```bash
# No build step required - open directly in browser
open index.html
# Or use any local web server:
python3 -m http.server 8000
# Navigate to http://localhost:8000
```

### Testing Physics Changes
- Modify constants at `index.html:819` (PX_TO_CM, DIST_M, G)
- Energy calculation at `index.html:887`
- Trajectory calculation at `index.html:888-893`

### Modifying Animation Poses
- Edit pose array at `index.html:664-687`
- Each pose: `{ la, lf, ra, rf, bt, bb, hx }`
- Angles in degrees (negative = counterclockwise from vertical)
- ANKF standard angles are documented in comments

### Adjusting Visual Feedback
- Replay thresholds: Hit (<18cm), Close Miss (≤500cm) at `index.html:919-937`
- Zoom scale factors: Face view (3.5x at line 536), Hawk-eye (0.4x at line 971)
- Impact animation: `.impact-pulse` keyframes at `index.html:337-360`

### Coordinate Systems
- **Main SVG viewBox**: 0,0 to 1200,800 (sky at 0-380, ground at 380-800)
- **Archer rig base**: (300, 402) before adjustments
- **Target center**: (600, 380)
- **Zoom SVG viewBox**: 400x300 for replay windows
- **Physics space**: Centimeters (convert via PX_TO_CM)

## Code Style & Conventions

- **Variable naming**:
  - SVG elements: descriptive (`arm-l-grp`, `fore-r-grp`)
  - Physics: abbreviated (`s.pow` = power, `s.wgt` = weight, `s.ax/ay` = aim offsets)
  - DOM refs: `el.{component}` object structure
- **State management**: Global state object `s` (line 820)
- **Control flow**: Requestanimationframe loops (no intervals)
- **Transforms**: SVG `transform` attributes (not CSS transforms on SVG elements)

## Known Technical Details

### String/Arrow Kinematics
The bow string connects three points (top tip, draw hand, bottom tip). Calculation requires:
1. Forward kinematics to find left hand position (shoulder → elbow → wrist → hand)
2. Right hand position (draw hand)
3. Bow angle accumulation: `la + lf + bt`
4. Rotation matrix application to bow tip offsets (±130/80px)
5. Path generation: `M${topX},${topY} L${rightHandX},${rightHandY} L${bottomX},${bottomY}`

See implementation at `index.html:726-788`

### Breathing/Tremor System
Three-layer sway simulation:
1. **Breath**: `Math.sin(t * 0.5) * (s.br * 1.5)` - slow vertical oscillation
2. **Jitter**: `(Math.random() - 0.5) * tremorMag` - frame-by-frame noise
3. **Cumulative noise**: Brownian-motion style drift with 0.98 decay

Applied only during aiming state (`s.aiming === true`)

### Animation Timing
- Pose interpolation: `progress += 0.015` per frame (~60fps = 1.11s per stage)
- Arrow flight: `p += 0.15` per frame (~0.44s flight time)
- Kai (会) breathing: `Math.sin(Date.now() / 400) * 2` for idle sway

## Browser Compatibility

- Modern browsers (ES6+, SVG 1.1, Web Audio API)
- Touch/pointer events for mobile support
- Responsive layout with `@media (max-width: 768px)` breakpoint
- Audio context requires user interaction (handled by `SoundEngine.resume()`)
