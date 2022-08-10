---
title: "Scalapay Connector"
slug: "vtex-integration-scalapay"
excerpt: "vtex.integration-scalapay@0.1.24"
hidden: true
createdAt: "2022-07-19T14:30:03.009Z"
updatedAt: "2022-07-19T14:30:03.009Z"
---
This application integrates Scalapay API with VTEX checkout through the **[scalapay-payment](https://www.notion.so/Scalapay-06e57f2829ce47cc8343ecb47d4b55ee)** Front APP.
The middleware makes use of the **[Payment Protocol Provider](https://help.vtex.com/es/tutorial/payment-provider-protocol--RdsT2spdq80MMwwOeEq0m) ,** API **[Scalapay](https://docs.api.scalapay.com/)** and the `paymentProvider 1.x` builder, it is developed under .Net.

# Install and configuration

1. Install `vtex.integration-scalapay` in your account.

```powershell
vtex install vtex.integration-scalapay 0.1.x
```

2. Then go to admin account in module  `Transactions/Payments/Settings` , in tab `Gateway affiliations`  search Scalapay and click in Scalapay.

    ![firefox_V3BrAtA606](https://user-images.githubusercontent.com/14004558/136470692-4d1ec4c5-fab5-4476-9a87-969a93414256.png)
    
3. Field fileds:
    - Fill in the `Application Key` field with the vtex account name.
    - Fill in the `Application Token` field with the token assigned for the Scalapay account.
    - `Workspace` with the name of the default development environment for testing is master.
    
    ![firefox_ZIkZaRQY3T](https://user-images.githubusercontent.com/14004558/136470862-88ffd401-f981-42f4-a6d0-8ba69d70a580.png)

    **Note**: If the Scalapay `Application Token` field is not filled, the connector will not work.

# Functional Guide

To use Scalapay payment method, at checkout select Scalapay as your payment method, this will open modal window the payment method that will redirect to Scalapay, for more information check **[scalapay-payment](https://www.notion.so/Scalapay-06e57f2829ce47cc8343ecb47d4b55ee).**

![BdLeOwPSxU](https://user-images.githubusercontent.com/14004558/136470987-be6a1eb5-a6dd-4f12-a64d-5142d836c5c9.gif)

# Middleware Guide

---

## Arquitecture

![Untitled](https://user-images.githubusercontent.com/14004558/136471063-c49e0cc3-d72e-4666-8821-0f871add16a3.png)

## Workflow

![Payment Workflow - Integration VTEX-ScalaPay-WorkFlow V3 drawio](https://user-images.githubusercontent.com/14004558/136471091-6b7bead6-5f8f-4299-80b7-29f9dd304ce3.png)

## Repository

It is located on github [link](https://github.com/vtex-apps/scalapay-connector) private.

## Controllers

It is located `Controllers/RoutesController.cs` . It contains the different endpoints for the scalapay flow.

- **Authorize**
    
    Endpoint is `/payments` . Custom endpoint. It is responsible for creating the order in the middleware, the order is assigned the `undefined` status. If the user reached the checkout but did not let the order expire it is validated and cancelled in the VTEX backend by calling the Callback and assigning a `denied` status.
    
- **Orderdetail**
    
    Endpoint is `/payments/{paymentId}/inbound/orderdetail` . Custom  endpoint in charge of creating the order in Scalapay and delivering in the `responseData` the URL of the checkout generated by Scalapay for the redirection of the user.
    In the `requestData.body` field the front-end delivers the data for the creation of the order.
    
    ```json
    {
        "requestId": "LA4E20D3B4E07B7E871F5B5BC9F91",
        "transactionId": "7EA2B84046B24D3F9D80DEFDD2E82935",
        "paymentId": "03902386FB55445EAE69E7FE0203FCC20",
        "authorizationId": null,
        "tid": null,
        "requestData": {
         "body": "{\"totalAmount\":{\"amount\":\"30.0\",\"currency\":\"EUR\"},\"consumer\":{\"phoneNumber\":\"0400000001\",\"givenNames\":\"Nombres\",\"surname\":\"Apellidos\",\"email\":\"prueba@vtex.com.br\"},\"shipping\":{\"name\":\"Joe Consumer\",\"line1\":\"Via della Rosa, 23\",\"suburb\":\"Montelupo Fiorentino\",\"postcode\":\"50056\",\"countryCode\":\"IT\",\"phoneNumber\":\"0400000000\"},\"items\":[{\"name\":\"T-Shirt\",\"category\":\"clothes\",\"subcategory\":[\"shirt\",\"long-sleeve\"],\"brand\":\"TopChoice\",\"gtin\":\"123458791330\",\"sku\":\"12341234\",\"quantity\":1,\"price\":{\"amount\":\"10.00\",\"currency\":\"EUR\"}},{\"name\":\"Jeans\",\"category\":\"clothes\",\"subcategory\":[\"pants\",\"jeans\"],\"brand\":\"TopChoice\",\"gtin\":\"123458722222\",\"sku\":\"12341235\",\"quantity\":1,\"price\":{\"amount\":\"20.00\",\"currency\":\"EUR\"}}],\"merchant\":{\"redirectConfirmUrl\":\"https:\/\/portal.staging.scalapay.com\/success-url\",\"redirectCancelUrl\":\"https:\/\/portal.staging.scalapay.com\/failure-url\"},\"merchantReference\":\"11112223333\",\"orderExpiryMilliseconds\":1800000}"
        }
    }
    ```
    
    ```json
    {
        "paymentId": "03902386FB55445EAE69E7FE0203FCC20",
        "responseData": {
            "statusCode": 200,
            "contentType": "application/json",
            "content": "{\"checkoutUrl\":\"https://portal.staging.scalapay.com/checkout/D6B9KSJ4Q89I\",\"expiresDate\":\"2021-08-19T16:49:46.902Z\",\"token\":\"D6B9KSJ4Q89I\"}"
        },
        "code": "",
        "message": "",
        "requestId": "LA4E20D3B4E07B7E871F5B5BC9F91"
    }
    ```
    
     
    
- **Capture**
    
    Endpoint is `/payments/{paymentId}/inbound/capture` . Custom endpoint. It is in charge of confirming the capture in Scalapay. The Middleware calls the callback to update the status to approved in VTEX.
    
- **Settle**
    
    Endpoint is `/payments/{paymentId}/settlements` . Endpoint called by VTEX to confirm the capture and settlement of the order. Within this method the validation of the status of the order is `charged` and that the status capture is `captured` in Mollie.
    
- **Refund**
    
    Endpoint is `/payments/{paymentId}/refunds` . Endpoint called by VTEX. It is responsible for refunding in Mollie.
    
- **Cancel**
    
    Endpoint is `/payments/{paymentId}/cancellations` . Endpoint called by VTEX to cancellation of the order. If the order has already been captured and the request arrives to this method it performs the order refund.
    
- **Cancellation**
    
    Endpoint is `/payments/{paymentId}/cancellations` . Custom endpoint. Endpoint called by FrontEnd to cancellation of the order.
    

## Data

It contains the interfaces of the methods to be used for updating, creating and querying in DynamoDB.

## Models

It contains the input and output classes used in DynamoDB, Scalapay and VTEX.They are segregated by their function

![Code_OpVjrPfMG0](https://user-images.githubusercontent.com/14004558/136471150-2c47cf62-fb36-4a83-9003-43074c21e47e.png)

## Services

Contains the interfaces and services (clients) used for DynamoDB, Scalapay and VTEX.

## Utils

It contains the constants, enum and messages used in the connector. If a new message needs to be modified or added, it must be added or modified in the `Messages.cs` file.

![Code_ieG52vZRfo](https://user-images.githubusercontent.com/14004558/136471181-2014ae86-b74e-47fa-a322-d0997b8d96bd.png)

## PaymentProvider

Contains the payment methods that will be accepted in the connector, this configuration is compiled by the Builder `"paymentProvider": "1.x"` declared in the manifest.

## appsettings.json

Contains the connector configurations. The value `ScpParam.paymentAppName` is the name of the front APP so that the modal can be shown, if this name is not equal to the front APP the modal will not be shown in the VTEX checkout.


**Upcoming documentation:**

 - [Fix refund](https://github.com/vtex-apps/scalapay-connector/pull/3)