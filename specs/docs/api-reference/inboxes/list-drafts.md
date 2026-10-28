> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Drafts

> Retrieve the unsent drafts in an inbox.

Returns the unsent drafts in the inbox, most recently updated first.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

## Query Parameters

**limit** `number`

Number of drafts to return. Default is `20`, maximum is `100`, minimum is `1`.

**after** `string`

The ID of the last draft on the current page. Returns the next, older page.

**before** `string`

The ID of the first draft on the current page. Returns the previous, newer
page. Cannot be combined with `after`.

## Response Fields

**object** `string`

Always `list`.

**has\_more** `boolean`

Whether more drafts exist beyond this page. Pass the last draft's `id` as
`after` to continue.

**data** `array`

The drafts on this page.

**properties**

**id** `string`

The ID of the draft.

**type** `string`

`reply` when the draft replies to an email in an existing thread.
`standalone` when the draft starts a new thread.

**to** `string[] | null`

Recipients. `null` or empty when no recipients are set.

**cc** `string[]`

CC recipients.

**bcc** `string[]`

BCC recipients.

**subject** `string | null`

The subject.

**snippet** `string | null`

A short preview of the body.

**thread\_id** `string | null`

The Thread ID when this draft is a reply. `null` otherwise.

**reply\_to\_email\_id** `string | null`

The Email ID being replied to. `null` otherwise.

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

const { data, error } = await resend.inboxes.drafts.list({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->drafts->list('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1');
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Drafts.list("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Inboxes::Drafts.list({ inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" })
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Drafts.List("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", nil)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result, list_opts::ListOptions};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _drafts = resend
    .inboxes
    .list_drafts("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", ListOptions::default())
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.ListInboxDraftsResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        ListInboxDraftsResponseSuccess data = resend.inboxes().drafts()
                .list("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxDraftListAsync( new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ) );
Console.WriteLine( "Nr Drafts={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/drafts' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes drafts list b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "has_more": false,
  "data": [
    {
      "id": "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
      "type": "standalone",
      "to": ["ada@example.org"],
      "cc": [],
      "bcc": [],
      "subject": "Refund for order 1041",
      "snippet": "Refund issued for order 1041.",
      "thread_id": null,
      "reply_to_email_id": null,
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
  ]
}
```
