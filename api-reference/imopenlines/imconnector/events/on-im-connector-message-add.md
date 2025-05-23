# When Receiving New Messages OnImConnectorMessageAdd

{% note warning "We are still updating this page" %}

Some data may be missing — we will complete it soon.

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _not exported to prod_" %}

- check the link to CHAT_API
- types and requiredness of parameters are not specified
- 
{% endnote %}

{% endif %}

> Scope: [`imopenlines`](../../../scopes/permissions.md)
>
> Who can subscribe: any user

This event marks a new message from Open Lines. The event is triggered for full-fledged connectors, such as Telegram or VKontakte. It does not work with the [widget or online chat](*widget_key), which are more like js-applications.

It is essential to call the method [**imconnector.send.status.delivery**](../imconnector-send-status-delivery.md) in response; otherwise, the message will be marked as undelivered in the messenger.

## Parameters

#|
|| **Parameter** | **Description** | **Version** ||
|| **CONNECTOR** | Connector ID (this is used to check if the event belongs to the verifier). | ||
|| **LINE** | Open line ID. | ||
|| **MESSAGES** | An array of messages, where each message is described by an array of the following format:


```json
{
"im": {
    "chat_id": 845,
    "message_id": 344029
},
"message": {
    "text": "Sergey \"Pokoiev\":\n Test message"
},
"chat": {
    "id": "2"
}
}
```
| ||
|#

{% include [Footnote on parameters](../../../../_includes/required.md) %}

[*widget_key]: See the documentation for CHAT API. [Learn more...](../../../chats/index.md)