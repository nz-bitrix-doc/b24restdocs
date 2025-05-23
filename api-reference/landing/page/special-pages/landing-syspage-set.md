# Set a special page for the site landing.syspage.set

{% note warning "We are still updating this page" %}

Some data may be missing here — we will complete it shortly.

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _not exported to prod_" %}

- missing parameters or fields
- parameter types not specified
- parameter requirements not specified
- examples missing
- success response missing
- error response missing

{% endnote %}

{% endif %}

> Scope: [`landing`](../../../scopes/permissions.md)
>
> Who can execute the method: any user

The method `landing.syspage.set` sets a special page for the site. If the **lid** parameter is not provided, the corresponding page type, not the page itself, will be removed. The method does not return a result.

## Examples

{% list tabs %}

- JS

    ```js
    BX24.callMethod(
        'landing.syspage.set',
        {
            id: 1390,// Site ID
            type: 'personal',// Page type
            lid: 8593// Page ID that will be considered of this type within the site
        },
        function(result)
        {
            if(result.error())
            {
                console.error(result.error());
            }
            else
            {
                console.info(result.data());
            }
        }
    )
    ```

{% endlist %}

{% include [Footnote about examples](../../../../_includes/examples.md) %}