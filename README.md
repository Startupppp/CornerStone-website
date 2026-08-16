# CornerStone-website

The pre-launch site for **Cornerstone** — construction materials from our own dark stores in
60–120 minutes, plus verified labour to the same site. Launching across four Hyderabad zones.

One file, no build step, no dependencies: [`index.html`](index.html).

## Run it

```bash
python3 -m http.server 4321
```

Then open <http://127.0.0.1:4321>. Opening `index.html` directly from the filesystem works too.

## What's in it

A single self-contained page — all CSS and JS inline, no external requests, no fonts or scripts
fetched from a CDN. It will render correctly offline and from any static host.

**The model.** The background is raw WebGL2 (no three.js, no library): a 45,000-point cloud that
re-assembles into a different object for each section as you scroll — cornerstone block, structure
under construction, dark store, dispatch truck, zone network, crew, ledger, city grid — over a
blueprint ground grid. The point count drops to 24,000 on small screens, and the whole scene falls
back to a static CSS gradient if WebGL2 is unavailable.

`prefers-reduced-motion` is honoured throughout: no auto-rotation, no morph turbulence, no pointer
parallax, no reveal transitions.

## Before this goes public

**Replace the contact address.** It is a placeholder in one place — the `CONTACT` constant at the
top of the `<script>` block in `index.html`:

```js
var CONTACT = 'hello@cornerstone.co.in';
```

Both "Get early access" buttons build their `mailto:` from it.

## Publishing

Any static host works. For GitHub Pages: **Settings → Pages → Source: Deploy from a branch →
`main` / `(root)`**. Note this repository is currently private — Pages on a private repository
needs a paid plan, so either make the repository public or deploy the single file elsewhere.

## A note on the copy

Every claim on this page is one the product can actually keep: 60–120 minutes in four named zones,
08:00–20:00 IST, 24-hour returns, 10-minute cancellation, last-known rider position. The "What we
will not claim" panel is deliberate, and it is the part to be most careful about editing — it
names the things we have decided not to promise (10-minute delivery, all of Hyderabad,
second-by-second tracking, escrow). Keep new copy on the same side of that line.
