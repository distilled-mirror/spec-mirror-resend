> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# inbox.updated

> Received when an inbox's settings change.

Event triggered whenever an **inbox's settings change**.

## Response Body Parameters

All webhook payloads follow a consistent top-level structure with
event-specific data nested within the `data` object.

**type** `string`

The event type that triggered the webhook (e.g., `inbox.updated`).
**created\_at** `string`

ISO 8601 timestamp when the webhook event was created.
**data** `object`

Event-specific data containing detailed information about the event. The
data object for the `inbox.updated` event contains the following
parameters:

**object parameters**

**source** `api | dashboard | agent | system`

What made the change

**inbox\_id** `string`

The ID of the inbox

**inbox** `object`

The inbox, as it is when the webhook is sent. Absent when the inbox no longer exists

**inbox object**

**object** `string`

Always `inbox`

**id** `string`

The ID of the inbox

**name** `string`

Internal name for the inbox. Recipients do not see it. Falls back to the inbox
address

**email\_address** `string`

The address of the inbox

**domain\_id** `string`

The ID of the domain the inbox belongs to

**receiving\_address** `string | null`

The address to forward mail to when forwarding is enabled. `null` otherwise

**from\_name** `string | null`

The name recipients see when mail is sent from this inbox. `null` when not set

**unread** `number`

The number of unread threads in the Inbox folder

**drafts** `number`

The number of unsent drafts

**last\_received** `string | null`

ISO 8601 timestamp of the newest received email in the Inbox folder. `null`
when the folder has no received email

**created\_at** `string`

ISO 8601 timestamp when the inbox was created

**updated\_at** `string`

ISO 8601 timestamp set when the inbox is created and updated whenever its name
or from name changes

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "type": "inbox.updated",
  "created_at": "2026-09-29T12:00:00.000Z",
  "data": {
    "source": "dashboard",
    "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    "inbox": {
      "object": "inbox",
      "id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "name": "Customer Support",
      "email_address": "support@example.com",
      "domain_id": "d91cd9bd-1176-453e-8fc1-35364d380206",
      "receiving_address": null,
      "from_name": "Ada from Support",
      "unread": 3,
      "drafts": 2,
      "last_received": "2026-09-29T11:42:08.000Z",
      "created_at": "2026-09-01T09:30:00.000Z",
      "updated_at": "2026-09-03T09:30:00.000Z"
    }
  }
}
```
