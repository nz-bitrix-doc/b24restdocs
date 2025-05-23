# When Adding a Message to the Chat OnOpenLineMessageAdd

> Scope: [`imopenlines`](../../../scopes/permissions.md) 
>
> Who can subscribe: any user

The event `OnOpenLineMessageAdd` is triggered when a message is added to the open line chat.

[Subscribe](../../../events/event-bind.md) to the event only through the application. You can only receive events intended for the [connector](../../imconnector/index.md) added by the application.

## What the Handler Receives

Data is transmitted in the form of a POST request

```php
[
    'event' => 'ONOPENLINEMESSAGEADD',
    'eventId' => 1,
    'data' => [
        'DATA' => [
            [
                'connector' => [
                    'connector_id' => 'livechat',
                    'line_id' => 128,
                    'chat_id' => 10587,
                    'user_id' => 1985,
                ],
                'chat' => [
                    'id' => 10585
                ],
                'message' => [
                    'id' => 80964,
                    'date' => '',
                    'text' => 'hello',
                    'files' => [
                    ],
                    'attach' => '',
                    'system' => 'N',
                    'user_id' => 1985
                ],
                'ref' => [
                ],
                'extra' => [
                    'EXTRA_URL' => '' 
                ],
            ],
        ],
    ],
    'ts' => 1714649632,
    'auth' => [
        'access_token' => 's6p6eclrvim6da22ft9ch94ekreb52lv',
        'expires_in' => 3600,
        'scope' => 'imopenlines',
        'domain' => 'some-domain.bitrix24.com',
        'server_endpoint' => 'https://oauth.bitrix.info/rest/&#39;',
        'status' => 'F',
        'client_endpoint' => 'https://some-domain.bitrix24.com/rest/&#39;',
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
[`string`](../../../data-types.md) | Symbolic event code ||
|| **eventId***
[`integer`](../../../data-types.md) | Event identifier ||
|| **data***
[`object`](../../../data-types.md) | Object with [event data](#data) ||
|| **ts***
[`integer`](../../../data-types.md) | Timestamp of the event sent from the event queue ||
|| **auth***
[`object`](../../../data-types.md) | Object with authorization parameters and information about the account where the event occurred ||
|#

### Parameter data {#data}

{% include [Note on required parameters](../../../../_includes/required.md) %}

#|
|| **Name**
`type` | **Description** ||
|| **DATA***
[`object`](../../../data-types.md) | Object with [chat data](#chat-params) ||
|#

#### Parameter DATA {#chat-params}

{% include [Note on required parameters](../../../../_includes/required.md) %}

#|
|| **Name**
`type` | **Description** ||
|| **connector***
[`object`](../../../data-types.md) | Object with information about the connector:
- `connector_id` — connector identifier
- `line_id` — open line identifier
- `chat_id` — chat identifier
- `user_id` — user identifier in the external system
||
|| **chat***
[`object`](../../../data-types.md) | Object with information about the chat:
- `id` — chat identifier ||
|| **message***
[`object`](../../../data-types.md) | Object with information about the message:
- `id` — message identifier
- `date` — date and time of addition
- `text` — message text
- `files` — files
- `attach` — attached files
- `system` — flag indicating if the message is system. Has value `Y` if it is system 
- `user_id` — user identifier
||
|| **ref***
[`object`](../../../data-types.md) | Tracker code `trackId` for linking the message to a CRM object ||
|| **extra***
[`object`](../../../data-types.md) | Object with additional information:
- `EXTRA_URL` — external link for Bitrix24.Network ||
|#

### Parameter auth

{% include notitle [Parameter auth](../../../../_includes/auth-params-in-events.md) %}