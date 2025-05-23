# Get a List of CRM Activity Fields crm.activity.fields

> Scope: [`crm`](../../../../scopes/permissions.md)
>
> Who can execute the method: any user

The method `crm.activity.fields` returns a description of the fields of the system activity.

## Method Parameters

No parameters

## Code Examples

{% include [Footnote on examples](../../../../../_includes/examples.md) %}

{% list tabs %}

- cURL (Webhook)

    ```bash
     curl -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{}' \
    https://**put_your_bitrix24_address**/rest/**put_your_user_id_here**/**put_your_webhook_here**/crm.activity.fields
    ```

- cURL (OAuth)

    ```bash
    curl -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{"auth":"**put_access_token_here**"}' \
    https://**put_your_bitrix24_address**/rest/crm.activity.fields
    ```

- JS
    
    ```javascript
    BX24.callMethod(
        'crm.activity.fields',
        {},
        result => {
            if (result.error())
                console.error(result.error());
            else
                console.dir(result.data());
        }
    );
    ```

- PHP

    ```php
    require_once('crest.php');

    $result = CRest::call(
        'crm.activity.fields',
        []
    );

    echo '<PRE>';
    print_r($result);
    echo '</PRE>';
    ```

{% endlist %}

## Response Handling

HTTP status: **200**

```json
{
    "result": {
        "ID": {
            "type": "integer",
            "isRequired": false,
            "isReadOnly": true,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "ID"
        },
        "OWNER_ID": {
            "type": "integer",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": true,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Owner ID"
        },
        "OWNER_TYPE_ID": {
            "type": "crm_enum_ownertype",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": true,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Owner Type"
        },
        "TYPE_ID": {
            "type": "crm_enum_activitytype",
            "isRequired": true,
            "isReadOnly": false,
            "isImmutable": true,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Type"
        },
        "PROVIDER_ID": {
            "type": "string",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Provider ID"
        },
        "PROVIDER_TYPE_ID": {
            "type": "string",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Provider Type"
        },
        "PROVIDER_GROUP_ID": {
            "type": "string",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Connector Type"
        },
        "ASSOCIATED_ENTITY_ID": {
            "type": "integer",
            "isRequired": false,
            "isReadOnly": true,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "ID of the entity associated with the activity"
        },
        "SUBJECT": {
            "type": "string",
            "isRequired": true,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Subject"
        },
        "START_TIME": {
            "type": "datetime",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Start"
        },
        "END_TIME": {
            "type": "datetime",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Deadline"
        },
        "DEADLINE": {
            "type": "datetime",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Due Date"
        },
        "COMPLETED": {
            "type": "char",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Completed"
        },
        "STATUS": {
            "type": "crm_enum_activitystatus",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Status"
        },
        "RESPONSIBLE_ID": {
            "type": "user",
            "isRequired": true,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Responsible"
        },
        "PRIORITY": {
            "type": "crm_enum_activitypriority",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Priority"
        },
        "NOTIFY_TYPE": {
            "type": "crm_enum_activitynotifytype",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Notification Type"
        },
        "NOTIFY_VALUE": {
            "type": "integer",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Notification Parameter"
        },
        "DESCRIPTION": {
            "type": "string",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Description"
        },
        "DESCRIPTION_TYPE": {
            "type": "crm_enum_contenttype",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Description Type"
        },
        "DIRECTION": {
            "type": "crm_enum_activitydirection",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Direction"
        },
        "LOCATION": {
            "type": "string",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Location"
        },
        "CREATED": {
            "type": "datetime",
            "isRequired": false,
            "isReadOnly": true,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Creation Date"
        },
        "AUTHOR_ID": {
            "type": "user",
            "isRequired": false,
            "isReadOnly": true,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Created By"
        },
        "LAST_UPDATED": {
            "type": "datetime",
            "isRequired": false,
            "isReadOnly": true,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Last Updated"
        },
        "EDITOR_ID": {
            "type": "user",
            "isRequired": false,
            "isReadOnly": true,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Edited By"
        },
        "SETTINGS": {
            "type": "object",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Settings"
        },
        "ORIGIN_ID": {
            "type": "string",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "External Code"
        },
        "ORIGINATOR_ID": {
            "type": "string",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "External Source"
        },
        "RESULT_STATUS": {
            "type": "integer",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "RESULT_STATUS"
        },
        "RESULT_STREAM": {
            "type": "integer",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "RESULT_STREAM"
        },
        "RESULT_SOURCE_ID": {
            "type": "string",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "RESULT_SOURCE_ID"
        },
        "PROVIDER_PARAMS": {
            "type": "object",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Provider Parameters"
        },
        "PROVIDER_DATA": {
            "type": "string",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Provider Data"
        },
        "RESULT_MARK": {
            "type": "integer",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "RESULT_MARK"
        },
        "RESULT_VALUE": {
            "type": "double",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "RESULT_VALUE"
        },
        "RESULT_SUM": {
            "type": "double",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "RESULT_SUM"
        },
        "RESULT_CURRENCY_ID": {
            "type": "string",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "RESULT_CURRENCY_ID"
        },
        "AUTOCOMPLETE_RULE": {
            "type": "integer",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "Autocomplete"
        },
        "BINDINGS": {
            "type": "crm_activity_binding",
            "isRequired": false,
            "isReadOnly": true,
            "isImmutable": false,
            "isMultiple": true,
            "isDynamic": false,
            "title": "Bindings"
        },
        "COMMUNICATIONS": {
            "type": "crm_activity_communication",
            "isRequired": true,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": true,
            "isDynamic": false,
            "title": "Communication Channel"
        },
        "FILES": {
            "type": "diskfile",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": true,
            "isDynamic": false,
            "title": "Files"
        },
        "WEBDAV_ELEMENTS": {
            "type": "diskfile",
            "isRequired": false,
            "isReadOnly": false,
            "isImmutable": false,
            "isMultiple": true,
            "isDynamic": false,
            "isDeprecated": true,
            "title": "Added Files"
        },
        "IS_INCOMING_CHANNEL": {
            "type": "char",
            "isRequired": false,
            "isReadOnly": true,
            "isImmutable": false,
            "isMultiple": false,
            "isDynamic": false,
            "title": "IS_INCOMING_CHANNEL"
        }
    },
    "time": {
        "start": 1712132792.910734,
        "finish": 1712132793.530359,
        "duration": 0.6196250915527344,
        "processing": 0.032338857650756836,
        "date_start": "2024-04-03T10:26:32+02:00",
        "date_finish": "2024-04-03T10:26:33+02:00",
        "operating_reset_at": 1705765533,
        "operating": 3.3076241016387939
    }
}
```

### Returned Data

#|
|| **Name**
`type` | **Description** ||
|| **result**
[`object`](../../../../data-types.md) | Root element of the response. Values for the `result` field correspond to [fields of the object](#all-fields). ||
|| **time**
[`time`](../../../../data-types.md#time) | Information about the execution time of the request ||
|#

#### Overview of System Activity Fields {#all-fields}

{% include [Footnote on required parameters](../../../../../_includes/required.md) %}

#|
|| **Field** `type` | **Description** | **Note** ||
|| **ID***
[`integer`](../../../data-types.md) | Identifier of the activity | Read-only ||
|| **OWNER_ID***
[`integer`](../../../data-types.md) | Identifier of the CRM entity | Can be changed using the [crm.activity.binding.move](../binding/crm-activity-binding-move.md) method ||
|| **OWNER_TYPE_ID***
[`integer`](../../../data-types.md) | [Identifier of the CRM object type](../../../data-types.md#object_type) | Immutable ||
|| **TYPE_ID***
[`crm_enum_activitytype`](../../../data-types.md) | Type of activity | Required, immutable ||
|| **ASSOCIATED_ENTITY_ID**
[`integer`](../../../../data-types.md) | Integer identifier of the entity associated with the activity | Read-only ||
|| **AUTHOR_ID***
[`integer`](../../../../data-types.md) | Integer identifier of the user who created the activity | ||
|| **AUTOCOMPLETE_RULE**
[`integer`](../../../../data-types.md) | Integer identifier of the rule that triggered the autocomplete | ||
|| **BINDINGS**
[`crm_activity_binding`](../../../data-types.md) | Bindings to CRM entities | Multiple, read-only ||
|| **COMMUNICATIONS***
[`crm_activity_communication`](../../../data-types.md) | [Description of communication](./crm-activity-communication-fields.md) | Multiple, required ||
|| **COMPLETED***
[`char`](../../../data-types.md) | Flag indicating whether the activity is completed (`Y`|`N`) | ||
|| **CREATED***
[`datetime`](../../../data-types.md) | Date and time the activity was created | ||
|| **DEADLINE**
[`datetime`](../../../data-types.md) | Date and time of the activity's due date | This field is not set directly; the value is taken from START_TIME for calls and meetings and from END_TIME for tasks ||
|| **DESCRIPTION**
[`string`](../../../data-types.md) | Text description of the activity | ||
|| **DESCRIPTION_TYPE**
[`crm.enum.contenttype`](../../../data-types.md) | Description type | ||
|| **DIRECTION**
[`crm.enum.activitydirection`](../../../data-types.md) | Direction of the activity: incoming/outgoing. | Relevant for calls and emails; not used for meetings ||
|| **EDITOR_ID**
[`user`](../../../data-types.md) | Integer identifier of the user who edited the activity | Read-only ||
|| **END_TIME**
[`datetime`](../../../data-types.md) | End time of the activity | ||
|| **FILES**
[`diskfile`](../../../data-types.md) | Files added to the activity | Multiple ||
|| **LAST_UPDATED**
[`datetime`](../../../data-types.md) | Date of the last update | Read-only ||
|| **LOCATION**
[`string`](../../../data-types.md) | Location | ||
|| **NOTIFY_TYPE**
[`crm.enum.activitynotifytype`](../../../data-types.md) | Notification type | ||
|| **NOTIFY_VALUE**
[`integer`](../../../data-types.md) | Notification value | Read-only ||
|| **ORIGINATOR_ID**
[`string`](../../../data-types.md) | Identifier of the data source | Used only for binding to an external source ||
|| **ORIGIN_ID**
[`string`](../../../data-types.md) | Identifier of the element in the data source | Used only for binding to an external source ||
|| **ORIGIN_VERSION**
[`string`](../../../data-types.md) | Original version | Used to protect data from accidental overwriting by an external system. If the data was imported and not changed in the external system, such data can be edited in CRM without fear that the next export will lead to data overwriting ||
|| **PRIORITY**
[`crm.enum.activitypriority`](../../../data-types.md) | Priority | ||
|| **PROVIDER_DATA**
[`string`](../../../data-types.md) | Additional provider data | ||
|| **PROVIDER_GROUP_ID**
[`string`](../../../data-types.md) | Identifier of the provider group | ||
|| **PROVIDER_ID**
[`string`](../../../data-types.md) | Identifier of the provider | Read-only ||
|| **PROVIDER_TYPE_ID**
[`string`](../../../data-types.md) | Identifier of the provider type | Status from the directory ||
|| **PROVIDER_PARAMS**
[`object`](../../../data-types.md) | Additional provider parameters | ||
|| **RESPONSIBLE_ID***
[`user`](../../../data-types.md) | Integer identifier of the user responsible for the activity | Required ||
|| **RESULT_CURRENCY_ID**
[`string`](../../../data-types.md) | | ||
|| **RESULT_MARK**
[`integer`](../../../data-types.md) | | ||
|| **RESULT_SOURCE_ID**
[`string`](../../../data-types.md) | | ||
|| **RESULT_STATUS**
[`integer`](../../../data-types.md) | | ||
|| **RESULT_STREAM**
[`integer`](../../../data-types.md) | Report statistics | ||
|| **RESULT_SUM**
[`double`](../../../data-types.md) | | ||
|| **RESULT_VALUE**
[`double`](../../../data-types.md) | | ||
|| **SETTINGS**
[`object`](../../../data-types.md) | Additional settings | ||
|| **START_TIME**
[`datetime`](../../../data-types.md) | Start time of the activity | ||
|| **STATUS**
[`crm_enum_activitystatus`](../../../data-types.md) | Status of the activity | ||
|| **SUBJECT**
[`string`](../../../data-types.md) | Additional description of the activity | Required ||
|| **WEBDAV_ELEMENTS**
[`diskfile`](../../../data-types.md) | Added files | Multiple. Deprecated, kept for compatibility ||
|| **IS_INCOMING_CHANNEL**
[`char`](../../../data-types.md) | Flag indicating whether the activity was created from an incoming channel (`Y`/`N`) |  ||
|#

## Error Handling

HTTP status: **400**

```json
{
    "error": "",
    "error_description": "Access denied."
}
```

{% include notitle [error handling](../../../../../_includes/error-info.md) %}

### Possible Error Codes

{% include [system errors](../../../../../_includes/system-errors.md) %}

## Continue Learning

- [{#T}](./crm-activity-add.md)
- [{#T}](./crm-activity-update.md)
- [{#T}](./crm-activity-delete.md)
- [{#T}](./crm-activity-list.md)
- [{#T}](./crm-activity-communication-fields.md)
- [{#T}](./crm-activity-get.md)