# Update the imbot.command.update

{% note warning "We are still updating this page" %}

Some data may be missing — we will complete it soon.

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _not exported to prod_" %}

- edits needed for writing standards
- parameter types are not specified
- not all parameters have examples in the table
- examples are missing
- no response in case of success
- no response in case of error
- links to pages that have not yet been created are not specified

{% endnote %}

{% endif %}

> Scope: [`imbot`](../../scopes/permissions.md)
>
> Who can execute the method: any user

The method `imbot.command.update` updates data in the team.

#|
|| **Parameter** | **Example** | **Description** | **Revision** ||
|| **COMMAND_ID^*^**
[`unknown`](../../data-types.md) | `13` | Identifier of the command to update | ||
|| **FIELDS^*^**
[`unknown`](../../data-types.md) | | Fields to update. At least one field must be specified. | ||
|| **EVENT_COMMAND_ADD**
[`unknown`](../../data-types.md) | `'http://www.hazz/chatApi/bot.php'` | Link to the command handler | ||
|| **HIDDEN**
[`unknown`](../../data-types.md) | `'N'` | Is the command hidden or not | ||
|| **EXTRANET_SUPPORT**
[`unknown`](../../data-types.md) | `'N'` | Is the command available to Extranet users | ||
|| **CLIENT_ID**
[`unknown`](../../data-types.md) | `''` | String identifier of the chatbot, used only in Webhook mode | ||
|| **LANG^*^**
[`unknown`](../../data-types.md) | 
```php
Array(
    Array(
        'LANGUAGE_ID' => 'en',
        'TITLE' => 'Get echo message',
        'PARAMS' => 'some text'
    )
)
```
 | New translation phrases, all previous ones will be deleted | ||
|#

{% include [Parameter notes](../../../_includes/required.md) %}

{% note warning %}

To process the command, the application must handle the command addition event [ONIMCOMMANDADD](./events/on-im-command-add.md).

{% endnote %}

{% note warning %}

It is mandatory to specify the translation array `LANG` for at least EN and DE. If there is no phrase for BY, UA, KZ, the default phrases from EN will be shown; if there is no phrase in EN, the command will be hidden. The same applies to other languages — if there are no phrases, the default phrases from EN will be shown; if there is no phrase in EN, the command will be hidden in the public part.

{% endnote %}

## Examples

{% include [Explanation about restCommand](../_includes/rest-command.md) %}

{% list tabs %}

- PHP

    ```php
    $result = restCommand(
        'imbot.command.update',
        Array(
            'COMMAND_ID' => 13,
            'FIELDS' => Array(
                'EVENT_COMMAND_ADD' => 'http://www.hazz/chatApi/bot.php',
                'HIDDEN' => 'N',
                'EXTRANET_SUPPORT' => 'N',
                'CLIENT_ID' => '',
                'LANG' => Array(
                    Array(
                        'LANGUAGE_ID' => 'en',
                        'TITLE' => 'Get echo message',
                        'PARAMS' => 'some text'
                    ),
                ),
            )
        ),
        $_REQUEST[
            "auth"
        ]
    );
    ```

{% endlist %}

{% include [Examples notes](../../../_includes/examples.md) %}

## Response in case of success

`true`

## Response in case of error

error

### Possible error codes

#|
|| **Code** | **Description** ||
|| **COMMAND_ID_ERROR** | Command not found. ||
|| **APP_ID_ERROR** | The chatbot does not belong to this application. It can only work with chatbots installed within the application. ||
|| **EVENT_COMMAND_ADD** | The event handler link is invalid or not specified. ||
|| **WRONG_REQUEST** | Something went wrong. ||
|#