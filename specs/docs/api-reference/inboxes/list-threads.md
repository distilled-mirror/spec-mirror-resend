> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Threads

> Retrieve the threads in an inbox, filtered by folder, label, and read status.

A thread is a conversation within an inbox, made up of one or more messages.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

## Query Parameters

**folders** `string`

Comma-separated folders to list. Defaults to `inbox`, or to
`inbox,archive,sent` when `labels` is set.

* `inbox`: The default. The thread holds at least one received message.
* `archive`: The thread was archived.
* `spam`: The thread was marked as spam.
* `trash`: The thread is scheduled for deletion in 30 days.
* `sent`: Threads whose messages are all outbound.

**labels** `string`

Comma-separated label IDs. Returns threads with any of these labels. Up to
`50` IDs.

**read** `boolean`

`true` returns threads where every email is read. `false` returns threads with
at least one unread email.

**limit** `number`

Number of threads to return. Default is `20`, maximum is `100`, minimum is
`1`.

**after** `string`

The ID of the last thread on the current page. Returns the next, older page.
Must be a thread ID. To filter by date, use [Search
Threads](/docs/api-reference/inboxes/search-threads.md) with `start_date`.

**before** `string`

The ID of the first thread on the current page. Returns the previous, newer
page. Cannot be combined with `after`. Must be a thread ID. To filter by date,
use [Search Threads](/docs/api-reference/inboxes/search-threads.md) with `end_date`.

To find threads by text, sender, recipient, attachment, or date, use [Search
Threads](/docs/api-reference/inboxes/search-threads.md).

## Response Fields

**object** `string`

Always `list`.

**has\_more** `boolean`

Whether more threads exist beyond this page. Pass the last thread's `id` as
`after` to continue.

**data** `array`

The matching threads, most recently active first.

**properties**

**id** `string`

The ID of the thread.

**subject** `string | null`

The subject of the thread.

**from** `string | null`

Sender email address. Can include the display name.

**to** `string[]`

The recipients of the most recent message. For a received email, these
are the addresses it was delivered to, not the full `To` header.

**cc** `string[]`

The CC recipients of the most recent message.

**bcc** `string[]`

The BCC recipients of the most recent message. Always empty for a
received email.

**labels** `array`

The labels attached to the thread.

**properties**

**id** `string`

The ID of the label.

**name** `string`

The name of the label.

**color** `string`

The color of the label as an uppercase `#RRGGBB` hex code.

**email\_count** `number`

The number of emails in the thread.

**has\_attachment** `boolean`

Whether the most recent message in the thread has an attachment.

**has\_draft** `boolean`

Whether the thread has an unsent draft.

**read** `boolean`

True only when every message in the thread is read.

**received\_at** `string`

ISO 8601 timestamp when the thread was last active.

**folder** `string`

The folder the thread lives in. Every thread sits in exactly one folder
within its inbox. You can move a thread to `inbox`, `archive`, `spam`, or
`trash`. `sent` is assigned automatically.

* `inbox`: The default. The thread holds at least one received message.
* `archive`: The thread was archived.
* `spam`: The thread was marked as spam.
* `trash`: The thread is scheduled for deletion in 30 days.
* `sent`: Threads whose messages are all outbound.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.threads.list({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->threads->list('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1');
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Threads.list("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Inboxes::Threads.list({ inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" })
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Threads.List("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", nil)
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{
  list_opts::ListOptions,
  types::ListInboxThreadsOptions,
  Resend, Result,
};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _threads = resend
    .inboxes
    .list_threads(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      ListInboxThreadsOptions::new(),
      ListOptions::default(),
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.ListInboxThreadsResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        ListInboxThreadsResponseSuccess data = resend.inboxes().threads()
                .list("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxThreadListAsync( new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ) );
Console.WriteLine( "Nr Threads={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads list b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "has_more": true,
  "data": [
    {
      "id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
      "subject": "Refund for order 1041",
      "from": "Ada Lovelace <ada@example.org>",
      "to": ["support@example.com"],
      "cc": [],
      "bcc": [],
      "labels": [
        {
          "id": "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
          "name": "Urgent",
          "color": "#E93D82"
        }
      ],
      "email_count": 2,
      "has_attachment": true,
      "has_draft": false,
      "read": false,
      "received_at": "2026-08-05T14:03:11.229Z",
      "folder": "inbox"
    }
  ]
}
```
