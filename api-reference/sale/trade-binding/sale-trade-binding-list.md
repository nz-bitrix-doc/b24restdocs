# Get a list of orders from the sources sale.tradeBinding.list

> Scope: [`sale`](../../scopes/permissions.md)
>
> Who can execute the method: any user with the "View product catalog" access permission

The method `sale.tradeBinding.list` returns a list of orders from the sources.

## Method Parameters

{% include [Note on required parameters](../../../_includes/required.md) %}

#|
|| **Name**
`type` | **Description** ||
|| **select**
[`array`](../../data-types.md) | An array containing the list of fields to select (see fields of the object [sale_order_trade_binding](../data-types.md#sale_order_trade_binding)).

If not provided or an empty array is passed, all available order fields will be selected. ||
|| **filter**
[`object`](../../data-types.md) | An object for filtering the selected orders in the format `{"field_1": "value_1", ... "field_N": "value_N"}`. When specifying multiple fields, AND logic is used.

Possible values for `field` correspond to the fields of the object [sale_order_trade_binding](../data-types.md#sale_order_trade_binding).

An additional prefix can be assigned to the key to clarify the filter behavior. Possible prefix values:
- `=` — equals (works with arrays as well)
- `!=` - not equals
- `>` — greater than
- `<=` — less than or equal to
- `<` — less than
- `%` — LIKE, substring search. The `%` character in the filter value does not need to be passed. The search looks for the substring in any position of the string
- `=%` — LIKE, substring search. The `%` character needs to be passed in the value. Examples:
    - "mol%" — searching for values starting with "mol"
    - "%mol" — searching for values ending with "mol"
    - "%mol%" — searching for values where "mol" can be in any position
- `%=` — LIKE (see description above)
- `!%` — NOT LIKE, substring search. The `%` character in the filter value does not need to be passed. The search goes from both sides.
- `!=%` — NOT LIKE, substring search. The `%` character needs to be passed in the value. Examples:
    - "mol%" — searching for values not starting with "mol"
    - "%mol" — searching for values not ending with "mol"
    - "%mol%" — searching for values where the substring "mol" is not present in any position
- `!%=` — NOT LIKE (see description above) ||
|| **order**
[`object`](../../data-types.md) | An object for sorting the selected orders in the format `{"field_1": "order_1", ... "field_N": "order_N"}`.

Possible values for `field` correspond to the fields of the object [sale_order_trade_binding](../data-types.md#sale_order_trade_binding).

Possible values for `order`:
- `asc` — in ascending order
- `desc` — in descending order ||
|| **start**
[`integer`](../../data-types.md) | This parameter is used for managing pagination.

The page size of results is always static: 50 records.

To select the second page of results, you need to pass the value `50`. To select the third page of results — the value `100`, and so on.

The formula for calculating the `start` parameter value:

`start = (N-1) * 50`, where `N` is the desired page number ||
|#

## Code Examples

{% include [Note on examples](../../../_includes/examples.md) %}

{% list tabs %}

- cURL (Webhook)

    ```curl
    -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{"select":["orderId","tradingPlatformId"],"filter":{"!=tradingPlatformID":10},"order":{"tradingPlatformId":"DESC"}}' \
    https://**put_your_bitrix24_address**/rest/**put_your_user_id_here**/**put_your_webhook_here**/sale.tradeBinding.list
    ```

- cURL (OAuth)

    ```curl
    -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{"select":["orderId","tradingPlatformId"],"filter":{"!=tradingPlatformID":10},"order":{"tradingPlatformId":"DESC"},"auth":"**put_access_token_here**"}' \
    https://**put_your_bitrix24_address**/rest/sale.tradeBinding.list
    ```

- JS

    ```js
    BX24.callMethod(
        "sale.tradeBinding.list",
        {
            select: ['orderId', 'tradingPlatformId'],
            filter: {'!=tradingPlatformID': 10},
            order: {'tradingPlatformId': 'DESC'}
        },
        function(result)
        {
            if(result.error())
            {
                console.error(result.error());
            }
            else
            {
                console.dir(result.data());
            }
        }
    );
    ```

- PHP

    ```php
    require_once('crest.php');

    $result = CRest::call(
        'sale.tradeBinding.list',
        [
            'select' => ['orderId', 'tradingPlatformId'],
            'filter' => ['!=tradingPlatformID' => 10],
            'order' => ['tradingPlatformId' => 'DESC']
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
    "result": {
        "tradeBindings": [
            {
                "orderId": 685,
                "tradingPlatformId": "18"
            },
            {
                "orderId": 690,
                "tradingPlatformId": "4"
            },
            {
                "orderId": 607,
                "tradingPlatformId": "3"
            }
        ]
    },
    "total": 3,
    "time": {  
        "start": 1712135957.057659,  
        "finish": 1712135957.407821,  
        "duration": 0.3501620292663574,  
        "processing": 0.011919021606445312,  
        "date_start": "2024-04-03T11:19:17+02:00",  
        "date_finish": "2024-04-03T11:19:17+02:00",  
        "operating_reset_at": 1705765533,  
        "operating": 3.3076241016387939  
    }  
}
```

### Returned Data

#|
|| **Name**
`type` | **Description** ||
|| **result**
[`object`](../../data-types.md) | The root element of the response ||
|| **tradeBindings**
[`sale_order_trade_binding[]`](../data-types.md#sale_order_trade_binding) | An array of objects with information about the selected orders ||
|| **total**
[`integer`](../../data-types.md) | The total number of records found ||
|| **time**
[`time`](../../data-types.md) | Information about the execution time of the request ||
|#

## Error Handling

HTTP status: **400**

```json
{
    "error":200040300010,
    "error_description":"Access Denied"
}
```

{% include notitle [error handling](../../../_includes/error-info.md) %}

### Possible Error Codes

#|
|| **Code** | **Description** ||
|| `200040300010` | Insufficient permissions to execute the method ||
|| `0` | Other errors (e.g., fatal errors) ||
|#

{% include [system errors](../../../_includes/system-errors.md) %}

## Continue Learning 

- [{#T}](./sale-trade-binding-get-fields.md)