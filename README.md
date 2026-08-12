# चौराहा — Chauraha

## Changing the widget images
Every stall's picture is a real file in `/images`, referenced by path in the
`STALLS` array near the top of the `<script>` in `index.html`:

```js
{ id:'chai', ..., img:'images/chai.jpg', ... }
```

To change a stall's look, just replace that file in `/images` with your own
(same filename, or update the `img` path) — no code edit needed. Placeholder
images are already in there so the site looks right immediately; swap them
whenever you're ready. Recommended size: ~800x400px, landscape, jpg/webp.

If an image ever fails to load (missing file, bad URL), the card falls back
to a plain color block using that stall's `c1`/`c2` colors — it never breaks
the layout.

## The soundtrack
There's no button — the site always loads one fixed Spotify track as a
floating player, bottom-left. Change it any time in `CONFIG` near the top
of the `<script>`:

```js
const CONFIG = {
  spotifyTrackId: "62O5vcMfejaWFhHkll3ju5",  // swap this id to change the track
  backdropImageUrl: ""
};
```

Grab the id from any Spotify share link: `open.spotify.com/track/<THIS PART>?si=...`

One honest limitation, true of every website, not just this one: browsers
block audio autoplay-with-sound until the visitor has interacted with the
page at least once (a click, a scroll, a tap). No embed can override that —
it's a browser policy, not a Spotify or Chauraha setting. The player starts
the moment they click anywhere on the page, and Spotify's own controls
inside the embed let them pause or skip.

## Visiting a stall — no redirects
Clicking "Andar chalo" opens the destination site inline, inside the
chauraha, in a full-size in-site view — the visitor never leaves the page or
gets sent to a new tab automatically. A small "Naya tab mein kholo" link
stays available in the corner in case a particular site refuses to be
embedded (some sites set security headers — `X-Frame-Options` / CSP
`frame-ancestors` — that block being shown inside another site's page, as a
clickjacking protection; the chauraha can't override that from its side).
If chaitapri.wtf, saloon.wtf, or truckpemusic.online happen to set that
header, embedding will show blank there and the fallback link is the way
out — worth checking once you deploy this for real.

## Adding a new built-in stall
Add one object to the `STALLS` array with `id`, `hi`, `en`, `status`
(`"live"` or `"soon"`), `desc`, `open`/`close` hours (IST, 24h), `moods`
(an array of write-up lines — one is shown at random each time someone opens
the card), and `img` pointing at a file in `/images`. That's the whole API.

## "Apni Jagah" (visitor-added stalls)
Visitors can add up to 3 of their own stalls via the "+" tile. This is stored
in *their own browser* (`localStorage`), so it's personal to each visitor,
not shared publicly. If you want everyone's submissions visible to all
visitors, that needs a small backend/database instead — happy to help wire
that up if you want it.

## Hosting
- **GitHub Pages**: push this folder as a repo, enable Pages in
  Settings → Pages. Free, works with the relative `images/` and `sounds/`
  paths as-is.
- **Custom domain (e.g. a `.wtf`)**: buy from Porkbun or Namecheap, add a
  `CNAME` file with your domain to the repo root, point DNS at GitHub Pages
  per their current docs (`docs.github.com/pages`).
