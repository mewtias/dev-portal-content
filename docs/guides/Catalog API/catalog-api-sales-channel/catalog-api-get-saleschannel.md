---
title: "Get Sales Channel by Id"
slug: "catalog-api-get-saleschannel"
excerpt: "Retrieves a specific sales channel by its ID."
hidden: false
createdAt: "2020-02-05T23:07:29.210Z"
updatedAt: "2022-02-03T16:34:00.088Z"
---
## Response object has the following properties:


| Attribute    | Type        | Description |
| --------------- |:---------:| -------------------------------------------------------------------------------------------:|
| `id` | integer | ID of Sales Channel |
| `Name` | string |  Sales Channel Name |
| `IsActive` | boolean | If the Sales Channel is Active |
| `ProductClusterId` | integer | If the Sales Channel has releated Product Cluster  |
| `CountryCode`  | string | Country Code in ISO 3166-1 alfa-3 Standard |
| `CultureInfo` | string     | Language Country code in LCIDstring Standard |
| `TimeZone` | string | Name of Time Zone |
| `CurrencyCode` | string | Currency Code in ISO 4217 standard  |
| `CurrencySymbol` | string | Currency symbol |
| `CurrencyLocale` | string | Currency Locale Code in LCID standard |
| `CurrencyFormatInfo` | object | Object with currency format details  |
| `CurrencyDecimalDigits` | integer | Quantity of Currency Decimal Digits |
| `CurrencyDecimalSeparator` | string | Define what Currency Decimal Separator will be apply|
| `CurrencyGroupSeparator` | string | Define what Currency Group Separator will be apply|
| `CurrencyGroupSize` | string | Define how many characters that will be grouped |
| `StartsWithCurrencySymbol` | boolean | Define if all prices will be initiated with Currency Symbol|
| `Origin` | string ||
| `Position` | integer | Define the position on index |
| `ConditionRule` | integer | Define what is the rule to activate de Sales Channel |




## Authentication

This is a public API so you do not need credentials to access it.