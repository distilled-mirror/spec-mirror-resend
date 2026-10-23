> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Set Thread Labels

> Replace every label on a thread.

The thread ends up with exactly the labels given, in one atomic change. Labels
on the thread that are not listed are taken off, and the labels themselves are
kept. If any label ID is not found, the request returns a `404` and nothing
changes.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

The Thread ID.

## Body Parameters

**labels** `string[]` *required*

The IDs of the labels the thread should carry. Up to 100 IDs, each belonging
to the inbox. Pass an empty array to take every label off the thread.

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

const { data, error } = await resend.inboxes.threads.labels.set({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  labels: ['2a8b4c6d-1e3f-4a5b-9c7d-8e0f1a2b3c4d'],
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->threads->labels->set(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  [
    'labels' => ['2a8b4c6d-1e3f-4a5b-9c7d-8e0f1a2b3c4d'],
  ]
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Threads.Labels.SetParams = {
    "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    "thread_id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
    "labels": ["2a8b4c6d-1e3f-4a5b-9c7d-8e0f1a2b3c4d"],
}

resend.Inboxes.Threads.Labels.set(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  thread_id: "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  labels: ["2a8b4c6d-1e3f-4a5b-9c7d-8e0f1a2b3c4d"]
}

Resend::Inboxes::Threads::Labels.set(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.SetInboxThreadLabelsRequest{
		Labels: []string{"2a8b4c6d-1e3f-4a5b-9c7d-8e0f1a2b3c4d"},
	}

	client.Inboxes.Threads.Labels.Set(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
		params,
	)
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _labels = resend
    .inboxes
    .set_thread_labels(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
      &["2a8b4c6d-1e3f-4a5b-9c7d-8e0f1a2b3c4d"],
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.SetInboxThreadLabelsOptions;
import com.resend.services.inboxes.model.SetInboxThreadLabelsResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        SetInboxThreadLabelsOptions params = SetInboxThreadLabelsOptions.builder()
                .labels("2a8b4c6d-1e3f-4a5b-9c7d-8e0f1a2b3c4d")
                .build();

        SetInboxThreadLabelsResponseSuccess data = resend.inboxes().threads().setLabels(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
                params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxThreadLabelSetAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12" ),
    [ new Guid( "2a8b4c6d-1e3f-4a5b-9c7d-8e0f1a2b3c4d" ) ]
);
Console.WriteLine( "Nr Labels={0}", resp.Content.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X PUT 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12/labels' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "labels": ["2a8b4c6d-1e3f-4a5b-9c7d-8e0f1a2b3c4d"]
}'
```

```bash Clear all labels theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X PUT 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12/labels' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "labels": []
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads labels set b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12 \
  --labels 2a8b4c6d-1e3f-4a5b-9c7d-8e0f1a2b3c4d
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
