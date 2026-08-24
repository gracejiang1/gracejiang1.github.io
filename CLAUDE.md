# Site context for Claude Code

This is Grace Jiang's personal website: a single-file, minimalist, old-school personal
site (`index.html`) hosted free on GitHub Pages at `<username>.github.io`. Please read
this before making changes, and follow it the same way you'd follow a style guide.

## Hard constraints — do not deviate without being asked

- **Single `index.html`** — CSS inside `<style>`, JS inside `<script>`. No separate
  `.css`/`.js` files, no build step, no frameworks (no React, no Bootstrap).
- **GitHub Pages compatible** — relative asset paths only (`images/...`, `videos/...`,
  `trip-reports/...`), no server-side anything.
- **Make the smallest reasonable edit.** Don't redesign or reformat unrelated sections
  when asked for a small change.
- **Never replace existing content with placeholder comments** like
  `<!-- existing content preserved -->`. If something needs to move or be hidden,
  actually keep the real markup (see the EE Projects section for the pattern: it's
  wrapped in an HTML comment, not deleted, so it can be restored later).

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

- **Header**: name + one-line welcome.
- **Nav**: "Skip to section:" label + a grid of tile links (`.tiles` / `.tile`), one
  per section, in the order Trip Reports, Misc Projects, Reading, About (EE Projects
  tile is hidden, see below). Tiles show **title only**, no blurb underneath (blurbs
  were intentionally removed).
- **EE Projects**: hidden from public view — both the nav tile and the full section
  are wrapped in `<!-- -->` comments, not deleted. Uncomment both together when ready
  to publish. Content is grouped by year (`.year` divs with `.year-heading`).
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
  year heading rather than repeating it.
- **Photo/video cards**: 120×120px square thumbnails, black border, `object-fit:
  cover`. Images sit in a `.thumb-wrap` div (needed because hover overlays can't be
  pseudo-elements on `<img>` directly). Hover = semi-transparent white overlay, no
  resizing. Click = lightbox at ~50% screen size with dark page overlay; Escape or
  clicking the overlay closes it. Video thumbnails use the same square format, no
  native browser controls in the thumbnail, small (~24px) dark translucent play
  button bottom-right; click opens the same lightbox with real controls + autoplay.
- **Reading**: placeholder content, comes after Misc Projects.
- **About**: placeholder content, comes after Reading.
- **Footer**: single "↑ Back to top" link (only one, at the very end — not repeated
  per section), auto-updating copyright year via JS, "Hosted on GitHub Pages."
