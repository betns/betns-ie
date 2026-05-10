# Blessington Educate Together — Hugo site

A static rebuild of <https://www.educatetogether-blessington.ie/wp/>, generated
from the WordPress REST export under `../blessington-et-export/` and intended
for hosting on GitHub Pages.

## Quickstart

```bash
hugo server -D
```

Visit <http://localhost:1313/>. Hugo extended ≥ 0.128 is recommended (the
GitHub Actions workflow pins 0.139.4).

## Editing content

Pages live under `content/` as page bundles (`index.md` per page, `_index.md`
for sections). Front matter is TOML; the most useful fields:

| field            | purpose                                                 |
|------------------|---------------------------------------------------------|
| `title`          | shown in the page header and `<title>`                  |
| `weight`         | sort order in section listings and dropdowns            |
| `aliases`        | redirects from old WP URLs (`/wp/<slug>/`)              |
| `featured_image` | path under `static/uploads/`; rendered above the body    |

Top-level navigation is configured under `[[menu.main]]` in `hugo.toml`.

### Image layout — staying in markdown

Editors don't need raw HTML for common image treatments. Append a `#variant`
fragment to the image URL and the render hook at
`layouts/_default/_markup/render-image.html` picks the right wrapper + class
(defined in `layouts/_default/baseof.html`):

| Markdown                                  | Effect                                          |
|-------------------------------------------|-------------------------------------------------|
| `![alt](src)`                             | plain inline image, capped at column width      |
| `![alt](src#banner)`                      | full-width hero across the column (max 260 px tall) |
| `![alt](src#strike)`                      | right-floated 350 px hero (homepage style)      |
| `![alt](src#icon)`                        | inline icon (sits next to text in lists/prose)  |
| `![alt](src#thumb)`                       | left-floated 220 px thumb that text wraps around |
| `![alt](src#center "Optional caption")`   | block-centred image; title becomes a caption    |

The `#fragment` is invisible to browsers — the image still resolves correctly
even if the render hook is absent. The converter auto-tags obvious cases
(images inside `<figure class="strike-image">` → `#strike`, images at the
start of a list item → `#icon`, images whose alt or filename contains
"banner" → `#banner`); editors can override or add fragments as needed.

When an image carries pixel dimensions in the WP source (`style="width:535px"`,
`width="464"`, etc.), the converter passes it through as raw HTML rather than
losing the sizing — the variant system above is for layout-class hints, not
for pixel-perfect overrides.

## Deploying to GitHub Pages

1. Push this directory to a GitHub repository.
2. In the repo settings → **Pages**, set the source to **GitHub Actions**.
3. Push to `main`. The `Deploy Hugo site to Pages` workflow at
   `.github/workflows/hugo.yml` will build and publish.

The workflow injects the right `baseURL` from the configured Pages URL, so
the placeholder `https://example.com/` in `hugo.toml` only matters for local
preview.

## Regenerating from the WP export

If the WordPress source is re-exported into `../blessington-et-export/raw/`,
rerun the converter and recopy media:

```bash
/app/python/source_code/.venv/bin/python3 scripts/convert.py
cp -r ../blessington-et-export/raw/media/wp-content/uploads/. static/uploads/
mkdir -p static/uploads/videos
cp ../blessington-et-export/raw/media/7TAJJOHq/virtual-open-day.mov static/uploads/videos/
```

The converter:

- walks `pages.json` and emits Markdown bundles under `content/`
- strips WP block comments, `<style>`/`<script>` tags, and Photon resize queries
- rewrites `https://...ie/wp/wp-content/uploads/` → `/uploads/`
- rewrites `https://...ie/wp/<slug>/` → `/<slug>/`
- resolves `?page_id=N` permalinks via the page id → slug map
- emits TOML front matter with `aliases` set to the original WP path

## What's stubbed / known gaps

- **Contact form.** The original page used a Jetpack contact form; this build
  shows a `mailto:` block instead. Plug in Formspree (or similar) by editing
  `content/contact-us/index.md` and adding a small form snippet.
- **Missing media.** 41 originals 404'd during the WP export; see
  `../blessington-et-export/raw/media_404s.txt`. References to those files
  remain in the markdown and will render as broken image/file links.
- **Featured images.** Set per-page via `featured_image` in front matter.
  None are seeded automatically by the converter.
- **`baseURL`.** Left as `https://example.com/` so the local preview works
  without configuration. The Pages workflow overrides this at build time.

## Source of truth

- WordPress export: `../blessington-et-export/`
- REST JSON: `../blessington-et-export/raw/json/pages.json`
- Rendered HTML mirror (used to recover the nav menu):
  `../blessington-et-export/raw/html/wp/index.html`
- Conversion plan: `../blessington-et-export/CONVERSION-PLAN.md`
