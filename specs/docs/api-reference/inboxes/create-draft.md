> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Draft

> Create a draft in an inbox, either to start a new thread or reply to an existing thread.

A draft lets you prepare a message before sending it.

Omit `thread_id` and `reply_to_email_id` to start a new thread. Pass both for a
reply draft.

An email can have only one unsent reply draft. A request for an email that
already has one returns a `200` with the existing Draft ID. It changes only the
`attachments` of that draft.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

## Body Parameters

At least one of `to`, `cc`, `bcc`, `subject`, `text`, `html`, or `attachments`
must be non-empty. `to`, `cc`, and `bcc` combined cannot exceed 50 recipients.

**to** `string | string[] | null`

Recipients. For multiple addresses, send an array of strings. Each value can
include a friendly name, for example `Ada Lovelace <ada@example.org>`. On a
reply draft, when you omit `to` or send `null`, the draft gets the recipients
of a [reply](/docs/api-reference/inboxes/reply-thread-email.md). Send `[]` for no
recipients.

**cc** `string | string[] | null`

CC recipients.

**bcc** `string | string[] | null`

BCC recipients.

**subject** `string | null`

The subject. 1 to 2000 characters, with no line breaks.

**html** `string | null`

The HTML body.

**text** `string | null`

The plain-text body.

**attachments** `array | null`

Files to store on the draft, up to 25 MB in total. Drafts do not accept
`path` or `content_id`.

**properties**

**content** `buffer | string` *required*

Content of an attached file, passed as a buffer or Base64 string.

**filename** `string` *required*

Name of attached file.

Content type for the attachment. Must be a valid MIME type, such as
`application/pdf`.

The Thread ID to reply in. Must be sent with `reply_to_email_id`.

The Email ID to reply to, as returned by [List Thread
Emails](/docs/api-reference/inboxes/list-thread-emails.md) in `data[].id`. Must be
sent with `thread_id`.

## Headers

**Idempotency-Key** `string`

Add an idempotency key to prevent duplicated drafts.

* Should be **unique per API request**
* Idempotency keys expire after **24 hours**
* Have a maximum length of **256 characters**
* A retry with the same key returns the first successful response, with the
  `idempotent-replayed: true` header
* A failed request is not stored, so you can retry it with the same key
* Reusing the key with a different body, or while the first request is still
  running, returns a `409`

[Learn more](/docs/dashboard/emails/idempotency-keys.md)

## Response Fields

**object** `string`

Always `inbox_draft`.

**id** `string`

The ID of the draft.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.drafts.create({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  to: ['ada@example.org'],
  subject: 'Refund for order 1041',
  html: '<p>Refund issued for order 1041.</p>',
  text: 'Refund issued for order 1041.',
  attachments: [
    {
      filename: 'note.txt',
      content: 'aGVsbG8=',
      contentType: 'text/plain',
    },
  ],
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->drafts->create('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1', [
  'to' => ['ada@example.org'],
  'subject' => 'Refund for order 1041',
  'html' => '<p>Refund issued for order 1041.</p>',
  'text' => 'Refund issued for order 1041.',
  'attachments' => [
    [
      'filename' => 'note.txt',
      'content' => 'aGVsbG8=',
      'content_type' => 'text/plain',
    ],
  ],
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Drafts.CreateParams = {
    "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    "to": ["ada@example.org"],
    "subject": "Refund for order 1041",
    "html": "<p>Refund issued for order 1041.</p>",
    "text": "Refund issued for order 1041.",
    "attachments": [
        {
            "filename": "note.txt",
            "content": "aGVsbG8=",
            "content_type": "text/plain",
        }
    ],
}

resend.Inboxes.Drafts.create(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  to: ["ada@example.org"],
  subject: "Refund for order 1041",
  html: "<p>Refund issued for order 1041.</p>",
  text: "Refund issued for order 1041.",
  attachments: [{ filename: "note.txt", content: "aGVsbG8=", content_type: "text/plain" }]
}

Resend::Inboxes::Drafts.create(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.CreateInboxDraftRequest{
		To:      []string{"ada@example.org"},
		Subject: "Refund for order 1041",
		Html:    "<p>Refund issued for order 1041.</p>",
		Text:    "Refund issued for order 1041.",
		Attachments: []*resend.InboxDraftAttachmentInput{
			{
				Content:     []byte("hello"),
				Filename:    "note.txt",
				ContentType: "text/plain",
			},
		},
	}

	client.Inboxes.Drafts.Create("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params)
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{
  types::{CreateInboxDraftAttachment, CreateInboxDraftOptions},
  Resend, Result,
};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let opts = CreateInboxDraftOptions::new()
    .with_to(["ada@example.org"])
    .with_subject("Refund for order 1041")
    .with_html("<p>Refund issued for order 1041.</p>")
    .with_text("Refund issued for order 1041.")
    .with_attachment(CreateInboxDraftAttachment::new(
      b"hello".to_vec(),
      "note.txt",
      "text/plain",
    ));

  let _draft = resend
    .inboxes
    .create_draft("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", opts)
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.emails.model.Attachment;
import com.resend.services.inboxes.model.CreateInboxDraftOptions;
import com.resend.services.inboxes.model.CreateInboxDraftResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        CreateInboxDraftOptions params = CreateInboxDraftOptions.builder()
                .to("ada@example.org")
                .subject("Refund for order 1041")
                .html("<p>Refund issued for order 1041.</p>")
                .text("Refund issued for order 1041.")
                .attachments(Attachment.builder()
                        .fileName("note.txt")
                        .content("aGVsbG8=")
                        .contentType("text/plain")
                        .build())
                .build();

        CreateInboxDraftResponseSuccess data = resend.inboxes().drafts()
                .create("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxDraftCreateAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new InboxDraftCreateData()
    {
        To = "ada@example.org",
        Subject = "Refund for order 1041",
        HtmlBody = "<p>Refund issued for order 1041.</p>",
        TextBody = "Refund issued for order 1041.",
        Attachments =
        [
            new EmailAttachment()
            {
                Filename = "note.txt",
                Content = System.Text.Encoding.UTF8.GetBytes( "hello" ),
                ContentType = "text/plain",
            },
        ],
    }
);
Console.WriteLine( "Draft Id={0}", resp.Content );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/drafts' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "to": ["ada@example.org"],
  "subject": "Refund for order 1041",
  "html": "<p>Refund issued for order 1041.</p>",
  "text": "Refund issued for order 1041.",
  "attachments": [
    {
      "filename": "note.txt",
      "content": "aGVsbG8=",
      "content_type": "text/plain"
    }
  ]
}'
```

```bash Reply draft theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/drafts' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "thread_id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  "reply_to_email_id": "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
  "text": "Refund issued for order 1041."
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes drafts create b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --to ada@example.org \
  --subject "Refund for order 1041" \
  --html "<p>Refund issued for order 1041.</p>" \
  --text "Refund issued for order 1041." \
  --attachment "./note.txt;type=text/plain"
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "inbox_draft",
  "id": "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32"
}
```
