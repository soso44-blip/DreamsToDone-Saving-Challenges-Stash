# Stash (PWA)

The web app build of Stash, hosted on GitHub Pages.

**This deployment is unlisted.** It serves the full product, so the URL is meant
to be shared with buyers only. It carries `noindex, nofollow` and a `robots.txt`
that disallows everything, but a URL someone guesses or shares still works.
Do not link to it from the shop, Pinterest or the site.

## Files

| File | What it does |
| --- | --- |
| `index.html` | The app. Built from the customer file, do not edit here. |
| `manifest.webmanifest` | Name, icons, colours, standalone display. |
| `sw.js` | Service worker. Caches the app so it opens offline. |
| `icons/` | Home screen icons, including maskable versions for Android. |
| `screenshots/` | Shown in the Chrome install dialog. |
| `robots.txt` | Asks search engines to stay away. |
| `.nojekyll` | Stops GitHub Pages running Jekyll over the files. |

## Publishing

1. Push this folder to the repository root on the `main` branch.
2. Settings, then Pages, then set Source to `Deploy from a branch`, branch `main`, folder `/ (root)`.
3. Wait for the green tick, then open the URL. It will look like
   `https://<your-username>.github.io/<repo-name>/`.

Every path in here is relative, so the bundle works at any repo name without changes.

## Updating the app

1. Rebuild with `python3 build-pwa.py` from the parent folder.
2. **Bump `CACHE_VERSION` in `build-pwa.py` first.** If you skip this, people who
   already opened the app keep the old cached copy and never see the change.
3. Commit and push. Returning visitors get a small "A new version is ready" bar.

## Notes

- Saved progress lives in the browser under `dreamstodone.stash.v1`, same as the
  file version. It is per browser and per device, so the transfer code in the
  settings panel is still how someone moves between devices.
- The app was already offline capable as a single file. The service worker is
  what lets it open from a home screen icon with no connection at all.
- iOS does not support install prompts, so the in app card tells iPhone users to
  use Share, then Add to Home Screen. Android and desktop Chrome get a button.
