# Create Department department.add

> Scope: [`department`](../scopes/permissions.md)
>
> Who can execute the method: user with rights to modify the structure

The method `department.add` adds a new department to the company's structure.

## Method Parameters

{% include [Note on required parameters](../../_includes/required.md) %}

#|
|| **Name**
`type` | **Description** ||
|| **NAME***
[`string`](../data-types.md) | Name of the department ||
|| **SORT**
[`int`](../data-types.md) | Sorting field for the department ||
|| **PARENT***
[`int`](../data-types.md) | Identifier of the parent department ||
|| **UF_HEAD**
[`int`](../data-types.md) | Identifier of the user who will become the head of the department ||
|#

## Code Examples

{% include [Note on examples](../../_includes/examples.md) %}

{% list tabs %}

- cURL (Webhook)

    ```curl
    -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{
        "NAME": "Muggle Studies Department",
        "SORT": 450,
        "UF_HEAD": 1,
        "PARENT": 15
    }' \
    https://**put_your_bitrix24_address**/rest/**put_your_user_id_here**/**put_your_webhook_here**/department.add
    ```

- cURL (OAuth)

    ```curl
    -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{
        "NAME": "Muggle Studies Department",
        "SORT": 450,
        "UF_HEAD": 1,
        "PARENT": 15,
        "auth": "**put_access_token_here**"
    }' \
    https://**put_your_bitrix24_address**/rest/department.add
    ```

- JS

    ```js
    BX24.callMethod(
        'department.add',
        {
            "NAME": "Muggle Studies Department",
            "SORT": 450,
            "UF_HEAD": 1,
            "PARENT": 15
        },
        function(result)
        {
            if(result.error())
                console.error(result.error().ex);
            else
                console.log(result.data());
        }
    );
    ```

- PHP

    ```php
    require_once('crest.php');

    $result = CRest::call(
        'department.add',
        [
            'NAME' => 'Muggle Studies Department',
            'SORT' => 450,
            'UF_HEAD' => 1,
            'PARENT' => 15,
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
    "result": 18,
    "time": {
        "start": 1736927311.779587,
        "finish": 1736927312.132503,
        "duration": 0.35291600227355957,
        "processing": 0.17050600051879883,
        "date_start": "2025-01-15T07:48:31+00:00",
        "date_finish": "2025-01-15T07:48:32+00:00",
        "operating": 0.1704881191253662
    }
}
```

### Returned Data

#|
|| **Name**
`type` | **Description** ||
|| **result**
[`int`](../data-types.md) | Identifier of the created department ||
|| **time**
[`time`](../data-types.md) | Information about the execution time of the request ||
|#

## Error Handling

HTTP status: **400**

```json
{
    "error": "ERROR_CORE",
    "error_description": "The department name is not provided.\u003Cbr\u003E"
}
```

{% include notitle [error handling](../../_includes/error-info.md) %}

### Possible Error Codes

#|
|| **Code** | **Error Message** | **Description** ||
|| `ERROR_CORE` | The department name is not provided.\u003Cbr\u003E | The required parameter `NAME` is missing ||
|| `ERROR_CORE` | There can only be one top-level department in the company structure | The `PARENT` parameter is incorrectly specified ||
|| `ERROR_CORE` | Access denied | Insufficient rights to add a department ||
|#

{% include [system errors](../../_includes/system-errors.md) %}

## Continue Learning

- [{#T}](./department-update.md)
- [{#T}](./department-get.md)
- [{#T}](./department-delete.md)
- [{#T}](./department-fields.md)