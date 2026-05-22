## What I picked
The bundle builder progress text on `/pages/bundle-builder` had a hardcoded `(15%)` discount value in `sections/bundle-builder.liquid` (line 83), despite the section schema supporting configurable discount tiers (10% at 3 items, 15% at 5 items).

## Why it's the highest-impact thing here
The bundle builder is a direct revenue driver — it exists to upsell customers into multi-item purchases. Showing the wrong discount percentage at the most critical decision point (before any item is selected) breaks customer trust and undersells the entry tier. A customer seeing "15%" before selecting 3 items, then only getting 10% off, feels misled. This is a conversion killer.

## What I did
Replaced the hardcoded `(15%)` string with dynamic Liquid logic that reads the first configured `discount_tier` block and displays the correct minimum items and discount percentage. The fix is a pure Liquid change — no JS, no CSS, no risk of regression.

## What I'd do next
- Add a full tier breakdown display in the header (e.g. "3 items = 10% off, 5 items = 15% off") so customers see the full incentive ladder upfront
- Audit the sticky summary bar copy for similar hardcoded strings
- Add a Shopify theme editor warning if no discount_tier blocks are configured