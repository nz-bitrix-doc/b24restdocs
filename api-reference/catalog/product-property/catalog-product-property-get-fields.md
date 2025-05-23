# Get Product Property or Variation Fields catalog.productProperty.getFields

{% note warning "We are still updating this page" %}

Some data may be missing — we will fill it in shortly.

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _not exported to prod_" %}

- no response in case of error
- no response in case of success
- no examples in other languages
  
{% endnote %}

{% endif %}

> Scope: [`catalog`](../../scopes/permissions.md)
>
> Who can execute the method: any user

## Description

```js
catalog.productProperty.getFields()
```

The method returns the fields of product properties or variations.

## Parameters

No parameters.

## Examples

{% include [Examples Note](../../../_includes/examples.md) %}

{% list tabs %}

- cURL (Webhook)

    ```bash
    curl -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{}' \
    https://**put_your_bitrix24_address**/rest/**put_your_user_id_here**/**put_your_webhook_here**/catalog.productProperty.getFields
    ```

- cURL (OAuth)

    ```bash
    curl -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{"auth":"**put_access_token_here**"}' \
    https://**put_your_bitrix24_address**/rest/catalog.productProperty.getFields
    ```

- JS

    ```js
    BX24.callMethod(
        'catalog.productProperty.getFields',
        {},
        function(result)
        {
            if(result.error())
                console.error(result.error().ex);
            else
                console.log(result.data());
        }
    );
    ```

- PHP

    ```php
    require_once('crest.php');

    $result = CRest::call(
        'catalog.productProperty.getFields',
        []
    );

    echo '<PRE>';
    print_r($result);
    echo '</PRE>';
    ```

{% endlist %}

## Returned Fields

#| 
|| **Field** | **Description** | **Note** ||
|| **active** 
[`char`](../../data-types.md) | Is the property active. | ||
|| **code** 
[`string`](../../data-types.md) | Symbolic code. | ||
|| **rowCount, colCount**
[`integer`](../../data-types.md) | Size of the input field (Rows x Columns). | ||
|| **defaultValue** 
[`text`](../../data-types.md) | Default value. | ||
|| **filtrable** 
[`char`](../../data-types.md) | Should the field for filtering by this property be displayed on the item list page. | ||
|| **hint** 
[`string`](../../data-types.md) | Hint. | ||
|| **iblockId^*^** 
[`integer`](../../data-types.md) | Identifier of the information block. | ||
|| **id** 
[`integer`](../../data-types.md) | Identifier of the property. | Read-only. ||
|| **isRequired** 
[`char`](../../data-types.md) | Is it required. | ||
|| **linkIblockId** 
[`integer`](../../data-types.md) | Identifier of the information block associated with the value. Currently, this field is not used (this field is intended for types that are not yet supported in REST). | ||
|| **listType**
[`char`](../../data-types.md) | Appearance. | Only for "List" type fields. ||
|| **multiple** 
[`char`](../../data-types.md) | Is the property multiple. | ||
|| **multipleCnt** 
[`integer`](../../data-types.md) | Number of fields for entering new multiple values. | ||
|| **name^*^** 
[`string`](../../data-types.md) | Name. | ||
|| **propertyType^*^** 
[`string`](../../data-types.md) | Type of property. |  ||
|| **searchable** 
[`char`](../../data-types.md) | Are the property values included in the search. | ||
|| **sort** 
[`integer`](../../data-types.md) | Sort order. | ||
|| **timestampX** 
[`datetime`](../../data-types.md) | Date of the last modification of parameters. | Read-only. ||
|| **userType** 
[`string`](../../data-types.md) | User-defined property type. | ||
|| **withDescription** 
[`char`](../../data-types.md) | Should the field for value description be displayed. | ||
|| **xmlId** 
[`string`](../../data-types.md) | External identifier. | ||
|#

{% include [Parameters Note](../../../_includes/required.md) %}