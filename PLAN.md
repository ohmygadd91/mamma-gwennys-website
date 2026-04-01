# Mamma Gwenny's Website - Build Plan

## Project Overview
- **Brand:** Mamma Gwenny's Authentic Caribbean — Caribbean food & seasoning brand
- **Type:** E-commerce storefront
- **Stack:** Astro (static site generator) + Snipcart (commerce)
- **Hosting:** Netlify or Vercel
- **Shipping:** Europe-wide, EUR currency
- **Products:** 8 seasonings initially (Fish, All Purpose, Goat, Lamb, Beef, Chicken, Vegetarian, Jerk)
- **Reference site:** spicebox.co.uk (replicate design/structure, adapted for brand)

---

## Tech Stack
- **Framework:** Astro (static HTML, JS only for interactive islands)
- **Commerce:** Snipcart (2% fee, no monthly cost under $500/mo, handles cart/checkout/VAT/shipping)
- **Styling:** Custom CSS with CSS custom properties (no framework)
- **Interactivity:** Vanilla JS Web Components (cart drawer, mobile menu, carousels, sticky header)
- **Fonts:** Passion One (display), Dancing Script (script accents), Poppins (body) via Google Fonts
- **Forms:** Netlify Forms or Formspree
- **Deployment:** GitHub -> Netlify/Vercel auto-deploy

---

## Brand Color Palette

| Color | Hex | Usage |
|-------|-----|-------|
| Teal | #1a6b6a | Primary brand color, header, CTAs |
| Orange | #e8651a | Secondary, buttons, accents |
| Brown | #5c3a1e | Footer, dark sections |
| Terracotta | #8b4522 | Warm accent |
| Magenta | #a83279 | Accent (jerk product) |
| Gold | #d4a843 | Text accents, highlights |
| Cream | #fdf8f0 | Page background |

Each product also has its own color from the packaging.

---

## Directory Structure

```
/
├── public/
│   ├── fonts/
│   ├── images/
│   │   ├── products/
│   │   ├── hero/
│   │   ├── story/
│   │   ├── icons/
│   │   └── patterns/
│   └── favicon.ico
├── src/
│   ├── components/
│   │   ├── global/        # Header, Footer, AnnouncementBar, CartDrawer, MobileMenu
│   │   ├── home/          # Hero, FeatureCards, FeaturedProducts, Testimonials, OurStory
│   │   ├── product/       # ProductCard, ProductGrid, ProductGallery, ProductInfo
│   │   └── ui/            # Button, Icon, Accordion, Carousel
│   ├── layouts/
│   │   └── BaseLayout.astro
│   ├── pages/
│   │   ├── index.astro
│   │   ├── shop.astro
│   │   ├── products/[slug].astro
│   │   ├── about.astro
│   │   ├── contact.astro
│   │   ├── faq.astro
│   │   └── delivery.astro
│   ├── data/
│   │   └── products.json
│   ├── styles/
│   │   ├── global.css
│   │   ├── utilities.css
│   │   └── fonts.css
│   └── scripts/
│       ├── cart-drawer.js
│       ├── mobile-menu.js
│       ├── carousel.js
│       ├── sticky-header.js
│       └── announcement-bar.js
├── astro.config.mjs
├── package.json
└── netlify.toml
```

---

## Build Phases

### Phase 1: Foundation
1. Initialize Astro project
2. Set up directory structure
3. Create design system (CSS custom properties, fonts, base styles)
4. Create BaseLayout.astro (HTML shell, meta, Snipcart script)
5. Create products.json data file
6. Prepare/rename image assets

### Phase 2: Global Components
7. AnnouncementBar (rotating messages, teal background)
8. SiteHeader (two-row sticky, logo, nav, cart icon, scroll-aware)
9. SiteFooter (pattern background, 4-column, mobile accordions)
10. MobileMenu (slide-in drawer)

### Phase 3: Homepage
11. HeroBanner (full-width, heading, CTA)
12. FeatureCards (3-column: "Mixed by Hand", "Authentic Recipes", "Europe-Wide Delivery")
13. FeaturedProducts + ProductCard (carousel/grid with Snipcart buttons)
14. TestimonialsCarousel
15. OurStorySection (50/50 image + text)
16. Assemble homepage

### Phase 4: Shop & Product Pages
17. Shop page (ProductGrid, all products)
18. Product detail pages (dynamic [slug], gallery + info, Snipcart add-to-cart)

### Phase 5: Content Pages
19. About/Our Story page
20. Contact page (form via Netlify Forms)
21. FAQ page (accordion, structured data)
22. Delivery Information page

### Phase 6: Cart & Polish
23. CartDrawer (slide-in, Snipcart JS API integration, shipping progress bar)
24. Snipcart CSS overrides to match brand
25. Full purchase flow testing

### Phase 7: Testing & Deployment
26. Responsive testing (375px - 1920px)
27. Accessibility audit (WCAG AA)
28. Performance optimization (Lighthouse >90)
29. SEO (meta tags, structured data, sitemap)
30. Deploy to Netlify/Vercel
31. Configure custom domain + HTTPS
32. Switch Snipcart to production API key

---

## Homepage Sections (replicating spicebox.co.uk structure)

1. **Announcement Bar** — Teal background, white text, rotating messages
2. **Sticky Header** — Row 1: logo + icons (always visible). Row 2: nav links (hides on scroll down)
3. **Hero Banner** — Full-width, ~70vh, dark overlay, heading + CTA
4. **Feature Cards** — 3-column grid: "Mixed by Hand", "Authentic Recipes", "Europe-Wide Delivery"
5. **Featured Products** — "Most Popular" heading, 4-product carousel/grid
6. **Testimonials** — Teal background, rotating quotes with star ratings
7. **Our Story** — 50/50 image + text, "Read More" link
8. **Footer** — Dark brown + pattern background, 4 columns, payment icons

---

## Snipcart Setup

- Add CSS + JS from Snipcart CDN in BaseLayout
- Use `data-config-modal-style="side"` for built-in side cart (v1)
- Each product button needs: `data-item-id`, `data-item-name`, `data-item-price`, `data-item-url`, `data-item-image`
- `data-item-url` must match the actual product page URL (Snipcart crawls to validate)
- Currency: EUR
- Configure shipping zones, rates, VAT in Snipcart dashboard
- Use test API key during development, switch to production for go-live

---

## Responsive Breakpoints

```css
/* Mobile: default (0-639px) */
@media (min-width: 640px)  { /* Tablet */ }
@media (min-width: 1024px) { /* Desktop */ }
@media (min-width: 1280px) { /* Wide */ }
```

---

## Asset Preparation Needed

- [ ] Rename packaging JPGs to semantic names (fish-seasoning.jpg, etc.)
- [ ] Remove duplicate (1) files
- [ ] Extract tropical pattern as tileable PNG/SVG for header/footer backgrounds
- [ ] Extract Mamma Gwenny portrait as standalone transparent PNG for logo
- [ ] Create/source hero banner image(s)
- [ ] Create product mockup images (labels on jars/pouches) or style flat labels

---

## Go-Live Checklist

- [ ] Snipcart production API key
- [ ] Payment gateway configured (Stripe)
- [ ] Shipping rates and zones set
- [ ] EU VAT settings configured
- [ ] Order notification emails set
- [ ] Custom domain connected
- [ ] HTTPS verified
- [ ] Test real purchase end-to-end
- [ ] Sitemap submitted to Google Search Console
- [ ] Analytics set up
