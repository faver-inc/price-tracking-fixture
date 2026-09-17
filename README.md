# price-tracking-fixture

Static product pages used to test Faver universal price tracking end to end. Edit a product's price or availability in the JSON-LD and og tags, push, and the tracker picks it up on its next check.

## Snapshots

Snapshots live under `products/`, one self-contained HTML file per product page: every stylesheet inlined, every asset URL made absolute, and all scripts stripped except the `application/ld+json` and Shopify `application/json` blobs the price tracker reads. They're generated from a live store page with `packages/backend/scripts/snapshot-product-page.ts` in `faver-mono`, run as `npx tsx scripts/snapshot-product-page.ts <url> --out products/<name>.html` from `packages/backend` (add `--price <amount>` or `--availability instock|oos` to rewrite as you capture).

To change a price on an existing snapshot, either re-run the script against the live URL with `--price <amount>` and re-save the output, or hand-edit the file directly — but do it consistently: the JSON-LD `price` field, any `og:price:amount`/`product:price:amount` meta tags, Shopify JSON cents fields (`price`, `price_min`, `price_max`, and each `variants[].price`), and the visible currency-prefixed text all need to agree, or the tracker and a human glancing at the page will disagree on what it costs.
