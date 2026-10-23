> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Thread

> Mark a thread read or unread, or move it to another folder.

To change a thread's labels, use
[Add Thread Labels](/docs/api-reference/inboxes/add-thread-labels.md),
[Set Thread Labels](/docs/api-reference/inboxes/set-thread-labels.md), or
[Remove Thread Label](/docs/api-reference/inboxes/remove-thread-label.md).

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

The Thread ID.

## Body Parameters

At least one of `read` or `folder` is required. Omitted fields keep their
current value.

**read** `boolean`

Marks every message in the thread read or unread.

**folder** `string`

Moves the thread to this folder. Every thread sits in exactly one folder within
its inbox. `sent` is assigned automatically and cannot be set.

* `inbox`: The default. The thread holds at least one received message.
* `archive`: The thread was archived.
* `spam`: The thread was marked as spam.
* `trash`: The thread is scheduled for deletion in 30 days.

## Response Fields

**object** `string`

Always `inbox_thread`.

**id** `string`

The ID of the thread.

**subject** `string | null`

The subject of the thread.

**folder** `string`

The folder the thread lives in after the update.

* `inbox`: The default. The thread holds at least one received message.
* `archive`: The thread was archived.
* `spam`: The thread was marked as spam.
* `trash`: The thread is scheduled for deletion in 30 days.
* `sent`: Threads whose messages are all outbound.

**labels** `array`

The labels attached to the thread.

**properties**

**id** `string`

The ID of the label.

**name** `string`

The name of the label.

**color** `string`

The color of the label as an uppercase `#RRGGBB` hex code.

**read** `boolean`

True only when every message in the thread is read.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.threads.update({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  read: true,
  folder: 'spam',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->threads->update(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  [
    'read' => true,
    'folder' => 'spam',
  ]
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Threads.UpdateParams = {
    "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    "id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
    "read": True,
    "folder": "spam",
}

resend.Inboxes.Threads.update(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  thread_id: "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  read: true,
  folder: "spam"
}

Resend::Inboxes::Threads.update(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	read := true
	params := &resend.UpdateInboxThreadRequest{
		Read:   &read,
		Folder: resend.InboxMoveThreadFolderSpam,
	}

	client.Inboxes.Threads.Update(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
		params,
	)
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{
  types::{UpdateInboxThreadFolder, UpdateInboxThreadOptions},
  Resend, Result,
};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let opts = UpdateInboxThreadOptions::new()
    .with_read(true)
    .with_folder(UpdateInboxThreadFolder::Spam);

  let _thread = resend
    .inboxes
    .update_thread(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
      opts,
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.MoveInboxThreadFolder;
import com.resend.services.inboxes.model.UpdateInboxThreadOptions;
import com.resend.services.inboxes.model.UpdateInboxThreadResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        UpdateInboxThreadOptions params = UpdateInboxThreadOptions.builder()
                .read(true)
                .folder(MoveInboxThreadFolder.SPAM)
                .build();

        UpdateInboxThreadResponseSuccess data = resend.inboxes().threads().update(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
                params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxThreadUpdateAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12" ),
    new InboxThreadUpdateData()
    {
        IsRead = true,
        Folder = InboxMoveFolder.Spam,
    }
);
Console.WriteLine( "Thread folder={0}", resp.Content.Folder );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X PATCH 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "read": true,
  "folder": "spam"
}'
```

```bash Restore a trashed thread theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X PATCH 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "folder": "inbox"
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads update b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12 \
  --read \
  --folder spam
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "inbox_thread",
  "id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  "subject": "Refund for order 1041",
  "folder": "spam",
  "labels": [],
  "read": true
}
```
