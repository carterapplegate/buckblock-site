# buckblock-site

Public site for **Bison LLC** at `buckblock.app` — company landing page plus the Apple App Site Association (AASA) file that makes BuckBlock's NFC Universal Links launch the iOS app.

## Structure

```
.
├── index.html                           # company + product landing page
├── styles.css
├── _headers                             # Cloudflare Pages headers (AASA content-type, security)
├── assets/
│   └── applogo.png
└── .well-known/
    └── apple-app-site-association       # DO NOT EDIT without coordinating
```

## Do not break

- `.well-known/apple-app-site-association` is what makes NFC station taps launch the BuckBlock iOS app. If you edit it, keep the existing `appIDs` value (`6TA4BVYK2P.app.buckblock.ios`) and the `/s/*` path component — that's what the programmed tags point at.
- `_headers` forces `Content-Type: application/json` on the AASA. iOS will silently reject the file if it comes back as `text/plain` or `application/octet-stream`.

## Deploy

Served via Cloudflare Pages at `buckblock.app`. Push to `main` → Pages redeploys automatically.

Verify after a deploy:

```bash
curl -sI https://buckblock.app/.well-known/apple-app-site-association
# Expect: HTTP/2 200
# Expect: content-type: application/json
```

## Editing the landing page

- Copy: edit `index.html` directly (single page, no build step).
- Colors/typography: CSS variables at the top of `styles.css`. Palette matches the iOS app (indigo → violet gradient).
- Founders, company facts: search `founders-wrap` in `index.html`.
- Contact email: `hello@buckblock.app` — set up Cloudflare Email Routing on the domain so this forwards to a real inbox before publicizing.
