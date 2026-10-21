> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# inbox.email.received

> Received when an inbound email is added to a thread.

Event triggered whenever an **inbound email is added to a thread**.

*Note: `source` is always `system`, because the email pipeline sends this event, even when the API or an agent sent the email.*

## Response Body Parameters

All webhook payloads follow a consistent top-level structure with
event-specific data nested within the `data` object.

**type** `string`

The event type that triggered the webhook (e.g., `inbox.email.received`).
**created\_at** `string`

ISO 8601 timestamp when the webhook event was created.
**data** `object`

Event-specific data containing detailed information about the event. The
data object for the `inbox.email.received` event contains the following
parameters:

**object parameters**

**source** `api | dashboard | agent | system`

What made the change

**inbox\_id** `string`

The ID of the inbox

**thread\_id** `string`

The ID of the thread

**email\_id** `string`

The ID of the email

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

**email** `object`

The email, as it is when the webhook is sent, without `html` or `text`. Fetch the body with [Retrieve Thread Email](/docs/api-reference/inboxes/get-thread-email). Absent when the email no longer exists

**email object**

**id** `string`

The ID of the email

**direction** `inbound | outbound`

Whether the email was received by the inbox or sent from it

**from** `string`

Sender email address. Can include the display name.

**to** `string[]`

The recipients of the email

**cc** `string[]`

The CC recipients of the email

**bcc** `string[]`

The BCC recipients of the email

**reply\_to** `string[]`

The Reply-To addresses

**subject** `string | null`

The subject of the email

**message\_id** `string | null`

The Message-ID header of the email

**attachments** `array`

The attachments on the email

**attachment object**

**id** `string`

The ID of the attachment

**filename** `string | null`

The filename of the attachment

**size** `number | null`

The size of the attachment in bytes

**read** `boolean`

Whether the email has been read

**received\_at** `string`

ISO 8601 timestamp when the email arrived or was sent

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "type": "inbox.email.received",
  "created_at": "2026-09-29T12:00:00.000Z",
  "data": {
    "source": "system",
    "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    "thread_id": "7c1f0a2e-5d3b-4e8a-9f61-2b8d4c6e1a90",
    "email_id": "4ef9a417-02e9-4d39-ad75-9611e0fcc33c",
    "thread": {
      "object": "inbox_thread",
      "id": "7c1f0a2e-5d3b-4e8a-9f61-2b8d4c6e1a90",
      "subject": "Question about my invoice",
      "folder": "inbox",
      "labels": [],
      "read": false
    },
    "email": {
      "id": "4ef9a417-02e9-4d39-ad75-9611e0fcc33c",
      "direction": "inbound",
      "from": "Steve Wozniak <steve.wozniak@gmail.com>",
      "to": ["support@example.com"],
      "cc": [],
      "bcc": [],
      "reply_to": [],
      "subject": "Question about my invoice",
      "message_id": "<CAF7c1f0a2e5d3b@mail.gmail.com>",
      "attachments": [
        {
          "id": "2a0c9ce0-3112-4728-976e-47ddcd16a318",
          "filename": "invoice.pdf",
          "size": 48213
        }
      ],
      "read": false,
      "received_at": "2026-09-29T12:00:00.000Z"
    }
  }
}
```
