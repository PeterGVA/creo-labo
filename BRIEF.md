# Brief: Swiss Grid in Motion

Make one self-contained HTML file at the path given. Nothing else.
No libraries, no CDN, no external fonts, no images, no network.

Frame: 1080x1350 portrait, scaled to fit the window, centered.
Style: International Typographic Style (Müller-Brockmann, Ruder, Gerstner).
Strict 6-column grid. Flush-left, ragged-right. Helvetica, Arial, sans-serif.
Colors only: ground #ffffff, ink #111111, accent #e30613.
Avoid: cream backgrounds, italic accent words, 01/02/03 labels,
monospace, pill shapes.

6-second seamless loop: the picture at t=6 equals t=0.
Every element is a pure function of t via a global window.seek(t).
Drive it with requestAnimationFrame, t = elapsed seconds mod 6.
No CSS transitions, no timers that carry state, no unseeded Math.random.
Damped springs (computed from time) when things land, eases when they leave.
Space pauses; left/right arrows step 1/30 s.

Beats:
0.0–0.4  faint column lines draw down from the top
0.4–1.6  GRID drops in letter by letter, huge, flush left
1.6–2.6  a red circle rolls along the baseline, stops on column 5
2.6–3.8  GRID slides up; RHYTHM and TIME stack below, staggered
3.8–5.0  the whole layout snaps to a 45° rotation, then back
5.0–6.0  everything exits upward, lines fade, back to frame one

Comment the code in plain English for a beginner.
