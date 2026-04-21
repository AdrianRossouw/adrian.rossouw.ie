# adrian.rossouw.ie

Personal site. Single static HTML file, no build step, no runtime dependencies beyond a Google Fonts link.

## Deploy (GitHub Pages)

Easiest path — a user/org site that serves from the root:

1. Create a repo named `<your-github-username>.github.io` (or any repo if you want a project-site URL).
2. Copy the contents of this `dist/` folder into the repo root:
   ```
   index.html
   CNAME
   .nojekyll
   ```
3. Commit and push to `main`.
4. Repo → **Settings → Pages** → set **Source** to `Deploy from a branch`, **Branch** = `main` / `(root)`.
5. DNS: point `adrian.rossouw.ie` at GitHub Pages.
   - For the **apex** (`rossouw.ie`) you'd use A records:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - For the **subdomain** `adrian.rossouw.ie`, a single `CNAME` record pointing at
     `<your-github-username>.github.io` is cleaner and what you want here.
6. Back in Pages settings, set the **Custom domain** to `adrian.rossouw.ie` and tick **Enforce HTTPS** once the cert provisions (a minute or two).

The `CNAME` file in this folder makes GitHub respect the custom domain on push.
`.nojekyll` disables Jekyll so no filenames get rewritten.

## Edit

Everything is in `index.html`. One file, one CSS block, a tiny scrollspy in vanilla JS.
No Node, no bundler, no framework at runtime.
