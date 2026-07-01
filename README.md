# Handoff: BTM Stainless Steel — Marketing Site + Product Catalogue

## Overview
A bilingual-ready (Thai-first) marketing website for **หจก. บัวทอง เมททัล (Buatong Metal Ltd., Part. — "BTM")**, a Thai fabricator of custom food-grade stainless-steel kitchen equipment (SUS304/316) for restaurants, hotels, and hospitals.

**Primary business goal:** a prospective customer (mostly arriving from Facebook/LINE, on a phone) should *understand* what BTM makes, *choose* products and exact sizes from the catalogue, and *request a quote* that lands directly with the factory. The site's spine is: **browse → select sizes → request quote (via LINE / phone)**.

Two pages:
1. **`BTM Website.dc.html`** — the main site: hero, "how it works" 3-step flow, the full 47-product catalogue with per-category cover banners, size selection, a persistent quote-request list (drawer + sticky bar), trust band, CTA strip, footer.
2. **`BTM About.dc.html`** — company story, capabilities, stats, and a "Find us" block with both phone numbers, LINE, email, and an embedded Google Map.

## About the Design Files
These are **design references authored in HTML** — working prototypes showing the intended look, content, and behavior. They are **not** production code to ship as-is.

They use a **"Design Component" (`.dc.html`)** format: a single file whose markup is a template and whose logic is a small React-like class, mounted at runtime by the bundled `support.js`. **Do not port `support.js` or the `.dc.html` runtime.** Instead **recreate the design in the target stack** using its normal component/styling patterns. For a public marketing/catalogue site, the natural choice is **Next.js (App Router) + React + Tailwind** (or any static-site framework).

Product data currently lives inline in `BTM Website.dc.html` as a JavaScript array (`buildData()`); in production this should become structured data — see **Data Model**.

## Fidelity
**High-fidelity.** Colors, typography, spacing, copy, and interactions are all final and intended — recreate faithfully. The one caveat is imagery: product line-drawings are cropped scans of BTM's printed catalogue sheets (clean line-art, "BTM" watermark deliberately kept, white background used with `mix-blend-mode:multiply`). Category cover banners and the About hero are currently empty drag-and-drop photo slots awaiting real photography.

---

## Design Direction
**Industrial-editorial.** Charcoal near-black surfaces + a single bold "welding-orange" accent, with technical "spec-plate" product cards (faint blueprint grid background, mono SKU tags, corner labels). Confident display type paired with a monospaced technical voice.

### Color tokens
| Token | Hex | Use |
|---|---|---|
| accent (welding orange) | `#e8552d` | logo tick, kickers, primary CTAs, SKU tags, "add" button, dots, highlights |
| ink | `#17181c` | hero/header/trust/footer surfaces, primary text, selected chips |
| ink-deep (footer) | `#101114` | footer base |
| page bg | `#ecebe7` | body background |
| panel | `#f4f3ef` | image panel behind drawings |
| card | `#ffffff` | product cards |
| LINE green | `#06C755` | LINE buttons |
| body text | `#5a584f` | paragraphs |
| muted | `#9a978d` / `#8a887f` | captions, mono labels |
| hairline | `rgba(0,0,0,.09)` | card borders, dividers |
| blueprint grid | `rgba(0,0,0,.05)` lines @ 20–22px | `.blux` card/hero image backgrounds |

Note: an alternate "steel" (`#5d7585`) accent exists as a leftover switch, but the **chosen and only palette is welding orange `#e8552d`**. Five other accent options (cobalt/emerald/crimson/amber/indigo) were explored and rejected.

### Typography (Google Fonts)
- **Anuphan** (400–800) — headings, product titles, big numerals, wordmark. Display weight 800 for hero/section titles.
- **IBM Plex Sans Thai** (300–600) — Thai body copy, buttons, labels.
- **IBM Plex Mono** (400–700) — SKUs, dimensions (mm), eyebrow/kicker labels, phone numbers. Letter-spacing ~.05–.2em on labels.

Import: `https://fonts.googleapis.com/css2?family=Anuphan:wght@400;500;600;700;800&family=IBM+Plex+Sans+Thai:wght@300;400;500;600&family=IBM+Plex+Mono:wght@400;500;600;700&display=swap`

### Radius, shadow, spacing
- Radius: cards `14px`, chips/buttons `8–11px`, pills `999px`, cover banners `16px`.
- Content max-width **1240px**, centered. Section side padding `24px` desktop / `18px` mobile.
- Product grid: `repeat(auto-fill, minmax(272px, 1fr))`, gap `18px`.
- Single responsive breakpoint at **820px** (grids collapse to 1–2 cols; header hides secondary items via `.hide-sm`).

### Logo
Inline SVG "table" icon (bronze/orange table-top bar + three legs) to the left of the **BTM** wordmark (Anuphan 800) with a small orange tick square. No raster asset — re-draw as a component and export SVG + favicon in production.

---

## Screens / Sections

### Main site — `BTM Website.dc.html`
1. **Sticky header** (charcoal): logo · nav (สินค้า / ขั้นตอน / เกี่ยวกับเรา) · phone pill · green **LINE** button · **คำขอราคา** (quote) button with a live count badge that opens the quote drawer.
2. **Hero** (charcoal, 2-col): kicker "STAINLESS FABRICATION · ตั้งแต่ 2545" · big title "ครัวสแตนเลส สั่งทำ **ทั้งใบ**" · description (TH + small EN line) · two CTAs (เลือกดูสินค้า / ขอใบเสนอราคา) · 3 stats (47 แบบ / 6 หมวด / 20+ ปี). Right: a spec-plate panel showing a featured drawing with "FIG. 01" and "SUS304" corner labels.
3. **How it works** (`#how`): 3 cards — 01 เลือกสินค้า → 02 เลือกขนาด → 03 ขอใบเสนอราคา (3rd card is inverted/charcoal).
4. **Catalogue** (`#catalogue`): header with search input; a **sticky category filter bar** (ทั้งหมด + 6 categories). Then, per category: a **cover banner** (drag-drop photo slot + dark gradient + number/title overlay) followed by the product card grid.
5. **Product card** (spec-plate): image area (`.blux` grid bg, 186px, drawing with `mix-blend-mode:multiply`) with a corner SKU tag and, when multiple size-variant drawings exist, a **dot carousel**; body has Thai title + English subtitle, a **size selector** (toggle chips — widths in mm, or full size strings for fixed items), an optional meta line (depth · height · option), and an **"เพิ่มลงคำขอ · N"** add button (orange when sizes are selected, disabled-grey otherwise).
6. **Trust band** (charcoal, 4 cols): SUS304/316 · Factory price · 20+ years · Made to order.
7. **CTA strip** (orange): "พร้อมสั่งทำครัวในฝันแล้วหรือยัง?" + phone + LINE buttons.
8. **Footer** (near-black): brand blurb · contact (both numbers + email) · menu links.
9. **Quote system** (see Interactions).

### About — `BTM About.dc.html`
Header (matches main site) · hero (intro + "20+ ปี / ช่างมืออาชีพ / ราคาโรงงาน" chips + a photo slot for factory/shopfront) · "What we do" (4 capability cards) · dark stats strip (SUS304/316 · 47 แบบ · 20+ ปี · รับประกัน) · **Find us** (contact card with both phone numbers, LINE, email, directions beside an embedded Google Map iframe with a tappable overlay) · footer. Linked both ways with the main site.

---

## Interactions & Behavior
- **Quote request (the key feature):** each product card lets the user multi-select sizes and "add to quote." Selections collect into a **quote list** shown in a slide-in **drawer** and a **sticky bottom bar** (with count). The list **persists across reloads via `localStorage`** (key `btm_quote`). The primary submit is **"ส่งทาง LINE"**, which builds a `https://line.me/R/msg/text/?<url-encoded message>` deep link containing every line item (`SKU · name · size มม.`) so the factory receives a clean itemized message; phone and "clear" are secondary. **Production opportunity:** replace/augment the LINE deep link with a real submission (LINE Messaging API, email, or DB + a simple admin view for the factory). This is the top backend feature to build.
- **Search:** case-insensitive over SKU + Thai + English name.
- **Category filter:** sticky chip bar; shows one category or all.
- **Size selection:** multi-select toggle chips per product; drive the add-button label/state.
- **Image carousel:** dot indicators per card cycle a product's size-variant drawings.
- **Category cover photos & About hero:** `<image-slot>` web components (drag-and-drop, persisted). In production these become normal `<img>`/`next/image` with real photography per category.
- **Contact:** `tel:0922303772`, `tel:0936656450`, `mailto:buatongm@hotmail.com`, LINE deep links. A green LINE button sits beside every phone number.
- **Responsive:** breakpoint 820px; charcoal header collapses secondary items.

## State (current, in-component)
`q` (search), `cat` (active category), `sel{}` (per-SKU selected sizes), `pi{}` (per-SKU carousel index), `quote[]` (line items, persisted), `drawer` (open/closed). Model these as normal component/store state in production and move product data out.

## Data Model
Products are defined in `BTM Website.dc.html` → `buildData()`: 6 category objects each with `items[]`. Two item shapes:
- **Width-based:** `{ sku, en, th, depth, height, widths:[…mm], opt? }` — a size = `width × depth × height (+opt)`.
- **Fixed-size** (`full:true`): `{ sku, en, th, full:true, sizes:[ "…strings…" ] }`.
- Optional `photo` (e.g. `TR-09` uses a real photo instead of a drawing).

Categories & counts: `01 work` (8) · `02 cabinet` (6) · `03 sink` (5) · `04 shelf` (13) · `05 range` (4) · `06 trolley` (11) = **47 SKUs**.

**Image convention:** primary drawing `catalog/d/<SKU>.png`; size variants `catalog/d/<SKU>-2.png … -6.png`. Variant counts are in the `vc()` map in the logic class. **Recommend extracting `buildData()` + `vc()` into a `products.json`** (or a headless CMS so BTM can self-edit).

## Assets (included in this bundle)
- `catalog/d/*.png` — 47 primary product line-drawings + size variants (~104 files). Cropped from scanned catalogue sheets; watermark retained; white bg for `mix-blend-mode:multiply`.
- `catalog/photos/cart-1.jpg` — one real product photo (Room Service Cart, TR-09).
- `image-slot.js` — the drag-and-drop photo-slot web component used for category covers + About hero (reference only; replace with real `<img>` in production).
- Fonts via Google Fonts (Anuphan, IBM Plex Sans Thai, IBM Plex Mono).
- Map: Google Maps embed iframe (exact pin) on About.
- Logo: inline SVG (see any header) — regenerate SVG + favicon.

## Business / Contact Facts (footer, contact, schema.org)
- Company: หจก. บัวทอง เมททัล · Buatong Metal Ltd., Part. (BTM)
- Address: 68 หมู่ 9 ต.บางคูรัด อ.บางบัวทอง จ.นนทบุรี 11110
- Phone: 092-230-3772 (คุณป้อม) · 093-665-6450 (คุณน้ำ)
- Email: buatongm@hotmail.com
- Google Maps pin: https://maps.app.goo.gl/rTsRaiRYpxPfNiDT9
- Est. ~2545 (2002); 20+ years; factory-direct pricing (no storefront); work quality guaranteed.

## Files (in this bundle)
- `BTM Website.dc.html` — main site (product data + all UI + quote system).
- `BTM About.dc.html` — about + capabilities + contact + map.
- `image-slot.js` — photo-slot component (reference).
- `support.js` — the design-component runtime (reference only; **do not port**).
- `catalog/d/` — product drawings (+ variants). `catalog/photos/` — real photo(s).

## Suggested production build
- **Next.js (App Router) + Tailwind.** Recreate the two pages as routes (`/` and `/about`).
- Product data in `products.json` or a headless CMS (so BTM edits products/sizes themselves).
- i18n scaffold (Thai default; the copy is ready to add an EN toggle later).
- `next/image` for optimized drawings + real category/hero photos.
- **A real quote-submission endpoint** (LINE Messaging API / email / DB + minimal factory admin) — keep the LINE deep link as a fallback.
- Open Graph tags + favicon (the BTM mark) so shared Facebook/LINE links preview well.
- Host on Vercel with a custom domain.

## What to build first
1. Scaffold Next.js + Tailwind with the tokens above; port the header/footer + hero.
2. Move `buildData()`/`vc()` into `products.json`; render the catalogue + category covers.
3. Rebuild the size-selection + quote-list (persisted) + LINE deep-link submit.
4. Add the About page + map.
5. Then: real photos, EN toggle, and a proper quote-submission backend.
