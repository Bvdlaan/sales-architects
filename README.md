# Sales Architects

Source for the [sales-architects.nl](https://sales-architects.nl) website — a single self-contained `index.html` (no build step) covering:

- **What we do** — AI training, AI tools, website design, hosting, and SEO/GEO optimization
- **Projects** — a recap linking out to sites we've designed or built

## Publishing with GitHub Pages

This repo is set up to be served directly by GitHub Pages:

1. In the repo settings, under **Pages**, set the source to the `main` branch, `/ (root)` folder.
2. The `CNAME` file already points Pages at `sales-architects.nl`.
3. At your DNS host (Vimexx), point the domain at GitHub Pages while keeping DNS management there:
   - **Apex domain** `sales-architects.nl` → four `A` records to
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - **www subdomain** (optional) → a `CNAME` record for `www` pointing to `bvdlaan.github.io`
4. Once DNS propagates, GitHub issues an HTTPS certificate for the domain automatically.

No build tools, dependencies, or server are required — it's a static HTML file.
