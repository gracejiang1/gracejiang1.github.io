# GitHub Pages Starter (No Build Tools)

Simple, fast starter for a personal site hosted on GitHub Pages.

## Quick Start

1. Create a new public repo on GitHub (you can name it `<your-username>.github.io` for a user site).
2. Upload these files to the repo root (`index.html` must be at the top level).
3. In the repo: **Settings → Pages** → Source = `main` branch → Save.
4. Your site appears at `https://<your-username>.github.io/` (or at `/repo/` for a project site).
5. (Optional) Add your custom domain in **Settings → Pages → Custom domain**. That creates a `CNAME` file.

### DNS for a Custom Domain

- Root `example.com` (A records):
  - 185.199.108.153
  - 185.199.109.153
  - 185.199.110.153
  - 185.199.111.153

- `www` (CNAME):
  - `www` → `<your-username>.github.io`

After DNS propagates, enable **Enforce HTTPS** in Pages settings.

## Customize

- Edit `index.html` text and links.
- Replace `/assets/favicon.svg` with your own.
- Update Open Graph meta tags in `<head>` of `index.html`.
- Hook up the contact form using Formspree or any static form backend.

## Notes

- `.nojekyll` disables Jekyll processing.
- `404.html` provides a friendly not‑found page.
