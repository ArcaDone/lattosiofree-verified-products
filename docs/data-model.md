# Data Model

## Product Records

Each file in `products/` represents one barcode and stores the best reviewed
classification currently available.

### Product identity

- `barcode`: EAN/UPC code used as the unique key.
- `productName`: human-readable product name.
- `brands`: brand list as an array.
- `language`: main language used in the record.

### Review status

- `reported`: raw or unresolved.
- `supported`: reviewed and supported by external sources, but not fully verified
  from packaging or direct inspection.
- `verified`: manually verified with the highest confidence.

### Classification

- `severity`: one of `SAFE`, `TRACES`, `CONTAINS`, `UNKNOWN`
- `reason`: short machine-readable explanation of why that severity was chosen.

### Signals

Signals are grouped so app logic can explain the result:

- `contains`: direct milk or lactose evidence.
- `traces`: contamination or may-contain evidence.
- `lactoseFree`: positive lactose-free claims.

### Ingredients and allergens

Store raw ingredient text whenever possible, plus source and confidence.
Allergens should be split into:

- `contains`
- `mayContain`

## Report Records

Files in `reports/` preserve the original incoming report payload with minimal
changes. This keeps auditability and helps reprocess old cases later.

## Source Types

- `packaging_photo_verified`
- `manufacturer_source`
- `supporting_web_source`
- `community_report`
- `user_report`

## Editorial Rules

1. Do not promote a product to `verified` without packaging-level or equivalent
   direct evidence.
2. Use `supported` when the evidence is strong but indirect.
3. Keep raw reports untouched as much as possible.
4. Prefer storing exact ingredient text over paraphrases.
5. Add notes when an external source such as Open Food Facts was incomplete.
