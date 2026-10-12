# Brief 6: Unus Flow

Make one self-contained HTML file at the path given. Nothing else.
Vanilla JavaScript and Canvas 2D only. No libraries, no CDN, no external
fonts, no images, no network, no WebGL.

This is Brief 5 (Unus Smooth) again with changes. The aim of this round:
smooth, hypnotic, immersive and artistic, yet calm and safe to watch.
Always gently alive: nothing freezes, nothing jumps, nothing flashes.
The strict rules are about safety, cleanliness and smoothness. Inside
them, the design is yours: surprise us.

FORMAT
1080x1350 portrait, scaled to fit the window, centered on #000000.
16-second seamless loop at 90 BPM, 4/4: one beat = 2/3 s, one bar = 8/3 s,
16 s = 24 beats = 6 bars. The picture at t=16 equals t=0 (plain white).
Must run smoothly at 60 fps on an iPhone 13 or 15, a Galaxy S24 or S25
and a Pixel 9 Pro in the Brave browser.
Everything the viewer needs to see stays inside the frame. Nothing is lost
off the edge.

WORDS
The only text is this Latin sentence:
UNUS PRO OMNIBUS, OMNES PRO UNO  (one for all, all for one)
Always in capitals. Keep the comma after OMNIBUS everywhere OMNIBUS
appears: draw "OMNIBUS," as one word with its comma.
No caption, no other text.

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
- Shapes: use all three families in the piece: squares (or rectangles),
  circles and triangles. A triangle is drawn as a path.
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
- Use the whole frame: spread the ink over the left and the right half
  (aim for at least 30% of the inked area in each half). This is
  guidance, not checked.

CLEAN SPACING
- At least 17 px of empty space between any two things on screen: word
  and word, word and shape, shape and shape, line and word, line and
  shape. In every frame, also while things move, grow, breathe or pulse.
  No touching, not even at corners. No overlapping.
- Lines never cross or touch a shape or a word.
- The only exception is the background field (see BACKGROUND):
  everything sits on it. Any other filled area is a shape, so a block
  behind a word must also keep 17 px from that word.
- Measure real outlines, not rough boxes:
  rect = its box (no rotation; a turned square counts as a path),
  circle = centre and radius (two circles may come closer at the
  corners of their boxes), line = a segment with its thickness,
  word = its ink box from measureText (actualBoundingBoxLeft, Right,
  Ascent, Descent, so the comma counts), path = its box (a triangle
  too).
- Shapes have homes on the grid. A home box is one grid cell, or a
  block of whole cells, shrunk by the same inset on all four sides.
  Pick one inset for the whole piece, at least 9 px, so neighbouring
  homes keep at least 18 px apart. A shape is "settled" when none of
  its edges has moved more than 1 px per frame for 6 frames in a row.
  A settled shape (rect, circle or triangle) sits inside its home box,
  and each side of its box is at least 80% of the home box's side: it
  may breathe or drift slowly inside its home, never out of it. At full
  size, a circle or a triangle fills its home box. Small hi-hat marks
  (both sides at most 34 px), when settled, are centred within 8 px of
  a grid-line crossing or a cell centre. Lines at rest (unchanged for
  6 frames) lie on a grid line or on a cell's centre line. Lines and
  shapes still keep 17 px apart, so choose the inset with that in mind.
- Split and merge without contact. A new shape never starts under or on
  top of another one: it grows or fades in at its own place, gap kept.
  "Merge" means a hand-over, not a collision: shapes never join, overlap
  or slide over each other on the way.
- Nothing pops. No word or shape appears or disappears in a single
  frame: it fades in or out, or grows from or shrinks to nothing, over
  at least 1/8 beat (5 frames).

FLOW: ALWAYS GENTLY ALIVE
- Nothing freezes. From 0.667 s until the final fade starts (15.333),
  something on screen moves in every frame ("moves" = its box changes).
  Slow breathing (a gentle grow and shrink) and slow drift count.
- No shape (rect, circle, triangle, small mark) stays exactly the same
  (box and alpha unchanged) for more than 40 frames (one beat). Words
  and lines may hold still; words must, so they can be read.
- Waves: in at least three acts, a wave travels across the grid:
  neighbouring elements make the same move one after another, each a
  little later than the one before (for example 1/8 beat per cell),
  like wind passing over a field of grass.
- Slow and calm: one breathing or drifting cycle lasts at least one
  bar (2.667 s).

SAFE TO WATCH (no flashing)
- Nothing larger than one grid cell (area above 18,225 px²) changes its
  alpha by more than 0.05 between two frames: big things fade in or out
  over at least 20 frames (half a beat). So no large area can flash,
  and the picture never goes light-dark-light more than 3 times in any
  second.
- No red flashes: red areas bigger than a small mark never blink; they
  only fade, grow, shrink or move.
- No fine stripes: never more than five parallel lines or bars side by
  side closer than 34 px, and no fine high-contrast patterns over large
  areas.
- Fast rhythms (16ths, 6 per second) only on small marks (both sides at
  most 34 px), and at most 10% of the frame area blinks on any one hit.

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
2. 2.667-5.333 PRO OMNIBUS. The one square multiplies across the grid
   into squares, circles and triangles. Each new shape grows or fades
   in at its own place. PRO and OMNIBUS, (with its comma) build word
   by word.
3. 5.333-8.000 MANY. Many modules fill the grid and move with the
   rhythm. Use the full width. The background eases to black,
   finishing on 8.000.
4. 8.000-10.667 OMNES. Black field. The many gather, keeping their gaps.
   OMNES in white.
5. 10.667-13.333 PRO UNO. The many become one red circle: a morph,
   without contact. The many shrink, fade or leave; one shape, clear of
   them, morphs into the circle. PRO UNO. The background eases back to
   white, finishing on 13.333.
6. 13.333-16.000 LOCKUP. White. The whole sentence lands on beat 1, fully
   readable, broken into lines at word boundaries. Tight line spacing:
   the empty space between one line's ink and the next line's ink is
   between 17 and 34 px. Something beside the words keeps breathing
   (nothing freezes). The sentence holds for at least 2 beats; on the
   last beat everything fades away to plain white.

MORPH RULE
Every in-between shape of the act 5 morph is clean: one simple closed
shape, no crossed edges, no spikes, no kinks, no flicker.

RHYTHM: think of a drum kit. Guidance for the design, not checked.
- KICK, beat 1 of every bar: the big move, or the composition changes
  (by moving, growing or fading, never by a cut).
- SNARE, beats 2 and 4: medium moves.
- Beat 3: a softer kick or hi-hat level.
- HI-HAT, the fillers: small events on 8ths, 16ths, triplets or
  off-beats. Ticks, pulses, blinks, small marks that move at most 34 px.
  Mix the patterns as you like.
These stay strict: words move only on a kick or a snare, and hi-hats
never move a word.

SMOOTHNESS (strict)
- Every move eases in and out, and nothing jumps.
- Speed limit: no edge of any element moves more than 24 px between two
  frames (1440 px per second), size changes included.
- Speed-change limit (new): for every edge of every element, its move
  from frame n-1 to n and its move from frame n to n+1 differ by at
  most 2 px. So moves start gently and stop gently, never in a burst.
  For example, a 3-cell move (405 px) on a smooth S-curve such as
  smootherstep needs at least 40 frames (one beat): start it early
  enough to land exactly on the hit. Small hi-hat marks (both sides at
  most 34 px) and the background field are exempt.
- A small settle (overshoot) is allowed if it stays within 10% and keeps
  both limits. Note: a damped spring that starts at full speed breaks
  the speed-change limit.
- Moves start before their hit and land exactly on it, except the very
  first beat at t=0, which starts from plain white and lands late.

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
centre and radius, line ends and thickness, a triangle's three corners,
text and text size, colour, alpha. The helpers both draw and record, so
the records always match the picture.
window.frameCheck() steps t from 0 to 16 in steps of 1/60 s and returns
every problem with its time and the ids involved:
- a word not fully inside the live area, or a cut word
- OMNIBUS without its comma
- two things closer than 17 px (words, shapes, lines; real outlines as
  described in CLEAN SPACING; only the background field is exempt)
- a settled shape outside its home box or with a side smaller than 80%
  of the home box's side; a settled small mark more than 8 px from a
  grid-line crossing or cell centre; a line at rest off the grid lines
  and cell centre lines
- a resting word at a text size other than 52, 84 or 136, or red text
  below 84
- a shape touching the frame edge that isn't the background field or a
  full-width or full-height rule
- any edge of an element moving more than 24 px between two frames
  (the background field is exempt)
- any edge whose move changes by more than 2 px from one frame to the
  next (small hi-hat marks and the background field are exempt)
- a shape that stays exactly the same (box and alpha) for more than 40
  frames
- a frame between 0.667 and 15.333 in which nothing moves
- an element larger than one grid cell whose alpha changes by more than
  0.05 between two frames
- a word or shape that appears or disappears between two frames while
  drawn with alpha above 0.25 and both sides larger than 17 px
- a background change shorter than 40 frames, or more than 5% of the
  background changing between two frames
- a word on screen while the background is changing
- in the lockup, more than 34 px of empty space between one line's ink
  and the next
- more than 200 shapes in one frame
Test exactly these rules. Don't loosen the check to make it pass.
Key F draws every recorded outline (circles as circles): green if fine,
red if it breaks a rule.

SELF-CHECK
Build in stages and keep the file working after each one:
1 grid, drawing helpers and frame check, 2 the six acts, 3 flow and
rhythm polish (breathing, waves), drum metronome and tap buttons.
Then the full check: render t=0, the landing of every beat and t=15.99.
Look at them at 1080x1350 and at a 360x780 viewport. Look at the act 5
morph and at both background changes at 25%, 50% and 75%, and at one
wave as it travels. Run frameCheck(). Measure draw time with painting
included: play normally for 10 seconds and record the time between
requestAnimationFrame calls (average, worst, and how many frames took
longer than 20 ms); also give the average and worst time spent inside
seek(t).
Fix rounds: one fix round = change the code to fix what the full check
found, then run the full check again. Small fixes while building the
stages don't count. You get the first full check plus at most two fix
rounds. After the second fix round, stop fixing and report.
If something is too ambitious, a smaller version that fully works beats
a big broken one: say what you cut and why. Say what you checked and
what's left.

Comment the code in plain English for a beginner.
