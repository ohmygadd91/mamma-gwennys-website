# Trade Enquiry Landing Page — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a `/trade` landing page that converts restaurants, retailers, and distributors into trade enquiry leads via a Netlify Forms submission.

**Architecture:** Single Astro page (`src/pages/trade.astro`) using the existing `BaseLayout.astro` layout, product data from `products.json`, and the project's CSS custom properties. No new components or dependencies needed — everything is self-contained in the page file with scoped styles.

**Tech Stack:** Astro 6, Netlify Forms, existing CSS design system (custom properties from `global.css`), Material Symbols icons, Google Fonts (already loaded via BaseLayout).

---

## File Structure

- **Create:** `src/pages/trade.astro` — the entire trade landing page (all 4 sections + scoped styles)

No other files need to be created or modified.

---

### Task 1: Hero Section with Embedded Trade Enquiry Form

**Files:**
- Create: `src/pages/trade.astro`

This task creates the page file with the hero section — the most important part of the page. Two-column layout: value proposition on the left, Netlify Forms enquiry form on the right.

- [ ] **Step 1: Create `src/pages/trade.astro` with frontmatter and hero markup**

```astro
---
import BaseLayout from '../layouts/BaseLayout.astro';
import products from '../data/products.json';
---

<BaseLayout
  title="Trade Enquiries — Mamma Gwenny's"
  description="Partner with Mamma Gwenny's for premium Caribbean seasonings. Bulk pricing, free samples, and Europe-wide delivery for restaurants, retailers, and distributors."
>
  <!-- Hero with Form -->
  <section class="trade-hero" id="trade-form">
    <div class="trade-hero__pattern"></div>
    <div class="trade-hero__overlay"></div>
    <div class="container trade-hero__inner">
      <div class="trade-hero__content">
        <span class="label" style="color: var(--color-secondary-container);">Trade Enquiries</span>
        <h1 class="trade-hero__title">BRING AUTHENTIC CARIBBEAN FLAVOUR TO YOUR BUSINESS</h1>
        <p class="trade-hero__subtitle">
          Partner with Mamma Gwenny's for premium handcrafted seasonings. Bulk pricing available. Free sample packs for qualifying businesses.
        </p>
        <div class="trade-hero__badges">
          <div class="trade-badge">
            <span class="material-symbols-outlined" style="font-variation-settings: 'FILL' 1;">history_edu</span>
            <span>Handcrafted Recipes</span>
          </div>
          <div class="trade-badge">
            <span class="material-symbols-outlined" style="font-variation-settings: 'FILL' 1;">inventory_2</span>
            <span>Bulk Pricing</span>
          </div>
          <div class="trade-badge">
            <span class="material-symbols-outlined" style="font-variation-settings: 'FILL' 1;">redeem</span>
            <span>Free Samples</span>
          </div>
        </div>
      </div>
      <div class="trade-hero__form-wrapper">
        <div class="trade-form-card">
          <h2 class="trade-form-card__title">Request Trade Pricing</h2>
          <form class="trade-form" name="trade-enquiry" method="POST" data-netlify="true" netlify-honeypot="bot-field">
            <input type="hidden" name="form-name" value="trade-enquiry" />
            <p class="visually-hidden">
              <label>Don't fill this out if you're human: <input name="bot-field" /></label>
            </p>
            <div class="trade-form__field">
              <label for="trade-name" class="trade-form__label">Name</label>
              <input type="text" id="trade-name" name="name" required class="trade-form__input" placeholder="Your name" />
            </div>
            <div class="trade-form__field">
              <label for="trade-business" class="trade-form__label">Business Name</label>
              <input type="text" id="trade-business" name="business-name" required class="trade-form__input" placeholder="Your business" />
            </div>
            <div class="trade-form__field">
              <label for="trade-email" class="trade-form__label">Email</label>
              <input type="email" id="trade-email" name="email" required class="trade-form__input" placeholder="you@business.com" />
            </div>
            <div class="trade-form__field">
              <label for="trade-type" class="trade-form__label">Business Type</label>
              <select id="trade-type" name="business-type" required class="trade-form__input">
                <option value="">Select your business type</option>
                <option value="restaurant">Restaurant / Takeaway</option>
                <option value="retailer">Retailer / Supermarket</option>
                <option value="distributor">Distributor / Wholesaler</option>
                <option value="other">Other</option>
              </select>
            </div>
            <div class="trade-form__field">
              <label for="trade-message" class="trade-form__label">Message <span style="font-weight: 400; color: var(--color-outline);">(optional)</span></label>
              <textarea id="trade-message" name="message" rows="3" class="trade-form__input trade-form__textarea" placeholder="Tell us about your needs..."></textarea>
            </div>
            <button type="submit" class="btn btn-primary" style="width: 100%; justify-content: center;">Request Trade Pricing</button>
            <p class="trade-form__note">We'll respond within 24 hours</p>
          </form>
        </div>
      </div>
    </div>
  </section>
</BaseLayout>
```

- [ ] **Step 2: Add scoped styles for the hero section**

Add this `<style>` block at the bottom of `trade.astro`, after the closing `</BaseLayout>` tag:

```html
<style>
  /* --- Hero --- */
  .trade-hero {
    position: relative;
    min-height: 100vh;
    display: flex;
    align-items: center;
    overflow: hidden;
    padding: 10rem 0 var(--space-9);
  }

  .trade-hero__pattern {
    position: absolute;
    inset: 0;
    background-image: url('/images/patterns/tropical-pattern.png');
    background-size: 400px;
    background-repeat: repeat;
    z-index: 0;
  }

  .trade-hero__overlay {
    position: absolute;
    inset: 0;
    background: rgba(0, 0, 0, 0.6);
    z-index: 1;
  }

  .trade-hero__inner {
    position: relative;
    z-index: 2;
    display: grid;
    grid-template-columns: 1.1fr 0.9fr;
    gap: var(--space-8);
    align-items: center;
  }

  .trade-hero__title {
    color: var(--color-white);
    font-size: clamp(2.5rem, 5vw, 4rem);
    margin: var(--space-4) 0 var(--space-6);
  }

  .trade-hero__subtitle {
    color: rgba(255, 255, 255, 0.85);
    font-size: var(--text-lg);
    font-weight: 500;
    line-height: 1.7;
    max-width: 520px;
    margin-bottom: var(--space-6);
  }

  .trade-hero__badges {
    display: flex;
    flex-wrap: wrap;
    gap: var(--space-4);
  }

  .trade-badge {
    display: flex;
    align-items: center;
    gap: var(--space-2);
    color: rgba(255, 255, 255, 0.9);
    font-size: var(--text-sm);
    font-weight: 600;
  }

  .trade-badge .material-symbols-outlined {
    font-size: 20px;
    color: var(--color-secondary-container);
  }

  /* --- Form Card --- */
  .trade-form-card {
    background: var(--color-white);
    border-radius: var(--radius-xl);
    padding: var(--space-7);
    box-shadow: 0 24px 48px rgba(0, 0, 0, 0.2);
  }

  .trade-form-card__title {
    font-size: var(--text-2xl);
    color: var(--color-primary);
    margin-bottom: var(--space-6);
  }

  .trade-form {
    display: flex;
    flex-direction: column;
    gap: var(--space-4);
  }

  .trade-form__label {
    display: block;
    font-size: var(--text-sm);
    font-weight: 500;
    color: var(--color-text);
    margin-bottom: var(--space-2);
  }

  .trade-form__input {
    width: 100%;
    padding: var(--space-3) var(--space-4);
    border: 2px solid var(--color-outline-variant);
    border-radius: var(--radius-md);
    font-size: var(--text-base);
    color: var(--color-text);
    background: var(--color-white);
    transition: border-color var(--transition-fast);
  }

  .trade-form__input:focus {
    outline: none;
    border-color: var(--color-primary);
  }

  .trade-form__textarea {
    resize: vertical;
    min-height: 80px;
  }

  .trade-form__note {
    text-align: center;
    font-size: var(--text-sm);
    color: var(--color-outline);
    margin: 0;
  }
</style>
```

- [ ] **Step 3: Build and verify hero renders**

Run:
```bash
cd "/c/Users/mdgad/Downloads/Mamma Gwenny's" && npx astro build 2>&1 | tail -5
```
Expected: Build succeeds, `/trade/index.html` appears in output.

- [ ] **Step 4: Screenshot and verify visually**

Run:
```bash
node serve.mjs &
sleep 2
node screenshot.mjs http://localhost:3000/trade hero
```
Then read the screenshot from `temporary screenshots/` to verify the hero looks correct: two-column layout, form card visible, tropical pattern background with dark overlay.

- [ ] **Step 5: Commit**

```bash
git add src/pages/trade.astro
git commit -m "feat: add trade landing page with hero and enquiry form"
```

---

### Task 2: Product Range Section

**Files:**
- Modify: `src/pages/trade.astro`

Add the product range grid section below the hero, showing all 8 seasonings without prices.

- [ ] **Step 1: Add product range section markup**

In `trade.astro`, add this section inside `<BaseLayout>`, after the closing `</section>` of the hero and before `</BaseLayout>`:

```astro
  <!-- Product Range -->
  <section class="trade-products section">
    <div class="container">
      <div class="trade-products__header text-center">
        <span class="label" style="color: var(--color-secondary);">What We Offer</span>
        <h2 style="margin-top: var(--space-2);">OUR SEASONING RANGE</h2>
        <p class="trade-products__subtitle">8 handcrafted blends, available in bulk quantities</p>
      </div>
      <div class="grid grid-4 trade-products__grid">
        {products.map((product) => (
          <div class="trade-product-card">
            <div class="trade-product-card__image">
              <img src={product.image} alt={product.name} width="400" height="500" loading="lazy" />
            </div>
            <h3 class="trade-product-card__name">{product.name}</h3>
            <p class="trade-product-card__desc">{product.shortDescription}</p>
          </div>
        ))}
      </div>
      <p class="trade-products__footer text-center">
        Available in 100g retail packs and bulk catering sizes. Custom quantities available on request.
      </p>
    </div>
  </section>
```

- [ ] **Step 2: Add scoped styles for the product range**

Add these rules inside the existing `<style>` block in `trade.astro`:

```css
  /* --- Product Range --- */
  .trade-products__header {
    margin-bottom: var(--space-8);
  }

  .trade-products__subtitle {
    font-size: var(--text-lg);
    color: var(--color-text-muted);
    margin-top: var(--space-3);
  }

  .trade-products__grid {
    gap: var(--space-6);
  }

  .trade-product-card {
    text-align: center;
  }

  .trade-product-card__image {
    aspect-ratio: 3 / 4;
    background: var(--color-surface-low);
    border-radius: var(--radius-xl);
    overflow: hidden;
    margin-bottom: var(--space-4);
    display: flex;
    align-items: center;
    justify-content: center;
    padding: var(--space-3);
  }

  .trade-product-card__image img {
    width: 100%;
    height: 100%;
    object-fit: contain;
    transition: transform var(--transition-slow);
  }

  .trade-product-card:hover .trade-product-card__image img {
    transform: scale(1.05);
  }

  .trade-product-card__name {
    font-size: var(--text-lg);
    margin-bottom: var(--space-2);
  }

  .trade-product-card__desc {
    font-size: var(--text-sm);
    color: var(--color-text-muted);
  }

  .trade-products__footer {
    margin-top: var(--space-8);
    font-size: var(--text-lg);
    font-weight: 500;
    color: var(--color-text-muted);
  }
```

- [ ] **Step 3: Build and verify**

Run:
```bash
cd "/c/Users/mdgad/Downloads/Mamma Gwenny's" && npx astro build 2>&1 | tail -5
```
Expected: Build succeeds.

- [ ] **Step 4: Screenshot and verify visually**

Run:
```bash
node screenshot.mjs http://localhost:3000/trade products
```
Read the screenshot. Verify: 4-column product grid, product images visible, names and descriptions shown, no prices.

- [ ] **Step 5: Commit**

```bash
git add src/pages/trade.astro
git commit -m "feat: add product range section to trade page"
```

---

### Task 3: Why Partner With Us Section

**Files:**
- Modify: `src/pages/trade.astro`

Add 4 benefit cards highlighting trade advantages.

- [ ] **Step 1: Add benefits section markup**

In `trade.astro`, add this section after the product range section and before `</BaseLayout>`:

```astro
  <!-- Why Partner -->
  <section class="trade-benefits section" style="background: var(--color-surface-low);">
    <div class="container">
      <div class="text-center" style="margin-bottom: var(--space-8);">
        <span class="label" style="color: var(--color-secondary);">Why Choose Us</span>
        <h2 style="margin-top: var(--space-2);">WHY PARTNER WITH US</h2>
      </div>
      <div class="grid grid-4 trade-benefits__grid">
        <div class="trade-benefit">
          <div class="trade-benefit__icon" style="background: var(--color-primary);">
            <span class="material-symbols-outlined" style="color: var(--color-on-primary); font-variation-settings: 'FILL' 1;">trending_down</span>
          </div>
          <h3>BULK PRICING</h3>
          <p>Competitive wholesale rates with tiered pricing based on volume</p>
        </div>
        <div class="trade-benefit">
          <div class="trade-benefit__icon" style="background: var(--color-secondary-container);">
            <span class="material-symbols-outlined" style="color: var(--color-on-secondary-container); font-variation-settings: 'FILL' 1;">redeem</span>
          </div>
          <h3>FREE SAMPLES</h3>
          <p>Try before you commit. Request a sample pack with your enquiry</p>
        </div>
        <div class="trade-benefit">
          <div class="trade-benefit__icon" style="background: var(--color-secondary);">
            <span class="material-symbols-outlined" style="color: var(--color-on-secondary); font-variation-settings: 'FILL' 1;">restaurant</span>
          </div>
          <h3>HANDCRAFTED QUALITY</h3>
          <p>Small-batch, freshly ground spices using heritage family recipes</p>
        </div>
        <div class="trade-benefit">
          <div class="trade-benefit__icon" style="background: var(--color-tertiary);">
            <span class="material-symbols-outlined" style="color: var(--color-on-tertiary); font-variation-settings: 'FILL' 1;">local_shipping</span>
          </div>
          <h3>EUROPE-WIDE DELIVERY</h3>
          <p>Reliable shipping across Europe with flexible order schedules</p>
        </div>
      </div>
    </div>
  </section>
```

- [ ] **Step 2: Add scoped styles for benefits**

Add these rules inside the existing `<style>` block:

```css
  /* --- Benefits --- */
  .trade-benefits__grid {
    gap: var(--space-6);
  }

  .trade-benefit {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    gap: var(--space-4);
  }

  .trade-benefit__icon {
    width: 64px;
    height: 64px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: var(--radius-xl);
    transition: transform var(--transition-base);
  }

  .trade-benefit__icon .material-symbols-outlined {
    font-size: 28px;
  }

  .trade-benefit:hover .trade-benefit__icon {
    transform: scale(1.1);
  }

  .trade-benefit h3 {
    font-size: var(--text-lg);
  }

  .trade-benefit p {
    line-height: 1.7;
    color: var(--color-text-muted);
  }
```

- [ ] **Step 3: Build and verify**

Run:
```bash
cd "/c/Users/mdgad/Downloads/Mamma Gwenny's" && npx astro build 2>&1 | tail -5
```
Expected: Build succeeds.

- [ ] **Step 4: Screenshot and verify visually**

Run:
```bash
node screenshot.mjs http://localhost:3000/trade benefits
```
Read the screenshot. Verify: 4 benefit cards in a row with icons, headings, and descriptions.

- [ ] **Step 5: Commit**

```bash
git add src/pages/trade.astro
git commit -m "feat: add why partner with us section to trade page"
```

---

### Task 4: Footer CTA Section and Responsive Styles

**Files:**
- Modify: `src/pages/trade.astro`

Add the bottom CTA that anchors back to the form, plus all responsive breakpoints for mobile/tablet.

- [ ] **Step 1: Add footer CTA markup**

In `trade.astro`, add this section after the benefits section and before `</BaseLayout>`:

```astro
  <!-- Footer CTA -->
  <section class="trade-cta">
    <div class="trade-cta__pattern"></div>
    <div class="trade-cta__overlay"></div>
    <div class="container trade-cta__inner text-center">
      <h2 style="color: var(--color-white);">READY TO STOCK<br/>MAMMA GWENNY'S?</h2>
      <p style="color: rgba(255,255,255,0.85); font-size: var(--text-lg); margin: var(--space-5) 0 var(--space-7); font-weight: 500;">
        Get in touch today and let's bring Caribbean flavour to your customers.
      </p>
      <a href="#trade-form" class="btn btn-primary btn-lg">Get In Touch</a>
    </div>
  </section>
```

- [ ] **Step 2: Add footer CTA and responsive styles**

Add these rules inside the existing `<style>` block:

```css
  /* --- Footer CTA --- */
  .trade-cta {
    position: relative;
    padding: var(--space-9) 0;
    overflow: hidden;
  }

  .trade-cta__pattern {
    position: absolute;
    inset: 0;
    background-image: url('/images/patterns/tropical-pattern.png');
    background-size: 400px;
    background-repeat: repeat;
    z-index: 0;
  }

  .trade-cta__overlay {
    position: absolute;
    inset: 0;
    background: rgba(0, 0, 0, 0.6);
    z-index: 1;
  }

  .trade-cta__inner {
    position: relative;
    z-index: 2;
    max-width: 700px;
  }

  /* --- Responsive --- */
  @media (max-width: 1023px) {
    .trade-hero__inner {
      grid-template-columns: 1fr;
      gap: var(--space-7);
    }

    .trade-hero__subtitle {
      max-width: 100%;
    }

    .trade-benefits__grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (max-width: 639px) {
    .trade-hero {
      padding-top: 8rem;
    }

    .trade-hero__badges {
      flex-direction: column;
      gap: var(--space-3);
    }

    .trade-form-card {
      padding: var(--space-5);
    }

    .trade-benefits__grid {
      grid-template-columns: 1fr;
    }
  }
```

- [ ] **Step 3: Build and verify**

Run:
```bash
cd "/c/Users/mdgad/Downloads/Mamma Gwenny's" && npx astro build 2>&1 | tail -5
```
Expected: Build succeeds.

- [ ] **Step 4: Screenshot full page and verify**

Run:
```bash
node screenshot.mjs http://localhost:3000/trade final
```
Read the screenshot. Verify all 4 sections render correctly: hero with form, product grid, benefits, footer CTA. Check the "Get In Touch" button links to `#trade-form`.

- [ ] **Step 5: Commit**

```bash
git add src/pages/trade.astro
git commit -m "feat: add footer CTA and responsive styles to trade page"
```

---

### Task 5: Final Visual QA and Polish

**Files:**
- Modify: `src/pages/trade.astro` (only if fixes needed)

Full-page visual review at multiple viewports. Fix any spacing, alignment, or brand consistency issues.

- [ ] **Step 1: Screenshot at desktop (1440px)**

Run:
```bash
node screenshot.mjs http://localhost:3000/trade qa-desktop
```
Read screenshot. Check: hero two-column balance, form card shadow/elevation, product grid alignment, benefit icons centered, footer CTA contrast.

- [ ] **Step 2: Screenshot at mobile (375px)**

Temporarily modify the screenshot viewport or use Puppeteer's mobile emulation. Run:
```bash
node -e "
import puppeteer from 'puppeteer';
const browser = await puppeteer.launch({headless:true,args:['--no-sandbox']});
const page = await browser.newPage();
await page.setViewport({width:375,height:812});
await page.goto('http://localhost:3000/trade',{waitUntil:'networkidle2'});
await page.screenshot({path:'temporary screenshots/qa-mobile.png',fullPage:true});
await browser.close();
console.log('Saved qa-mobile.png');
"
```
Read screenshot. Check: single-column stack, form readable, product grid 1-column on small screens, badges stack vertically.

- [ ] **Step 3: Fix any visual issues found**

Apply targeted CSS fixes if needed. Common things to check:
- Form inputs not overflowing on mobile
- Hero text readable over the dark overlay
- Product images consistent sizing
- Spacing between sections consistent

- [ ] **Step 4: Rebuild and final screenshot if fixes were made**

```bash
cd "/c/Users/mdgad/Downloads/Mamma Gwenny's" && npx astro build 2>&1 | tail -5
node screenshot.mjs http://localhost:3000/trade final-polished
```

- [ ] **Step 5: Commit if any fixes were made**

```bash
git add src/pages/trade.astro
git commit -m "fix: polish trade page spacing and mobile layout"
```
