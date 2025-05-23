# Get Network Address Ranges timeman.networkrange.get

> Scope: [`timeman`](../../scopes/permissions.md)
>
> Who can execute the method: administrator

The method `timeman.networkrange.get` retrieves the ranges of network addresses for the office network.

## Method Parameters

No parameters.

## Code Examples

{% include [Examples Note](../../../_includes/examples.md) %}

{% list tabs %}

- cURL (Webhook)

    ```bash
    curl -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{}' \
    https://**put_your_bitrix24_address**/rest/**put_your_user_id_here**/**put_your_webhook_here**/timeman.networkrange.get
    ```

- cURL (OAuth)

    ```bash
    curl -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{"auth":"**put_access_token_here**"}' \
    https://**put_your_bitrix24_address**/rest/timeman.networkrange.get
    ```

- JS

    ```js
    BX24.callMethod(
        'timeman.networkrange.get',
        {},
        function(result){
            if(result.error())
            {
                console.error(result.error().ex);
            }
            else
            {
                console.log(result.data());
            }
        }
    );
    ```

- PHP

    ```php
    require_once('crest.php');

    $result = CRest::call(
        'timeman.networkrange.get',
        []
    );

    echo '<PRE>';
    print_r($result);
    echo '</PRE>';
    ```

{% endlist %}

## Response Handling

HTTP Status: **200**

```json
{
    "result": [
        {
            "ip_range": "10.0.0.0-10.255.255.255",
            "name": "10.x.x.x"
        },
        {
            "ip_range": "172.16.0.0-172.31.255.255",
            "name": "172.x.x.x"
        },
        {
            "ip_range": "192.168.0.0-192.168.255.255",
            "name": "192.168.x.x"
        }
    ],
    "time": {
        "start": 1742999109.792954,
        "finish": 1742999109.827862,
        "duration": 0.034908056259155273,
        "processing": 0.0008471012115478516,
        "date_start": "2025-03-26T17:25:09+02:00",
        "date_finish": "2025-03-26T17:25:09+02:00",
        "operating_reset_at": 1742999709,
        "operating": 0
    }
}
```

### Returned Data

#|
|| **Name**
`type` | **Description** ||
|| **result**
[`array`](../../data-types.md) | Root element of the response.

Contains a list of objects. Each object contains a description of the [network address range](#ip_range) ||
|| **time**
[`time`](../../data-types.md#time) | Information about the request execution time ||
|#

#### Range Object {#ip_range}

#|
|| **Name**
`type` | **Description** ||
|| **ip_range**
 [`string`](../../data-types.md) | Network address range ||
|| **name**
 [`string`](../../data-types.md) | Name of the range ||
|#

## Error Handling

HTTP Status: **400**

```json
{
    "error": "ACCESS_ERROR",
    "error_description": "You don't have access to user this method"
}
```

{% include notitle [error handling](../../../_includes/error-info.md) %}

### Possible Error Codes

#|
|| **Code** | **Description** | **Value** ||
|| `ACCESS_ERROR` | You don't have access to user this method | Method is only available to the administrator ||
|#

{% include [system errors](../../../_includes/system-errors.md) %}

## Continue Learning 

- [{#T}](./index.md)
- [{#T}](./timeman-networkrange-set.md)
- [{#T}](./timeman-networkrange-check.md)