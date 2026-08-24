# Site context for Claude Code

This is Grace Jiang's personal website: a single-file, minimalist, old-school personal
site (`index.html`) hosted free on GitHub Pages at `<username>.github.io`, with a
custom domain `gracejiang.net` pointed at it via the repo's `CNAME` file (DNS records
live with the domain registrar, outside this repo — `gracej.org` was the original plan
but its DNS was never pointed here; `gracejiang.net` is what's actually live). Please
read this before making changes, and follow it the same way you'd follow a style guide.

## Hard constraints — do not deviate without being asked

- **Single `index.html`** — CSS inside `<style>`, JS inside `<script>`. No separate
  `.css`/`.js` files, no build step, no frameworks (no React, no Bootstrap).
- **GitHub Pages compatible** — relative asset paths only (`images/...`, `videos/...`,
  `trip-reports/...`), no server-side anything.
- **Asset filenames are case-sensitive on GitHub Pages** even though this is usually
  authored on Windows, which isn't. A reference/file case mismatch (e.g. `.mov` vs
  `.MOV`) works fine locally and silently 404s once live — this has actually happened
  (`rubens_tube.MOV` vs a `.mov` reference). When adding or referencing an asset,
  double-check the on-disk filename case matches the `src`/`href` exactly.
- **Make the smallest reasonable edit.** Don't redesign or reformat unrelated sections
  when asked for a small change.
- **Never replace existing content with placeholder comments** like
  `<!-- existing content preserved -->`. If something needs to move or be hidden,
  actually keep the real markup (see the EE Projects section for the pattern: it's
  wrapped in an HTML comment, not deleted, so it can be restored later).

## Working style — stay focused, don't rabbit-hole

- **This is a zero-build static site on purpose.** Don't install or reach for new
  tooling (npm/node, chromium-cli, headless browsers, image libraries, etc.) to verify
  a change unless explicitly asked to. If something isn't obviously working, apply the
  most likely fix directly and have the user confirm in their own browser, rather than
  standing up infrastructure to prove it first.
- **Diagnose in a few steps, then act.** If a bug investigation is several tool calls in
  without a clear answer, stop investigating and apply the most likely fix instead of
  building more verification harnesses (test-copy HTML files, screenshot scripts, etc.)
  for what's usually a small CSS/layout issue. Cheap, reversible fixes don't need proof
  before applying — the user can eyeball the real page after a push.
- **When the user redirects mid-task, drop the current approach immediately.** A steer
  like "just do X" or "refocus" means stop the current path now, not finish the
  tangent "just to be sure" first.
- **Match effort to blast radius.** No build pipeline, no tests, easy to revert — most
  changes here are cheap to try. Don't over-engineer verification for something the
  user can check themselves in a few seconds.
- **Clean up scratch/test files you create for debugging** (temp HTML copies, staging
  folders) — don't leave them in the repo or scratchpad past the task that needed them.

## Aesthetic

- Minimalist, slightly old-school / personal-web feel — not a modern portfolio
  template. No gradients, no rounded "card" UI, no hero sections.
- White background, `Georgia, serif` font, black borders, chunky boxes with a flat
  drop-shadow (`box-shadow: Npx Npx 0 var(--shadow)`), classic blue links.
- Narrow centered content column, `max-width: 760px` (`--maxw` CSS var).
- Muted/earthy accent colors per section, used as a colored vertical stripe (10px)
  on both the nav tile and the matching section:
  - EE Projects: `#2E7D32` (currently hidden, see below)
  - Trip Reports: `#00695C`
  - Misc Projects: `#8B4513`
  - Reading: `#1E3A8A`
  - About: `#5A5A5A`
- Keep spacing airy but compact — don't blow out whitespace. Current rough values:
  sections `margin-top: 40px` / `padding-top: 20px`; years within a section ~24px
  apart; project cards ~14px vertical margin.

## Structure / current state

- **Header**: name ("Grace Jiang") + one-line welcome.
- **Nav**: "Skip to section:" label + a grid of tile links (`.tiles` / `.tile`), one
  per section, order Trip Reports, Misc Projects, Reading, About, plus EE Projects.
  **The entire `<main>` nav block is currently wrapped in `<!-- -->` and hidden** —
  temporary, uncomment when ready to bring section-jump nav back. Tiles show **title
  only**, no blurb underneath (blurbs were intentionally removed).
- **EE Projects**: hidden from public view — both the nav tile and the full section
  are wrapped in `<!-- -->` comments, not deleted. Uncomment both together when ready
  to publish. Content is grouped by year (`.year` divs with `.year-heading`).
- **Reading** and **About**: also currently hidden the same way (nav tile + section
  wrapped in `<!-- -->`, not deleted) — temporary, uncomment each pair together when
  ready to publish. Placeholder content only, not yet written.
- **Trip Reports** (was "Hiking" — renamed everywhere: id, CSS class/var, folder):
  homepage section is a `.trip-grid` of `.trip-box` link-tiles (same visual language
  as the main nav tiles: border, drop shadow, teal stripe), positioned first, above
  Misc Projects. Each box links to a per-trip HTML page under the `trip-reports/`
  folder. Trip pages are self-contained (own `<style>` block, matching site aesthetic:
  Georgia serif, black borders, teal accent), with a back link to `#trip-reports` at
  top and bottom. Photos for a trip live under `trip-reports/images/<trip-slug>/` as
  resized/compressed JPEGs (originals are typically phone photos/HEIC — convert HEIC
  to JPEG and strip EXIF/GPS metadata before publishing, since exact cave/trailhead
  locations are often intentionally not shared in the caving community). Expect many
  trips over time, added incrementally.
- **Misc Projects**: grouped by year, uses `.project-card` (thumbnail + text). Two
  2018 entries (MasSpec Pen, two-photon microscopy) intentionally share one "2018"
  year heading rather than repeating it. **MasSpec Pen thumbnail is currently broken**
  — `index.html` references `images/masspec.jpg` but the file was never added to the
  repo; needs the actual photo dropped into `images/` before it'll show.
- **Photo/video cards**: 120×120px square thumbnails, black border, `object-fit:
  cover`. Images sit in a `.thumb-wrap` div (needed because hover overlays can't be
  pseudo-elements on `<img>` directly). Hover = semi-transparent white overlay, no
  resizing. Click = lightbox with dark page overlay, image/video scaled to fit within
  90vw/90vh (preserves aspect ratio, no forced-width overflow on portrait photos);
  Escape or clicking the overlay closes it. Video thumbnails use the same square format, no
  native browser controls in the thumbnail, small (~24px) dark translucent play
  button bottom-right; click opens the same lightbox with real controls + autoplay.
- **Footer**: single "↑ Back to top" link (only one, at the very end — not repeated
  per section), auto-updating copyright year via JS, "Hosted on GitHub Pages."
