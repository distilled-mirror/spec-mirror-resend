> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Retrieve Draft

> Retrieve a single draft by its ID.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

The Draft ID.

## Response Fields

**object** `string`

Always `inbox_draft`.

**id** `string`

The ID of the draft.

**type** `string`

`reply` when the draft replies to an email in an existing thread. `standalone`
when the draft starts a new thread.

**to** `string[] | null`

Recipients. `null` or empty when no recipients are set.

**cc** `string[]`

CC recipients.

**bcc** `string[]`

BCC recipients.

**subject** `string | null`

The subject.

**html** `string | null`

The HTML body.

**text** `string | null`

The plain-text body.

**thread\_id** `string | null`

The Thread ID when this draft is a reply. `null` otherwise.

**reply\_to\_email\_id** `string | null`

The Email ID being replied to. `null` otherwise.

**email\_id** `string | null`

The ID of the outbound email queued when the draft was sent. `null` until the
draft is sent.

**created\_at** `string`

ISO 8601 timestamp when the draft was created.

**updated\_at** `string`

ISO 8601 timestamp when the draft was last saved.

**attachments** `array`

The files saved on the draft.

**properties**

**id** `string`

The ID of the attachment.

**filename** `string`

The filename of the attachment.

**content\_type** `string`

The MIME type of the attachment, such as `application/pdf`.

**size** `number`

The size of the attachment in bytes.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.drafts.get({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  draftId: 'c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->drafts->get(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  'c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32'
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Drafts.get(
    inbox_id="b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    draft_id="c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  draft_id: "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32"
}

Resend::Inboxes::Drafts.get(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Drafts.Get(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
	)
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _draft = resend
    .inboxes
    .get_draft(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
    )
    .await?;

  Ok(())
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxDraftRetrieveAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32" )
);
Console.WriteLine( "Draft subject={0}", resp.Content.Subject );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/drafts/c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes drafts get b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "inbox_draft",
  "id": "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
  "type": "standalone",
  "to": ["ada@example.org"],
  "cc": [],
  "bcc": [],
  "subject": "Refund for order 1041",
  "html": "<p>Refund issued for order 1041.</p>",
  "text": "Refund issued for order 1041.",
  "thread_id": null,
  "reply_to_email_id": null,
  "email_id": null,
  "created_at": "2026-08-05T14:12:04.110Z",
  "updated_at": "2026-08-05T14:12:04.110Z",
  "attachments": [
    {
      "id": "9d4f2b81-6c3a-4e7d-8b12-0a5c6d7e8f90",
      "filename": "note.txt",
      "content_type": "text/plain",
      "size": 5
    }
  ]
}
```
