---
title: "Activate Warehouse"
slug: "activatewarehouse"
excerpt: "Activates a given warehouse, by warehouse ID."
hidden: false
createdAt: "2020-01-23T15:28:46.231Z"
updatedAt: "2020-02-17T21:20:01.581Z"
---
[block:api-header]
{
  "title": "Request body example"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "curl --location --request POST 'https://{accountName}.{environment}.com.br/api/logistics/pvt/configuration/warehouses/warehouseId/activation' \\\n--header 'x-vtex-api-appKey: {{X-VTEX-API-AppKey}}' \\\n--header 'x-vtex-api-appToken: {{X-VTEX-API-AppToken}}' \\\n--header 'Content-Type: application/json'",
      "language": "text",
      "name": "Request example"
    }
  ]
}
[/block]