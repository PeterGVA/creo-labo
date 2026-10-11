# creo-labo

One piece of content, made by several Claude setups, so you can compare them blind.

## How it works

- `BRIEF.md` is the exact instruction every setup receives. Never edit it mid-comparison.
- `pieces/swiss-grid/` holds the results: one folder per setup (`opus`, `sonnet`, `haiku`, `team`), each with an `index.html`.
- `index.html` (open it in a browser) shows the versions side by side under shuffled labels A–D. Press **Reveal** to see who made which.
- `pieces/swiss-grid/results.md` is where you note time, cost and your score.

## Adding a new run

1. Give a setup the brief and have it write `pieces/swiss-grid/<setup>/index.html`.
2. Open the root `index.html`. The empty "not built yet" box is replaced by the animation.
3. Score it blind, then press Reveal and fill in `results.md`.

To compare a different piece, add `pieces/<new-name>/` with the same folder layout and point the gallery's paths at it.
