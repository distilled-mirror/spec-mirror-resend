> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# contact.updated

> Received when a contact is updated.

Event triggered whenever a **contact was successfully updated**.

## Response Body Parameters

All webhook payloads follow a consistent top-level structure with
event-specific data nested within the `data` object.

**type** `string`

The event type that triggered the webhook (e.g., `contact.updated`).
**created\_at** `string`

ISO 8601 timestamp when the webhook event was created.
**data** `object`

Event-specific data containing detailed information about the event. The
data object for the `contact.updated` event contains the following
parameters:

**object parameters**

**id** `string` *required*

Unique identifier for the contact

**audience\_id** `string`

Unique identifier for the audience this contact belongs to

**segment\_ids** `array`

Array of segment IDs the contact belongs to

**created\_at** `string` *required*

ISO 8601 timestamp when the contact was created

**updated\_at** `string` *required*

ISO 8601 timestamp when the contact was last updated

**email** `string` *required*

Contact's email address

**first\_name** `string | null`

Contact's first name. May be absent from the payload

**last\_name** `string | null`

Contact's last name. May be absent from the payload

**unsubscribed** `boolean` *required*

Whether the contact has unsubscribed from all Broadcasts and Automation emails
sent from your team

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "type": "contact.updated",
  "created_at": "2026-10-11T23:47:56.678Z",
  "data": {
    "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
    "audience_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "segment_ids": ["78261eea-8f8b-4381-83c6-79fa7120f1cf"],
    "created_at": "2026-10-10T15:11:54.110Z",
    "updated_at": "2026-10-11T23:47:56.678Z",
    "email": "steve.wozniak@gmail.com",
    "first_name": "Steve",
    "last_name": "Wozniak",
    "unsubscribed": false
  }
}
```
