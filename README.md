# CornerStone-website

The pre-launch site for **Cornerstone** — construction materials from our own dark stores in
60–120 minutes, plus verified labour to the same site. Launching across four Hyderabad zones.

No build step, no dependencies. [`index.html`](index.html) is fully self-contained; the policy pages
share [`policy.css`](policy.css).

| Page | File | Why it exists |
|---|---|---|
| Landing | `index.html` | The product |
| Contact us | `contact.html` | Razorpay activation |
| Pricing | `pricing.html` | Razorpay activation |
| Shipping & delivery | `shipping.html` | Razorpay activation |
| Cancellation & refunds | `refunds.html` | Razorpay activation |
| Terms & conditions | `terms.html` | Razorpay activation |
| Privacy policy | `privacy.html` | Razorpay activation |

All six policy pages are linked from the landing page footer, which is what Razorpay's automated
website check crawls.

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

## Before this goes public — required

### 1. Fill in the business details

The policy pages carry `[[TOKENS]]` where real legal details belong. They render in rust so an
unfilled one is impossible to miss. Nothing was invented — a payment processor uses these pages for
KYC, so they have to be your actual registered details.

| Token | What goes there |
|---|---|
| `[[LEGAL ENTITY NAME]]` | Registered company name, exactly as on the certificate of incorporation |
| `[[REGISTERED ADDRESS]]` | Full registered office address with pincode |
| `[[SUPPORT EMAIL]]` | A monitored support inbox |
| `[[SUPPORT PHONE]]` | A working phone number with STD/country code |
| `[[GRIEVANCE OFFICER NAME]]` | Named person, required under the IT Act and the E-Commerce Rules |
| `[[GSTIN]]` | 15-character GSTIN, or delete the row if not registered |
| `[[CIN]]` | 21-character CIN, or delete the row if not a registered company |

Replace across all files, then verify none remain:

```bash
grep -rn "\[\[" *.html
```

That command must print nothing before you submit the site to Razorpay.

### 2. Replace the contact address on the landing page

Separate from the tokens — the `CONTACT` constant at the top of the `<script>` block in
`index.html`:

```js
var CONTACT = 'hello@cornerstone.co.in';
```

Both "Get early access" buttons build their `mailto:` from it. Use the same address as
`[[SUPPORT EMAIL]]`.

### 3. Confirm these three claims are true for you

The policy pages state them as fact, so check each one before publishing:

- **Prices are inclusive of GST.** `pricing.html` says so. If you list ex-GST, change it there and in `terms.html`.
- **Refunds credited in 5–7 working days.** In `refunds.html`. Match it to what your gateway and bank actually do.
- **Labour cancellation is free up to 12 hours before.** In `refunds.html`. Set your real window.

## Publishing

Any static host works. For GitHub Pages: **Settings → Pages → Source: Deploy from a branch →
`main` / `(root)`**. Note this repository is currently private — Pages on a private repository
needs a paid plan, so either make the repository public or deploy the files elsewhere.

Razorpay requires the site to be served over **HTTPS**. GitHub Pages, Netlify, Vercel and
Cloudflare Pages all issue a certificate automatically.

## Razorpay activation

Razorpay runs an automated check against your primary website URL and looks for these pages:
Contact us, Terms and conditions, Privacy policy, Shipping policy, Cancellation and refunds, and
pricing information. All six exist here and are linked from the landing page footer.

Two things this repository cannot fix for you:

1. **The business name on the site must match the entity on your Razorpay KYC.** That is what
   `[[LEGAL ENTITY NAME]]` is for — a mismatch is a common rejection reason.
2. **Razorpay expects a live, functional site.** A pre-launch page with no catalogue and no
   checkout may draw a request for more information even with every policy page in place. The
   policy pages are necessary, not sufficient.

## A note on the copy

Every claim on this page is one the product can actually keep: 60–120 minutes in four named zones,
08:00–20:00 IST, 24-hour returns, 10-minute cancellation, last-known rider position. The "What we
will not claim" panel is deliberate, and it is the part to be most careful about editing — it
names the things we have decided not to promise (10-minute delivery, all of Hyderabad,
second-by-second tracking, escrow). Keep new copy on the same side of that line.
