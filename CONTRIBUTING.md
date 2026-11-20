# Contributing

Thanks for looking. Glyphwriter is small on purpose, and the constraints below are what keep it that way.

## Two hard rules

**Zero dependencies, zero build step.** No npm, no bundler, no framework, no CDN script tags. Plain HTML, CSS, and ES modules that run when you double-click `index.html`. If a change needs a package, it needs a different design.

**Everything stays client-side.** No backend, no API keys, no analytics, no uploads. A user's scan must never leave their machine. The only permitted network request is the existing Google Fonts CSS, which supplies the interface typeface and the reference faces that Fill missing measures against.

A pull request that breaks either rule will not be merged, however good the feature is.

## Running it

```sh
git clone https://github.com/giannacrisha/glyphwriter.git
open glyphwriter/index.html
```

That is the whole setup. Edit the file, reload the page.

If you need a local server for a change that touches module loading:

```sh
python3 -m http.server 8000
```

## Testing a change

There is no test suite yet, so test by hand before opening a pull request:

1. Load a scan, or use the demo sheet, and confirm Detect still finds every glyph.
2. Move each slider you touched to both ends and watch for crashes or blank glyphs.
3. Run Fill missing and check that generated characters still match your letters in weight.
4. Download the `.ttf` and install it. Type in a real app, not only in the preview.
5. Reload the page and confirm your session came back from `localStorage`.
6. Check light and dark mode.

Say in the pull request which of these you ran.

## Code style

- No em dashes anywhere, in copy, code comments, or commit messages.
- Interface copy: short labels over sentences. Lean on the visual.
- Colors come from the tokens on `:root`. Do not hardcode hex values, and keep the dark mode override in sync.
- Match the surrounding code. It is terse by habit, with short function names and few abstractions.
- `CLAUDE.md` documents how `index.html` is organized. Read the section you are about to touch, and update it if you move things.

## What is open

The backlog in `CLAUDE.md` lists what is planned, including a per-letter editor, OpenType alternates, kerning for proportional mode, and WOFF2 export. Open an issue before starting anything large so the approach can be agreed first.

Small fixes need no discussion. Send them.

## Reporting a bug

Include the scan if you can share it, the browser and version, what you expected, and what happened instead. Detection problems are almost always about the input, so a sample sheet is worth more than a description of one.
