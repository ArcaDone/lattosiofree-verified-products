# Verified Products Dataset

This repository stores lactose-related product classifications curated for the app.

## Purpose

The dataset is used as a trusted layer before, or alongside, Open Food Facts.
When a barcode exists here with a reliable status, the app can prefer this dataset
over incomplete external responses.

## Status Levels

- `reported`: user-reported or imported data that has not been reviewed yet.
- `supported`: reviewed data supported by one or more external sources, but not
  yet verified from packaging photos or direct inspection.
- `verified`: reviewed data confirmed from packaging photos, direct inspection,
  or manufacturer-level evidence.

## Source Priority

When multiple sources exist for the same product, use this priority:

1. `packaging_photo_verified`
2. `manufacturer_source`
3. `supporting_web_source`
4. `community_report`

## Repository Layout

- `products/`: resolved products that the app can query directly.
- `reports/`: raw incoming reports and supporting material grouped by barcode.
- `schemas/`: JSON schemas for repository files.
- `docs/`: editorial rules and data model notes.

## App Resolution Strategy

Recommended app lookup order:

1. Search this dataset by barcode.
2. If a matching product has status `verified` or `supported`, use it.
3. If no reliable product exists here, query Open Food Facts.
4. If Open Food Facts is incomplete and this dataset has a reviewed result, this
   dataset should win.
