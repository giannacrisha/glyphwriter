# Glyphwriter: context for Claude Code

Scanned glyph sheet to TrueType font builder that preserves rough, typewritten edges. Built by Gi (Gianna Crisha Saludo). Launching open source on GitHub.

## Hard constraints
- Zero dependencies, zero build step. Plain HTML, CSS, and ES modules that run from `index.html` on GitHub Pages.
- Everything runs client-side. No API calls, no tokens, no backend. Keep it that way unless Gi says otherwise.
- Only external request: Google Fonts CSS (style references for Fill, plus IBM Plex Mono for UI).
- Copy rules: no em dashes anywhere. Short labels over sentences; lean on visuals.

## Design system ("paper studio")
- Tokens live on `:root`: `--bg #F2ECDE`, `--paper #FCF9F0`, `--panel #EAE4D6`, `--ink #292722`, `--muted #70695C`, `--line #CFC5B0`, `--accent #903D32` (oxblood). Dark mode overrides exist; keep both.
- UI font: IBM Plex Mono. Display font: the user's own generated font ("gerif"), loaded live via `FontFace` as `GliphoriaPreview*`.
- Texture: `.tx` elements draw their background on `::before` with `filter: url(#edge)` for rough printed edges. Sliders use `#slider-grit` and wobble via `#slider-live` while dragging.
- Figma source: https://www.figma.com/design/3QQoa7kWLRQRIYdyOn4kPx (node 14:247).

## How the single file is organized (index.html)
1. **Detect**: `loadSource`, `components` (connected components), `regroup` (rows + merging dots/accents into glyphs), `assign` (reading-order to characters).
2. **Trace**: `traceGlyph` (crop, optional blur, `march` = marching squares, `rdpClosed` simplification), cached per settings.
3. **Layout**: `layout` (baselines per row, cap height = 700 units, per-glyph edits via `applyAdj`), `finishGlyph` (spacing, wobble, winding).
4. **Font writer**: `buildTTF`, `encodeGlyph`, `nameTable` (hand-written glyf/loca/cmap/hmtx/OS2/name/post tables).
5. **Fill**: `rankSources` (IoU match vs Google Fonts), `calibrate` (width, stroke weight, edge roughness), `traceText`, `composeAccent` (her base letter + generated mark), `addGenerated`.
6. **Google Fonts search**: `GF_LIST`, `registerGoogleFont`, combobox UI.
7. **UI**: tabs, workbench loupe (`drawLoupe`, `drawLoupeGen`), steppers, coverage strip, sheet cells, comment mode, persistence in `localStorage` (`glyphwriter:*` keys).

## Done since launch
- Public at github.com/giannacrisha/glyphwriter, live on Pages, MIT licensed.
- Create modal: printable template (helplines + character references, both optional), or upload a filled sheet.
- Detection auto-tunes speck filter and part joining by matching the glyph count to `#order`.
- Template prints entirely in light blue, and the detector drops light bluish pixels (`b > r * 1.15 && L > 75`) before the luminance-140 threshold. A scan can darken the page 30% and the guides are still ignored, while dark ink and blue pen are still read.
- Glyph delete: select plus Backspace, or the hover x on a cell. Both undoable.
- Wordmark and bigmark are pinned to the static gerif face, never the generated font.
- Favicon, apple-touch-icon, Open Graph card, post-download support panel.

## Open tasks
1. Split `index.html` into `index.html`, `styles.css`, and ES modules (`detect.js`, `trace.js`, `ttf.js`, `fill.js`, `ui.js`). No bundler.
2. Move the embedded demo scan (base64 PNG in `<img id="demo">`) to `assets/demo-sheet.png`.
3. Add a smoke test: headless Chromium loads the page, waits for "Ready", downloads the font, and `fontTools` validates it.
4. Add a demo GIF to the README (sheet to font).

## Backlog (ask Gi before starting any)
- Per-letter editor: erase specks, redraw, flip, rotate.
- Alternates: 2 to 3 drawings per letter cycled with OpenType `calt` for real typewriter variation.
- Kerning pairs for proportional mode.
- WOFF2 export plus a CSS snippet.
- Save/load project file (`.glyphwriter`).
- Template maker: printable sheet for missing characters.
