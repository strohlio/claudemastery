# Deploying Maya's Draw to Cloudflare Pages

The app is a single static file: `mayas-draw/index.html` (no build step, no dependencies).

## Do this on your own computer (full network access)

1. **Get the latest code**
   ```bash
   git clone https://github.com/strohlio/claudemastery.git
   cd claudemastery
   git checkout claude/daughter-creative-project-kzg873
   ```
   (Or if you already have the repo: `git fetch origin claude/daughter-creative-project-kzg873 && git checkout claude/daughter-creative-project-kzg873 && git pull`)

2. **Log in to Cloudflare once** (opens a browser to authorize)
   ```bash
   npx wrangler login
   ```

3. **Deploy** (creates the project the first time, updates it after)
   ```bash
   npx wrangler pages deploy mayas-draw --project-name=mayas-draw
   ```

   Wrangler will print the live URL, e.g. `https://mayas-draw.pages.dev`.

That's it. To publish a new version later, re-run step 3.

## Alternative: auto-deploy from GitHub (no CLI)

In the Cloudflare dashboard: **Workers & Pages → Create → Pages → Connect to Git**,
pick `strohlio/claudemastery`, then set:

- **Production branch:** `claude/daughter-creative-project-kzg873` (or whichever you merge to)
- **Build command:** *(leave empty)*
- **Build output directory:** `mayas-draw`

Save, and Cloudflare rebuilds automatically every time the branch is pushed.

## Tip: a friendlier URL

After the first deploy, in the project's **Custom domains** tab you can attach a
custom domain (e.g. `draw.yourdomain.com`) if you own one in Cloudflare.

---

Note: `mayas-draw/index.html` is a copy of `../draw.html`. If the app is edited in
`draw.html`, copy it over again with `cp draw.html mayas-draw/index.html` before deploying.
