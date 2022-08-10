---
title: "Save user data opt-in on Checkout"
slug: "save-user-data-opt-in-on-checkout"
hidden: false
createdAt: "2022-06-13T19:32:17.594Z"
updatedAt: "2022-06-13T19:58:36.709Z"
---
To comply with GDPR (General Data Protection Regulation - Europe) and LGPD - Lei Geral de Proteção de Dados (General Data Protection Law - Brazil), among other solutions, VTEX offers the **Save User Data opt-in** functionality. Through it, users can select whether they want the store to keep their personal and payment data saved.
[block:callout]
{
  "type": "warning",
  "body": "The **Save user data opt-in** feature is only available for Checkout v6."
}
[/block]
##Save user data opt-in activation

To use the **Save user data opt-in** functionality in your store, you must first enable it. Then, follow the settings below:

1. Make a `GET` request using the endpoint [Get orderForm configuration](https://developers.vtex.com/vtex-rest-api/reference/configuration).
2. Make a `POST` request using the endpoint [Update orderForm configuration](https://developers.vtex.com/vtex-rest-api/reference/updateorderformconfiguration) with the same data obtained in the GET request, just modifying the value of the `savePersonalDataAsOptIn` parameter from `null` to `true`.
3. Make a new `GET` request using the endpoint [Get orderForm configuration](https://developers.vtex.com/vtex-rest-api/reference/getorderformconfiguration) to confirm activation. This will be indicated by the presence of the `savePaymentData` and `savePersonalData` fields under the `clientPreferencesData` object in the `orderForm`.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/df79aae-savePersonalData1.PNG",
        "savePersonalData1.PNG",
        714,
        508,
        "#959799"
      ]
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "body": "Under the `storePreferencesData` object, the `saveUserData` field may be indicated as `true`. This field is ignored, and kept in this configuration for backwards compatibility only."
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/103d591-savePersonalData2.PNG",
        "savePersonalData2.PNG",
        928,
        481,
        "#828487"
      ]
    }
  ]
}
[/block]
##Saving personal and payment data

Once the **Save user data opt-in** is enabled, the user will have access to checkboxes on the Checkout page to select whether their personal and payment data should be kept by the store and used in future orders.

Checkbox for saving personal data:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3cccdf1-Contact_Information.png",
        "Contact Information.png",
        1266,
        854,
        "#f6f8f5"
      ]
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "body": "Previously, it was possible to display this checkbox by modifying the `display` property of the `.save-data` element, via CSS. However, with the **Save user data opt-in** enabled, the method through CSS is no longer recommended."
}
[/block]
Checkbox for saving payment data:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f1601b3-Pagamento.PNG",
        "Pagamento.PNG",
        1266,
        638,
        "#f9f9f9"
      ]
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "body": "The checkbox for saving payment data will only be shown if the user has already selected the option to save their personal data."
}
[/block]
Checkbox not available to save payment data if (the user has not previously selected the option to save personal data):


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5d3b723-Payment_No_Checkbox.png",
        "Payment_No Checkbox.png",
        1266,
        627,
        "#f9fafa"
      ]
    }
  ]
}
[/block]
If the user chooses to use two cards to pay for the purchase, when selecting the option to save payment data, the data of both cards will be saved. There is no option to save only one of the cards.

Checkbox to save payment data from both cards:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/32f86b5-Payment_two_cards.png",
        "Payment two cards.png",
        1266,
        906,
        "#fafafb"
      ]
    }
  ]
}
[/block]