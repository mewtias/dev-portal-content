---
title: "How to activate an SKU"
slug: "how-to-activate-an-sku"
hidden: false
createdAt: "2021-03-25T20:21:22.710Z"
updatedAt: "2021-08-25T22:08:03.928Z"
---
When creating a new SKU, there are restrictions set up in our platform that you will need to pay attention to. If you do not follow these, you will be unable to activate your SKU and it will not be displayed to customers.

When creating an SKU using the [Create SKU](https://developers.vtex.com/vtex-developer-docs/reference/catalog-api-sku#catalog-api-post-sku) endpoint, you should not set the `IsActive` as `true`. If you send the request to activate the SKU, you will receive a `400 Bad Request` error. The value to `IsActive` must always be `false` when sending that request.

To activate your SKU, it needs to have at least one image associated with it. If your SKU is a kit, it will also need to have at least one active component associated with it as well. If you send a request to [Update SKU](https://developers.vtex.com/vtex-developer-docs/reference/catalog-api-sku#catalog-api-put-sku) without meeting these conditions, you will receive a `400 Bad Request` error. 

There are two ways that you can activate your SKU - [manually](#manual-activation) or [automatically](#automatic-activation). 

## Manual activation
1. To manually activate your SKU, follow these steps:
2. [Create the SKU](https://developers.vtex.com/vtex-developer-docs/reference/catalog-api-sku#catalog-api-post-sku), setting `IsActive` as  `false`.
3. If the SKU is a kit, [create and associate SKU components](https://developers.vtex.com/vtex-developer-docs/reference/catalog-api-sku-kit#catalog-api-post-sku-kit).
4. [Create and associate SKU files](https://developers.vtex.com/vtex-developer-docs/reference/catalog-api-sku-file#catalog-api-post-sku-file).
5. [Update the SKU](https://developers.vtex.com/vtex-developer-docs/reference/catalog-api-sku#catalog-api-put-sku) as active, setting `IsActive` as `true`.

Now the SKU should be active in your store.

## Automatic activation
This configuration will automatically update the SKU as active once it is associated with an image or an active component. You do not need to update the SKU as in the previous steps.

1. To automatically activate your SKU, follow these steps:
2. [Create the SKU](https://developers.vtex.com/vtex-developer-docs/reference/catalog-api-sku#catalog-api-post-sku), setting `IsActive` as  `false` and the `ActivateIfPossible` attribute as `true`.
3. If the SKU is a kit, [create and associate SKU components](https://developers.vtex.com/vtex-developer-docs/reference/catalog-api-sku-kit#catalog-api-post-sku-kit).
4. [Create and associate SKU files](https://developers.vtex.com/vtex-developer-docs/reference/catalog-api-sku-file#catalog-api-post-sku-file).

Now the SKU should be active in your store.