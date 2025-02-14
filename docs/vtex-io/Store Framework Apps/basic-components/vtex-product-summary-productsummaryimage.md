---
title: "Product Summary Image"
slug: "vtex-product-summary-productsummaryimage"
excerpt: "vtex.product-summary@2.80.1-perftest.1"
hidden: false
createdAt: "2020-06-09T14:48:52.826Z"
updatedAt: "2022-07-02T00:50:33.284Z"
---
`product-summary-image` is a block exported by the [Product Summary app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-product-summary) that renders the product's image.

![foto-product-summary-image](https://cdn.jsdelivr.net/gh/vtexdocs/dev-portal-content@main/images/vtex-product-summary-productsummaryimage-0.png)

## Configuration

1. Import the `vtex.product-summary` app to your theme's dependencies in the `manifest.json`:

```json
  dependencies: {
    "vtex.product-summary": "2.x"
  }
```

2. Add the `product-summary-image` block as a child of the `product-summary.shelf` block:

```json
{
  "shelf#home": {
    "blocks": ["product-summary.shelf"]
  },
    "product-summary.shelf": {
      "children": [
        "product-summary-name",
        "product-summary-description",
        "product-summary-image",
        "product-summary-price",
        "product-summary-sku-selector",
        "product-summary-buy-button"
      ]
    },
```
3. Then, declare the `product-summary-image` and configure its behavior using the props stated below.

```json
    "product-summary-image": {
      "props": {
        "showBadge": true,
        "height": 220
      }
    }
}
```

| Prop name | Type | Description | Default value |
| :--------:| :--: | :---------: | :-----------: |
| `showBadge` | `boolean` | Whether a discount badge (if there is any) will be displayed on the product's image (`true`) or not (`false`) | `true` |
| `badgeText` | `string` | Text displayed on the discount badge (in case the badge is configured to be displayed on the image). | `undefined` |
| `showCollections` | `boolean` | Whether collection badges (if there are any) will be displayed (`true`) or not (`false`). | `false` |
| `displayMode` | `enum` | Defines the Product Summary Image display mode. Possible values are: `normal` and `inline`. | `normal` |
| `placeholder` | `string` | Defines the Product Summary Image placeholder image. | `undefined` |
| `mainImageLabel` | `string \| object` | Matches the value defined in the `imageLabel` field from the admin's Catalog. Once matched, it defines which product image will be the main image displayed in the Product Summary component. | `undefined`|
| `hoverImageLabel` | `string` | ![https://img.shields.io/badge/-Deprecated-red](https://cdn.jsdelivr.net/gh/vtexdocs/dev-portal-content@main/images/vtex-product-summary-productsummaryimage-1.png) Text value that matches the value defined in the `imageLabel` field from the admin's Catalog. Once matched, it defines which product image will be displayed when the user is hovering. If you set a label and no match is found, no image will be displayed during the hover. *Caution*: Use the `hoverImage` prop instead. | `undefined` | 
| `hoverImage` | `object` | Defines which criteria should be used to define the hover image according to the product images in the admin's Catalog. | `undefined`|
| `width` | `object` | Defines the Product Summary Image width. | `undefined` |
| `height` | `object` | Defines the Product Summary Image height. | `undefined` |
| `aspectRatio` | `object` | Aspect ratio of the Product Summary Image. It defines whether the image should be displayed in a square, portrait, landscape or in another format. The prop value should follow the [common aspect ratio notation](https://en.wikipedia.org/wiki/Aspect_ratio_(image)), which gives two numbers separated by a colon. For example: `1:1` for a square format or `3:4` for an upright portrait. Note that this prop won't work if you've already configured the `width` or `height` props. | `undefined` |
| `maxHeight` | `object` | Defines the Product Summary Image max height. Note that this prop won't work if you've already configured the `width` or `height` props.| `undefined` |

- `mainImageLabel` object:

| Prop name | Type | Description | Default value |
| :--------:| :--: | :---------: | :-----------: |
| `label` | `string` | Text value that matches the value defined in the `imageLabel` field from the admin's Catalog. Once matched, it defines which product image will be the main image displayed in the Product Summary component.  If you set a label and no match is found, the main image of the product will be shown instead. | `undefined` |
| `labelMatchCriteria`| `enum` | Criteria to define if the image's `label` searched value should be exactly as provided or if it just needs to contain the substring anywhere in the image's `label`. Possible values are: `exact` (finds the image that matches exactly the string filled in `label` field) and `contains` (finds the first image that contains the substring filled in `label` field). | `exact` |


- `hoverImage` object:

| Prop name | Type | Description | Default value |
| :--------:| :--: | :---------: | :-----------: |
| `criteria` | `enum` | Criteria that should be used to define the hover image according to the product images in the admin's Catalog. Possible values are: `label` (the hover image will be the one that matches the `label` value) and `index` (the hover image should be the one with the same `index` value). | `label` |
| `label` | `string` | Text string to match the desired image's `label` value. If no match is found, no image will be displayed during the hover. *Caution*: This prop should only be used when the `criteria` prop is set as `label`. | `undefined`   |
| `labelMatchCriteria` | `enum` | Criteria to define if the image's `label` searched value should be exactly as provided or if it just needs to contain the substring anywhere in the image's `label`. Possible values are: `exact` (finds the image that matches exactly the string filled in `label` field) and `contains` (finds the first image that contains the substring filled in `label` field). *Caution*: This prop should only be used when the `criteria` prop is set as `label`. | `exact`   |
| `index` | `number` | Index number to match with the desired image's. If no match is found, no image will be displayed during the hover. *Caution*: This prop should only be used when the `criteria` prop is set as `index`. | `undefined`   |

- `width` object:

| Prop name | Type | Description | Default value |
| :--------:| :--: | :---------: | :-----------: |
| `desktop` | `number` | Image width for desktop users. | `undefined` |
| `mobile`| `number` | Image width for mobile device users. | `undefined` |

-  `height` object:

| Prop name | Type | Description | Default value |
| :--------:| :--: | :---------: | :-----------: |
| `desktop` | `number` | Image height for desktop users. | `undefined` |
| `mobile`| `number` | Image height for mobile device users. | `undefined` |
  
- `aspectRatio` object:

| Prop name | Type | Description | Default value |
| :--------:| :--: | :---------: | :-----------: |
| `desktop` | `string` | Image aspect ratio for desktop users. | `undefined` |
| `mobile`| `string` | Image aspect ratio for mobile device users. | `undefined` |
  
- `maxHeight` object:

| Prop name | Type | Description | Default value |
| :--------:| :--: | :---------: | :-----------: |
| `desktop` | `string` | Image maximum height for desktop users. | `undefined` |
| `mobile`| `string` | Image maximum height for mobile device users. | `undefined` |

The `width`, `height`, `aspectRatio` and `maxHeight` props use the [responsive values logic](https://github.com/vtex-apps/responsive-values#vtexresponsive-values).

## Customization

To apply CSS customizations in this and other blocks, follow the [Using CSS Handles for store customization](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-css-handles-for-store-customization) guide.

| CSS Handles |
| :----------:|
| `hoverImage` |
| `hoverEffect` |
| `imageContainer` |
| `imageInline` |
| `imageNormal` |
| `imageStackContainer` |
| `mainImageHovered` |