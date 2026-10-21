> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# contact.topics.updated

> Received when a contact's topic subscriptions change.

Event triggered whenever a **contact's topic subscriptions change**.

## Response Body Parameters

All webhook payloads follow a consistent top-level structure with
event-specific data nested within the `data` object.

**type** `string`

The event type that triggered the webhook (e.g., `contact.topics.updated`).
**created\_at** `string`

ISO 8601 timestamp when the webhook event was created.
**data** `object`

Event-specific data containing detailed information about the event. The
data object for the `contact.topics.updated` event contains the following
parameters:

**object parameters**

**email** `string`

Contact's email address

**topics** `array`

Topics changed in this update, each with its new subscription

**topic object**

**id** `string`

Unique identifier for the topic

**subscription** `opt_in | opt_out`

The contact's new subscription to the topic

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "type": "contact.topics.updated",
  "created_at": "2026-02-12T10:00:00.000Z",
  "data": {
    "email": "steve.wozniak@gmail.com",
    "topics": [
      {
        "id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e",
        "subscription": "opt_in"
      },
      {
        "id": "07d84122-7224-4881-9c31-1c048e204602",
        "subscription": "opt_out"
      }
    ]
  }
}
```
