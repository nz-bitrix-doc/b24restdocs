# Bottom Dropdown Menu

Items in the bottom dropdown menu of the [timeline entry](../index.md) `MenuItemDto`.

## Parameters of the `MenuItemDto` Object

{% include [Parameters Note](../../../../../../_includes/required.md) %}

#|
|| **Field** | **Description** ||
|| **title^*^**
[`textWithTranslation`](./field-types.md#textwithtranslation) | Button text ||
|| **action^*^**
[`ActionDto`](./action.md) | Action to be performed when the button is pressed ||
|| **scope**
[`string`](../../../../data-types.md) | [Scope](./field-types.md#scope), for example `web` ||
|| **hideIfReadonly**
[`boolean`](../../../../data-types.md) | Flag. Hides the tag if the user does not have edit access, default is `false` ||
|#

## Example

```json
{
    "title": "Confirm Process",
    "action": {
        "type": "restEvent",
        "id": "confirmProcess",
        "animationType": "loader"
    },
    "scope": "web",
    "hideIfReadonly": true
}
```

## Continue Exploring

- [{#T}](./layout.md)
- [{#T}](./icon.md)
- [{#T}](./body.md)
- [{#T}](./content-block.md)
- [{#T}](./header.md)
- [{#T}](./footer.md)
- [{#T}](./action.md)
- [{#T}](./field-types.md)
- [{#T}](./rest-app-layout-dto.md)
- [{#T}](./examples.md)