> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# inbox.thread.labels.updated

> Received when a label is applied to or removed from a thread.

Event triggered whenever a **label is applied to or removed from a thread**.

*Note: Moving a thread to a label can send both this event and `inbox.thread.folder.updated` for the same thread.*

*Note: Deleting a label doesn't send this event for the threads that had it.*

## Response Body Parameters

All webhook payloads follow a consistent top-level structure with
event-specific data nested within the `data` object.

**type** `string`

The event type that triggered the webhook (e.g., `inbox.thread.labels.updated`).
**created\_at** `string`

ISO 8601 timestamp when the webhook event was created.
**data** `object`

Event-specific data containing detailed information about the event. The
data object for the `inbox.thread.labels.updated` event contains the following
parameters:

**object parameters**

**added** `array`

The labels applied, each with an `id`, `name`, and `color`. One event carries every label changed by the same request

**removed** `array`

The labels removed, each with an `id`, `name`, and `color`. One event carries every label changed by the same request

**source** `api | dashboard | agent | system`

What made the change

**inbox\_id** `string`

The ID of the inbox

**thread\_id** `string`

The ID of the thread

**thread** `object`

The thread, as it is when the webhook is sent. Absent when the thread no longer exists

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
  "type": "inbox.thread.labels.updated",
  "created_at": "2026-09-29T12:00:00.000Z",
  "data": {
    "added": [
      {
        "id": "c0a8012e-3b4f-4d7a-9e21-5f6a7b8c9d0e",
        "name": "Billing",
        "color": "#F76B15"
      }
    ],
    "removed": [],
    "source": "dashboard",
    "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    "thread_id": "7c1f0a2e-5d3b-4e8a-9f61-2b8d4c6e1a90",
    "thread": {
      "object": "inbox_thread",
      "id": "7c1f0a2e-5d3b-4e8a-9f61-2b8d4c6e1a90",
      "subject": "Question about my invoice",
      "folder": "inbox",
      "labels": [
        {
          "id": "c0a8012e-3b4f-4d7a-9e21-5f6a7b8c9d0e",
          "name": "Billing",
          "color": "#F76B15"
        }
      ],
      "read": false
    }
  }
}
```
