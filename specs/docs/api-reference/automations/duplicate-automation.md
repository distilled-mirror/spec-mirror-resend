> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Duplicate Automation

> Duplicate an existing automation.

## Path Parameters

The automation ID.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.automations.duplicate(
  'c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd',
);
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->automations->duplicate('c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd');
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Automations.duplicate("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd")
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Automations.duplicate("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd")
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Automations.Duplicate("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd")
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _automation = resend
    .automations
    .duplicate("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd")
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.automations.model.DuplicateAutomationResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        DuplicateAutomationResponseSuccess data = resend.automations().duplicate("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

var resp = await resend.AutomationDuplicateAsync( new Guid( "c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd" ) );
Console.WriteLine( "AutomationId={0}", resp.Content );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/automations/c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd/duplicate' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend automations duplicate c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "automation",
  "id": "e169aa45-1ecf-4183-9955-b1499d5701d3"
}
```
