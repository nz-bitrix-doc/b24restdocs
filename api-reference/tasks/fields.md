# Task Fields

{% if build == 'dev' %}

{% note alert "TO-DO _not exported to prod_" %}

Write an article that outlines which fields can be modified and which can only be read. Mention that system fields can only be modified with admin rights and explain why. Additionally, specify how the connection with CRM is implemented.

{% endnote %}

{% endif %}

{% note warning "We are still updating this page" %}

Some data may be missing here — we will complete it shortly.

{% endnote %}

{% note info "" %}

The recording and modification of fields are carried out according to business logic and the user's existing rights. That is, it depends on the user's role, group permission settings, hierarchy, certain flags in the task (for example, `ALLOW_CHANGE_DEADLINE`), and the task's status.

{% endnote %}

#|
|| **Field** / **Type** | **Description** | Value ||
|| **ID**
[`integer`](../data-types.md) | Task identifier. | ||
|| **PARENT_ID**
[`integer`](../data-types.md) | Parent task ID. | Default - 0 ||
|| **TITLE^*^**
[`string`](../data-types.md) | Title. The length of the TITLE field must not exceed 460 characters. Otherwise, the task title will be truncated from the end without warning. | ||
|| **DESCRIPTION**
[`string`](../data-types.md) | Description. | ||
|| **MARK**
[`enum`](../data-types.md) | Rating. | N - Negative,
P - Positive.
Default - null ||
|| **PRIORITY**
[`enum`](../data-types.md) | Priority. | 2 - High,
1 - Medium,
0 - Low.
Default - 1 ||
|| **STATUS**
[`enum`](../data-types.md) | Status. | 2 - Waiting for execution,
3 - In progress,
4 - Awaiting control,
5 - Completed,
6 - Deferred.
Default - 2 ||
|| **MULTITASK**
[`enum`](../data-types.md) | Multiple task. | Y - Yes,
N - No.
Default - No. ||
|| **NOT_VIEWED**
[`enum`](../data-types.md) | NOT_VIEWED | Y - Yes,
N - No.
Default - No. ||
|| **REPLICATE**
[`enum`](../data-types.md) | Recurring task. | Y - Yes,
N - No.
Default - No. ||
|| **GROUP_ID**
[`integer`](../data-types.md) | Group or project | Default - 0 ||
|| **FLOW_ID**
[`integer`](../data-types.md) | Flow | null ||
|| **STAGE_ID**
[`integer`](../data-types.md) | Stage. | Default - 0 ||
|| **CREATED_BY^*^**
[`integer`](../data-types.md) | Creator. | ||
|| **CREATED_DATE**
[`datetime`](../data-types.md) | Creation date. | ||
|| **RESPONSIBLE_ID^*^**
[`integer`](../data-types.md) | Assignee. | ||
|| **ACCOMPLICES**
[`array`](../data-types.md) | Participants. | ||
|| **AUDITORS**
[`array`](../data-types.md) | Observers. | ||
|| **CHANGED_BY**
[`integer`](../data-types.md) | Modified by. | ||
|| **CHANGED_DATE**
[`integer`](../data-types.md) | Modification date. | ||
|| **STATUS_CHANGED_BY**
[`integer`](../data-types.md) | Status changed by. | ||
|| **CLOSED_BY**
[`integer`](../data-types.md) | Closed by. | ||
|| **CLOSED_DATE**
[`datetime`](../data-types.md) | Closing date. | ||
|| **DATE_START**
[`datetime`](../data-types.md) | Start date. | null ||
|| **DEADLINE**
[`datetime`](../data-types.md) | Deadline. | null ||
|| **START_DATE_PLAN**
[`datetime`](../data-types.md) | Planned start. | null ||
|| **END_DATE_PLAN**
[`datetime`](../data-types.md) | Planned completion. | null ||
|| **GUID**
[`string`](../data-types.md) | GUID | null ||
|| **XML_ID**
[`string`](../data-types.md) | XML_ID | null ||
|| **COMMENTS_COUNT**
[`integer`](../data-types.md) | Number of comments | ||
|| **NEW_COMMENTS_COUNT**
[`integer`](../data-types.md) | Number of new comments. | ||
|| **ALLOW_CHANGE_DEADLINE**
[`enum`](../data-types.md) | Allow changing deadlines. | Y - Yes,
N - No.
Default - No. ||
|| **ALLOW_TIME_TRACKING**
[`enum`](../data-types.md) | Allow time tracking for the task | Y - Yes,
N - No.
Default - No. ||
|| **TASK_CONTROL**
[`enum`](../data-types.md) | Accept work. | Y - Yes,
N - No.
Default - No. ||
|| **ADD_IN_REPORT**
[`enum`](../data-types.md) | Add to report. | Y - Yes,
N - No.
Default - No. ||
|| **FORKED_BY_TEMPLATE_ID**
[`enum`](../data-types.md) | Created from a template. | Y - Yes,
N - No.
Default - No. ||
|| **TIME_ESTIMATE**
[`integer`](../data-types.md) | Time allocated for the task. | ||
|| **TIME_SPENT_IN_LOGS**
[`integer`](../data-types.md) | Time spent from change history. | ||
|| **MATCH_WORK_TIME**
[`integer`](../data-types.md) | Skip weekends. | ||
|| **FORUM_TOPIC_ID**
[`integer`](../data-types.md) | Forum topic identifier. | ||
|| **FORUM_ID**
[`integer`](../data-types.md) | Forum identifier. | ||
|| **SITE_ID**
[`string`](../data-types.md) | Site identifier. | ||
|| **SUBORDINATE**
[`enum`](../data-types.md) | Subordinate task. | Y - Yes,
N - No.
Default - No. ||
|| **FAVORITE**
[`enum`](../data-types.md) | Added to Favorites. | ||
|| **EXCHANGE_MODIFIED**
[`datetime`](../data-types.md) | EXCHANGE_MODIFIED | null ||
|| **EXCHANGE_ID**
[`integer`](../data-types.md) | EXCHANGE_ID | null ||
|| **OUTLOOK_VERSION**
[`integer`](../data-types.md) | OUTLOOK_VERSION | null ||
|| **VIEWED_DATE**
[`datetime`](../data-types.md) | Last viewed date. | ||
|| **SORTING**
[`double`](../data-types.md) | Sorting index. | ||
|| **DURATION_PLAN**
[`integer`](../data-types.md) | Time spent (planned). | ||
|| **DURATION_FACT**
[`integer`](../data-types.md) | Time spent (actual). | ||
|| **CHECKLIST**
[`array`](../data-types.md) | Checklist. | ||
|| **DURATION_TYPE**
[`enum`](../data-types.md) | DURATION_TYPE. | \[0\] => secs
\[1\] => mins
\[2\] => hours
\[3\] => days
\[4\] => weeks
\[5\] => months
\[6\] => years.
Default - 3 ||
|| **UF_CRM_TASK**
[`crm`](../data-types.md) | Link to CRM entities
L_XX - lead,
C_XX - contact,
D_XX - deal | ||
|| **UF_TASK_WEBDAV_FILES**
[`disk_file`](../data-types.md) | File (Drive). | ||
|| **UF_MAIL_MESSAGE**
[`mail_message`](../data-types.md) | E-mail. | ||
|| **IS_MUTED**
[`enum`](../data-types.md) | Notifications. | Y - Yes,
N - No.
Default - No. ||
|| **IS_PINNED**
[`enum`](../data-types.md) | Pinned. | Y - Yes,
N - No.
Default - No. ||
|| **IS_PINNED_IN_GROUP**
[`enum`](../data-types.md) | Pinned in group. | Y - Yes,
N - No.
Default - No. ||
|| **SERVICE_COMMENTS_COUNT**
[`integer`](../data-types.md) | SERVICE_COMMENTS_COUNT | ||
|#

{% include [Footnote on parameters](../../_includes/required.md) %}

**Date/time fields that are read/written in ISO 8601 format:**

- DEADLINE
- START_DATE_PLAN
- END_DATE_PLAN
- DATE_START
- CREATED_DATE
- CLOSED_DATE
- CHANGED_DATE
- STATUS_CHANGED_DATE
- VIEWED_DATE