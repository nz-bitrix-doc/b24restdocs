# Event When Adding a Product CATALOG.PRODUCT.ON.ADD

> Scope: [`catalog`](../../../scopes/permissions.md)
>
> Who can subscribe: any user

The event occurs when a product is added.

## What the Handler Receives

Data is transmitted as a POST request {.b24-info}

```
[
    'event' => 'CATALOG.PRODUCT.ON.ADD',    
    'event_handler_id' => 1,
    'data' => [
        'FIELDS' => [
            'ID' => 1,            
            'TYPE' => 1,
        ],
    ],
    'ts' => 1714649632,
    'auth' => [
        'access_token' => 's6p6eclrvim6da22ft9ch94ekreb52lv',
        'expires_in' => 3600,
        'scope' => 'catalog',
        'domain' => 'some-domain.bitrix24.com',
        'server_endpoint' => 'https://oauth.bitrix.info/rest/',
        'status' => 'F',
        'client_endpoint' => 'https://some-domain.bitrix24.com/rest/',
        'member_id' => 'a223c6b3710f85df22e9377d6c4f7553',
        'refresh_token' => '4s386p3q0tr8dy89xvmt96234v3dljg8',
        'application_token' => '51856fefc120afa4b628cc82d3935cce',
    ],
]
```

## Parameters

{% include [Note on Required Parameters](../../../../_includes/required.md) %}

#|
|| **Name**
`type` | **Description** ||
|| **event***
[`string`](../../data-types.md) | Symbolic code of the event ||
|| **event_handler_id***
[`integer`](../../data-types.md) | Identifier of the event handler ||
|| **data***
[`object`](../../data-types.md) | Object with event data.

The structure is described [below](#data) ||
|| **ts***
[`integer`](../../data-types.md) | Timestamp of the event sent from the event queue ||
|| **auth***
[`object`](../../data-types.md) | Object with authorization parameters and information about the account where the event occurred ||
|#

### Parameter data {#data}

{% include [Note on Required Parameters](../../../../_includes/required.md) %}

#|
|| **Name**
`type` | **Description** ||
|| **FIELDS***
[`object`](../../data-types.md) | Object with product properties.

The structure is described [below](#fields) ||
|#

### Parameter FIELDS {#fields}

{% include [Note on Required Parameters](../../../../_includes/required.md) %}

#|
|| **Name**
`type` | **Description** ||
|| **ID***
[`catalog_product.id`](../../data-types.md#catalog_product)\|
[`catalog_product_sku.id`](../../data-types.md#catalog_product_sku)\|
[`catalog_product_offer.id`](../../data-types.md#catalog_product_offer)\|
[`catalog_product_service.id`](../../data-types.md#catalog_product_service) | Identifier of the product. You can retrieve all product fields by its identifier using the methods:
- [catalog.product.get](../../product/catalog-product-get.md) — for simple products
- [catalog.product.sku.get](../../product/sku/catalog-product-sku-get.md) — for parent products
- [catalog.product.offer.get](../../product/offer/catalog-product-offer-get.md) — for variations
- [catalog.product.service.get](../../product/service/catalog-product-service-get.md) — for services
||
|| **TYPE***
[`integer`](../../data-types.md) | Type of product:
- `1` — simple product
- `3` — parent product with variations
- `4` — variation
- `5` — variation without a product
- `6` — parent product without variations
- `7` — service
||
|#

### Parameter auth {#auth}

{% include notitle [Table with Keys in the auth Array](../../../../_includes/auth-params-in-events.md) %}

## Continue Learning

- [{#T}](./catalog-product-on-update.md)
- [{#T}](./catalog-product-on-delete.md)