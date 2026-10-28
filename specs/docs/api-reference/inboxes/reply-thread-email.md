> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Reply to Thread Email

> Send a reply to a message in an inbox thread.

Sends a reply from the inbox address.

The reply goes to the `Reply-To` addresses of the message. Without them, it goes
to the sender. A reply to a message the inbox sent goes to that message's `to`
recipients.

Attachments can have at most 25 MB of `content` in total. Files sent with
`path` do not count toward it. The whole email can be at most 40 MB.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

The Thread ID.

The Email ID of the message to reply to, as returned by [List Thread
Emails](https://resend.com/docs/api-reference/inboxes/list-thread-emails.md) in `data[].id`.

## Body Parameters

At least one of `html` or `text` is required. `cc` and `bcc` combined can have
at most 49 addresses, and the whole reply at most 50 recipients.

**cc** `string | string[] | null`

CC recipient email address.

**bcc** `string | string[] | null`

BCC recipient email address.

**html** `string`

The HTML body of the reply.

**text** `string`

The plain-text body of the reply.

**subject** `string`

The subject of the reply. 1 to 2000 characters, with no line breaks. Defaults
to the thread subject with a `Re:` prefix.

Reply to everyone on the original message.

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

const { data, error } = await resend.inboxes.threads.emails.reply({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  emailId: '5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60',
  cc: ['billing@example.com'],
  bcc: ['records@example.com'],
  html: '<p>Refund issued for order 1041.</p>',
  text: 'Refund issued for order 1041.',
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

$resend->inboxes->threads->emails->reply(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  '5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60',
  [
    'cc' => ['billing@example.com'],
    'bcc' => ['records@example.com'],
    'html' => '<p>Refund issued for order 1041.</p>',
    'text' => 'Refund issued for order 1041.',
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

params: resend.Inboxes.Threads.Emails.ReplyParams = {
    "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    "thread_id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
    "email_id": "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
    "cc": ["billing@example.com"],
    "bcc": ["records@example.com"],
    "html": "<p>Refund issued for order 1041.</p>",
    "text": "Refund issued for order 1041.",
    "attachments": [
        {
            "path": "https://resend.com/static/sample/invoice.pdf",
            "filename": "invoice.pdf",
        }
    ],
}

resend.Inboxes.Threads.Emails.reply(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  thread_id: "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  email_id: "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
  cc: ["billing@example.com"],
  bcc: ["records@example.com"],
  html: "<p>Refund issued for order 1041.</p>",
  text: "Refund issued for order 1041.",
  attachments: [{ path: "https://resend.com/static/sample/invoice.pdf", filename: "invoice.pdf" }]
}

Resend::Inboxes::Threads::Emails.reply(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.ReplyInboxThreadEmailRequest{
		Cc:   []string{"billing@example.com"},
		Bcc:  []string{"records@example.com"},
		Html: "<p>Refund issued for order 1041.</p>",
		Text: "Refund issued for order 1041.",
		Attachments: []*resend.Attachment{
			{
				Path:     "https://resend.com/static/sample/invoice.pdf",
				Filename: "invoice.pdf",
			},
		},
	}

	client.Inboxes.Threads.Emails.Reply(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
		"5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
		params,
	)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{
  types::{CreateAttachment, ReplyInboxThreadEmailOptions},
  Resend, Result,
};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let opts = ReplyInboxThreadEmailOptions::new()
    .with_cc(["billing@example.com"])
    .with_bcc(["records@example.com"])
    .with_html("<p>Refund issued for order 1041.</p>")
    .with_text("Refund issued for order 1041.")
    .with_attachment(
      CreateAttachment::from_path("https://resend.com/static/sample/invoice.pdf")
        .with_filename("invoice.pdf"),
    );

  let _reply = resend
    .inboxes
    .reply_thread_email(
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
import com.resend.services.inboxes.model.ReplyInboxThreadEmailOptions;
import com.resend.services.inboxes.model.ReplyInboxThreadEmailResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        ReplyInboxThreadEmailOptions params = ReplyInboxThreadEmailOptions.builder()
                .cc("billing@example.com")
                .bcc("records@example.com")
                .html("<p>Refund issued for order 1041.</p>")
                .text("Refund issued for order 1041.")
                .attachments(Attachment.builder()
                        .fileName("invoice.pdf")
                        .path("https://resend.com/static/sample/invoice.pdf")
                        .build())
                .build();

        ReplyInboxThreadEmailResponseSuccess data = resend.inboxes().threads().emails().reply(
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

var resp = await resend.InboxThreadEmailReplyAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12" ),
    new Guid( "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60" ),
    new InboxThreadEmailReplyData()
    {
        Cc = "billing@example.com",
        Bcc = "records@example.com",
        HtmlBody = "<p>Refund issued for order 1041.</p>",
        TextBody = "Refund issued for order 1041.",
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
curl -X POST 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12/emails/5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60/reply' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "cc": ["billing@example.com"],
  "bcc": ["records@example.com"],
  "html": "<p>Refund issued for order 1041.</p>",
  "text": "Refund issued for order 1041.",
  "attachments": [
    {
      "path": "https://resend.com/static/sample/invoice.pdf",
      "filename": "invoice.pdf"
    }
  ]
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads emails reply b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12 5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60 \
  --cc billing@example.com \
  --bcc records@example.com \
  --html "<p>Refund issued for order 1041.</p>" \
  --text "Refund issued for order 1041." \
  --attachment ./invoice.pdf
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "id": "6a0c8e58-3d9e-4f7a-8b14-2e3f4a5b6c71"
}
```
