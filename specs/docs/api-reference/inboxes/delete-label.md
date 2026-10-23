> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Delete Label

> Remove an existing label from an inbox.

Deletes the label and removes it from every thread that carries it.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

The Label ID.

## Response Fields

**object** `string`

Always `inbox_label`.

**id** `string`

The ID of the label.

**deleted** `boolean`

Returns `true` when the label is deleted.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.labels.remove({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  labelId: '7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->labels->remove(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  '7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34'
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Labels.remove(
    inbox_id="b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    label_id="7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  label_id: "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34"
}

Resend::Inboxes::Labels.remove(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Labels.Remove(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
	)
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _deleted = resend
    .inboxes
    .delete_label(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.RemoveInboxLabelResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        RemoveInboxLabelResponseSuccess data = resend.inboxes().labels().remove(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxLabelDeleteAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34" )
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X DELETE 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/labels/7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes labels delete b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34 \
  --yes
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "inbox_label",
  "id": "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
  "deleted": true
}
```
