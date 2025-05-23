# Set a common card for all users crm.lead.details.configuration.forceCommonScopeForAll

{% note warning "We are still updating this page" %}

Some data may be missing here — we will complete it shortly.

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _not exported to prod_" %}

- parameter types are not specified
- parameter requirements are not indicated
- examples are missing
- success response is absent
- error response is absent

{% endnote %}

{% endif %}

> Scope: [`crm`](../../../scopes/permissions.md)
>
> Who can execute the method: any user

The method `crm.lead.details.configuration.forceCommonScopeForAll` forcibly sets a common lead card for all users.

{% note warning %}

Please note that the settings for repeat lead cards may differ from those for simple lead cards. The parameter **leadCustomerType** is used to switch between lead card settings.

{% endnote %}

#|
|| **Parameter** | **Description** ||
|| **extras**
[`unknown`](../../../data-types.md) | Additional parameters. Here, for leads, the parameter `leadCustomerType` can be specified with the following acceptable values:

- **1** - simple leads,
- **2** - repeat leads 
  ||
|#

## Examples

{% list tabs %}

- JS

    ```js
    //---
    //Set a common lead card for all users.
    BX24.callMethod(
        "crm.lead.details.configuration.forceCommonScopeForAll",
        {},
        function(result)
        {
            if(result.error())
                console.error(result.error());
            else
                console.dir(result.data());
        }
    );
    //---
    ```

{% endlist %}

{% include [Footnote about examples](../../../../_includes/examples.md) %}