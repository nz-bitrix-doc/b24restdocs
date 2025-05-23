# Get a List of Department Field Names `department.fields`

> Scope: [`department`](../scopes/permissions.md)
>
> Who can execute the method: any user

The method `department.fields` returns a list and description of available department fields.

No parameters.

## Code Examples

{% include [Footnote on examples](../../_includes/examples.md) %}

{% list tabs %}

- cURL (Webhook)

    ```curl
    -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{}' \
    https://**put_your_bitrix24_address**/rest/**put_your_user_id_here**/**put_your_webhook_here**/department.fields
    ```

- cURL (OAuth)

    ```curl
    -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{"auth":"**put_access_token_here**"}' \
    https://**put_your_bitrix24_address**/rest/department.fields
    ```

- JS

    ```js
    BX24.callMethod(
        "department.fields", {},
        function(result) {
            if (result.error()) {
                console.error(result.error());
            } else {
                console.info(result.data());
            }
        }
    );
    ```

- PHP

    ```php
    require_once('crest.php');

    $result = CRest::call('department.fields');

    echo '<PRE>';
    print_r($result);
    echo '</PRE>';
    ```

{% endlist %}

## Response Handling

HTTP Status: **200**

```json
{
    "result": {
        "ID": "ID",
        "NAME": "Department Name",
        "SORT": "Sorting Order",
        "PARENT": "Parent Department",
        "UF_HEAD": "Manager"
    },
    "time": {
        "start": 1736926600.426408,
        "finish": 1736926600.667272,
        "duration": 0.24086403846740723,
        "processing": 0.0050868988037109375,
        "date_start": "2025-01-15T07:36:40+00:00",
        "date_finish": "2025-01-15T07:36:40+00:00",
        "operating": 0
    }
}
```

### Returned Data

#|
|| **Name**
`type` | **Description** ||
|| **result**
[`object`](../data-types.md) | Root element of the response. Contains the list and description of fields ||
|| **time**
[`time`](../data-types.md) | Information about the execution time of the request ||
|#

## Error Handling

{% include [system errors](../../_includes/system-errors.md) %}

## Continue Learning 

- [{#T}](./department-add.md)
- [{#T}](./department-update.md)
- [{#T}](./department-get.md)
- [{#T}](./department-delete.md)