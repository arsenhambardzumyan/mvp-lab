# Video-clips landing — deploy to GitHub Pages (owner, ~5 min, $0)

The page is final in `landing/video-clips/index.html` (plain HTML, no build step,
no JavaScript). LemonSqueezy checkout links in it were verified live on 2026-11-10
in a headless Chromium: both loaded full checkout pages with correct titles and
prices ("5 short vertical clips…" $99, "12 short vertical clips…" $199).
CLI HTTP checks 404 on `/checkout/*` — that is LemonSqueezy bot-filtering, not a
dead link. Verify in a real browser iff needed.

## What only the owner can do (agents cannot push)

1. Create a public repo, e.g. `video-clips-landing`, on the GitHub account.
2. Push just this folder:
   ```bash
   git init /tmp/video-clips-landing && git -C /tmp/video-clips-landing checkout -b main
   cp ~/ai-company/landing/video-clips/index.html /tmp/video-clips-landing/index.html
   cp ~/ai-company/landing/video-clips/README-OWNER-DEPLOY.md /tmp/video-clips-landing/
   git -C /tmp/video-clips-landing add . && git -C /tmp/video-clips-landing commit -m "video-clips landing"
   git -C /tmp/video-clips-landing remote add origin https://github.com/<owner-username>/video-clips-landing.git
   git -C /tmp/video-clips-landing push -u origin main
   ```
3. Repo Settings → Pages → Source: `Deploy from a branch` → branch `main`,
   folder `/ (root)` → Save.
4. Live URL: `https://<owner-username>.github.io/video-clips-landing/`.

## Before counting this as done

- [ ] The live URL opens (http → https redirect works)
- [ ] "Order 5 clips" opens the LemonSqueezy checkout with price 99
- [ ] "Order 12 clips" opens the checkout with price 199

## Rollback

- Repo Settings → Pages → Source: Change source → set to `None` — the URL stops
  serving immediately, no data loss.
- Or archive/delete the repo (same effect; the local copy stays in this repo).

## After the URL is live

Post the URL in the ITF-188 comment (acceptance asks for the live URL list).
Phishing-economics note: the checkout domain (lemonsqueezy.com) is separate from
the page domain (github.io), same as every other company landing — no action needed.
