# Prima Agro Tech — Website (v1 handoff)

A custom-coded, bilingual (EN/ID) rebuild of primaagrotech.com, built from the
`PAT_Website_Visualization_Brief.docx` design brief and `WebsiteFlow+ContentPlan.pdf`
sitemap. Plain HTML/CSS/JS — no build step, no framework — so it can be hosted
anywhere.

## What's here

```
index.html              Homepage
solutions.html          Solutions hub (search + type/crop filters)
product.html?slug=...   Product detail (data-driven from data/products.json)
about.html               About Us
our-sciences.html        6-stage R&D journey, links to microbe pages
facilities.html           R&D lab + production
sustainability.html       ESG / compliance framing
testimonials.html         Cerita Tani videos + farmer quotes
career.html                Field agent recruiting page
contact.html                Contact form + office details
microbe.html?slug=...      Organism detail (data-driven from data/microbes.json)
css/style.css               Full design system (brand palette, type, components)
js/main.js                   Nav, language toggle, filters, carousels, data rendering
data/products.json            27 products mapped to the 5 solution categories
data/microbes.json             8 organism profiles
```

## 1. Hosting — zero backend required

This is a static site. Upload the whole `prima-agro-tech/` folder to any of:
- **Netlify / Vercel / Cloudflare Pages** — drag-and-drop the folder, done, free tier is enough.
- **Any shared web host / cPanel** — upload via FTP into `public_html/`.
- **GitHub Pages** — push to a repo, enable Pages on the `main` branch.

There's no `npm install`, no build step — the browser reads the files directly.

## 2. IMPORTANT — fabricated regulatory data, replace before launch

`data/products.json` was generated to demonstrate the product-detail template
end to end. The product names, benefit copy and descriptions come from PAT's
real published solutions page. **But the following fields per product are
placeholder/invented for layout purposes and are NOT real:**
- `registration` (Kementan-style registration numbers)
- `trial` (field trial location, partner, duration, outcome %)
- `certifications` assigned per product
- `application` dosage/method/timing rows

These look like real regulatory and technical data and **must be replaced
with your actual registration numbers and verified trial data before this
site goes live** — publishing invented registration numbers for regulated
agricultural inputs is a compliance risk, not just a content gap.

## 3. Before you launch — content that needs real material

**a) Photography.** Per the brief ("real photography only — minimum stock/AI
images"), no photos are included. Every image slot is a styled placeholder
(look for the small camera-icon caption, e.g. "Field photography — Central
Java rice trial"). Replace each `<div class="photo">...</div>` block with a
real `<img src="images/your-photo.jpg" alt="...">` inside it. Suggested shots
are already captioned in the HTML so you know what to shoot/source for each slot.

**b) Testimonials.** The quotes on the homepage and Testimonials page are
clearly tagged "Sample quote — pending verified testimonial." Swap in real
farmer/dealer/plantation quotes (with permission) before launch, and remove
the sample tag.

**c) Contact form.** `js/main.js` currently makes the contact form and the
"submit your story" form open a pre-filled email (zero backend needed to
demo). For production, wire `#contactForm` to a real backend — the two
easiest options:
- [Formspree](https://formspree.io) — add `action="https://formspree.io/f/yourid"` to the `<form>`, remove the JS override.
- [EmailJS](https://www.emailjs.com) — client-side email sending, no server needed.

## 4. WhatsApp number

The floating WhatsApp button and CTA buttons use `+62 852-8379-0848` (pulled
from the current primaagrotech.com site). Update `WA_NUMBER` at the top of
`js/main.js` if that's not the right sales number.

## 5. Adding or editing products

Products are entirely data-driven — edit `data/products.json`, no HTML
changes needed. Each entry needs: `slug`, `name`, `category` (one of
`bio-fertilizers`, `bio-fungicides`, `bio-insecticides`, `soil-remediation`,
`nutrition`), `crops` (array — use `Paddy`, `Chilli`, `Tomato`, `Potato`,
`Corn`, `Oil Palm`, `Sugarcane`, `Banana` to match existing filters),
bilingual `benefitEn/Id` and `descriptionEn/Id`, `organism`,
`formulationType`, `shelfLife`, `registration`, `application` (array of
dosage rows), `trial` (field trial data), and `certifications`.

Adding a product automatically makes it appear in the Solutions grid, its
own detail page at `product.html?slug=your-slug`, and any "related products"
lists — no other file needs touching.

Same pattern for `data/microbes.json` (organism pages linked from Our Sciences).

## 6. Design system reference

All brand colours, type pairing and component rules from the visualization
brief are implemented as CSS variables at the top of `css/style.css` —
change a colour once there and it updates everywhere. The microbe-dot motif
(list bullets, carousel dots, the Our Sciences connecting thread) rotates
through Microbe Green → Spore Yellow → Amber Gold automatically; no manual
colour-picking needed when adding new list items or steps.

## 7. Bilingual content

Every piece of copy is written twice inline, e.g.:
```html
<span lang="en">English copy</span><span lang="id">Salinan Indonesia</span>
```
The toggle in the top nav swaps a class on `<html>` that shows/hides these
via CSS — no page reload, and the choice persists across pages via
`localStorage`. When adding new copy, always write both spans.

## 8. What's NOT included yet (flagged intentionally)

- Real photography (see above)
- Verified testimonials (see above)
- A working form backend (see above)
- Downloadable PDFs (catalogue, spec sheets, SDS) — buttons are wired up and
  waiting for real files; point their `href` at the actual PDFs.
- Cerita Tani video embeds — currently placeholder cards on the Testimonials page.
- Google Maps embed on the Contact page — currently a placeholder block.

Everything else — layout, animation, bilingual toggle, product/microbe data
rendering, filtering, responsive behaviour — is fully functional today.
