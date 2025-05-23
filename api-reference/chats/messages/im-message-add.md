# Add Message im.message.add

{% note warning "We are still updating this page" %}

Some data may be missing — we will complete it shortly.

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

The method `im.message.add` sends a message from the current user to a chat.

#|
|| **Parameter** | **Example** | **Description** | **Revision** ||
|| **DIALOG_ID^*^**
[`string`](../../data-types.md) | `chat13`
or
`256` | Identifier of the dialog. Format:
- **chatXXX** – chat of the recipient if the message is for chats
- **XXX** – identifier of the recipient if the message is for a private dialog | 18 ||
|| **MESSAGE^*^**
[`text`](../../data-types.md) | `Message text` | The text of the message.
[Formatting](./index.html) is supported | 18 ||
|| **SYSTEM**
[`boolean`](../../data-types.md) | `N` | Whether to display messages as a system message or not, optional field, defaults to 'N' | 18 ||
|| **ATTACH**
[`object`](../../data-types.md) | [Example](./attachments/index.html) | Attachment | 18 ||
|| **URL_PREVIEW**
[`boolean`](../../data-types.md) | `Y` | Convert links to rich links, optional field, defaults to 'Y' | 18 ||
|| **KEYBOARD**
[`object`](../../data-types.md) | [Example](./keyboards.html) | Keyboard | 18 ||
|| **MENU**
[`object`](../../data-types.md) | [Example](./menu.html) | Context menu | 18 ||
|#

{% include [Parameter Notes](../../../_includes/required.md) %}

## Examples

{% include [Examples Notes](../../../_includes/examples.md) %}

{% list tabs %}

- cURL (Webhook)

    ```bash
    curl -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{DIALOG_ID: "chat5",MESSAGE: "Message [B]with attachment[/B] in primary color and supporting [I]bb-codes[/I]",ATTACH: [{MESSAGE: "API will be available in update [B]im 24.0.0[/B]"}]}' \
    https://**put_your_bitrix24_address**/rest/**put_your_user_id_here**/**put_your_webhook_here**/im.message.add
    ```

- cURL (OAuth)

    ```bash
    curl -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{DIALOG_ID: "chat5",MESSAGE: "Message [B]with attachment[/B] in primary color and supporting [I]bb-codes[/I]",ATTACH: [{MESSAGE: "API will be available in update [B]im 24.0.0[/B]"}]}' \
    https://**put_your_bitrix24_address**/rest/im.message.add
    ```

- JS

    ```js
    BX24.callMethod(    
        'im.message.add',
        {
            DIALOG_ID: "chat5",
            MESSAGE: "Message [B]with attachment[/B] in primary color and supporting [I]bb-codes[/I]",
            ATTACH: [
                {
                    MESSAGE: "API will be available in update [B]im 24.0.0[/B]"
                },
            ],
        },
        function(result) {
            console.log('response', result.answer);
            if(result.error())
                alert("Error: " + result.error());
            else
            console.log(result.data());
        }
    );
    ```

- PHP

    ```php
    require_once('crest.php');

    $result = CRest::call(
        'im.message.add',
        [
            "DIALOG_ID" => "chat20921",
            "MESSAGE"   => "Message [B]with attachment[/B] in primary color and supporting [I]bb-codes[/I]",
            "ATTACH"   => [
                [
                    "MESSAGE" => "API will be available in update [B]im 24.0.0[/B]"
                },
            ],
        ]
    );

    echo '<pre>';
    print_r($result);
    echo '</pre>';
    ```

{% endlist %}

{% note tip "Typical use-cases and scenarios" %}

- [Example of using the method in the "EchoBot" application](https://github.com/bitrix24com/bots)

{% endnote %}

## Success Response

```json
{
    "result": 11
}
```

**Execution result**: message identifier `MESSAGE_ID` or error.

## Error Response

```json
{
    "error": "USER_ID_EMPTY",
    "error_description": "Recipient identifier is not specified when sending a message in a one-on-one chat"
}
```

### Key Descriptions

- `error` – code of the occurred error
- `error_description` – brief description of the occurred error

### Possible Error Codes

#|
|| **Code** | **Description** ||
|| **USER_ID_EMPTY** | Recipient identifier is not specified when sending a message in a one-on-one chat ||
|| **CHAT_ID_EMPTY** | Recipient chat identifier is not specified when sending a message in a chat ||
|| **ACCESS_ERROR** | Insufficient permissions to send a message ||
|| **MESSAGE_EMPTY** | Message text is not provided ||
|| **ATTACH_ERROR** | The entire provided attachment object failed validation ||
|| **ATTACH_OVERSIZE** | The maximum allowable size of the attachment (30 KB) has been exceeded ||
|| **KEYBOARD_ERROR** | The entire provided keyboard object failed validation ||
|| **KEYBOARD_OVERSIZE** | The maximum allowable size of the keyboard (30 KB) has been exceeded ||
|| **MENU_ERROR** | The entire provided menu object failed validation ||
|| **MENU_OVERSIZE** | The maximum allowable size of the menu (30 KB) has been exceeded ||
|| **PARAMS_ERROR** | Something went wrong ||
|#

## Related Links

- [How to work with keyboards](./keyboards.html)
- [How to work with attachments](./attachments/index.html)
- [Message formatting](./index.html)
- [Working with context menus](./menu.html)