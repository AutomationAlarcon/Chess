# Chess App Codex Context

## Repository

GitHub repository: `AutomationAlarcon/Chess`

The main development target is currently:

```text
chess_site_v3.html
```

Older versions are kept in the repo for reference:

```text
chess_site_v1.html
chess_site_v2.html
chess_editor_mode_v1.html
chess_pwa.html
```

Do not overwrite older versions unless the user explicitly asks for it. New significant iterations should normally be saved as a new versioned HTML file.

## Current App Structure

`chess_site_v3.html` loads Stockfish from:

```text
stockfish/stockfish-10.js
```

The Stockfish license file is:

```text
stockfish/Copying.txt
```

The required runtime layout is:

```text
chess_site_v3.html
stockfish/
  stockfish-10.js
  Copying.txt
```

`Copying.txt` is not loaded by the app at runtime, but should remain in the repo because Stockfish is GPL licensed.

## Decisions Made

- `chess_site_v3.html` is the current version with Stockfish integration.
- Easy difficulty uses the original lightweight in-page AI.
- Medium difficulty uses Stockfish with limited strength and shorter thinking time.
- Hard difficulty uses Stockfish with higher strength and longer thinking time.
- The app does not use a chess database.
- The app does not auto-learn from games.
- Stockfish runs locally in the browser via Web Worker.
- If Stockfish cannot load, the game falls back to the lightweight in-page AI.

## Features Already Improved

- Added checkmate and stalemate detection so the game does not remain stuck on "IA pensando...".
- Added strategic castling preference for black in the opening.
- Integrated Stockfish for stronger medium and hard difficulty.
- Added local Stockfish files to the repo so the game is not dependent on a CDN at runtime.

## Important Technical Notes

- The board is represented as a flat array of 64 cells.
- White pieces are uppercase letters, black pieces are lowercase letters.
- Move generation is handled by `getLegalMoves()` and `getAllMoves()`.
- The old lightweight evaluation uses material values in `VALS`.
- Stockfish receives positions as FEN through `boardToFen()`.
- Stockfish returns UCI moves, parsed by `parseUciMove()`.
- Black AI moves are applied through `playBlackMove()`.

When changing chess rules, be careful with:

- castling rights
- promotion
- check detection
- move history
- undo state
- FEN generation for Stockfish

## How To Test Locally

Prefer serving the folder over localhost instead of opening the HTML directly with `file://`, because Stockfish runs in a Worker and some browsers block Workers from local file URLs.

From the repo root:

```powershell
python -m http.server 8765 --bind 127.0.0.1
```

Then open:

```text
http://127.0.0.1:8765/chess_site_v3.html
```

If using Codex bundled Python, the path may be similar to:

```powershell
C:\Users\alfon\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe -m http.server 8765 --bind 127.0.0.1
```

## Future Improvement Ideas

- Implement en passant.
- Implement the fifty-move rule.
- Implement threefold repetition.
- Improve PGN notation and export.
- Add save/load game state.
- Add player color selection.
- Add a proper game-over modal.
- Improve mobile layout and touch interactions.
- Turn the app into a proper PWA.
- Add a settings panel for Stockfish strength and thinking time.

## Git Safety

Do not push changes to GitHub unless the user explicitly asks.

Before committing, inspect `git status --short --branch` and stage only the files requested by the user. The user may have local changes that should not be reverted.
