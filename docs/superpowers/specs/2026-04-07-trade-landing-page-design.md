# Trade Enquiry Landing Page — Design Spec

## Overview

A standalone landing page at `/trade` to attract and convert trade enquiries from restaurants, retailers, and distributors interested in stocking or using Mamma Gwenny's Caribbean seasonings.

**Approach:** Split Hero (Approach B) — form above the fold alongside the value proposition, with supporting content below.

## Target Audience

- Restaurants & takeaways (Caribbean restaurants, jerk shops, street food vendors, catering companies)
- Retail shops & supermarkets (independent grocers, Caribbean food shops, specialty retailers)
- Distributors & wholesalers (cash-and-carry, wholesale companies)

## Trade Offerings

- Bulk/wholesale pricing tiers (volume-based)
- Free sample packs for qualifying businesses

## Page Structure

### Section 1: Hero with Embedded Form

**Layout:** Two-column on desktop (60/40 split), stacked on mobile (content first, then form).

**Left column:**
- Label: "TRADE ENQUIRIES"
- Headline: "BRING AUTHENTIC CARIBBEAN FLAVOUR TO YOUR BUSINESS"
- Subtext: "Partner with Mamma Gwenny's for premium handcrafted seasonings. Bulk pricing available. Free sample packs for qualifying businesses."
- 3 mini trust badges (icon + text): "Handcrafted Recipes" | "Bulk Pricing" | "Free Samples"

**Right column:**
- Form card with white/light background, elevated with shadow
- Heading: "Request Trade Pricing"
- Fields:
  1. Name (text, required)
  2. Business Name (text, required)
  3. Email (email, required)
  4. Business Type (dropdown, required): Restaurant / Retailer / Distributor / Other
  5. Message (textarea, optional)
- CTA button: "Request Trade Pricing" (primary brand style)
- Helper text below button: "We'll respond within 24 hours"

**Background:** Tropical pattern with dark overlay, matching the main site's story section style.

**Form handling:** Netlify Forms (already configured in project via netlify.toml).

### Section 2: Product Range

- Heading: "OUR SEASONING RANGE"
- Subtitle: "8 handcrafted blends, available in bulk quantities"
- Grid of all 8 products: image, name, short description. No retail prices shown.
- Footer line: "Available in 100g retail packs and bulk catering sizes. Custom quantities available on request."
- Uses existing product data from `src/data/products.json`

### Section 3: Why Partner With Us

4 benefit cards in a responsive grid:

1. **Bulk Pricing** — "Competitive wholesale rates with tiered pricing based on volume"
2. **Free Samples** — "Try before you commit. Request a sample pack with your enquiry"
3. **Handcrafted Quality** — "Small-batch, freshly ground spices using heritage family recipes"
4. **Europe-Wide Delivery** — "Reliable shipping across Europe with flexible order schedules"

Each card: icon (Material Symbols) + heading + description.

### Section 4: Footer CTA

- Dark section with tropical pattern background (matching main site footer aesthetic)
- Heading: "READY TO STOCK MAMMA GWENNY'S?"
- Button that anchor-scrolls to the hero form: "Get In Touch"
- Standard site footer below for navigation consistency

## Technical Details

- **File:** `src/pages/trade.astro`
- **Layout:** Uses existing `BaseLayout.astro`
- **Styling:** Scoped `<style>` block within the page, using existing CSS custom properties from `global.css`
- **Data:** Imports from `src/data/products.json` for the product grid
- **Form:** Netlify Forms with `data-netlify="true"` attribute, form name "trade-enquiry"
- **No new dependencies required**

## Brand Consistency

- Uses existing design system: colors, typography (Tun Up De Ting headlines, Plus Jakarta Sans body), spacing tokens, shadows, border radii
- Tropical pattern background from `/images/patterns/tropical-pattern.png`
- Product images from `/images/products/`
- Logo from `/images/logo.png`
- Same header/footer as main site via BaseLayout

## Trust Signals (Soft)

Since formal certifications are TBD, the page uses:
- "Handcrafted" / "Family Recipes" / "Small-Batch" messaging
- Product photography showing quality packaging
- Consistent, professional brand presentation
- Quick response time promise ("within 24 hours")

Certification badges can be added to the hero trust bar when available.

## Success Metrics

- Form submissions (tracked via Netlify Forms dashboard)
- Page visits (via analytics when configured)

## Out of Scope

- Phone/WhatsApp contact option
- Private/white label offerings
- Online trade account / login portal
- Automated pricing calculator
