# @particular./shopify-request

[![npm version](https://img.shields.io/npm/v/@particular./shopify-request.svg)](https://www.npmjs.com/package/@particular./shopify-request) [![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release) [![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg)](https://github.com/prettier/prettier) [![CircleCI](https://img.shields.io/circleci/project/github/uniquelyparticular/shopify-request.svg?label=circleci)](https://circleci.com/gh/uniquelyparticular/shopify-request)
![dependency status: david](https://img.shields.io/david/uniquelyparticular/shopify-request.svg)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Funiquelyparticular%2Fshopify-request.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Funiquelyparticular%2Fshopify-request?ref=badge_shield)

> 🎮 Minimal [Shopify](https://www.shopify.com) API request library for Node

## Installation

```bash
yarn add @particular./shopify-request # npm install @particular./shopify-request
```

## Quickstart (OAuth)

```js
const { createClient } = require('@particular./shopify-request');
// import { createClient } from '@particular./shopify-request'

const shopify = new createClient({
  store_name: '...', //Shopify Store Name
  admin_access_token: '...', //Shopify OAuth token received after registering as Public App and installing to Store
  storefront_access_token: '...' //Shopify OAuth token received after using admin_access_token to call 'admin/storefront_access_tokens.json'
});

shopify
  .delete('admin/products/:product_id.json')
  .then(console.log)
  .catch(console.error);

shopify
  .get('admin/products.json')
  .then(console.log)
  .catch(console.error);

shopify
  .post('admin/products.json', {
    product: {
      title: 'My Product',
      body_html: "<strong>It's great!</strong>",
      variants: [
        {
          option1: 'S',
          price: '10.00',
          sku: '123'
        }
      ]
    }
  })
  .then(console.log)
  .catch(console.error);

shopify
  .put('admin/products/:product_id.json', {
    product: {
      id: 632910392,
      tags: 'tag 1, tag 2, tag 3'
    }
  })
  .then(console.log)
  .catch(console.error);
```

## Quickstart (Basic Auth)

**_NOTE: This should not be used in production as it passes `client_pass` in base64 encoded clear text using basic auth._**

```js
const shopify = new createClient({
  store_name: '...', //Shopify Store Name
  client_key: '...', //Shopify API Key
  client_pass: '...' //Shopify API Password
});
```

## Kitchen sink

```js
const shopify = new createClient({
    store_name: '...',
    admin_access_token: '...',
    storefront_access_token: '...',
    application: '...',
    headers: {
        // ...
    }
})

-OR- //access_token (above) -OR- client_key AND client_pass BUT INSECURE (below)

const shopify = new createClient({
    store_name: '...',
    client_key: '...',
    client_pass: '...'
    application: '...',
    headers: {
        // ...
    }
})
```

## Custom headers per request

The API provides you the ability to send various request headers that change the way data is stored or retrieved.

By default this library will encode all data as JSON, however you can customise this by setting your own `Content-Type` header as an additional argument to `get`, `patch`, `post`, `put` and `delete`.

**Note**: If you add the `Content-Type` custom header to `patch`, `post`, `put` or `delete` you will need to encode `data` yourself.

```js
const shopify = new createClient({
  store_name: '...',
  admin_access_token: '...',
  storefront_access_token: '...'
});

const headers = {
  'X-My-Header': 'custom'
};

shopify
  .get('admin/products.json', headers)
  .then(console.log)
  .catch(console.error);
```

_Contact [Adam Grohs](https://www.linkedin.com/in/adamgrohs/) @ [Particular.](https://uniquelyparticular.com) for any questions._


## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Funiquelyparticular%2Fshopify-request.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Funiquelyparticular%2Fshopify-request?ref=badge_large)