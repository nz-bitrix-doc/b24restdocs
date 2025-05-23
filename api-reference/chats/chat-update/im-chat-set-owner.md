# Change Chat Owner im.chat.setOwner

{% note warning "We are still updating this page" %}

Some data may be missing here — we will complete it soon.

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _not exported to prod_" %}

- edits needed for writing standards
- parameter types are not specified
- examples are missing

{% endnote %}

{% endif %}

> Scope: [`im`](../../scopes/permissions.md)
>
> Who can execute the method: any user

The `im.chat.setOwner` method changes the owner of the chat.

#|
|| **Parameter** | **Example** | **Description** | **Revision** ||
|| **CHAT_ID^*^**
[`unknown`](../../data-types.md) | `13` | Chat identifier | 18 ||
|| **USER_ID^*^**
[`unknown`](../../data-types.md) | `2` | Identifier of the new chat owner | 18 ||
|#

{% include [Parameter Note](../../../_includes/required.md) %}

## Examples

{% include [Explanation of restCommand](../_includes/rest-command.md) %}

{% list tabs %}

- PHP

    ```php
    $result = restCommand(
        'im.chat.setOwner',
        Array(
            'CHAT_ID' => 13,
            'USER_ID' => '2'
        ),
        $_REQUEST[
            "auth"
        ]
    );
    ```

{% endlist %}

{% include [Examples Note](../../../_includes/examples.md) %}

## Response on Success

```json
{
    "result": true
}
```

## Response on Error

```json
{
    "error": "CHAT_ID_EMPTY",
    "error_description": "Chat identifier not provided"
}
```

### Description of Keys

- `error` – error code
- `error_description` – brief description of the error

### Possible Error Codes

#|
|| **Code** | **Description** ||
|| **CHAT_ID_EMPTY** | Chat identifier not provided ||
|| **USER_ID_EMPTY** | Identifier of the new chat owner not provided ||
|| **WRONG_REQUEST** | Method called not by the chat owner or the specified user is not a participant of the chat ||
|#