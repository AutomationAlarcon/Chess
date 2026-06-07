# Chess Site README

A standalone browser chess app with multiple historical HTML versions and a Stockfish-powered AI in the latest version.

## Current Version

Use:

```text
chess_site_v3.html
```

This version includes:

- playable chess board
- position editor
- undo
- move list
- checkmate and stalemate detection
- black castling strategy in the opening
- Stockfish integration for stronger AI on medium and hard difficulty

## Difficulty Levels

- Easy: lightweight built-in AI, easier to beat.
- Medium: Stockfish with limited strength and shorter calculation time.
- Hard: Stockfish with higher strength and longer calculation time.

## Required Files

Keep this structure:

```text
chess_site_v3.html
stockfish/
  stockfish-10.js
  Copying.txt
```

`stockfish-10.js` is required for medium and hard difficulty. `Copying.txt` is the Stockfish license file.

## Local Testing

The recommended way to run the app is through a local web server, not by opening the HTML directly with `file://`.

From the repository root:

```powershell
python -m http.server 8765 --bind 127.0.0.1
```

Then open:

```text
http://127.0.0.1:8765/chess_site_v3.html
```

This matters because Stockfish is loaded through a Web Worker, and some browsers restrict Workers when files are opened directly from disk.

## Project Files

```text
chess_editor_mode_v1.html
chess_pwa.html
chess_site_v1.html
chess_site_v2.html
chess_site_v3.html
stockfish/
```

Older files are kept as previous versions. The main file to improve is currently `chess_site_v3.html`.

## Notes

The app does not use an online chess database and does not auto-learn from games. Stockfish calculates moves locally in the browser.

Stockfish is GPL licensed. Keep the included license file when redistributing the app.
