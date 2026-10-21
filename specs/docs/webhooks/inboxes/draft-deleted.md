> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# inbox.draft.deleted

> Received when a draft is discarded.

Event triggered whenever a **draft is discarded**.

*Note: The draft is already gone, so the payload has no `draft` object.*

## Response Body Parameters

All webhook payloads follow a consistent top-level structure with
event-specific data nested within the `data` object.

**type** `string`

The event type that triggered the webhook (e.g., `inbox.draft.deleted`).
**created\_at** `string`

ISO 8601 timestamp when the webhook event was created.
**data** `object`

Event-specific data containing detailed information about the event. The
data object for the `inbox.draft.deleted` event contains the following
parameters:

**object parameters**

**source** `api | dashboard | agent | system`

What made the change

**inbox\_id** `string`

The ID of the inbox

**thread\_id** `string`

The ID of the thread. Only on reply drafts

**draft\_id** `string`

The ID of the draft

**thread** `object`

The thread, as it is when the webhook is sent. Absent when the thread no longer exists. Only on reply drafts

**thread object**

**object** `string`

Always `inbox_thread`

**id** `string`

The ID of the thread

**subject** `string | null`

The subject of the thread

**folder** `inbox | archive | spam | sent | trash`

The folder the thread lives in

**labels** `array`

The labels attached to the thread, each with an `id`, `name`, and `color`

**read** `boolean`

True only when every message in the thread is read

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "type": "inbox.draft.deleted",
  "created_at": "2026-09-29T12:00:00.000Z",
  "data": {
    "source": "dashboard",
    "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    "thread_id": "7c1f0a2e-5d3b-4e8a-9f61-2b8d4c6e1a90",
    "draft_id": "9a2b7c4d-1e3f-4a5b-8c6d-0e1f2a3b4c5d",
    "thread": {
      "object": "inbox_thread",
      "id": "7c1f0a2e-5d3b-4e8a-9f61-2b8d4c6e1a90",
      "subject": "Question about my invoice",
      "folder": "inbox",
      "labels": [],
      "read": false
    }
  }
}
```
