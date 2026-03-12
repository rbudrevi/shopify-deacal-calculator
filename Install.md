
---

# INSTALL.md

```markdown
# How to Install the Decal Calculator in Shopify Dawn

This guide explains how to install the decal calculator modal into a Dawn-based product page.

## Files to add

Copy these snippet files into your theme's `snippets/` folder:

- `decal-calculator.liquid`
- `decal-calculator-trigger.liquid`
- `decal-calculator-modal.liquid`

## Step 1: Add the trigger to `main-product.liquid`

Open:

```text
sections/main-product.liquid

Find the area where you want the calculator link to appear. In your implementation, this is around the pricing / product purchase UI, around line 392.
Add:
```liquid
{% render 'decal-calculator-trigger' %}

### Example Placement
</price-per-item>
{%- endif -%}

{% render 'decal-calculator-trigger' %}

</div>

## Step 2: Add the modal render near the bottom of main-product.liquid
Near the end of the file, before the closing </product-info> tag, add:
{% render 'decal-calculator-modal', product: product %}

### Example Placement
{% render 'decal-calculator-modal', product: product %}
</product-info>

## Step 3: Confirm required metafields exist

The calculator reads product metafields from:

product.metafields.custom.display_style
product.metafields.custom.decal_shape
product.metafields.custom.silhouette_path
product.metafields.custom.average_size
product.metafields.custom.decal_count

These control:

layout mode
decal shape
SVG silhouette path
average decal size
decals per envelope

If some values are missing, the calculator uses built-in defaults.

## Step 4: Save and test

Go to a product page and verify:

- the calculator trigger appears
- clicking the trigger opens the modal
- the modal shows the calculator
- width / height inputs update the estimate
- the SVG visualization renders correctly

# Expected feature behavior

The calculator should:

open in a modal overlay
lock background scroll while open

close when:

clicking the close button
clicking outside the modal content
pressing Escape

### Architecture

This feature is split into three snippets:
- decal-calculator-trigger.liquid
- Renders the link/button that opens the calculator modal.
- decal-calculator-modal.liquid

Provides:

- modal wrapper
- modal styles
- modal open/close JavaScript
- renders the calculator snippet inside the modal

decal-calculator.liquid

Provides:

- metafield-to-JavaScript bridge
- calculator UI
- calculation logic
- SVG rendering

## Notes

This implementation is intentionally self-contained for simple installation.

No separate CSS or JS assets are required.

The calculator is designed to be easy to move between Dawn-based themes.

## Troubleshooting
#Trigger appears but modal does not open

Check that:

decal-calculator-modal.liquid is rendered near the end of main-product.liquid

The trigger ID and modal IDs match:
- open-decal-calc, dc-modal, close-decal-calc

# Modal opens but calculator is blank

Check that:

Decal-calculator.liquid exists in snippets/
the snippet is rendered inside decal-calculator-modal.liquid

# Calculations look wrong

Check that:

Product metafields are populated correctly, average_size and decal_count contain numeric values

# SVG does not render correctly

Check that:
Silhouette_path contains a valid SVG path or that decal_shape is set to a supported fallback shape

