> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# email.suppressed

> Received when an email is suppressed.

Event triggered whenever the **email is suppressed** by Resend.

> [!NOTE]
>
> Learn more about [suppressed
> emails](/docs/knowledge-base/why-are-my-emails-landing-on-the-suppression-list).

## Response Body Parameters

All webhook payloads follow a consistent top-level structure with
event-specific data nested within the `data` object.

**type** `string`

The event type that triggered the webhook (e.g., `email.suppressed`).
**created\_at** `string`

ISO 8601 timestamp when the webhook event was created.
**data** `object`

Event-specific data containing detailed information about the event. The
data object for the `email.suppressed` event contains the following
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

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "type": "email.suppressed",
  "created_at": "2026-11-22T23:41:12.126Z",
  "data": {
    "broadcast_id": "8b146471-e88e-4322-86af-016cd36fd216",
    "created_at": "2026-11-22T23:41:11.894Z",
    "email_id": "56761188-7520-42d8-8898-ff6fc54ce618",
    "message_id": "<111-222-333@email.example.com>",
    "from": "Acme <onboarding@resend.dev>",
    "to": ["delivered@resend.dev"],
    "subject": "Sending this example",
    "template_id": "43f68331-0622-4e15-8202-246a0388854b",
    "suppressed": {
      "message": "Resend has suppressed sending to this address because it is on the account-level suppression list. This does not count toward your bounce rate metric",
      "type": "OnAccountSuppressionList"
    },
    "tags": {
      "category": "confirm_email"
    }
  }
}
```
