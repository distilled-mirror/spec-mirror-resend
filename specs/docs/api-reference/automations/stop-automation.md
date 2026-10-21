> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Stop Automation

> Stop a running automation.

## Path Parameters

The automation ID.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.automations.stop(
  'c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd',
);
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->automations->stop('c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd');
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Automations.stop("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd")
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Automations.stop("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd")
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Automations.Stop("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd")
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _automation = resend
    .automations
    .stop("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd")
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.automations.model.StopAutomationResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        StopAutomationResponseSuccess data = resend.automations().stop("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

var resp = await resend.AutomationStopAsync( new Guid( "c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd" ) );
Console.WriteLine( "Status={0}", resp.Content.Status );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/automations/c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd/stop' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend automations stop c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "automation",
  "id": "c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd",
  "status": "disabled"
}
```
