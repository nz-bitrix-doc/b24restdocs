# Update Field crm.lead.userfield.update

{% note warning "We are still updating this page" %}

Some data may be missing here — we will complete it shortly.

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _not exported to prod_" %}

- parameter types are not specified
- adjustments needed to meet writing standards
- required parameters are not indicated
- examples are missing (in other languages)
- success response is missing
- error response is missing
- link to the yet-to-be-created page is not provided

{% endnote %}

{% endif %}

> Scope: [`crm`](../../../scopes/permissions.md)
>
> Who can execute the method: any user

The method `crm.lead.userfield.update` updates an existing custom field for leads.

#|
|| **Parameter** | **Description** ||
|| **id** | Identifier of the custom field. ||
|| **fields** | Set of fields - an array in the form of `array("field"=>"value"[, ...])`, where "updated field" can take values returned by the method [crm.userfield.fields](.). ||
|| **LIST** | Contains a set of list values for custom fields of type List. Specified when creating/updating the field. Each value is an array with the following fields: 
- **VALUE** - value of the list item. This field is required when creating a new item. 
- **SORT** - sorting. 
- **DEF** - if equal to `Y`, the list item is the default value. For multiple fields, multiple `DEF=Y` are allowed. For non-multiple fields, the first one will be considered default. 
- **XML_ID** - external code of the value. This parameter is only considered when updating already existing list item values. 
- **ID** - identifier of the value. If specified, it is considered that this is an update of an existing list item value, not the creation of a new one. 
- **DEL** - if equal to `Y`, the existing list item will be deleted. This is applied if the ID parameter is filled. ||
|#

## Example

{% list tabs %}

- JS

    ```js
    var id = prompt("Enter ID");
    var label = prompt("Enter new name");
    BX24.callMethod(
        "crm.lead.userfield.update",
        {
            id: id,
            fields:
            {
                "EDIT_FORM_LABEL": label,
                "LIST_COLUMN_LABEL": label
            }
        },
        function(result)
        {
            if(result.error())
                console.error(result.error());
            else
            {
                console.dir(result.data());
                if(result.more())
                    result.next();
            }
        }
    );
    ```

{% endlist %}


{% include [Footnote on examples](../../../../_includes/examples.md) %}