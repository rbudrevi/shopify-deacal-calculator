# Shopify Decal Calculator Modal for Dawn

A lightweight decal quantity calculator for Shopify Dawn product pages.

This feature adds a modal-based calculator that helps customers estimate how many decal sheets they need based on window dimensions, spacing, margins, and product-specific metafield values.

## What it does

The calculator:

- opens from a trigger link on the product page
- reads product metafields for decal shape, average size, display style, and decals per envelope
- lets customers enter window width and height
- calculates:
  - total decals needed
  - estimated number of envelopes/sheets needed
  - rows and columns in the pattern layout
- renders an SVG preview of the decal layout

## Files included

Install these snippets into your theme:

- `decal-calculator.liquid`
- `decal-calculator-trigger.liquid`
- `decal-calculator-modal.liquid`

## Theme integration

In `main-product.liquid`:

### 1. Add the trigger
Place this where you want the calculator link to appear:

```liquid
{% render 'decal-calculator-trigger' %}

This is typically near the product pricing / purchase controls.

Near the bottom of the section, before the closing </product-info>, add:

```liquid
{% render 'decal-calculator-modal', product: product %}

## Required Metafields
The calculator expects these product metafields:

product.metafields.custom.display_style
product.metafields.custom.decal_shape
product.metafields.custom.silhouette_path
product.metafields.custom.average_size
product.metafields.custom.decal_count

If some metafields are missing, the calculator falls back to:

display_style: grid
decal_shape: diamond
average_size: 1.25
decal_count: 1

## Notes

The calculator uses inline CSS and JavaScript inside the snippets for simple installation.

No theme assets are required.

The modal is product-page specific and intended for Dawn-based product templates.

The calculator body and modal wrapper are intentionally separated so the feature is easier to maintain and move.

## Recommended placement

Suggested integration point inside main-product.liquid:
trigger near the pricing / buying area
modal render near the end of the product section, before </product-info>

## Compatibility

Designed for Shopify Dawn
Best suited for product pages using the standard main-product.liquid section structure

## License

Use and modify as needed for your store or client projects.
