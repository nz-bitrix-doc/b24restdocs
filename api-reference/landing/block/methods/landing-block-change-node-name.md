# Change the Tag Name with landing.block.changeNodeName

{% note warning "We are still updating this page" %}

Some data may be missing here — we will fill it in shortly.

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _not exported to prod_" %}

- edits needed for writing standards
- parameter types are not specified
- parameter requirements are not indicated
- examples are missing
- success response is absent
- error response is absent

{% endnote %}

{% endif %}

> Scope: [`landing`](../../../scopes/permissions.md)
>
> Who can execute the method: any user

The method `landing.block.changeNodeName` changes the tag name. For example, it is required to change the h3 tag to an h1 tag. It will return _true_ on success or an error.

## Parameters

#|
|| **Method** | **Description** | **Available since** ||
|| **lid**
[`unknown`](../../../data-types.md) | Page identifier | ||
|| **block**
[`unknown`](../../../data-types.md) | Block identifier | ||
|| **data**
[`unknown`](../../../data-types.md) | Array of selectors and new values. See the example for more details. A selector can be passed without specifying a position (for example, `.landing-block-node-text`), in which case all cards matching this selector will be changed. It can also be passed with a position specified (for example, `.landing-block-node-text@2`), in which case only the card at the specified position (zero-based) will be changed. | ||
|#

## Examples

{% list tabs %}

- JS

    ```js
    BX24.callMethod(
        'landing.block.changeNodeName',
        {
            lid: 2006,
            block: 20476,
            data: {
                '.landing-block-node-small-title@0': 'i',
                '.landing-block-node-small-title@1': 'u'
            }
        },
        function (result)
        {
            if (result.error())
            {
                console.error(result.error());
            }
            else
            {
                console.info(result.data());
            }
        }
    );
    ```

{% endlist %}

{% include [Footnote about examples](../../../../_includes/examples.md) %}