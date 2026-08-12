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

## Turning on the ambient sound
Open `index.html`, find `CONFIG` near the top of the `<script>`:

```js
const CONFIG = {
  ambientSoundUrl: "",       // <-- put a link to a looping mp3/ogg here
  backdropImageUrl: ""       // optional: swap the illustrated skyline for a photo
};
```

Put a link to your own looping ambience file here — either a file you add to
a `/sounds` folder in this repo (e.g. `"sounds/chauraha-loop.mp3"`) or any
direct hosted audio URL. Until you set this, the button will tell the visitor
it isn't configured yet, instead of failing silently.

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
