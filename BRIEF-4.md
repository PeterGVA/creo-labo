# Brief 4: Unus

Make one self-contained HTML file at the path given. Nothing else.
Vanilla JavaScript and Canvas 2D only. No libraries, no CDN, no external
fonts, no images, no network, no WebGL.

FORMAT
1080x1350 portrait, scaled to fit the window, centered on #000000.
16-second seamless loop at 90 BPM, 4/4: one beat = 2/3 s, one bar = 8/3 s,
16 s = 24 beats = 6 bars. The picture at t=16 equals t=0 (plain white).
Must run smoothly at 60 fps on an iPhone 13 or 15 and a Galaxy S24 or S25.
Everything the viewer needs to see stays inside the frame. Nothing is lost
off the edge.

WORDS
The only text, besides one small caption, is this Latin sentence:
UNUS PRO OMNIBUS, OMNES PRO UNO  (one for all, all for one)
Always in capitals. Keep the comma after OMNIBUS.
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
- Words never overlap each other. Shapes never cross a word's box (a flat
  background field behind the word is fine).
- Every word holds still for at least 2 beats after it lands, so it can
  be read.
- Fonts differ slightly between phones. Measure every word with
  measureText on the device and keep at least 5% spare width.

FRAME RULES
- Nothing is cropped by the frame. Only flat full-frame background fields
  and full-width or full-height rules may touch the frame edge.
- Balance: use the whole frame. In every composition, at least 30% of the
  inked area sits in the left half and at least 30% in the right half
  (full-frame background fields don't count).

THE STORY: one act per bar. The design inside each act is yours.
1. 0.000-2.667 UNUS. From plain white, one red square lands on the grid.
   UNUS appears.
2. 2.667-5.333 PRO OMNIBUS. The one square multiplies across the grid.
   PRO OMNIBUS, builds word by word.
3. 5.333-8.000 MANY. Many modules fill the grid and play the hi-hat
   pattern of this act. Use the full width.
4. 8.000-10.667 OMNES. A hard cut to a black field is allowed on beat 1.
   The many gather. OMNES in white.
5. 10.667-13.333 PRO UNO. The many merge into one red circle: a morph.
   PRO UNO.
6. 13.333-16.000 LOCKUP. White. The whole sentence lands on beat 1, fully
   readable, broken into lines at word boundaries, with the caption.
   It holds for at least 2 beats; on the last beat everything clears to
   white.

MORPH RULE
Every in-between shape of the act 5 morph is clean: one simple closed
shape, no crossed edges, no spikes, no kinks, no flicker.

MUSIC RULES: think of a drum kit.
- KICK, beat 1 of every bar: the big move. A large element travels at
  least 3 grid cells, or the composition changes.
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
  Landings use a damped spring computed from t, with at most 10%
  overshoot. Moves start slightly before their hit and land exactly on
  it, except the very first beat at t=0, which starts from plain white
  and lands late. At most two hard cuts in the whole piece, each on a
  kick.

PHONE RULES
- At most 200 shapes drawn per frame. No canvas filters, no shadowBlur,
  no getImageData during playback.
- Pixel density capped at 2.

TECHNICAL
Every element is a pure function of t via a global window.seek(t).
Drive it with requestAnimationFrame, t = elapsed seconds mod 16.
No CSS transitions, no timers that carry state, no unseeded Math.random.
Keys: Space pauses; left/right arrows step one beat; D toggles a small
bar.beat overlay; M toggles a drum metronome (Web Audio, off by default,
in sync with t: kick on beat 1 and on beat 3 if the picture uses one,
snare on 2 and 4, closed hi-hat on the hi-hat pattern the current act
uses); F toggles the frame-check view below.

FRAME CHECK (built into the page)
Draw everything through a few small helpers (text, rect, circle, line,
path). Each helper takes a short id name and also records what it drew
in a list for that frame: id, kind, box, text size, colour.
window.frameCheck() steps t from 0 to 16 in steps of 1/60 s and returns
every problem with its time:
- a word not fully inside the live area, or a cut word
- two words overlapping, or a shape crossing a word's box
- a text size other than 52, 84 or 136, or red text below 84
- a shape touching the frame edge that isn't a full-frame field or rule
- at each beat, a composition that fails the 30% balance rule
  (skip plain white frames)
- an element whose box jumps more than 68 px between two frames 1/60 s
  apart, except at one of the two allowed hard cuts
- more than 200 shapes in one frame
Test exactly these rules. Don't loosen the check to make it pass.
Key F draws every recorded box: green if fine, red if it breaks a rule.

SELF-CHECK
Build in stages and keep the file working after each one:
1 grid, drawing helpers and frame check, 2 the six acts, 3 rhythm
polish and drum metronome.
Render t=0, the landing of every beat and t=15.99. Look at them at
1080x1350 and at a 360x780 viewport. Look at the act 5 morph at 25%,
50% and 75%. Run frameCheck(). Measure the average and worst time to
draw one frame.
Fix what's wrong, up to two rounds. If something is too ambitious, a
smaller version that fully works beats a big broken one: say what you
cut and why. Say what you checked and what's left.

Comment the code in plain English for a beginner.
