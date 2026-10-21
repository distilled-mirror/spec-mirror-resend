> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Labels

> Retrieve the labels on an inbox.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

## Response Fields

**object** `string`

Always `list`.

**data** `array`

The labels on the inbox, oldest first.

**properties**

**id** `string`

The ID of the label.

**name** `string`

The name of the label.

**color** `string`

The color of the label as an uppercase `#RRGGBB` hex code, like
`#E93D82`.

**created\_at** `string`

ISO 8601 timestamp when the label was created.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.labels.list({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->labels->list('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1');
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Labels.list("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Inboxes::Labels.list({ inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" })
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Labels.List("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _labels = resend
    .inboxes
    .list_labels("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
    .await?;

  Ok(())
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxLabelListAsync( new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ) );
Console.WriteLine( "Nr Labels={0}", resp.Content.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/labels' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes labels list b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "data": [
    {
      "id": "2a8b4c6d-1e3f-4a5b-9c7d-8e0f1a2b3c4d",
      "name": "Billing",
      "color": "#00A2C7",
      "created_at": "2026-08-01T09:12:03.004Z"
    },
    {
      "id": "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
      "name": "Urgent",
      "color": "#E93D82",
      "created_at": "2026-08-05T14:07:42.881Z"
    }
  ]
}
```
