> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Label

> Rename or recolor an existing label.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

The Label ID.

## Body Parameters

Omitted fields keep their current value.

**name** `string`

A new name for the label. Max 64 characters. A name that another label in the
inbox already uses, compared without case, returns a `422`.

**color** `string`

A new color for the label as a `#RRGGBB` hex code, like `#E93D82`.

## Response Fields

**object** `string`

Always `inbox_label`.

**id** `string`

The ID of the label.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.labels.update({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  labelId: '7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34',
  color: '#F76B15',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->labels->update(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  '7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34',
  ['color' => '#F76B15']
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Labels.UpdateParams = {
    "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    "id": "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
    "color": "#F76B15",
}

resend.Inboxes.Labels.update(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  label_id: "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
  color: "#F76B15"
}

Resend::Inboxes::Labels.update(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.UpdateInboxLabelRequest{
		Color: "#F76B15",
	}

	client.Inboxes.Labels.Update(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
		params,
	)
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{
  types::{UpdateInboxLabelOptions},
  Resend, Result,
};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let opts = UpdateInboxLabelOptions::new().with_color("#F76B15");

  let _label = resend
    .inboxes
    .update_label(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
      opts,
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.UpdateInboxLabelOptions;
import com.resend.services.inboxes.model.UpdateInboxLabelResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        UpdateInboxLabelOptions params = UpdateInboxLabelOptions.builder()
                .color("#F76B15")
                .build();

        UpdateInboxLabelResponseSuccess data = resend.inboxes().labels().update(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
                params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxLabelUpdateAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34" ),
    new InboxLabelUpdateData()
    {
        Color = "#F76B15",
    }
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X PATCH 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/labels/7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "color": "#F76B15"
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes labels update b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34 \
  --color '#F76B15'
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "inbox_label",
  "id": "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34"
}
```
