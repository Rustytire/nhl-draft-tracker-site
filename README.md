# NHL Draft Tracker — public site

This repo holds **only the published, self-contained static site** (`index.html`) —
a baked snapshot of the NHL Draft Tracker with no server, no database, and no
sensitive data. The code and data source-of-truth live in a **separate private
repo**; this repo exists purely to serve the site via GitHub Pages.

**What is safe here (by construction):** the snapshot is built by
`webapp/build_preview.py` in the private repo, which enforces the paywall data
policy — paywalled scouts' individual boards are never included (derived summary
only; coarse ranges in the aggregate). This file contains zero raw paid ranks
and no external references.

## Publish (one-time)

1. Create a **public** GitHub repo (e.g. `nhl-draft-tracker-site`).
2. Push the contents of this folder to `main`.
3. Repo **Settings → Pages → Source: Deploy from a branch → `main` / root**.
4. Site goes live at `https://<user>.github.io/<repo>/` (a minute or two later).

`.nojekyll` is included so GitHub serves the files as-is (no Jekyll build).

## Update after a data change

From the private repo:

```bash
python3 webapp/deploy_site.py     # rebuilds the snapshot, copies it to site/index.html
```

Then push this folder again (rebuild → commit → push).
