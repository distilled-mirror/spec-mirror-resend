> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# topic.created

> Received when a topic is created.

Event triggered whenever a **topic is created**.

## Response Body Parameters

All webhook payloads follow a consistent top-level structure with
event-specific data nested within the `data` object.

**type** `string`

The event type that triggered the webhook (e.g., `topic.created`).
**created\_at** `string`

ISO 8601 timestamp when the webhook event was created.
**data** `object`

Event-specific data containing detailed information about the event. The
data object for the `topic.created` event contains the following
parameters:

**object parameters**

**id** `string`

Unique identifier for the topic

**name** `string`

The topic name

**description** `string | null`

The topic description

**default\_subscription** `opt_in | opt_out`

The default subscription preference for new contacts

**deleted** `boolean`

Whether the topic was deleted

**created\_at** `string`

ISO 8601 timestamp when the topic was created

**updated\_at** `string`

ISO 8601 timestamp when the topic was last updated

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "type": "topic.created",
  "created_at": "2026-02-12T10:00:00.000Z",
  "data": {
    "id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e",
    "name": "Product Updates",
    "description": "New features and improvements",
    "default_subscription": "opt_in",
    "deleted": false,
    "created_at": "2026-02-12T10:00:00.000Z",
    "updated_at": "2026-02-12T10:00:00.000Z"
  }
}
```
