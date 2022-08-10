---
title: "Identifying whether marketing UTMs are being sent to Checkout"
slug: "identifying-whether-marketing-utms-are-being-sent-to-checkout"
hidden: false
createdAt: "2022-07-25T19:16:25.665Z"
updatedAt: "2022-07-25T20:04:40.744Z"
---
When the `utm_source`, `utm_campaign` or `utm_medium` parameters are used to load a store page, the system creates a cookie named **IPS** whose value is equal to the value of the parameter.

The orderForm of orders closed by the user will receive this cookie in the header of the request sent to Checkout (until this cookie expires). In other words, the moment the customer clicks the **Buy** button, the buy button native control (`<vtex.cmc:BuyButton/>`) will perform a **POST** request to send the value of the **utm_source** parameter to the Checkout.

In this way, the Checkout will be able to assemble the orderForm considering the `marketingData` used in the purchase.

# Simulation

To make sure the content of the `utm_source` parameter is being sent to the Checkout, you can follow the steps below:

1. Access any page of the store with the utm in the querystring (e.g. {*AccountName*}.com.br?utm_source=facebook).
2. Enter the **Developer tools** (**F12** in Chrome, if you are in Windows, or **Cmd+Opt+I** on a Mac)
3. Go to the **Application** tab.
4. Open the store's website cookies and look for the **IPS** cookie.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7b613ab-utmsource1.PNG",
        "utmsource1.PNG",
        1741,
        834,
        "#a5a6a6"
      ]
    }
  ]
}
[/block]
5. Go to a product page and add it to the cart.
6. Access the cart.
7. Refresh the page and monitor the requests on the **Network** tab (located in Developer tools).
8. In the preview, open the `marketingData` node.
9. Check the value of the `utmSource` field.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9a5c682-utmsource2.PNG",
        "utmsource2.PNG",
        1038,
        771,
        "#a3a2a2"
      ]
    }
  ]
}
[/block]
The presence of the `utmSource` field with the same value as `utm_source` means that the information was correctly received by Checkout. If the utmSource` field was empty in the orderForm, it would indicate that the value was not sent to the Checkout.
[block:callout]
{
  "type": "info",
  "body": "When the value is not sent to the Checkout, any benefits linked to the `utm_source` will **not** be applied to the orders, and OMS will **not** register these UTMs as order parameters."
}
[/block]
# Why was the value not passed to the checkout?

One of the most common reasons the marketing context is not sent to the Checkout is the **customization of the purchase call**.

As previously stated, the native buy button control (`<vtex.cmc:BuyButton/>`) performs a POST request sending all the data needed to the Checkout, including the value of the `utm_source`, `utm_campaign` and `utm_medium`.

However, if instead of using this control, your store decides to customize the call and therefore makes the POST of the purchase request on its own, you must remember to send in this POST all the data that may be useful to assemble the orderForm**, including the marketing context.

This value can be passed as a querystring or in the body of the request, in the `marketingData` field. For more information, access [Why are the UTMs not being applied to the cart?](https://developers.vtex.com/vtex-rest-api/docs/why-are-the-utms-not-being-applied-to-the-cart).