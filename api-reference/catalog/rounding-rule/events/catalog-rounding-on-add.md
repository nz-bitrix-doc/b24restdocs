# Event when adding a price rounding rule CATALOG.ROUNDING.ON.ADD

> Scope: [`catalog`](../../../scopes/permissions.md)
>
> Who can subscribe: any user

The event occurs when a price rounding rule is added.

## What the handler receives

Data is sent as a POST request {.b24-info}

```
[
    'event' => 'CATALOG.ROUNDING.ON.ADD',    
    'event_handler_id' => 1,
    'data' => [
        'FIELDS' => [
            'ID' => 1,
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

{% include [Note on required parameters](../../../../_includes/required.md) %}

#|
|| **Name**
`type` | **Description** ||
|| **event***  
[`string`](../../data-types.md) | Symbolic event code ||
|| **event_handler_id***  
[`integer`](../../data-types.md) | Event handler identifier ||
|| **data***  
[`object`](../../data-types.md) | Object containing event data.

The structure is described [below](#data) ||
|| **ts***  
[`integer`](../../data-types.md) | Timestamp of the event sent from the event queue ||
|| **auth***  
[`object`](../../data-types.md) | Object with authorization parameters and information about the account where the event occurred ||
|#

### Parameter data {#data}

{% include [Note on required parameters](../../../../_includes/required.md) %}

#|
|| **Name**
`type` | **Description** ||
|| **FIELDS***  
[`object`](../../data-types.md) | Object with properties of the price rounding rule.

The structure is described [below](#fields) ||
|#

### Parameter FIELDS {#fields}

{% include [Note on required parameters](../../../../_includes/required.md) %}

#|
|| **Name**
`type` | **Description** ||
|| **ID***  
[`catalog_rounding_rule.id`](../../data-types.md#catalog_rounding_rule) | Identifier of the price rounding rule. You can retrieve all fields of the price rounding rule by its identifier using the method [catalog.roundingRule.get](../catalog-rounding-rule-get.md) ||
|#

### Parameter auth {#auth}

{% include notitle [Table with keys in the auth array](../../../../_includes/auth-params-in-events.md) %}

## Continue exploring

- [{#T}](./catalog-rounding-on-update.md)
- [{#T}](./catalog-rounding-on-delete.md)