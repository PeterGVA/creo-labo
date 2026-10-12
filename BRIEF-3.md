# Brief 3: Swiss Machine

Make one self-contained HTML file at the path given. Nothing else.
Vanilla JavaScript only. No libraries, no CDN, no external fonts,
no images, no network, no audio. Everything is drawn from code.

FORMAT
1080x1350 portrait, scaled to fit the window, centered on #000000.
16-second seamless loop at 90 BPM, 4/4: one beat = 2/3 s, one bar = 8/3 s,
16 s = 24 beats = 6 bars. The picture at t=16 equals t=0 (plain white).
Must run smoothly at 60 fps on an iPhone 13 or a Galaxy S24.

THE THREE IDEAS
1. Its own typeface. Draw every letter with Canvas paths from code.
   No system fonts anywhere, not even for small text. Build A-Z, 0-9
   and the signs - / . : from one geometric skeleton system on the grid,
   with two continuous dials: weight (hairline to ultra heavy) and
   width (condensed to extended). Build letters from shared parts so
   any letter can morph into any other.
2. A design machine. Your own seeded random generator (e.g. mulberry32)
   composes a new edition every loop. Timing and the six acts never
   change; words, sizes, crops and placements do. Edition number = seed.
   ?seed=N opens edition N; default is edition 1. N = next edition,
   B = previous edition.
3. A built-in critic. Before an edition plays, code checks it against the
   RULES. If any rule fails, discard it and regenerate with the next
   sub-seed (deterministic). C toggles an overlay of the critic's checklist.

RULES (the critic enforces these)
- Grid: 6 columns x 8 rows, 135 px margins, so every cell is a 135 px
  square. Everything snaps to the grid.
- One typeface: yours. Two weights only, at the extremes: hairline and
  ultra heavy. The weight dial may sweep between them only while moving,
  never rest in the middle.
- Size ladder: cap heights 17, 34, 68, 135, 270, 540, 1080 px only
  (each step x2). Every composition sets at least one size of 540 or more
  against one of 34 or less.
- One axis: all text blocks hang flush-left on one vertical grid line
  chosen per edition. Rag-right, never justified.
- Rules group things: red and black lines, thickness 2, 4, 8, 17 or 34 px,
  separate or anchor groups.
- Edges: nothing touches the margins or corners unless the frame crops it
  on purpose, by at least 25% of its size.
- Colours: white #ffffff, black #111111, red #e30613. Where black and red
  overlap they overprint (multiply), like ink.
- Avoid: cream, italics, gradients, drop shadows, glow, pill shapes,
  01/02/03 labels, plain checkerboards.

WORDS
Each edition uses one German / French / Italian set.
Edition 1 always uses the first set.
PROGRAMM / PROGRAMME / PROGRAMMA
RASTER / TRAME / GRIGLIA
FORM / FORME / FORMA
ZEIT / TEMPS / TEMPO
RHYTHMUS / RYTHME / RITMO
PUNKT / POINT / PUNTO

MUSIC RULES
Every beat has a visible event. Beat 1 of each bar is the biggest.
Moves start slightly before the beat and land exactly on it, except the
very first beat at t=0, which starts from plain white and lands late.
Hard cuts only on a beat. Damped springs computed from t for landings,
eases for exits.

ACTS (one per bar; times in seconds)
1. 0.000-2.667 GRID. On beat 1 the grid draws in. Beats 2-4: cells fill
   by an arithmetic rule chosen by the seed, e.g. filled if
   (a*col + b*row) mod n < k. Visibly ordered, never a plain checkerboard.
2. 2.667-5.333 DIAL. One giant letter from word 1, cropped by the frame.
   Each beat it snaps between the dial extremes: hairline narrow, heavy
   wide, hairline wide, heavy narrow.
3. 5.333-8.000 MORPH. The letters of word 1 morph into each other, one
   per beat, skeleton to skeleton, at size 540 or 1080, with motion blur.
4. 8.000-10.667 DEPTH. The three words on three parallax layers moving at
   different speeds. On beat 3 the type block swings 90 degrees on a hinge
   in fake 3D (your own perspective maths) and locks to the axis.
5. 10.667-13.333 SWARM. Thousands of particles sampled from your own
   letter shapes. Beat 1 they sit as grid dots, beat 2 they swarm into a
   giant letter, beat 3 they burst into grid modules, beat 4 they snap
   back to dots. Run them on the GPU; with no WebGL2, use fewer on canvas.
6. 13.333-16.000 LOCKUP. The edition's final composition, obeying every
   rule: word 1 huge, words 2 and 3 small, red rules, and a caption in
   your own type: EDITION 0001 / 90 BPM / 4/4 / 16 S
   Slow push for three beats; on the last beat everything clears to white.

SURFACE AND DEPTH
- Motion blur: draw fast-moving elements at several sub-moments between
  t - 1/60 and t, layered (deterministic).
- Three depth layers: grid at the back, type in the middle, red elements
  in front. Draw each layer on its own canvas.
- Print finish: upload the layers to a WebGL2 shader that composites
  them, blurs the back layer slightly (depth of field), and adds a
  halftone or line screen and a fine paper grain. If WebGL2 is missing,
  show the clean canvas composite. F toggles the finish on and off.
- Crisp at any devicePixelRatio (capped at 2).

TECHNICAL
Every element is a pure function of t and the edition seed, via global
window.seek(t) and window.edition(n). Drive it with requestAnimationFrame,
t = elapsed seconds mod 16. No CSS transitions, no timers that carry
state, no unseeded Math.random.
Keys: Space pauses; left/right arrows step one beat; D toggles a small
bar.beat overlay; N, B, C and F as above.

SELF-CHECK
Build in stages and keep the file working after each one:
1 typeface, 2 grid and acts on canvas, 3 machine and critic,
4 GPU finish and swarm.
Render frames for editions 1, 2 and 3: t=0, one per act and t=15.99,
with and without the finish. Look at them. Run the critic on editions
1-100 and report how many passed on the first try. Measure the average
time to draw one frame. Check once at an iPhone-sized viewport.
Fix what's wrong, up to two rounds. If something is too ambitious, a
smaller version that fully works beats a big broken one: say what you
cut and why. Say what you checked and what's left.

Comment the code in plain English for a beginner.
