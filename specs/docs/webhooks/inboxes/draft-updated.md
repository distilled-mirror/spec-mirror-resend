> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# inbox.draft.updated

> Received when a draft is edited.

Event triggered whenever a **draft is edited**.

## Response Body Parameters

All webhook payloads follow a consistent top-level structure with
event-specific data nested within the `data` object.

**type** `string`

The event type that triggered the webhook (e.g., `inbox.draft.updated`).
**created\_at** `string`

ISO 8601 timestamp when the webhook event was created.
**data** `object`

Event-specific data containing detailed information about the event. The
data object for the `inbox.draft.updated` event contains the following
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

**draft** `object`

The draft, as it is when the webhook is sent, without `html` or `text`. Fetch the body with [Retrieve Draft](https://resend.com/docs/api-reference/inboxes/get-draft.md). Absent when the draft no longer exists

**draft object**

**object** `string`

Always `inbox_draft`

**id** `string`

The ID of the draft

**type** `standalone | reply`

`standalone` for a new conversation, or `reply`

**to** `string[] | null`

Recipients

**cc** `string[]`

CC recipients

**bcc** `string[]`

BCC recipients

**subject** `string | null`

The subject

**thread\_id** `string | null`

The Thread ID when this draft is a reply. `null` otherwise

**reply\_to\_email\_id** `string | null`

The Email ID being replied to. `null` otherwise

**email\_id** `string | null`

The queued outbound email after send. `null` until then

**created\_at** `string`

ISO 8601 timestamp when the draft was created

**updated\_at** `string`

ISO 8601 timestamp when the draft was last saved

**attachments** `array`

The files stored on the draft

**attachment object**

**id** `string`

The ID of the attachment

**filename** `string`

The filename of the attachment

**content\_type** `string`

The MIME type of the attachment

**size** `number`

The size of the attachment in bytes

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "type": "inbox.draft.updated",
  "created_at": "2026-09-29T12:00:00.000Z",
  "data": {
    "source": "agent",
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
    },
    "draft": {
      "object": "inbox_draft",
      "id": "9a2b7c4d-1e3f-4a5b-8c6d-0e1f2a3b4c5d",
      "type": "reply",
      "to": ["steve.wozniak@gmail.com"],
      "cc": [],
      "bcc": [],
      "subject": "Re: Question about my invoice",
      "thread_id": "7c1f0a2e-5d3b-4e8a-9f61-2b8d4c6e1a90",
      "reply_to_email_id": "4ef9a417-02e9-4d39-ad75-9611e0fcc33c",
      "email_id": null,
      "created_at": "2026-09-29T11:58:00.000Z",
      "updated_at": "2026-09-29T12:00:00.000Z",
      "attachments": []
    }
  }
}
```
