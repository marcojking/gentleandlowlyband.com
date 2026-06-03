# gentleandlowlyband.com

Official site for **Gentle & Lowly**, the music sub-brand of the Worship
Music & Arts Club at Penn State. Lightweight static site — no build step,
no framework. Open `index.html` and go.

Built on the WM&A Design System (Gentle & Lowly variant): espresso canvas,
cream ink, amber `&`, Cormorant Garamond italic + Source Sans 3. Fonts are
bundled locally in `/fonts` (offline-safe, no Google Fonts call).

## Structure

```
index.html        Single-page site: hero billboard + EP hub + footer
css/styles.css    All styling + brand tokens (mirrors the design system)
fonts/            Source Sans 3 + Cormorant Garamond variable TTFs
img/
  peace-like-a-river.jpg   Single cover / hero atmosphere (DSC09113_cropped)
  your-son-before-me.jpg   EP cover (DSC09144)
  notehead-ripples-white.svg  Favicon (brand-neutral mark)
presave/index.html  Portable /presave → DistroKid fallback (any host)
vercel.json       Server-side /presave redirect + clean URLs (Vercel)
_redirects        Server-side /presave redirect (Netlify)
```

## The /presave vanity URL

`/presave` redirects to the DistroKid HyperFollow for the EP. Three layers,
so it works wherever you host:

- **Vercel** → `vercel.json` issues a 307 before any file is served.
- **Netlify** → `_redirects` issues a 302.
- **Any other host / local file** → `presave/index.html` does a meta-refresh
  + JS `location.replace`.

To repoint it, change the URL in **all three** files (each is commented).

## Updating through the waterfall release

Everything that changes between now and the July 5 full drop is marked with
`TODO ▸` comments. The two recurring jobs:

1. **Add the single's streaming link.** The "Listen" CTA currently points at
   the pre-save. Set the real smartlink once in `index.html` →
   `LISTEN_URL` (top of the inline script). Every "Listen" button uses it.

2. **Unlock a track when it releases.** In `index.html`, find the track's
   `<li>` and:
   - change `track--locked` → `track--live`
   - give the inner `<a>` a real `href` (or use `data-listen-link`)
   - swap the lock icon block for the `.track__play` circle (copy track 1)
   - fill in the real title (tracks 2 & 3 are placeholders: "Track two/three")
   - bump the progress: edit `.ep__progress .bar > span { width }` in
     `css/styles.css` and the "1 of 3 released" copy.

The countdown ("July 5" → "N days" → "Out now") updates itself from the
`DROP` date in the script.

## Local preview

Open `index.html` directly, or serve the folder:

```bash
npx serve .        # then visit the printed URL; test /presave
```
