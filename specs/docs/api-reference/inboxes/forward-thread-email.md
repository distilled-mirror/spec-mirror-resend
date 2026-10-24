> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Forward Thread Email

> Forward a message in an inbox thread to new recipients.

Forwards a message from the inbox address.

The attachments of the original message are sent with the forward, together
with any `attachments` you add. The request fails when they exceed 25 MB of
`content` in total. Files you add with `path` do not count toward it. An original
attachment that was sent from a URL (`path`) cannot be forwarded, and the
request returns a `422`. The whole email can be at most 40 MB.

The forward carries the same `In-Reply-To` and `References` headers as a
[reply](https://resend.com/docs/api-reference/inboxes/reply-thread-email.md) to the original message, so
mail clients may group it with the original conversation.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

The Thread ID.

The Email ID of the message to forward, as returned by [List Thread
Emails](https://resend.com/docs/api-reference/inboxes/list-thread-emails.md) in `data[].id`.

## Body Parameters

**to** `string | string[]` *required*

Recipient email address. For multiple addresses, send as an array of strings.
Must name at least one address. `to`, `cc`, and `bcc` combined cannot exceed
50 recipients.

**cc** `string | string[] | null`

CC recipient email address.

**bcc** `string | string[] | null`

BCC recipient email address.

**html** `string`

An HTML note sent above the quoted original.

**text** `string`

A plain-text note sent above the quoted original.

**subject** `string`

The subject of the forward. 1 to 2000 characters, with no line breaks.
Defaults to the thread subject with a `Fwd:` prefix.

**attachments** `array | null`

Files to attach, as on [Send Email](https://resend.com/docs/api-reference/emails/send-email.md).

**properties**

**content** `buffer | string`

Content of an attached file, passed as a buffer or Base64 string.

**filename** `string`

Name of attached file.

**path** `string`

Path where the attachment file is hosted.

Content type for the attachment. When not set, it is derived from the
`filename`.

Content ID for embedding inline images with a `cid:` reference in the
`html`. [Learn about inline images](https://resend.com/docs/dashboard/emails/embed-inline-images.md).

**headers** `object | null`

Custom headers to add to the email. You cannot set `In-Reply-To`,
`References`, or `Reply-To`.

## Headers

**Idempotency-Key** `string`

Add an idempotency key to prevent duplicated emails.

* Should be **unique per API request**
* Idempotency keys expire after **24 hours**
* Have a maximum length of **256 characters**
* A retry with the same key returns the first successful response, with the
  `idempotent-replayed: true` header
* A failed request is not stored, so you can retry it with the same key
* Reusing the key with a different body, or while the first request is still
  running, returns a `409`

[Learn more](https://resend.com/docs/dashboard/emails/idempotency-keys.md)

## Response Fields

**id** `string`

The ID of the sent email. Use it with the [emails
endpoints](https://resend.com/docs/api-reference/emails/retrieve-email.md).

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.threads.emails.forward({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  emailId: '5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60',
  to: ['colleague@example.org'],
  cc: ['billing@example.com'],
  bcc: ['records@example.com'],
  text: 'Flagging this refund request for you.',
  attachments: [
    {
      path: 'https://resend.com/static/sample/invoice.pdf',
      filename: 'invoice.pdf',
    },
  ],
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->threads->emails->forward(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  '5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60',
  [
    'to' => ['colleague@example.org'],
    'cc' => ['billing@example.com'],
    'bcc' => ['records@example.com'],
    'text' => 'Flagging this refund request for you.',
    'attachments' => [
      [
        'path' => 'https://resend.com/static/sample/invoice.pdf',
        'filename' => 'invoice.pdf',
      ],
    ],
  ]
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Threads.Emails.ForwardParams = {
    "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    "thread_id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
    "email_id": "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
    "to": ["colleague@example.org"],
    "cc": ["billing@example.com"],
    "bcc": ["records@example.com"],
    "text": "Flagging this refund request for you.",
    "attachments": [
        {
            "path": "https://resend.com/static/sample/invoice.pdf",
            "filename": "invoice.pdf",
        }
    ],
}

resend.Inboxes.Threads.Emails.forward(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  thread_id: "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  email_id: "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
  to: ["colleague@example.org"],
  cc: ["billing@example.com"],
  bcc: ["records@example.com"],
  text: "Flagging this refund request for you.",
  attachments: [{ path: "https://resend.com/static/sample/invoice.pdf", filename: "invoice.pdf" }]
}

Resend::Inboxes::Threads::Emails.forward(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.ForwardInboxThreadEmailRequest{
		To:   []string{"colleague@example.org"},
		Cc:   []string{"billing@example.com"},
		Bcc:  []string{"records@example.com"},
		Text: "Flagging this refund request for you.",
		Attachments: []*resend.Attachment{
			{
				Path:     "https://resend.com/static/sample/invoice.pdf",
				Filename: "invoice.pdf",
			},
		},
	}

	client.Inboxes.Threads.Emails.Forward(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
		"5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
		params,
	)
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{
  types::{CreateAttachment, ForwardInboxThreadEmailOptions},
  Resend, Result,
};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let opts = ForwardInboxThreadEmailOptions::new(["colleague@example.org"])
    .with_cc(["billing@example.com"])
    .with_bcc(["records@example.com"])
    .with_text("Flagging this refund request for you.")
    .with_attachment(
      CreateAttachment::from_path("https://resend.com/static/sample/invoice.pdf")
        .with_filename("invoice.pdf"),
    );

  let _forward = resend
    .inboxes
    .forward_thread_email(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
      "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
      opts,
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.emails.model.Attachment;
import com.resend.services.inboxes.model.ForwardInboxThreadEmailOptions;
import com.resend.services.inboxes.model.ForwardInboxThreadEmailResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        ForwardInboxThreadEmailOptions params = ForwardInboxThreadEmailOptions.builder()
                .to("colleague@example.org")
                .cc("billing@example.com")
                .bcc("records@example.com")
                .text("Flagging this refund request for you.")
                .attachments(Attachment.builder()
                        .fileName("invoice.pdf")
                        .path("https://resend.com/static/sample/invoice.pdf")
                        .build())
                .build();

        ForwardInboxThreadEmailResponseSuccess data = resend.inboxes().threads().emails().forward(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
                "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
                params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxThreadEmailForwardAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12" ),
    new Guid( "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60" ),
    new InboxThreadEmailForwardData()
    {
        To = "colleague@example.org",
        Cc = "billing@example.com",
        Bcc = "records@example.com",
        TextBody = "Flagging this refund request for you.",
        Attachments =
        [
            new EmailAttachment()
            {
                Filename = "invoice.pdf",
                Path = "https://resend.com/static/sample/invoice.pdf",
            },
        ],
    }
);
Console.WriteLine( "Email Id={0}", resp.Content );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12/emails/5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60/forward' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "to": ["colleague@example.org"],
  "cc": ["billing@example.com"],
  "bcc": ["records@example.com"],
  "text": "Flagging this refund request for you.",
  "attachments": [
    {
      "path": "https://resend.com/static/sample/invoice.pdf",
      "filename": "invoice.pdf"
    }
  ]
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads emails forward b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12 5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60 \
  --to colleague@example.org \
  --cc billing@example.com \
  --bcc records@example.com \
  --text "Flagging this refund request for you." \
  --attachment ./invoice.pdf
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "id": "6a0c8e58-3d9e-4f7a-8b14-2e3f4a5b6c71"
}
```
