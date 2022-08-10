---
title: "Project flow"
slug: "electrolux-electrolux-middleware"
excerpt: "electrolux.electrolux-middleware@1.3.0"
hidden: true
createdAt: "2022-07-18T15:51:50.594Z"
updatedAt: "2022-07-28T18:42:12.117Z"
---
- This is a middleware project, meaning that its purpose is to be a intermediate solution for implementing security between requests going to the database.
- Every request that aims to change or retrieve any information in the database will have to go through this middleware.
- In order to acomplish a higher level of security we have only a single endpoint for requests.
- This endpoint only accepts requests with the POST method.
- The body of the request contains the information about the operation to be performed such as payload and security token.

## Request Flow

- The request is received and first dealt with in the index.ts file, then it follows this sequence:
- main.ts
- securityCheck.ts
- if no logged in session info or a partner password is found or validated then everything stops and a 403 Forbidden response is returned.
- if user is logged in or we find a password AND DON'T yet have the confirmation token:
- encrypt.ts will generate the token and return it
- if user is logged in or we find a partner password it AND HAVE the confirmation token:
- checkTokenTimeValidity.ts
- if the request comes back before a 5 min period of time has elapsed then the safe flow continues
- if the request comes back after a 5 min period of time has elapsed then everything stops and a 403 Forbidden response is returned.
- After all the security checks have been performed then we go to handleReq.ts
- In the handleReq we dynamically import the requested method and call it with a object literal syntax.

# Folder structure

This project folder structure was based off https://github.com/goldbergyoni/nodebestpractices#-11-structure-your-solution-by-components, trying to create components separated by folders.
Each folder containing a specific functionality, like one for security and other for error handling and so on.

# Service Example

A reference app implementing a VTEX IO service with HTTP route handlers.

![Service Example Architecture](https://user-images.githubusercontent.com/18706156/77381360-72489680-6d5c-11ea-9da8-f4f03b6c5f4c.jpg)

We use [**KoaJS**](https://koajs.com/) as the web framework, so you might want to get into that

We also use the [**node-vtex-api**](https://github.com/vtex/node-vtex-api), a VTEX set of utilities for Node services. You can import this package using NPM from `@vtex/api` (already imported on this project)

- Start from `node/index.ts` and follow the comments and imports :)

## Recipes

### Defining routes on _service.json_

```json
{
  "memory": 256,
  "ttl": 10,
  "timeout": 2,
  "minReplicas": 2,
  "maxReplicas": 4,
  "routes": {
    "status": {
      "path": "/_v/status/:code",
      "public": true
    }
  }
}
```

The `service.json` file that sits on the root of the `node` folder holds informations about this service, like the maximum timeout and number of replicas, what might be discontinued on the future, but also **sets its routes**.

Koa uses the [path-to-regexp](https://github.com/pillarjs/path-to-regexp) format for defining routes and, as seen on the example, we use the `:code` notation for declaring a **route param** named code, in this case. A HTTP request for `https://{{workspace}}--{{account}}.myvtex.com/_v/status/500` will match the route we've defined.

For cach _key_ on the `routes` object, there should be a **corresponding entry** on the exported Service object on `node/index.ts`, this will hook your code to a specific route.

### Access Control

You can also provide a `public` option for each route. If `true`, that resource will be reachable for everyone on the internet. If `false`, VTEX credentials will be requested as well.

Another way of controlling access to specific routes is using **ReBACs (Resource-based access)**, that supports more robust configuration. You can read more [on this document](https://docs.google.com/document/d/1ZxNHMFIXfXz3BgTN9xyrHL3V5dYz14wivYgQjRBZ6J8/edit#heading=h.z7pad3qd2qw7) (VTEX only).

#### Query String

For `?accepting=query-string`, you **don't need to declare anything**, as any query provided to the URL will already be available for you to use on the code as `ctx.query`, already parsed as an object, or `ctx.queryString`, taken directly from the URL as a string.

#### Route Params

Route Params will be available for you to use on the code as `ctx.vtex.params`, already parsed as an object.
For a path like `/_v/status/:code`, if you receive the request `/_v/status/200`, `ctx.vtex.params` will return `{ code: '200' }`

#### HTTP methods

When you define a route on the `service.json`, your NodeJS handlers for that route will be triggered **on every HTTP method** (GET, POST, PUT...), so, if you need to handle them separately you need to implement a "sub-router". Fortunately, the _node-vtex-api_ provides a helper function `method`, exported from `@vtex/api`, to accomplish that behaviour. Instead of passing your handlers directly to the corresponding route on `index.ts`, you pass a `method` call passing **an object with the desired method as key and one handler as its corresponding value**. Check this example:

```typescript
import { method } from '@vtex/api'
...

export default new Service<Clients, State>({
  clients,
  routes: {
    status: method({
      GET: statusGetHandler,
      POST: statusPostHandler,
    }),
  },
})
```

### Throwing errors

When building a HTTP service, we should follow HTTP rules regarding data types, cache, authorization, and status code. Our example app sets a `ctx.status` value that will be used as a HTTP status code return value, but often we also want to give proper information about errors as well.

The **node-vtex-api** already exports a handful of **custom error classes** that can be used for that purpose, like the `NotFoundError`. You just need to throw them inside one of the the route handlers that the appropriate response will be sent to the server.

```typescript
import { UserInputError } from '@vtex/api'

export async function validate(ctx: Context, next: () => Promise<any>) {
  const { code } = ctx.vtex.route.params
  if (isNaN(code) || code < 100 || code > 600) {
    throw new UserInputError('Code must be a number between 100 and 600')
  }
...
```

You can check all the available errors [here](https://github.com/vtex/node-vtex-api/tree/fd6139349de4e68825b1074f1959dd8d0c8f4d5b/src/errors), but some are not useful for just-HTTP services. Check the most useful ones:

| Error Class           | HTTP Code |
| --------------------- | :-------: |
| `UserInputError`      |    400    |
| `AuthenticationError` |    401    |
| `ForbiddenError`      |    403    |
| `NotFoundError`       |    404    |

You can also **create your custom error**, just see how it's done above ;)

### Reading a JSON body

When writing POST or PUT handlers, for example, often you need to have access to the **request body** that comes as a JSON format, which is not provided directly by the handler function.

For this, you have to use the [co-body](https://www.npmjs.com/package/co-body) package that will parse the request into a readable JSON object, used as below:

```typescript
import { json } from 'co-body'
export async function method(ctx: Context, next: () => Promise<any>) {
    const body = await json(ctx.req)
```

### Other example apps

We use Node services across all VTEX, and there are a lot inspiring examples. If you want to dive deeper on learning about this subject, don't miss those internal apps: [builder-hub](https://github.com/vtex/builder-hub) or [store-sitemap](https://github.com/vtex-apps/store-sitemap)

## Testing

`@vtex/test-tools` and `@types/jest` should be installed on `./node` package as `devDependencies`.

Run `vtex test` and [Jest](https://jestjs.io/) will do its thing.

Check the `node/__tests__/simple.test.ts` test case and also [Jest's Documentation](https://jestjs.io/docs/en/getting-started).

## Splunk Dashboard

We have an (for now, VTEX-only, internal) Splunk dashboard to show all metrics related to your app. You can find it [here](https://splunk7.vtex.com/en-US/app/vtex_colossus/node_app_metrics).

After linking this app and making some requests, you can select `vtex.service-example` and see the metrics for your app. **Don't forget to check the box Development, as you are linking your app in a development workspace**.

For convenience, the link for the current version: https://splunk7.vtex.com/en-US/app/vtex_colossus/node_app_metrics?form.time.earliest=-30m%40m&form.time.latest=%40m&form.picked_context=false&form.picked_region=aws-us-east-*&form.picked_service=vtex.service-example

### Fetch encrypt example:

>DON'T PUT THE KEYS WITH SPACE

```javascript
(async () => {
  const rawResponse = await fetch(`${URL}/middleware`, {
    method: 'POST',
    headers: {
      'Accept': 'application/json',
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
        "typeReq":"encInternal",
        "data": {"vtexKey":"","vtexToken":"","zendeskToken":""}
    })
  }).then(response => response.text())
    .then(data => console.log(data));
})();
```

### Fetch comunication zendesk example:

```javascript
(async () => {
  const rawResponse = await fetch(`${URL}/middleware`, {
    method: 'POST',
    headers: {
      'Accept': 'application/json',
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
        "typeReq":"createTicket",
        "data": {
    address:'Teste de Direccion',
    addressAdult: 'Teste Direccion',
    bienContratado:'Producto',
    claim:'Quiebra del Equipamento',
    comunication:'Correo Electrónico',
    contentClaim: 'Peça de Reposição',
    departamento:'AYACUCHO',
    descProduct:'Heladeira Frost',
    distrito:'CARAPOS',
    document:'DNI',
    email:'brooks6048@uorak.com',
    emailAdult: 'joritz1665@uorak.com',
    mayorEdad:'No',
    name:'Teste',
    nameAdult: 'Teste',
    nroDocument:'5134855464',
    origin:'Libro de Reclamaciones',
    phone:'24988965481',
    phoneAdult: '24988965481',
    provincia:'HUANCA SANCOS',
    storeAttendement:"Pagina Web",
    subjet:'Envio via API Libro de Reclamaciones',
    surnameFather: 'Teste Paterno',
    surnameMother:'Teste Materno',
    typeClaim:'Queja',
    typePhone:'Celular'
  }
    })
  });
  const content = await rawResponse.json();

  console.log(content);
})();
```

### Fetch comunication newsletter example

```javascript
(async () => {
  const rawResponse = await fetch(`${URL}/middleware`, {
    method: 'POST',
    headers: {
      'Accept': 'application/json',
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
        "typeReq":"saveNL",
        "data": {
            name: 'Test',
            email: 'test@test.com',
            terms: true,
            promotionAggreement: false,
            telephone: '(xx) xxxx-xxxx',
            origem: 'Origem',
            coupon: 'COUPON123'
          }
    })
  }).then(response => response.text())
    .then(data => console.log('data:',data));
})();
```

### Fetch comunication newsletter with interests example

```javascript
(async () => {
  const rawResponse = await fetch(`/middleware`, {
    method: 'POST',
    headers: {
      'Accept': 'application/json',
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
        "typeReq":"leadPlus",
        "data": {
            name: 'Test',
            email: 'test@test.com',
            terms: true,
            promotionAggreement: false,
            telephone: '(xx) xxxx-xxxx'
            origem: 'Origem',
            interests: 'Interests',
          }
    })
  }).then(response => response.text())
    .then(data => console.log('data:',data));
})();
```