# mtw1 — MasterTimeWaster (Option 1: Shopify)

A static ecommerce site built with Eleventy and deployed to Cloudflare Pages, using Shopify Starter's Buy Button for cart and checkout, and Printful for print-on-demand fulfillment.

**Live site:** https://mastertimewaster.shop

## Stack

- **Static site generator:** Eleventy (11ty) v3
- **Hosting:** Cloudflare Pages (free tier)
- **Ecommerce:** Shopify Starter ($5/month) — Buy Button embed
- **Fulfillment:** Printful, connected to Shopify store
- **Source control:** GitHub (nopolabs/mtw1)

## Monthly cost

| Service | Cost |
|---|---|
| Cloudflare Pages | $0 |
| Shopify Starter | $5 |
| Domain | ~$1 amortized |
| **Total** | **~$6/month** |

## Project structure

```
mtw1/
├── src/
│   ├── _includes/
│   │   └── layout.njk        # Shared HTML layout (nav, footer, head)
│   ├── _data/
│   │   └── products.json     # Product catalog — edit this to add/change products
│   ├── images/               # Product photos
│   ├── styles.css            # Site styles
│   ├── index.njk             # Home page with product cards and Buy Buttons
│   ├── about.njk             # About page
│   └── contact.njk           # Contact page
├── .eleventy.js              # Eleventy config (input: src/, output: _site/)
├── package.json
└── .gitignore
```

## Local development

```bash
npm install
npm start            # starts dev server at http://localhost:8080
npm run build        # builds static site to _site/
```

## Adding or changing products

Edit `src/_data/products.json`. Each product needs:

```json
{
  "name": "Product Name",
  "price": "27.00",
  "slug": "product-slug",
  "image": "/images/product-image.jpg",
  "shopify_id": "SHOPIFY_PRODUCT_ID",
  "shopify_node": "product-component-XXXXXXXXXX"
}
```

To get `shopify_id` and `shopify_node`: go to Shopify admin → Sales channels → Buy Button → Create a Buy Button → select product → generate code. Extract the `id` and `node` values from the snippet.

## Deployment

Deployment is automatic — push to `main` on GitHub and Cloudflare Pages builds and deploys.

- Build command: `npm run build`
- Build output directory: `_site`

## Shopify setup

- Plan: Starter ($5/month)
- Sales channel: Buy Button
- Products are published from Printful to Shopify
- Printful handles fulfillment automatically when orders are placed through Shopify checkout

## Shopify Buy Button

The Buy Button embed is configured to hide the product image, title, and price (these are rendered by Eleventy). Only the "Add to cart" button is shown. The Shopify SDK is loaded once and initializes all product components on the page.

The Shopify `storefrontAccessToken` in the client-side JS is intentionally public — this is by design in Shopify's architecture.

