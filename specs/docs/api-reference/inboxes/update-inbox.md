> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Inbox

> Update the internal inbox name or the name recipients see when sending.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

## Body Parameters

At least one of `name` or `from_name` is required. Omitted fields keep their
current value.

**name** `string`

New internal name for the inbox. Recipients do not see it. Between 1 and 64
characters after trimming.

The name recipients see when mail is sent from this inbox. Use a plain name,
without `:`, `<`, `>`, or line breaks. Max 78 characters. An email address in
the name must be on one of your verified domains. Send an empty string to
remove it.

## Response Fields

**object** `string`

Always `inbox`.

**id** `string`

The ID of the inbox.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.update(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  { name: 'Customer Support', fromName: 'Ada from Support' },
);
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->update('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1', [
  'name' => 'Customer Support',
  'from_name' => 'Ada from Support',
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.UpdateParams = {
    "id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    "name": "Customer Support",
    "from_name": "Ada from Support",
}

resend.Inboxes.update(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  name: "Customer Support",
  from_name: "Ada from Support"
}

Resend::Inboxes.update(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	fromName := "Ada from Support"
	params := &resend.UpdateInboxRequest{
		Name:     "Customer Support",
		FromName: &fromName,
	}

	client.Inboxes.Update("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params)
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{
  types::{UpdateInboxOptions},
  Resend, Result,
};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let opts = UpdateInboxOptions::new()
    .with_name("Customer Support")
    .with_from_name("Ada from Support");

  let _inbox = resend
    .inboxes
    .update("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", opts)
    .await?;

  Ok(())
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxUpdateAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new InboxUpdateData()
    {
        Name = "Customer Support",
        FromName = "Ada from Support",
    }
);
Console.WriteLine( "Inbox Id={0}", resp.Content );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X PATCH 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "name": "Customer Support",
  "from_name": "Ada from Support"
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes update b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --name "Customer Support" \
  --from-name "Ada from Support"
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "inbox",
  "id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1"
}
```
