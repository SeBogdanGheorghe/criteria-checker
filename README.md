# GitHub Pages wrapper — Availability Criteria Checker

`index.html` embeds the Apps Script web app in a full-screen iframe, so the
address bar always shows the short `github.io` URL instead of the long
`script.google.com/...` one. A small "Blank page? Sign in & open directly"
pill in the bottom-right corner covers users who aren't signed in to Google
yet (Google refuses to show its login screen inside iframes).

## Before publishing — redeploy the Apps Script app once

The wrapper only works if the app allows being iframed. `Code.gs` (version
0.93+) already includes `setXFrameOptionsMode(ALLOWALL)` in `doGet()` — copy
the updated `Code.gs` into the Apps Script editor, then
**Deploy → Manage deployments → ✏ Edit → Version: New version → Deploy**.
The exec URL stays the same.

## Publish on GitHub Pages (~5 minutes)

1. Create a **public** repository, e.g. `criteria-checker`, on github.com
   (free accounts can only serve Pages from public repos — fine here, the
   page contains no secrets and the tool itself still requires the
   @secretescapes.com Google login).
2. Upload `index.html` to the repository root (GitHub web UI: **Add file →
   Upload files**).
3. In the repo: **Settings → Pages → Build and deployment**:
   - Source: **Deploy from a branch**
   - Branch: **main**, folder **/ (root)** → **Save**
4. Wait ~1 minute. The site appears at:
   `https://<your-username-or-org>.github.io/criteria-checker/`
5. Share that link. Done — the long URL never appears in the address bar.

## If the exec URL ever changes

A new Apps Script *deployment* (as opposed to a new *version* of the existing
one) gets a new exec URL. If that happens, update the two `script.google.com`
URLs in `index.html` (the iframe `src` and the fallback link) and push —
the github.io link everyone uses stays the same.

## Notes

- Users already signed in to their work Google account load the tool
  seamlessly. In a fresh browser/incognito, the frame stays blank — the
  fallback pill opens the tool directly in a new tab, which triggers the
  normal Google sign-in; after that, the wrapper works too.
- `ALLOWALL` means any site could technically iframe the app. The data is
  still protected — every request inside the frame is authenticated against
  @secretescapes.com accounts.
