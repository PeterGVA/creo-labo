# Swiss Grid in Motion: team spec

Lead spec for the team build. Every number here is binding. If something is
not covered, choose the simplest option and leave a `// NOTE:` comment.
Read `BRIEF.md` (repo root) first; this spec makes it exact.

Final file: `pieces/swiss-grid/team/index.html`, one self-contained file.
No libraries, CDN, external fonts, images or network. No `Math.random`,
no `Date`, no `setTimeout`/`setInterval`, no CSS transitions or animations.
Comments in plain English for a beginner.

## 1. Rendering model

- One `<canvas>`. All drawing is in **design units**: a 1080 x 1350 frame,
  origin top-left, y grows downward.
- The canvas is scaled to fit the window, centered (letterboxed). Page
  background around the frame: `#ffffff`. Sharp on hi-DPI: backing store =
  `round(1080*s*dpr)` x `round(1350*s*dpr)`, CSS size `1080*s` x `1350*s`,
  where `s = min(innerWidth/1080, innerHeight/1350)`, `dpr = devicePixelRatio || 1`.
- `render(t)` redraws everything from scratch for time t. Nothing is
  remembered between frames.

## 2. Shared namespace (written by Part 1, used by Parts 2–4)

Part 1 creates `window.SG` with exactly these members:

```
SG.W = 1080, SG.H = 1350, SG.LOOP = 6
SG.GROUND = "#ffffff", SG.INK = "#111111", SG.ACCENT = "#e30613"
SG.FONT_FAMILY = "Helvetica, Arial, sans-serif"
SG.MARGIN = 90, SG.GUTTER = 24, SG.COL_W = 130
SG.colX(i)        // left edge of column i (1..6) = 90 + (i-1)*154
                  //   -> 90, 244, 398, 552, 706, 860 ; right edge of col 6 = 990
SG.clamp(x, a, b)
SG.lerp(a, b, u)
SG.easeOutCubic(u)   // 1 - (1-u)^3,   u clamped to [0,1]
SG.easeInCubic(u)    // u^3,           u clamped to [0,1]
SG.easeInQuad(u)     // u^2,           u clamped to [0,1]
SG.springDecay(tau, omega, zeta)
    // tau <= 0 -> 1.  Otherwise (underdamped, zeta < 1):
    //   wd = omega*sqrt(1-zeta^2)
    //   exp(-zeta*omega*tau) * (cos(wd*tau) + (zeta*omega/wd)*sin(wd*tau))
    // Goes 1 -> 0 with overshoot, zero starting velocity.
SG.spring(t, start, from, to, omega, zeta)
    // t < start -> from ; else to + (from - to) * springDecay(t - start, omega, zeta)
SG.exit(t, start, dur, dist)
    // 0 before start; dist * easeInCubic((t - start)/dur) after (holds at dist)
SG.layers = []       // parts push { name, z, draw(ctx, t) }
```

Layer contract: `draw(ctx, t)` receives a context already in design units
and already rotated (beat 5). It must wrap its work in `ctx.save()` /
`ctx.restore()`, set its own fill/stroke/font/alpha, and depend only on `t`.
Layers are drawn in ascending `z`.

## 3. Grid and type

- Margins 90 left and right; 6 columns of 130 with 24 gutters (see colX).
- Type: `bold <size>px Helvetica, Arial, sans-serif`, `textBaseline = "alphabetic"`,
  `textAlign = "left"`, fill `#111111`. Upper case. Never italic.
- Letter x positions (for per-letter drawing): `x_k = 90 + measure(word.slice(0,k)) + k*track`,
  with `track = -0.02 * size`. Lead review fix: add the first letter's
  `actualBoundingBoxLeft` to the 90 so the ink, not the glyph origin, sits on
  the column line (optical flush-left). Words are drawn letter by letter with this rule
  even when they move as one, so tracking is identical everywhere.

| Word   | Size | x  | Landed baseline (beat 2–3) | Final baseline (beat 4–5) |
|--------|------|----|----------------------------|---------------------------|
| GRID   | 340  | 90 | 760                        | 460                       |
| RHYTHM | 190  | 90 | –                          | 680                       |
| TIME   | 190  | 90 | –                          | 860                       |

- Red circle: radius 65 (diameter = one column), fill `#e30613`.
  Rests on the baseline line y = 1170, so center y = 1105.
  Rolling marker: a white (`#ffffff`) dot radius 11 at distance 38 from the
  center, angle = `(cx - cx0) / 65` radians (clockwise as it moves right),
  starting straight up (`-PI/2`).
- Column lines: 12 lines, at the left and right edge of each column
  (x = colX(i) and colX(i)+130). Stroke `#111111`, `globalAlpha 0.14`,
  `lineWidth 2`. Full length spans y = -300 to y = 1650 (longer than the
  frame so they still cover it during the 45° rotation).

## 4. Timeline (t in seconds, 0 <= t < 6)

### Beat 1 — 0.0–0.4 lines draw down (Part 1)
Line index j = 0..11 (left to right). `p = easeOutCubic((t - 0.01*j) / 0.28)`.
Draw from y = -300 to y = -300 + 1950*p. Nothing drawn while p = 0.

### Beat 2 — 0.4–1.6 GRID drops in, letter by letter (Part 2)
Letter k = 0..3 (G, R, I, D). `start_k = 0.40 + 0.18*k`.
Drop offset `dy_k = SG.spring(t, start_k, -1000, 0, 16, 0.5)`.
Do not draw letter k while `t < start_k`.

### Beat 3 — 1.6–2.6 red circle rolls in (Part 3)
`cx = SG.spring(t, 1.6, -80, 771, 9, 0.55)` (771 = center of column 5:
colX(5) + 65). cx0 = -80. Before 1.6 the circle sits at -80 (off frame).

### Beat 4 — 2.6–3.8 GRID up, RHYTHM and TIME stack in (Parts 2 and 4)
- GRID baseline `yG(t) = SG.spring(t, 2.6, 760, 460, 12, 0.6)` (Part 2).
  GRID letter k is drawn at baseline `yG(t) + dy_k(t) + exitGRID(t)`.
- RHYTHM (Part 4): baseline `680 + SG.spring(t, 2.80, 700, 0, 13, 0.6)`.
  Hidden while t < 2.80.
- TIME (Part 4): baseline `860 + SG.spring(t, 3.00, 700, 0, 13, 0.6)`.
  Hidden while t < 3.00.

### Beat 5 — 3.8–5.0 snap to 45° and back (Part 1, global)
Rotation θ (degrees, positive = clockwise) about the frame center (540, 675),
applied to every layer, lines included:
- t < 3.8: θ = 0
- 3.8 <= t < 4.4: `θa(t) = 45 * (1 - SG.springDecay(t - 3.8, 20, 0.55))`
- t >= 4.4 (until 6): `θ = θa(4.4) * SG.springDecay(t - 4.4, 20, 0.55)`
  (starts exactly where θa ended, so no jump; ≈ 0 well before 5.0.)

### Beat 6 — 5.0–6.0 exits up, lines fade (all parts)
Each element gets `SG.exit(t, start, 0.55, -1500)` added to its y:

| Element | start | Part |
|---------|-------|------|
| GRID    | 5.00  | 2    |
| RHYTHM  | 5.08  | 4    |
| TIME    | 5.16  | 4    |
| circle  | 5.24  | 3    |

Lines (Part 1) do not move; their alpha is multiplied by
`1 - SG.easeInQuad((t - 5.2) / 0.7)` → fully gone at 5.9.
From 5.9 to 6.0 the frame is plain white, identical to t = 0. Loop closes.

## 5. Clock, seek and keys (Part 1)

- `window.seek(t)`: `t = ((t % 6) + 6) % 6`, store it as the current time,
  call `render(t)` immediately. Does not change play/pause state; if playing,
  playback continues from t.
- `requestAnimationFrame` loop: when playing, `t = (now/1000 - offset) mod 6`
  where `offset` is set so playback continues from the current time after
  pause/seek/step. Then `render(t)`.
- Space: toggle pause (preventDefault). ArrowRight / ArrowLeft: pause, then
  step ±1/30 s via `seek`. 
- On window resize: recompute scale, re-render current t.
- Expose `window.SG.render` and `window.SG.isPaused()` for testing.

## 6. Parts and file format

| Part | File (in `team/parts/`) | Beats | Contents |
|------|-------------------------|-------|----------|
| 1 | `p1-core.html` | 1, 5, 6 (lines + rotation) | Full HTML page, `SG`, helpers, scaling, clock, seek, keys, column-lines layer (z 0), rotation |
| 2 | `p2-grid.js`   | 2, 4 (GRID), 6 (GRID) | GRID layer (z 10) |
| 3 | `p3-circle.js` | 3, 6 (circle) | Circle layer (z 20) |
| 4 | `p4-words.js`  | 4 (RHYTHM, TIME), 6 (their exits) | RHYTHM + TIME layer (z 10) |

- `p1-core.html` contains, in this order inside `<body>`: the canvas, a
  `<script>` that defines `SG` and the column-lines layer, then the exact
  line `<!-- PARTS -->`, then a `<script>` that starts the clock (first
  render + rAF). The assembler replaces `<!-- PARTS -->` with three
  `<script>` blocks holding p2, p3, p4.
- `p2`–`p4` are plain JS (no `<script>` tags), wrapped in an IIFE
  `(function () { ... })();`, using only `SG` members listed above, ending
  with `SG.layers.push({ name, z, draw })`.
- Measure text once per draw after setting `ctx.font` (cheap; no caching
  needed). Never read the canvas or keep state between draws.

## 7. Acceptance checks (assembler)

1. Page loads with no console errors; only one file, no external URLs.
2. `seek(0)` and `seek(5.95)` give identical pixels (all white).
   `seek(6)` equals `seek(0)`.
3. Spot frames: 0.2 (lines half drawn), 1.0 (some GRID letters), 2.2
   (circle rolling), 3.5 (three words), 4.1 (rotated ~45°), 5.3 (exiting).
4. `seek(t)` twice with the same t gives identical pixels (pure function).
5. Space pauses; arrows step one frame.
