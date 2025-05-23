# Get a list of business process tasks bizproc.task.list

> Scope: [`bizproc`](../../scopes/permissions.md)
>
> Who can execute the method: any user

This method retrieves a list of business process tasks.

An account administrator can request all tasks or tasks of any user. A regular user can request their own tasks or those of their subordinate.

To request their own tasks, the `USER_ID` filter does not need to be specified.

## Method Parameters

{% include [Footnote about parameters](../../../_includes/required.md) %}

#|
|| **Name**
`type` | **Description** ||
|| **SELECT**
[`array`](../../data-types.md) | The array contains a list of [fields](#fields) to be selected.

Only the necessary fields can be specified.

By default, it returns the fields `ENTITY`, `DOCUMENT_ID`, `ID`, `WORKFLOW_ID`, `DOCUMENT_NAME`, `NAME`, `DOCUMENT_URL` ||
|| **FILTER**
[`object`](../../data-types.md) | An object for filtering the list of tasks in the format `{"field_1": "value_1", ... "field_N": "value_N"}`, where
- `field_N` — [field](#fields) of the task for filtering
- `value_N` — value of the field

If `USER_ID` is present in the filter, user subordination is checked:
- a manager can request the list of tasks of their subordinates
- an administrator can request tasks of any users without restrictions 

If the method is called by a non-administrator and the `USER_ID` filter is not specified, by default, it selects the tasks of the current user
||
|| **ORDER**
[`object`](../../data-types.md) | An object for sorting the list of tasks in the format `{"field_1": "value_1", ... "field_N": "value_N"}`, where
- `field_N` — [field](#fields) of the task for sorting
- `value_N` — sorting direction

The sorting direction can take the values:
- `asc` — ascending
- `desc` — descending
  
Multiple fields can be specified for sorting, for example, `{NAME: 'ASC', ID: 'DESC'}` ||
|| **START**
[`integer`](../../data-types.md) | The parameter is used for managing pagination.

The page size of results is always static — 50 records.

To select the second page of results, the value `50` must be passed. To select the third page of results — the value `100`, and so on.

The formula for calculating the `start` parameter value:

`start = (N - 1) * 50`, where `N` — the number of the desired page ||
|#

## Code Examples

{% include [Footnote about examples](../../../_includes/examples.md) %}

{% list tabs %}

- cURL (Webhook)

    ```bash
    curl -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{"select":["ID","WORKFLOW_ID","DOCUMENT_NAME","DESCRIPTION","NAME","MODIFIED","WORKFLOW_STARTED","WORKFLOW_STARTED_BY","OVERDUE_DATE","WORKFLOW_TEMPLATE_ID","WORKFLOW_TEMPLATE_NAME","WORKFLOW_STATE","STATUS","USER_ID","USER_STATUS","MODULE_ID","ENTITY","DOCUMENT_ID","ACTIVITY","ACTIVITY_NAME","DOCUMENT_URL","PARAMETERS"],"order":{"ID":"DESC"},"filter":{"USER_ID":1,"STATUS":0,"ACTIVITY":"RequestInformationOptionalActivity"}}' \
    https://**put_your_bitrix24_address**/rest/**put_your_user_id_here**/**put_your_webhook_here**/bizproc.task.list
    ```

- cURL (OAuth)

    ```bash
    curl -X POST \
    -H "Content-Type: application/json" \
    -H "Accept: application/json" \
    -d '{"select":["ID","WORKFLOW_ID","DOCUMENT_NAME","DESCRIPTION","NAME","MODIFIED","WORKFLOW_STARTED","WORKFLOW_STARTED_BY","OVERDUE_DATE","WORKFLOW_TEMPLATE_ID","WORKFLOW_TEMPLATE_NAME","WORKFLOW_STATE","STATUS","USER_ID","USER_STATUS","MODULE_ID","ENTITY","DOCUMENT_ID","ACTIVITY","ACTIVITY_NAME","DOCUMENT_URL","PARAMETERS"],"order":{"ID":"DESC"},"filter":{"USER_ID":1,"STATUS":0,"ACTIVITY":"RequestInformationOptionalActivity"},"auth":"**put_access_token_here**"}' \
    https://**put_your_bitrix24_address**/rest/bizproc.task.list
    ```

- JS

    ```js
    BX24.callMethod(
        'bizproc.task.list',
        {
            select: [
                'ID',
                'WORKFLOW_ID',
                'DOCUMENT_NAME',
                'DESCRIPTION',
                'NAME',
                'MODIFIED',
                'WORKFLOW_STARTED',
                'WORKFLOW_STARTED_BY',
                'OVERDUE_DATE',
                'WORKFLOW_TEMPLATE_ID',
                'WORKFLOW_TEMPLATE_NAME',
                'WORKFLOW_STATE',
                'STATUS',
                'USER_ID',
                'USER_STATUS',
                'MODULE_ID',
                'ENTITY',
                'DOCUMENT_ID',
                'ACTIVITY',
                'ACTIVITY_NAME',
                'DOCUMENT_URL',
                'PARAMETERS'
            ],
            order: {
                ID: 'DESC'
            },
            filter: {
                'USER_ID': 1,
                'STATUS': 0,
                'ACTIVITY': 'RequestInformationOptionalActivity'
            }
        },
        function(result)
        {
            if(result.error())
                alert("Error: " + result.error());
            else
                console.log(result.data());
        }
    );
    ```

- PHP

    ```php
    require_once('crest.php');

    $result = CRest::call(
        'bizproc.task.list',
        [
            'select' => [
                'ID',
                'WORKFLOW_ID',
                'DOCUMENT_NAME',
                'DESCRIPTION',
                'NAME',
                'MODIFIED',
                'WORKFLOW_STARTED',
                'WORKFLOW_STARTED_BY',
                'OVERDUE_DATE',
                'WORKFLOW_TEMPLATE_ID',
                'WORKFLOW_TEMPLATE_NAME',
                'WORKFLOW_STATE',
                'STATUS',
                'USER_ID',
                'USER_STATUS',
                'MODULE_ID',
                'ENTITY',
                'DOCUMENT_ID',
                'ACTIVITY',
                'ACTIVITY_NAME',
                'DOCUMENT_URL',
                'PARAMETERS'
            ],
            'order' => [
                'ID' => 'DESC'
            ],
            'filter' => [
                'USER_ID' => 1,
                'STATUS' => 0,
                'ACTIVITY' => 'RequestInformationOptionalActivity'
            ]
        ]
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
    "result": [
        {
            "ENTITY": "BizprocDocument",
            "DOCUMENT_ID": "2249",
            "ID": "1477",
            "WORKFLOW_ID": "67a2ffdb2c57a3.35276854",
            "DOCUMENT_NAME": "Partner Conference",
            "DESCRIPTION": "",
            "NAME": "Add contractor information",
            "MODIFIED": "2025-02-05T09:06:19+02:00",
            "WORKFLOW_STARTED": "2025-02-05T09:06:19+02:00",
            "WORKFLOW_STARTED_BY": "1",
            "OVERDUE_DATE": null,
            "WORKFLOW_TEMPLATE_ID": "565",
            "WORKFLOW_TEMPLATE_NAME": "Event Organization",
            "WORKFLOW_STATE": "Waiting for additional information",
            "STATUS": "0",
            "USER_ID": "1",
            "USER_STATUS": "0",
            "MODULE_ID": "lists",
            "ACTIVITY": "RequestInformationActivity",
            "ACTIVITY_NAME": "A3651_68033_56029_16413",
            "PARAMETERS": {
                "CommentLabel": "Comment",
                "CommentRequired": "Y",
                "ShowComment": "Y",
                "StatusOkLabel": "Save result",
                "Fields": [
                    {
                        "Id": "contractor",
                        "Type": "E:ECrm",
                        "Name": "Contractor",
                        "Description": "Who performs the work",
                        "Multiple": false,
                        "Required": true,
                        "Options": {
                            "LEAD": "N",
                            "CONTACT": "Y",
                            "COMPANY": "Y",
                            "DEAL": "N",
                            "SMART_INVOICE": "N",
                            "DYNAMIC_136": "N",
                            "DYNAMIC_1038": "N"
                        },
                        "Settings": null,
                        "Default": [
                            "C_607"
                        ]
                    },
                    {
                        "Id": "phone_number",
                        "Type": "string",
                        "Name": "Phone number",
                        "Description": "",
                        "Multiple": false,
                        "Required": true,
                        "Options": null,
                        "Settings": null,
                        "Default": ""
                    }
                ]
            },
            "DOCUMENT_URL": "/bizproc/processes/?livefeed=y&list_id=171&element_id=2249"
        },
        {
            "ENTITY": "BizprocDocument",
            "DOCUMENT_ID": "2237",
            "ID": "1471",
            ...
        }
    ],
    "total": 2,
    "time": {
        "start": 1738735796.4730229,
        "finish": 1738735796.510215,
        "duration": 0.037192106246948242,
        "processing": 0.0080459117889404297,
        "date_start": "2025-02-05T09:09:56+02:00",
        "date_finish": "2025-02-05T09:09:56+02:00",
        "operating_reset_at": 1738736396,
        "operating": 0
    }
}
```

### Returned Data

#|
|| **Name**
`type` | **Description** ||
|| **result**
[`object`](../../data-types.md) | The root element of the response. 

Contains an array of objects with information about business process tasks.

Each object contains [fields](#fields) of the task specified in the `SELECT` parameter ||
|| **total**
[`integer`](../../data-types.md) | The total number of records found ||
|| **time**
[`time`](../../data-types.md#time) | Information about the execution time of the request ||
|#

#### Task Fields {#fields}

#|
|| **Name**
`type` | **Description** ||
|| **ID**
[`integer`](../../data-types.md) | Task identifier ||
|| **WORKFLOW_ID**
[`integer`](../../data-types.md) | Business process identifier ||
|| **DOCUMENT_NAME**
[`string`](../../data-types.md) | Document name ||
|| **DESCRIPTION**
[`string`](../../data-types.md) | Task description ||
|| **NAME**
[`string`](../../data-types.md) | Task name ||
|| **MODIFIED**
[`datetime`](../../data-types.md) | Modification date ||
|| **WORKFLOW_STARTED**
[`datatime`](../../data-types.md) | Business process start date ||
|| **WORKFLOW_STARTED_BY**
[`user`](../../data-types.md) | Who started the business process ||
|| **OVERDUE_DATE**
[`datetime`](../../data-types.md) | Deadline ||
|| **WORKFLOW_TEMPLATE_ID**
[`integer`](../../data-types.md) | Business process template identifier ||
|| **WORKFLOW_TEMPLATE_NAME**
[`string`](../../data-types.md) | Business process template name ||
|| **WORKFLOW_STATE**
[`string`](../../data-types.md) | Business process status ||
|| **STATUS**
[`integer`](../../data-types.md) | Task status. Possible values:

- `0` — in progress
- `1` — approved
- `2` — rejected
- `3` — completed
- `4` — task deadline expired ||

|| **USER_ID**
[`user`](../../data-types.md) | User identifier ||
|| **USER_STATUS**
[`integer`](../../data-types.md) | User response. Possible values:

- `0` — awaiting response
- `1` — approved
- `2` — rejected
- `3` — completed ||

|| **MODULE_ID**
[`string`](../../data-types.md) | Module identifier by document ||
|| **ENTITY**
[`string`](../../data-types.md) | Symbolic identifier of the object by document ||
|| **DOCUMENT_ID**
[`integer`](../../data-types.md) | Document identifier ||
|| **ACTIVITY**
[`string`](../../data-types.md) | Task type identifier. Possible values:

- `ApproveActivity` — document approval
- `ReviewActivity` — document review
- `RequestInformationActivity` — request for additional information
- `RequestInformationOptionalActivity` — request for additional information (with rejection)
||
|| **ACTIVITY_NAME**
[`string`](../../data-types.md) | Action identifier in the template ||
|| **PARAMETERS**
[`object`](../../data-types.md) | An object describing the [task parameters](#parameters) ||
|| **DOCUMENT_URL**
[`object`](../../data-types.md) | Link to the document ||
|#

#### PARAMETERS Object {#parameters}

#|
|| **Name**
`type` | **Description** ||
|| **CommentLabel**
[`string`](../../data-types.md) | Name of the Comment field ||
|| **CommentRequired**
[`string`](../../data-types.md) | Comment requirement. Possible values:
- `N` — no
- `Y` — yes
- `YA` — yes, upon approval
- `YR` — yes, upon rejection
||
|| **ShowComment**
[`boolean`](../../data-types.md) | Show comment. Possible values:
- `N` — no
- `Y` — yes
||
|| **StatusOkLabel**
[`string`](../../data-types.md) | Text of the Acknowledged button ||
|| **StatusYesLabel**
[`string`](../../data-types.md) | Text of the Approve button ||
|| **StatusNoLabel**
[`string`](../../data-types.md) | Text of the Reject button ||
|| **Fields**
[`array`](../../data-types.md) | An array of objects. Each object contains a description of the [field in the task](#task-fields) ||
|#

#### Fields Object {#task-fields}

#|
|| **Name**
`type` | **Description**||
|| **Id**
[`string`](../../data-types.md) | Symbolic identifier of the task parameter ||
|| **Type**
[`string`](../../data-types.md) | Parameter type. Basic values: 
  - `bool` — yes or no
  - `date` — date
  - `datetime` — date and time
  - `double` — number
  - `int` — integer 
  - `select` — list
  - `string` — string
  - `text` — text
  - `user` — user  

Other types depend on the document with which the business process works ||
|| **Name**
[`string` \| `object`](../../data-types.md) | Name of the parameter ||
|| **Description**
[`string` \| `object`](../../data-types.md) | Description of the parameter ||
|| **Multiple**
[`boolean`](../../data-types.md) | Parameter multiplicity. Possible values:
- `true` — yes
- `false` — no ||
|| **Required**
[`boolean`](../../data-types.md) | Parameter requirement. Possible values:
- `true` — yes
- `false` — no ||
|| **Options**
[`object`](../../data-types.md) | Field settings.

Values depend on the parameter type. Examples:
- for the List type `select`, these are the options of the list
```json
"Options": {
    "1": "First option",
    "2": "Second option",
    "3": "Third option",
},
```
- for the CRM Binding type `'E:ECrm'`, these are the available object types
```json
"Options": {
    "LEAD": "N",
    "CONTACT": "Y",
    "COMPANY": "Y",
    "DEAL": "N",
    "SMART_INVOICE": "N",
    "DYNAMIC_136": "N",
    "DYNAMIC_1038": "N"
},
```
||
|| **Settings**
[`object`](../../data-types.md) | Additional field settings ||
|| **Default**
[`any`](../../data-types.md) | Default value of the parameter ||
|#

## Error Handling

HTTP status: **400**

```json
{
    "error": "ACCESS_DENIED",
    "error_description": "Access denied!"
}
```

{% include notitle [error handling](../../../_includes/error-info.md) %}

### Possible Error Codes

#|
|| **Code** | **Error Message** | **Description** ||
|| `ACCESS_DENIED` | Access denied! | The method was called by a non-administrator or you cannot view the tasks of the specified employee ||
|#

{% include [system errors](../../../_includes/system-errors.md) %}

## Continue Learning 

- [{#T}](./index.md)
- [{#T}](./bizproc-task-complete.md)
- [{#T}](../../../tutorials/bizproc/how-to-kill-workflows.md)
- [{#T}](../../../tutorials/bizproc/how-to-filter-and-kill-workflows.md)