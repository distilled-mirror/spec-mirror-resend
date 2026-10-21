> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Automation

> Update an existing automation.

> [!NOTE]
>
> Provide at least one of `name`, `status`, or both `steps` and `connections`.
> When updating the workflow graph, `steps` and `connections` must be sent
> together.

## Path Parameters

The automation ID.

## Body Parameters

**name** `string`

The name of the automation.

**status** `string`

The status of the automation. Possible values are `enabled` or `disabled`.

**steps** `Step[]`

The steps that compose the automation graph. Must be provided together with
`connections`. The graph of an `enabled` automation cannot be updated: disable
the automation first, or duplicate it and edit the copy. See [Step
Properties](/docs/dashboard/automations/steps#step-properties) for full object
definition.

**connections** `Connection[]`

The connections between steps in the automation graph. Must be provided
together with `steps`. See [Connection
Properties](/docs/dashboard/automations/connections#connection-properties) for full
object definition.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.automations.update(
  'c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd',
  { status: 'enabled' },
);
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->automations->update('c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd', [
  'status' => 'enabled',
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Automations.UpdateParams = {
  "automation_id": "c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd",
  "status": "enabled",
}

resend.Automations.update(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  automation_id: "c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd",
  status: "enabled",
}

Resend::Automations.update(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.UpdateAutomationRequest{
		Status: resend.AutomationStatusEnabled,
	}

	client.Automations.Update("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd", params)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{
  types::{AutomationStatus, UpdateAutomationOptions},
  Resend, Result,
};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let opts = UpdateAutomationOptions::new().with_status(AutomationStatus::Enabled);
  let _automation = resend
    .automations
    .update("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd", opts)
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.automations.model.AutomationStatus;
import com.resend.services.automations.model.UpdateAutomationOptions;
import com.resend.services.automations.model.UpdateAutomationResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        UpdateAutomationOptions options = UpdateAutomationOptions.builder()
                .id("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd")
                .status(AutomationStatus.ENABLED)
                .build();

        UpdateAutomationResponseSuccess response = resend.automations().update(options);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

var resp = await resend.AutomationUpdateAsync(
    new Guid( "c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd" ),
    new AutomationUpdateData { Status = "enabled" }
);
Console.WriteLine( "AutomationId={0}", resp.Content );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X PATCH 'https://api.resend.com/automations/c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d '{
  "status": "enabled"
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend automations update c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd --status enabled
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "automation",
  "id": "c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd"
}
```
