> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Thread Emails

> Retrieve the messages in a thread.

Messages are returned oldest first. Each item has the same shape as [Retrieve
Thread Email](https://resend.com/docs/api-reference/inboxes/get-thread-email.md).

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

The Thread ID.

## Query Parameters

**limit** `number`

Number of messages to return. Default is `20`, maximum is `100`, minimum is
`1`.

**after** `string`

The ID of the last message on the current page. Returns the next, newer page.

**before** `string`

The ID of the first message on the current page. Returns the previous, older
page. Cannot be combined with `after`.

## Response Fields

**object** `string`

Always `list`.

**has\_more** `boolean`

Whether more messages exist beyond this page. Pass the last message's `id` as
`after` to continue.

**data** `array`

The messages on this page.

**properties**

**id** `string`

The ID of the message.

**direction** `string`

Whether the message was received by the inbox or sent from it. One of
`inbound` or `outbound`. A message the inbox sent to itself is `inbound`, so
a reply to it goes to its sender.

**from** `string`

Sender email address. Includes the display name when the sender has one, in
the format `Name <sender@domain.com>`.

**to** `string[]`

The recipients of the message. For a received message, these are the
addresses it was delivered to, not the full `To` header.

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

ISO 8601 timestamp when the inbox received the message, or when the inbox
sent it.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.threads.emails.list({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->threads->emails->list(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12'
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Threads.Emails.list(
    inbox_id="b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    thread_id="4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  thread_id: "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12"
}

Resend::Inboxes::Threads::Emails.list(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Threads.Emails.List(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
		nil,
	)
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result, list_opts::ListOptions};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _emails = resend
    .inboxes
    .list_thread_emails(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
      ListOptions::default(),
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.ListInboxThreadEmailsResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        ListInboxThreadEmailsResponseSuccess data = resend.inboxes().threads().emails().list(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxThreadEmailListAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12" )
);
Console.WriteLine( "Nr Emails={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12/emails' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads emails list b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "has_more": false,
  "data": [
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
  ]
}
```
