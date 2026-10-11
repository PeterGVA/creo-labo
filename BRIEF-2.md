# Brief 2: Swiss Hero Spot

Make one self-contained HTML file at the path given. Nothing else.
No libraries, no CDN, no external fonts, no images, no network.

FORMAT
1080x1350 portrait, scaled to fit the window, centered on #000000.
16-second seamless loop: the picture at t=16 equals t=0.
Synced to an imaginary track at 90 BPM, 4/4.
One beat = 2/3 s. One bar = 8/3 s (2.667 s). 16 s = 24 beats = 6 bars.
This is a 16-second hero spot: bold, fast, confident, made to stop a scroll.

STYLE
A distinctive blend of the International Typographic Style masters:
- Gerstner: the grid is a system that generates the images.
- Müller-Brockmann: concentric circles and arcs moving like music.
- Hofmann: extreme black/white contrast, huge letters cropped by the frame.
- Ruder: type as rhythm and texture, bold asymmetric white space.
- Vignelli: thick red rules, heavy weights, few sizes used with discipline.
- Bill and Lohse: mathematical colour sequences in square modules.
Grid: 6 columns x 8 rows, 60 px margins. Everything snaps to it.
Type: "Helvetica Neue", Helvetica, Arial, sans-serif. Bold and regular only.
Core colours: white #ffffff, black #111111, red #e30613.
Act 5 only adds this serial sequence, in this order:
#e30613 #ff6a00 #ffd200 #00a651 #0057b8 #5b2c86
Avoid: cream backgrounds, italic accent words, 01/02/03 labels,
monospace, pill shapes, gradients, drop shadows, glow.

MUSIC RULES
Every beat has a visible event. Beat 1 of each bar is the biggest.
Moves start slightly before the beat and land exactly on it.
Hard cuts are allowed, but only on a beat.
Damped springs (computed from time) for landings, eases for exits.
Act 5 also moves on half-beats.

ACTS (one per bar; times in seconds)
1. 0.000–2.667  GRID. White. On beat 1 the 6x8 grid lines draw in fast.
   On beats 2, 3, 4 black modules fill grid cells following a visible
   rule (a Gerstner-style permutation), not random.
2. 2.667–5.333  CIRCLES. Concentric arcs grow from the bottom-left corner,
   one new ring per beat, alternating black and white, cropped by the frame.
   On beat 4 one ring turns red.
3. 5.333–8.000  CONTRAST. Hard cut to a black field. One giant white letter
   per beat (R, T, G, then a tiny red square), each cropped by the frame
   edges, each a different extreme scale.
4. 8.000–10.667  RHYTHM. White. RASTER, TRAME, GRIGLIA set as a typographic
   texture: repeated lines in two sizes, flush left, asymmetric.
   A thick red rule sweeps across on beat 1. On beat 3 the whole text block
   rotates 90 degrees and locks to the grid.
5. 10.667–13.333  SERIES. A square of 4x4 modules. The six colours step
   through the modules on every half-beat in a strict rotating sequence.
   On beat 3 the square rotates 45 degrees; on beat 4 it snaps back.
6. 13.333–16.000  LOCKUP. Final composition on white: RASTER huge in black,
   TRAME and GRIGLIA smaller, one red rule, one red circle, all on the grid.
   Small caption flush left: 90 BPM — 4/4 — 16 s. It holds with a slow push
   for three beats. On the last beat everything clears so t=16 equals t=0
   (plain white).

TECHNICAL
Every element is a pure function of t via a global window.seek(t).
Drive it with requestAnimationFrame, t = elapsed seconds mod 16.
No CSS transitions, no timers that carry state, no unseeded Math.random.
Must run smoothly on a phone.
Keys: Space pauses; left/right arrows step one beat; M toggles a
synthesized metronome (Web Audio, louder click on beat 1 of each bar,
starts in sync with t); D toggles a small overlay showing bar.beat.

SELF-CHECK
Render at least one frame per act plus t=0 and t=15.99. Look at them.
Check the grid alignment, the cropping, that hits land on beats, and the loop.
Fix what's wrong, up to two rounds. Say what you checked and what's left.

Comment the code in plain English for a beginner.
