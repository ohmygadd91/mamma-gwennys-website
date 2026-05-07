# Product Size Variants + Stockist Nav Link — Design

Date: 2026-05-07

## Goals

1. Let customers pick a size variant per product (100g Tub, 100g Packet, 4.08kg Bulk).
2. Switch the site's display currency from EUR to GBP.
3. Add a "Become a Stockist" link to the top nav pointing at the existing `/trade` page.

---

## 1. Product variants

### Data model (`src/data/products.json`)

Replace each product's `price` and `weight` fields with a `variants` array. `currency` flips from `EUR` to `GBP`.

```json
{
  "id": "fish-seasoning",
  "slug": "fish-seasoning",
  "name": "Fish Flavour Seasoning",
  "currency": "GBP",
  "variants": [
    { "id": "fish-seasoning-tub-100g",    "label": "100g Tub",    "price": 2.49,  "weight": 100  },
    { "id": "fish-seasoning-packet-100g", "label": "100g Packet", "price": 2.49,  "weight": 100  },
    { "id": "fish-seasoning-bulk-4kg",    "label": "4.08kg Bulk", "price": 38.99, "weight": 4080 }
  ],
  "description": "...",
  "shortDescription": "...",
  "image": "...",
  ...
}
```

All 8 products get the same three variants with the same prices.

### Shop card (`ProductCard.astro`)

- Single price → `From £2.49` (computed as min of variants).
- "Add to Cart" button → "View Options" link to `/products/<slug>`.
- Strip the inline Snipcart `data-item-*` attributes (no longer adding to cart from the card).

### Product detail page (`ProductInfo.astro`)

- Add a **size picker** above the price block — three pill-style radio chips, mobile-friendly.
- Default selection: `100g Tub`.
- Selecting a chip updates the displayed price and the Snipcart Add-to-Cart button's `data-item-id`, `data-item-name` (e.g. `Fish Flavour Seasoning — 100g Tub`), `data-item-price`, and `data-item-weight` live via JS.
- Quantity stepper, accordion sections, and existing layout are unchanged.

### Cart behavior (Snipcart)

Each variant has a unique `id` (e.g. `fish-seasoning-tub-100g`). They appear as separate line items in the cart — a customer can buy a tub and a packet without them merging.

### Currency switch

`Intl.NumberFormat` calls (in `ProductCard.astro` and `ProductInfo.astro`) switch from `currency: product.currency` (which was `EUR`) to GBP. Because we set `"currency": "GBP"` in the JSON, no formatter code changes are needed — only the data.

---

## 2. "Become a Stockist" nav link

Add an entry to the `navLinks` array in two files:

- `src/components/global/SiteHeader.astro`
- `src/components/global/MobileMenu.astro`

```js
{ label: 'Become a Stockist', href: '/trade' }
```

Position: **last** in the list (after Delivery), since it's a secondary CTA aimed at trade buyers, not consumers.

---

## Files affected

- `src/data/products.json` — replace price/weight with variants array, currency → GBP
- `src/components/product/ProductCard.astro` — "From" pricing, "View Options" button
- `src/components/product/ProductInfo.astro` — size picker + variant-aware Add to Cart
- `src/components/global/SiteHeader.astro` — add Stockist nav link
- `src/components/global/MobileMenu.astro` — add Stockist nav link

## Out of scope

- Changes to the `/trade` page itself.
- Highlighting the 4.08kg specifically on the trade page (separate task if wanted).
- Any reshuffling of existing nav items.
