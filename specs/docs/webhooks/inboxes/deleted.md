> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# inbox.deleted

> Received when an inbox is deleted.

Event triggered whenever an **inbox is deleted**.

## Response Body Parameters

All webhook payloads follow a consistent top-level structure with
event-specific data nested within the `data` object.

**type** `string`

The event type that triggered the webhook (e.g., `inbox.deleted`).
**created\_at** `string`

ISO 8601 timestamp when the webhook event was created.
**data** `object`

Event-specific data containing detailed information about the event. The
data object for the `inbox.deleted` event contains the following
parameters:

**object parameters**

**source** `api | dashboard | agent | system`

What made the change

**inbox\_id** `string`

The ID of the inbox

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "type": "inbox.deleted",
  "created_at": "2026-09-29T12:00:00.000Z",
  "data": {
    "source": "api",
    "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1"
  }
}
```
