# Sales Architects

Source for the [sales-architects.nl](https://sales-architects.nl) website — a self-contained static site (no build step, no dependencies) covering:

- **What we do** — AI training, AI tools, website design, hosting, and SEO/GEO optimization
- **Projects** — a recap linking out to sites we've designed or built
- **Company details** — KvK number and a clear statement that we are *not* `salesarchitects.nl` (a separate, unaffiliated company with a similar name)

## Files

- `index.html` — the main site (home + projects), client-side routed via `#/` and `#/projects`
- `styles.css` — all styling
- `bedrijfsgegevens.html` — standalone company details page, its own real URL (for SEO and schema.org disambiguation from `salesarchitects.nl`)
- `sitemap.xml` — XML sitemap listing the two real, indexable URLs above
- `robots.txt` — points crawlers at the sitemap, blocks the dormant `/wp-admin/` and `/wp-includes/`
- `.htaccess` — sets `DirectoryIndex index.html index.php` (see "Hosting" below) plus static-asset caching headers
- `favicon.ico`, `favicon.svg` — the brand mark as a favicon; the SVG version switches color for dark browser tabs via `prefers-color-scheme`
- `apple-touch-icon.png` — 180×180 home-screen icon (dark background, since iOS doesn't handle transparency well)
- `og-image.png` — 1200×630 social share image, used by the Open Graph/Twitter Card tags in both HTML pages
- `CNAME` — legacy GitHub Pages custom-domain file, not currently used for hosting (see below)

## Hosting

The site is deployed by **FTP onto the existing PHP hosting (Vimexx)** — not GitHub Pages. An older WordPress install still lives on that same hosting account and is kept in place on purpose: other websites hotlink directly to images under `/wp-content/uploads/...`, and removing WordPress would break those links.

To serve this static site as the homepage while keeping WordPress's files (especially `wp-content/uploads/`) intact:

1. WordPress's root `index.php` is renamed to `index.php.bak`, so it's no longer picked up as the directory index.
2. WordPress's root `.htaccess` is renamed to `.htaccess.bak` and replaced with a minimal one:
   ```apache
   DirectoryIndex index.html index.php
   ```
3. `index.html`, `styles.css`, `bedrijfsgegevens.html`, `sitemap.xml`, `robots.txt`, `favicon.ico`, `favicon.svg`, `apple-touch-icon.png`, and `og-image.png` are uploaded to that same root via FTP, alongside the untouched `wp-content/`, `wp-admin/`, `wp-includes/`, and `wp-config.php`. (`.htaccess` replaces WordPress's own, as described above.)

Result:
- `sales-architects.nl/` serves this static site.
- `sales-architects.nl/wp-content/uploads/...` keeps serving the original images, so external hotlinks don't break.
- `sales-architects.nl/wp-admin/` still works, in case WordPress is ever needed again.
- Old WordPress permalinks (blog posts, pages) now 404 — expected, since that content is no longer in use.

Since WordPress stays reachable even though unused, keep its core and plugins updated (or deactivate what isn't needed) so it doesn't become a security liability.

No build tools or dependencies are required for the static files themselves — they're plain HTML/CSS.
