# Glyphwriter

Turn a scanned sheet of hand-made letters into a real font, and keep every rough, inky edge.

Most font builders smooth your letters into clean vectors. Glyphwriter traces the ink edge exactly as it was printed, so typewriter grit, ink bleed, and uneven strikes survive into the `.ttf`.

## What it does

| Step | What happens |
|---|---|
| **Upload** | Drop in a scan of your glyph sheet (Calligraphr-style templates work) |
| **Detect** | Finds every glyph, groups dots and accents with their letters, and maps them to characters in reading order |
| **Trace** | Converts each glyph to an outline that keeps the rough edges |
| **Tune** | Ink weight, smoothing, extra grit, monospace or proportional spacing, strike wobble, key pressure |
| **Edit** | Glyph workbench: nudge baselines, resize, stretch, compare against neighbors |
| **Fill** | Generates missing digits, symbols, and accents in a style matched to your letters |
| **Download** | Exports a TrueType font with your name, license, and version baked in |

## Runs entirely in your browser

No servers, no AI, no accounts. Every step (detection, tracing, glyph generation, font building) is plain JavaScript running on your own device. Your scans never leave your computer. The only network request is to Google Fonts, used as style references for filling in missing characters.

## Run it

Open `index.html` in a browser. That's it. No install, no build step.

To host it, push the repo and turn on GitHub Pages.

## Credits

Made by [Gianna Crisha Saludo](https://giannacrisha.com).
