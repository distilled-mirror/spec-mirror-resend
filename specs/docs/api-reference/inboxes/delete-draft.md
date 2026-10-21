> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Delete Draft

> Discard an unsent draft.

Discards an unsent draft. A draft that was already sent returns a `409`.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

The Draft ID.

## Response Fields

**object** `string`

Always `inbox_draft`.

**id** `string`

The ID of the draft.

**deleted** `boolean`

Returns `true` when the draft is deleted.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.drafts.remove({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  draftId: 'c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->drafts->remove(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  'c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32'
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Drafts.remove(
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

Resend::Inboxes::Drafts.remove(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Drafts.Remove(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
	)
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _deleted = resend
    .inboxes
    .delete_draft(
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

await resend.InboxDraftDeleteAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32" )
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X DELETE 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/drafts/c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes drafts delete b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32 \
  --yes
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "inbox_draft",
  "id": "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
  "deleted": true
}
```
