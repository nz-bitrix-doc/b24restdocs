# Set or Remove the "Unread" Flag for the Chat im.recent.unread

{% note warning "We are still updating this page" %}

Some data may be missing — we will complete it soon.

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

The method `im.recent.unread` sets the "unread" label on a chat or conversation.

#|
|| **Parameter** | **Example** | **Description** | **Revision** ||
|| **DIALOG_ID^*^**
[`unknown`](../../data-types.md) | `'chat74'` | Identifier of the conversation. Format:
- **chatXXX** – chat of the recipient, if the message is for a chat
- **XXX** – identifier of the recipient, if the message is for a private conversation | 30 ||
|| **ACTION**
[`unknown`](../../data-types.md) | `'Y'` | Set / remove the "unread" label on the conversation - `'Y'|'N'` | 30 ||
|#

{% include [Footnote about parameters](../../../_includes/required.md) %}

## Examples

{% list tabs %}

- JS

    ```js
    BX24.callMethod(
        'im.recent.unread',
        {
            DIALOG_ID: 'chat74',
            ACTION: 'Y'
        },
        res => {
            if (res.error())
            {
            console.error(result.error().ex);
            }
            else
            {
            console.log(res.data())
            }
        }
    )
    ```

{% endlist %}

{% include [Footnote about examples](../../../_includes/examples.md) %}

## Response on Success

```json
{
    "result": true //if the label was successfully set|removed
}
```

## Response on Error

```json
{
    "error":"DIALOG_ID_EMPTY",
    "error_description":"Dialog ID can't be empty"
}
```

### Description of Keys

- `error` – code of the occurred error
- `error_description` – brief description of the occurred error

### Possible Error Codes

#|
|| **Code** | **Description** ||
|| **DIALOG_ID_EMPTY** | The parameter `DIALOG_ID` was not provided or does not match the format. ||
|#