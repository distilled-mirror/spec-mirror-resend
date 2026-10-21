> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# email.received

> Received when an inbound email is received.

Event triggered whenever Resend **successfully receives an email**.

> [!NOTE]
>
> Webhooks do not include the email body, headers, or attachments, only their
> metadata. You must call the [Received emails
> API](/docs/api-reference/emails/retrieve-received-email) or the [Attachments
> API](/docs/api-reference/emails/list-received-email-attachments) to retrieve them.
> This design choice supports large attachments in serverless environments that
> have limited request body sizes.

## Response Body Parameters

All webhook payloads follow a consistent top-level structure with
event-specific data nested within the `data` object.

**type** `string`

The event type that triggered the webhook (e.g., `email.received`).
**created\_at** `string`

ISO 8601 timestamp when the webhook event was created.
**data** `object`

Event-specific data containing detailed information about the event. The
data object for the `email.received` event contains the following
parameters:

**object parameters**

**broadcast\_id** `string`

Unique identifier for the broadcast campaign (if applicable)

**created\_at** `string`

ISO 8601 timestamp when the email was created

**email\_id** `string`

Unique identifier for the specific email

**message\_id** `string`

RFC Message-ID header value for the email

**from** `string`

Sender's email address. For sent events, this matches the value passed at send time and may include a display name (e.g., `Name <email@domain.com>`). For received events, this is the bare email address only; the display name from the original `From:` header is preserved in `headers.from` on the [retrieve endpoint](/docs/api-reference/emails/retrieve-received-email).

**to** `array`

Array of impacted recipient email addresses

**subject** `string`

Email subject line

**template\_id** `string`

Unique identifier for the template used (if applicable)

**tags** `Record\<string, string\>`

Object of tag key-value pairs associated with the email.

Example:

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "category": "welcome",
  "user_id": "1234567890"
}
```

**received\_for** `array`

The recipient addresses the email was forwarded for, taken from the `for` clause of the message's `Received` headers.

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "type": "email.received",
  "created_at": "2026-02-22T23:41:12.126Z",
  "data": {
    "email_id": "56761188-7520-42d8-8898-ff6fc54ce618",
    "created_at": "2026-02-22T23:41:11.894Z",
    "from": "onboarding@resend.dev",
    "to": ["delivered@resend.dev"],
    "bcc": [],
    "cc": [],
    "received_for": ["forwarded@example.com"],
    "message_id": "<111-222-333@email.example.com>",
    "subject": "Sending this example",
    "attachments": [
      {
        "id": "2a0c9ce0-3112-4728-976e-47ddcd16a318",
        "filename": "avatar.png",
        "content_type": "image/png",
        "content_disposition": "inline",
        "content_id": "img001"
      }
    ]
  }
}
```
