# Brief 5: Unus Smooth

Make one self-contained HTML file at the path given. Nothing else.
Vanilla JavaScript and Canvas 2D only. No libraries, no CDN, no external
fonts, no images, no network, no WebGL.

This is Brief 4 (Unus) again with fixes. The aim of this round: calm,
clean and smooth. Nothing touches, nothing jumps, nothing flashes.

FORMAT
1080x1350 portrait, scaled to fit the window, centered on #000000.
16-second seamless loop at 90 BPM, 4/4: one beat = 2/3 s, one bar = 8/3 s,
16 s = 24 beats = 6 bars. The picture at t=16 equals t=0 (plain white).
Must run smoothly at 60 fps on an iPhone 13 or 15, a Galaxy S24 or S25
and a Pixel 9 Pro in the Brave browser.
Everything the viewer needs to see stays inside the frame. Nothing is lost
off the edge.

WORDS
The only text, besides one small caption, is this Latin sentence:
UNUS PRO OMNIBUS, OMNES PRO UNO  (one for all, all for one)
Always in capitals. Keep the comma after OMNIBUS everywhere OMNIBUS
appears: draw "OMNIBUS," as one word with its comma.
Caption, in act 6 only: 90 BPM — 4/4 — 16 S

STYLE
Swiss International Style: grid, asymmetry, few sizes, strong contrast.
- Grid: 6 columns x 8 rows, 135 px margins, so every cell is a 135 px
  square. The live area is the 810 x 1080 box inside the margins.
  Everything snaps to the grid.
- Type: "Helvetica Neue", Helvetica, Arial, sans-serif. Bold and regular
  only. Use the device's font; do not draw your own letters.
- Three text sizes only (font size in frame pixels): 52, 84, 136.
  Each is the one before x 1.618. On a 360 px wide phone they show as
  about 17, 28 and 45 px, which is readable.
- Colours: white #ffffff, black #111111, red #e30613. Red text only at
  84 or 136.
- Avoid: cream, italics, gradients, drop shadows, glow, blur, pill shapes,
  01/02/03 labels, plain checkerboards.

TEXT RULES
- Whole words, always. A word is never cut, cropped, split across lines,
  or partly outside the live area, not even while it moves.
- Every word holds still for at least 2 beats after it lands, so it can
  be read.
- A word at rest uses size 52, 84 or 136. When a word changes one size
  step, it may scale smoothly between the two sizes on the way.
- Fonts differ slightly between phones. Measure every word with
  measureText on the device and keep at least 5% spare width.

FRAME RULES
- Nothing is cropped by the frame. Only the background field and
  full-width or full-height rules may touch the frame edge.
- Balance: use the whole frame. In every composition, at least 30% of the
  inked area sits in the left half and at least 30% in the right half
  (the background field doesn't count).

CLEAN SPACING
- At least 17 px of empty space between any two things on screen: word
  and word, word and shape, shape and shape, line and word, line and
  shape. In every frame, also while things move, grow or pulse. No
  touching, not even at corners. No overlapping.
- Lines never cross or touch a shape or a word.
- The only exception is the background field (see BACKGROUND):
  everything sits on it. Any other filled area is a shape, so a block
  behind a word must also keep 17 px from that word.
- Measure real outlines, not rough boxes:
  rect = its box (no rotation; a turned square counts as a path),
  circle = centre and radius (two circles may come closer at the
  corners of their boxes), line = a segment with its thickness,
  word = its ink box from measureText (actualBoundingBoxLeft, Right,
  Ascent, Descent, so the comma counts), path = its box.
- Shapes at rest sit exactly on the grid. "At rest" = its box has not
  changed for 6 frames in a row. A resting shape's box is one grid cell,
  or a block of whole cells, shrunk by the same inset on all four sides.
  Pick one inset for the whole piece, at least 9 px, so neighbours keep
  at least 18 px apart. A circle at rest fills such a box. Small hi-hat
  marks (both sides at most 34 px) at rest are centred on a grid-line
  crossing or a cell centre. Lines at rest lie on a grid line or on a
  cell's centre line. Lines and shapes still keep 17 px apart, so choose
  the inset with that in mind.
- Split and merge without contact. A new shape never starts under or on
  top of another one: it grows or fades in at its own place, gap kept.
  "Merge" means a hand-over, not a collision: shapes never join, overlap
  or slide over each other on the way.
- Nothing pops. No word or shape appears or disappears in a single
  frame: it fades in or out, or grows from or shrinks to nothing, over
  at least 1/8 beat (5 frames).

BACKGROUND
- The background is one full-frame field, white or black.
- No hard cuts anywhere in the piece.
- The change to black finishes on beat 1 of act 4 (8.000). The change
  back to white finishes on beat 1 of act 6 (13.333), where the lockup
  lands on white.
- Each change lasts at least one beat (2/3 s, 40 frames) and eases in
  and out. Crossfade (the field fades from one colour to the other) or
  wipe (a field slides in from one edge until it fills the frame): your
  choice for each change.
- Gentle: between two frames, at most 5% of the background changes
  (crossfade: the mix moves at most 5 percentage points; wipe: the new
  field grows by at most 5% of the frame area).
- No words on screen while the background changes: words fade out
  before a change starts and new words come in after it ends. Shapes
  may stay.

THE STORY: one act per bar. The design inside each act is yours.
1. 0.000-2.667 UNUS. From plain white, one red square lands on the grid.
   UNUS appears.
2. 2.667-5.333 PRO OMNIBUS. The one square multiplies across the grid.
   Each new square grows or fades in at its own place. PRO and
   OMNIBUS, (with its comma) build word by word.
3. 5.333-8.000 MANY. Many modules fill the grid and play the hi-hat
   pattern of this act. Use the full width. The background eases to
   black, finishing on 8.000.
4. 8.000-10.667 OMNES. Black field. The many gather, keeping their gaps.
   OMNES in white.
5. 10.667-13.333 PRO UNO. The many become one red circle: a morph,
   without contact. The many shrink, fade or leave; one shape, clear of
   them, morphs into the circle. PRO UNO. The background eases back to
   white, finishing on 13.333.
6. 13.333-16.000 LOCKUP. White. The whole sentence lands on beat 1, fully
   readable, broken into lines at word boundaries, with the caption.
   It holds for at least 2 beats; on the last beat everything fades
   away to plain white.

MORPH RULE
Every in-between shape of the act 5 morph is clean: one simple closed
shape, no crossed edges, no spikes, no kinks, no flicker.

MUSIC RULES: think of a drum kit.
- KICK, beat 1 of every bar: the big move. A large element travels at
  least 3 grid cells, or the composition changes (by moving, growing or
  fading, never by a cut).
- SNARE, beats 2 and 4: medium moves. One element moves one grid cell,
  changes one size step, or a rule grows or shrinks.
- Beat 3: a softer kick (smaller than beat 1) or hi-hat level.
- HI-HAT, the fillers: small events on 8ths, 16ths, triplets or
  syncopated off-beats. Ticks, pulses, blinks, small marks that move
  at most 34 px. Hi-hats never move a word.
- Each act has its own hi-hat pattern: use straight 8ths, 16ths,
  triplets and syncopation, each in at least one act.
- Words move only on a kick or a snare.
- Smooth, never jerky: every move eases in and out, and nothing jumps.
  Speed limit: no edge of any element moves more than 24 px between two
  frames (1440 px per second), size changes included. A 3-cell kick
  move (405 px) therefore needs about one beat: start it early enough
  to land exactly on the hit. Landings use a damped spring computed
  from t, with at most 10% overshoot. Moves start before their hit and
  land exactly on it, except the very first beat at t=0, which starts
  from plain white and lands late.

PHONE RULES
- At most 200 shapes drawn per frame. No canvas filters, no shadowBlur,
  no getImageData during playback.
- Pixel density capped at 2.

TECHNICAL
Every element is a pure function of t via a global window.seek(t).
seek(t) draws frame t and returns that frame's list of records (see
FRAME CHECK). It also moves the playback clock: while playing, playback
carries on from t; while paused, frame t stays on screen.
Drive it with requestAnimationFrame, t = elapsed seconds mod 16.
No CSS transitions, no timers that carry state, no unseeded Math.random.
Keys: Space pauses; left/right arrows step one beat; D toggles a small
bar.beat overlay; M toggles a drum metronome (Web Audio, off by default,
in sync with t: kick on beat 1 and on beat 3 if the picture uses one,
snare on 2 and 4, closed hi-hat on the hi-hat pattern the current act
uses); F toggles the frame-check view below.
Phones have no keys. Tap the picture: a row of buttons appears along the
bottom for 3 seconds (Play/Pause, previous beat, next beat, D, M, F),
then fades away. Each button is at least 44 px tall on the phone screen.
The buttons are HTML on top of the canvas, not part of the artwork, and
frameCheck ignores them.

FRAME CHECK (built into the page)
Draw everything through a few small helpers (text, rect, circle, line,
path, field). Each helper draws and, in the same call, records what it
drew in a list for that frame: id, kind, box (x, y, w, h), plus circle
centre and radius, line ends and thickness, text and text size, colour,
alpha. The helpers both draw and record, so the records always match
the picture.
window.frameCheck() steps t from 0 to 16 in steps of 1/60 s and returns
every problem with its time and the ids involved:
- a word not fully inside the live area, or a cut word
- OMNIBUS without its comma
- two things closer than 17 px (words, shapes, lines; real outlines as
  described in CLEAN SPACING; only the background field is exempt)
- a resting shape that is not exactly on the grid
- a resting word at a text size other than 52, 84 or 136, or red text
  below 84
- a shape touching the frame edge that isn't the background field or a
  full-width or full-height rule
- at each beat, a composition that fails the 30% balance rule
  (skip plain white frames)
- any edge of an element moving more than 24 px between two frames
  (the background field is exempt)
- a word or shape that appears or disappears between two frames while
  drawn with alpha above 0.25 and both sides larger than 17 px
- a background change shorter than 40 frames, or more than 5% of the
  background changing between two frames
- a word on screen while the background is changing
- more than 200 shapes in one frame
Test exactly these rules. Don't loosen the check to make it pass.
Key F draws every recorded outline (circles as circles): green if fine,
red if it breaks a rule.

SELF-CHECK
Build in stages and keep the file working after each one:
1 grid, drawing helpers and frame check, 2 the six acts, 3 rhythm
polish, drum metronome and tap buttons.
Then the full check: render t=0, the landing of every beat and t=15.99.
Look at them at 1080x1350 and at a 360x780 viewport. Look at the act 5
morph and at both background changes at 25%, 50% and 75%. Run
frameCheck(). Measure draw time with painting included: play normally
for 10 seconds and record the time between requestAnimationFrame calls
(average, worst, and how many frames took longer than 20 ms); also give
the average and worst time spent inside seek(t).
Fix rounds: one fix round = change the code to fix what the full check
found, then run the full check again. Small fixes while building the
stages don't count. You get the first full check plus at most two fix
rounds. After the second fix round, stop fixing and report.
If something is too ambitious, a smaller version that fully works beats
a big broken one: say what you cut and why. Say what you checked and
what's left.

Comment the code in plain English for a beginner.
