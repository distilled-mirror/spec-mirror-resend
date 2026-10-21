> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# inbox.thread.assigned

> Received when a thread is assigned or reassigned.

Event triggered whenever a **thread is assigned or reassigned**.

## Response Body Parameters

All webhook payloads follow a consistent top-level structure with
event-specific data nested within the `data` object.

**type** `string`

The event type that triggered the webhook (e.g., `inbox.thread.assigned`).
**created\_at** `string`

ISO 8601 timestamp when the webhook event was created.
**data** `object`

Event-specific data containing detailed information about the event. The
data object for the `inbox.thread.assigned` event contains the following
parameters:

**object parameters**

**assignee\_email** `string | null`

The email of the member the thread is now assigned to

**assigned\_by\_email** `string | null`

The email of the member who made the assignment. `null` when no member made it

**previous\_assignee\_email** `string | null`

The email of the member the thread was assigned to before. `null` when it was unassigned

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
  "type": "inbox.thread.assigned",
  "created_at": "2026-09-29T12:00:00.000Z",
  "data": {
    "assignee_email": "ada@example.com",
    "assigned_by_email": "grace@example.com",
    "previous_assignee_email": null,
    "source": "dashboard",
    "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    "thread_id": "7c1f0a2e-5d3b-4e8a-9f61-2b8d4c6e1a90",
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
