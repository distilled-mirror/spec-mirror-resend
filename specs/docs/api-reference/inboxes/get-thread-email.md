> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Retrieve Thread Email

> Retrieve a single message from a thread.

Returns one message of a thread. Each item from [List Thread
Emails](/docs/api-reference/inboxes/list-thread-emails) has this shape.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

The Thread ID.

The Email ID, as returned by [List Thread
Emails](/docs/api-reference/inboxes/list-thread-emails) in `data[].id`.

## Response Fields

**id** `string`

The ID of the message.

**direction** `string`

Whether the message was received by the inbox or sent from it. One of
`inbound` or `outbound`. A message the inbox sent to itself is `inbound`, so a
reply to it goes to its sender.

**from** `string`

Sender email address. Includes the display name when the sender has one, in
the format `Name <sender@domain.com>`.

**to** `string[]`

The recipients of the message. For a received message, these are the addresses
it was delivered to, not the full `To` header.

**cc** `string[]`

The CC recipients of the message.

**bcc** `string[]`

The BCC recipients of the message. Always empty for a received message.

**reply\_to** `string[]`

The Reply-To addresses.

**subject** `string | null`

The subject of the message.

**message\_id** `string | null`

The Message-ID header of the message.

**html** `string | null`

The HTML body.

**text** `string | null`

The plain-text body.

**attachments** `array`

The attachments on the message.

**properties**

**id** `string`

The ID of the attachment.

**filename** `string | null`

The filename of the attachment.

**size** `number | null`

The size of the attachment in bytes.

**read** `boolean`

Whether the message has been read.

**received\_at** `string`

ISO 8601 timestamp when the inbox received the message, or when the inbox sent
it.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.threads.emails.get({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  emailId: '5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->threads->emails->get(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  '5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60'
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Threads.Emails.get(
    inbox_id="b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    thread_id="4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
    email_id="5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  thread_id: "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  email_id: "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60"
}

Resend::Inboxes::Threads::Emails.get(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Threads.Emails.Get(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
		"5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
	)
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _email = resend
    .inboxes
    .get_thread_email(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
      "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
    )
    .await?;

  Ok(())
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxThreadEmailRetrieveAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12" ),
    new Guid( "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60" )
);
Console.WriteLine( "Email subject={0}", resp.Content.Subject );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12/emails/5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads emails get b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12 5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "id": "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
  "direction": "inbound",
  "from": "Ada Lovelace <ada@example.org>",
  "to": ["support@example.com"],
  "cc": [],
  "bcc": [],
  "reply_to": ["replies@example.org"],
  "subject": "Refund for order 1041",
  "message_id": "<1041@example.org>",
  "html": "<p>Could I get a refund for order 1041?</p>",
  "text": "Could I get a refund for order 1041?",
  "attachments": [
    {
      "id": "9d4f2b81-6c3a-4e7d-8b12-0a5c6d7e8f90",
      "filename": "receipt.pdf",
      "size": 20841
    }
  ],
  "read": false,
  "received_at": "2026-08-05T14:03:11.229Z"
}
```
