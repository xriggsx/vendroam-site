# VendRoam Website — Working Rules

This is VendRoam's standalone marketing site (`vendroam.cunningcreekstudios.com`), hosted on GitHub Pages and deployed from the `main` branch root. **Google Play Console points at this domain's `privacy.html`, `terms.html`, and `delete-your-data.html`** — breaking those pages or their URLs breaks live Play Store compliance links, not just the marketing site.

## This repo deploys to TWO hosts

| Host | Serves | Configured by |
|---|---|---|
| GitHub Pages: `vendroam.cunningcreekstudios.com` | The main site and the legal pages | `CNAME`, `.nojekyll` |
| Netlify: `vendroam.netlify.app` | Every vendor follow link (`/v/<id>`) and the app-link verification files (`/.well-known/assetlinks.json`; `apple-app-site-association` is coming the same way) | `netlify.toml`, `wellknown/`, `.well-known/` |

- The Android app (live on Google Play) shares and verifies **`https://vendroam.netlify.app/v/<id>` only**, never a `cunningcreekstudios.com/v/` link. That's why GitHub Pages has no `/v/` handling or `404.html`, and doesn't need any.
- `netlify.toml`, `wellknown/` and `.well-known/` are **live, not leftovers**. Netlify rewrites `/v/*` to `v/index.html` and `/.well-known/assetlinks.json` to `wellknown/assetlinks.json`. Never remove, rename or "clean up" these files, or change their rewrites, without first checking what the Android app expects. Breaking them breaks every vendor's printed QR sign and follow link, and Android App Links verification.
- The `vendroam.netlify.app/v/...` placeholder in `sign.html` uses the correct domain. Leave it.

## Branching

- **Never commit or push directly to `main`.** `main` is what's live in production the moment it's pushed (GitHub Pages deploys straight from it — there is no staging).
- For every feature or fix, create a new branch off `main` first:
  - `git checkout main && git pull && git checkout -b <type>/<short-description>`
  - Branch prefixes: `feature/` for new functionality, `fix/` for bug fixes, `chore/` for maintenance/cleanup (e.g. removing unused images), `content/` for copy/legal-page text changes.
  - Name the branch after what it does, e.g. `fix/broken-delete-data-link`, `feature/deep-link-android-verify`, `content/update-privacy-policy`.
- Merge to `main` only after the change has been reviewed/tested — do not merge a branch into `main` in the same step as creating it unless the user explicitly says to ship directly.
- Before starting new work, always confirm the working tree is clean and branch off up-to-date `main` (don't stack unrelated work on a dirty tree or an old branch).

## Before touching hosting / DNS / Play Console URLs

Read `.well-known/assetlinks.json`, `wellknown/assetlinks.json`, `netlify.toml`, `v/index.html`, `privacy.html`, `terms.html`, and `delete-your-data.html` paths carefully before renaming or moving them — Play Console has these URLs hardcoded outside this repo. Confirm with the user before changing any URL path that Play Console might reference.

## Don't confuse this repo with the main studio site

This project (`F:\apps\vendroam-website`) is separate from the main Cunning Creek Studios site (`C:\dev2\admob_id-repo`, Netlify-hosted, `cunningcreekstudios.com`). Confirm which repo/domain you're in before making hosting or DNS changes.
