---
title: "MasterData API - v1 - Overview"
slug: "master-data-api-v1-overview"
hidden: false
createdAt: "2019-12-18T20:03:10.002Z"
updatedAt: "2021-04-20T14:25:54.637Z"
---
VTEX Master Data is an easy-to-use, secure, fast, scalable and extensible repository. It allows you to create your own entities, store data and consult directly from the storefront or use it to store info for some external integrations. More information can also be found in the [Master Data section](doc:master-data-introduction) of our API Guide.

There are internal VTEX modules that use VTEX Master Data as a data repository.

There are two ways to use Master Data:
1. Directly from the storefront.
2. Through an external integration.

## Directly from the storefront
If you need to use it inside the storefront, be aware of the following observations:
1. Use the storefront host to query or store information to avoid CORS.
2. Configure which information should be public and which shouldn't, inside the data entity.
3. Do *not* create query loops (the storefront may be affected with throttling and APIs may be turned off as a security protection).
4. Never add any type of authentication key via javascript code (`x-vtex-api-appkey` or `x-vtex-api-apptoken`).
[block:callout]
{
  "type": "warning",
  "body": "It's important to avoid CORS using the relative path."
}
[/block]
## External Integration
If you are dealing with an external integration, for example migrating client data from another service, be aware of the following observations:
1. Use the host `{{accountName}}.vtexcommercestable.com.br`.
2. Use the authentication keys (x-vtex-api-appkey ou x-vtex-api-apptoken).

## These are the most used attributes:
| Name | Description |
| -------- | -------- |
| accountName | Account name in VTEX License Manager |
| acronym | Data Entity acronym |
| id | Identifier of a document |
| x-vtex-api-appKey | User key |
| x-vtex-api-appToken | User token |