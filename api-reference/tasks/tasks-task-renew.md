# Renew a task after its completion tasks.task.renew

{% if build == 'dev' %}

{% note alert "TO-DO _not exported to prod_" %}

- parameter types are not specified
- parameter requirements are not indicated
- examples are missing (there should be three examples - curl, js, php)
- no response in case of error
- no response in case of success
 
{% endnote %}

{% endif %}

{% note warning "We are still updating this page" %}

Some data may be missing here — we will complete it soon

{% endnote %}

> Scope: [`task`](../scopes/permissions.md)
>
> Who can execute the method: any user

The method `tasks.task.renew` renews a task after its completion.

## Parameters

#|
|| **Parameter** / **Type** | **Description** ||
|| **taskId**
[`unknown`](../data-types.md) | Task identifier. ||
|#

## Example

{% list tabs %}

- JS

    ```js
    BX24.callMethod(
        'tasks.task.renew',
        {taskId:1},
        function(res){console.log(res.answer.result);}
    );
    ```

{% endlist %}

{% include [Note on examples](../../_includes/examples.md) %}