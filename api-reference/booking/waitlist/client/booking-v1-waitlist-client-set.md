# Add Clients to the Waitlist Record booking.v1.waitlist.client.set

> Scope: [`booking`](../../../scopes/permissions.md)
>
> Who can execute the method: any user

The method `booking.v1.waitlist.client.set` sets clients for the specified record in the waitlist.

## Method Parameters

{% include [Footnote on parameters](../../../../_includes/required.md) %}

#|
|| **Name**
`type` | **Description** ||
|| **waitListId*** 
[`integer`](../../../data-types.md) | Identifier of the waitlist record. 
Can be obtained using the methods [booking.v1.waitlist.add](../booking-v1-waitlist-add.md) and [booking.v1.waitlist.list](../booking-v1-waitlist-list.md) ||
|| **clients*** 
[`array`](../../../data-types.md) | Array of objects containing information about clients [(detailed description)](#clients) ||
|#

### Parameter clients {#clients}

#|
|| **Name**
`type` | **Description** ||
|| **id*** 
[`integer`](../../../data-types.md) | Identifier of the client, can be obtained using the method [crm.item.list](../../../crm/universal/crm-item-list.md) for contacts and companies ||
|| **type*** 
[`object`](../../../data-types.md) | Type of client in the format `{"module": "crm", "code": "CONTACT"}`.
Possible values for `code`: 
- `CONTACT` — [CRM contact](../../../crm/contacts/index.md)
- `COMPANY` — [CRM company](../../../crm/companies/index.md)

The structure of the object is returned by the method [booking.v1.clienttype.list](../../booking-v1-clienttype-list.md) ||
|#

## Code Examples

{% include [Footnote on examples](../../../../_includes/examples.md) %}

{% list tabs %}

- JS

    ```js
    BX24.callMethod(
        "booking.v1.waitlist.client.set",
        {
            waitListId: 4,
            clients: [
                {
                    id: 1,
                    type: {
                        module: "crm",
                        code: "CONTACT"
                    }
                },
                {
                    id: 2,
                    type: {
                        module: "crm",
                        code: "CONTACT"
                    }
                }
            ]
        },
        result => {
            if (result.error())
                console.error(result.error());
            else
                console.dir(result.data());
        }
    );
    ```

- cURL (Webhook)

    ```bash
    curl -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{"waitListId":4,"clients":[{"id":1,"type":{"module":"crm","code":"CONTACT"}},{"id":2,"type":{"module":"crm","code":"CONTACT"}}],"auth":"**put_access_token_here**"}' \
    https://**put_your_bitrix24_address**/rest/booking.v1.waitlist.client.set
    ```

- cURL (OAuth)

    ```bash
    curl -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{"waitListId":4,"clients":[{"id":1,"type":{"module":"crm","code":"CONTACT"}},{"id":2,"type":{"module":"crm","code":"CONTACT"}}]}' \
    https://**put_your_bitrix24_address**/rest/**put_your_user_id_here**/**put_your_webhook_here**/booking.v1.waitlist.client.set
    ```

- PHP

    ```php
    require_once('crest.php');

    $result = CRest::call(
        'booking.v1.waitlist.client.set',
        [
            'waitListId' => 4,
            'clients' => [
                [
                    'id' => 1,
                    'type' => [
                        'module' => 'crm',
                        'code' => 'CONTACT'
                    ]
                ],
                [
                    'id' => 2,
                    'type' => [
                        'module' => 'crm',
                        'code' => 'CONTACT'
                    ]
                ]
            ]
        ]
    );

    echo '<PRE>';
    print_r($result);
    echo '</PRE>';
    ```

{% endlist %}

## Response Handling

HTTP status: **200**

```json
{
    "result": true,
    "time": {
        "start": 1724068028.331234,
        "finish": 1724068028.726591,
        "duration": 0.3953571319580078,
        "processing": 0.13033390045166016,
        "date_start": "2025-01-21T13:47:08+02:00",
        "date_finish": "2025-01-21T13:47:08+02:00",
        "operating": 0
    }
}
```

### Returned Data

#|
|| **Name**
`type` | **Description** ||
|| **result**
[`boolean`](../../../data-types.md) | Root element of the response, contains `true` in case of success ||
|| **time**
[`time`](../../../data-types.md#time) | Information about the execution time of the request ||
|#

## Error Handling

HTTP status: **400**

```json
{
    "error": 1040,
    "error_description": "Wait list not found"
}
```

{% include notitle [error handling](../../../../_includes/error-info.md) %}

### Possible Error Codes

#|
|| **Code** | **Description** | **Value** ||
|| `0` | `Required fields:` | A required parameter inside `clients` is missing ||
|| `1040` | `Wait list not found` | The waitlist with the specified `id` was not found ||
|| `100` | `Could not find value for parameter` | A required parameter was not provided ||
|#

{% include [system errors](../../../../_includes/system-errors.md) %}

## Continue Learning

- [{#T}](./booking-v1-waitlist-client-unset.md)
- [{#T}](./booking-v1-waitlist-client-list.md)