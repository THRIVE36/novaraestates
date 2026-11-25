# Novara Estates – Real Estate Website

A complete, responsive, multi-page real estate website (HTML, CSS, vanilla JavaScript – no build step, no dependencies).
Novara Estates and all listings, people and contact details are **fictional**.

## Run it
Double-click `index.html`, or serve the folder for a production-like check:
```
python3 -m http.server 8000     # then open http://localhost:8000
```

## Pages
| File | Purpose |
|---|---|
| `index.html` | Home: hero, quick search, featured listings, testimonials |
| `properties.html` | Listings with search, location / type / bedrooms / price filters, sorting, saved-only view |
| `property.html?id=p01` | Property details: gallery + lightbox, specs, features, WhatsApp & viewing links |
| `about.html`, `services.html`, `contact.html` | Company, services + FAQ, validated contact form |

## Project structure
```
css/styles.css          design tokens (colours, fonts) + all styles
js/data.js              SITE settings and the PROPERTIES list  <- edit most content here
js/main.js              shared header/footer, favourites, cards, toasts, reveal animations
js/home.js, properties.js, property.js, contact.js   page logic
images/                 hero, banners, section images, team/, properties/pNN-1..5 (WebP)
tools/optimize_images.py   converts/resizes your own photos to WebP
```

## Customise
* **Contact details, WhatsApp number, currency:** `SITE` in `js/data.js` (WhatsApp number is digits only, international format; the included number is fictional).
* **Listings:** add/edit objects in `PROPERTIES`. Each property needs five images named `images/properties/<id>-1 … <id>-5`; their captions come from the optional `gallery` array (defaults in `GALLERY_LABELS`).
* **Colours:** `:root` variables at the top of `css/styles.css` (forest green, cream, gold).
* **Page titles/descriptions:** `<title>` and `<meta name="description">` in each HTML file (the property page sets them dynamically).
* **Favourites** are stored in the browser's `localStorage`.

## Images
All images are bundled locally in `/images` as optimised WebP (about 2.6 MB in total), so the site works fully offline and makes no external requests.

| Files | Used for |
|---|---|
| `hero.webp`, `hero-800.webp` | Homepage hero (responsive `srcset`) |
| `banner-villa/pool/terrace.webp` | Page-header and call-to-action backgrounds |
| `properties/pNN-1…5.webp` | Gallery for listing `pNN`: main photo, living room, kitchen, bedroom, extra (pool / skyline / hall) |
| `about.webp`, `services.webp`, `services-2.webp` | About and Services sections |
| `team/*.svg`, `favicon.svg` | Illustrated team portraits and logo mark |

**Quality notes.** Most interior/exterior photos were cropped from small promotional collages (about 270–390 px wide) and upscaled 2× with light sharpening, so they look good at card and gallery size but are not large-format photographs. Several rooms repeat across listings. For a production site, replace them with your own photography.

**Replace images.** Keep the same file names and format, or set `imageExt` in `js/data.js` (`'webp'`, `'jpg'`, `'png'`) and update the few `images/...` paths written in the HTML files. To convert your own photos:
```
pip install pillow
python3 tools/optimize_images.py my-photos/ images/properties/ 1600 80
```
Recommended sizes: gallery images 1200–1600 px wide, hero 1600–2000 px wide, each under about 250 KB.

**Licensing.** See `LICENSES.md`.

## Contact form
Validation (name, email, optional phone, topic, 20+ character message, consent, honeypot spam trap) runs in the browser. There is no server, so after a valid submission the visitor gets a confirmation and a button that opens WhatsApp with the message pre-filled. To receive submissions by email, post the form to a service such as Formspree or your own backend in `js/contact.js`.

## Browser support
Current Chrome, Edge, Firefox and Safari.
