# Chess Practice - Best Move Trainer

A fully client-side chess trainer. Make moves for both sides and after every move
the engine (Stockfish) shows the best reply as an arrow, an evaluation, and the
principal variation. No backend, no accounts, nothing leaves your browser.

## Features

- Click-to-move board with legal-move highlighting and a promotion picker.
- Always-on Stockfish analysis: best move arrow, eval bar, eval number, and the
  principal variation in human-readable notation.
- Adjustable engine think time (0.2s to 3s).
- Optional "Engine plays White / Black" toggles to use it as a sparring partner.
- Flip board, undo, new game, and "Play best" (auto-make the suggested move).
- Move list in standard notation.

## Run locally

Any static file server works. For example:

```
python -m http.server 8000
```

Then open http://localhost:8000

(It must be served over http, not opened as a `file://` URL, because the engine
runs in a Web Worker.)

## Deploy to GitHub Pages

1. Create a GitHub repo and push these files.
2. Repo Settings -> Pages -> Source: `Deploy from a branch`, branch `main`, folder `/ (root)`.
3. Your trainer will be live at `https://<user>.github.io/<repo>/`.

No build step, no server, no special headers required.

## How it works

- `vendor/chess.js` (chess.js) handles move legality and game state.
- `engine/stockfish.js` (Stockfish 10, single-threaded asm.js build) runs in a
  Web Worker and speaks the UCI protocol. The single-threaded build needs no
  `SharedArrayBuffer` and therefore no COOP/COEP headers, so it works on GitHub
  Pages out of the box.
- `index.html` wires the board to the engine and renders the analysis.

Stockfish is GPLv3. chess.js is BSD-2-Clause.
