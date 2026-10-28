> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Remove Thread Label

> Take one label off a thread.

The label itself is kept, and stays on every other thread that carries it. To
delete the label everywhere, use
[Delete Label](https://resend.com/docs/api-reference/inboxes/delete-label.md).

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

The Thread ID.

The Label ID.

## Response Fields

**object** `string`

Always `list`.

**data** `array`

Every label on the thread after the change.

**properties**

**id** `string`

The ID of the label.

**name** `string`

The name of the label.

**color** `string`

The color of the label as an uppercase `#RRGGBB` hex code, like
`#E93D82`.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.threads.labels.remove({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  labelId: '7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->threads->labels->remove(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  '7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34'
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Threads.Labels.remove(
    inbox_id="b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    thread_id="4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
    label_id="7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  thread_id: "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  label_id: "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34"
}

Resend::Inboxes::Threads::Labels.remove(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Threads.Labels.Remove(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
		"7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
	)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _labels = resend
    .inboxes
    .remove_thread_label(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
      "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.RemoveInboxThreadLabelResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        RemoveInboxThreadLabelResponseSuccess data = resend.inboxes().threads().removeLabel(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
                "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxThreadLabelRemoveAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12" ),
    new Guid( "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34" )
);
Console.WriteLine( "Nr Labels={0}", resp.Content.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X DELETE 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12/labels/7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads labels remove b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12 7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "data": [
    {
      "id": "2a8b4c6d-1e3f-4a5b-9c7d-8e0f1a2b3c4d",
      "name": "Billing",
      "color": "#00A2C7"
    }
  ]
}
```
