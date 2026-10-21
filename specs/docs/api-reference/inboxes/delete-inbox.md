> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Delete Inbox

> Remove an existing inbox.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

## Response Fields

**object** `string`

Always `inbox`.

**id** `string`

The ID of the inbox.

**deleted** `boolean`

Returns `true` when the inbox is deleted.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.remove(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
);
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->remove('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1');
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.remove("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Inboxes.remove("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Remove("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _deleted = resend
    .inboxes
    .delete("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
    .await?;

  Ok(())
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxDeleteAsync( new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ) );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X DELETE 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes delete b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 --yes
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "inbox",
  "id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "deleted": true
}
```
