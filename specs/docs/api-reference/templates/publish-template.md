> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Publish Template

> Publish a template.

## Path Parameters

**id | alias** `string`

The ID or alias of the template to publish.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.templates.publish(
  '34a080c9-b17d-4187-ad80-5af20266e535',
);
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->templates->publish('34a080c9-b17d-4187-ad80-5af20266e535');
```

```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Templates.publish("34a080c9-b17d-4187-ad80-5af20266e535")
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Templates.publish("34a080c9-b17d-4187-ad80-5af20266e535")
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import (
	"context"

	"github.com/resend/resend-go/v4"
)

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Templates.PublishWithContext(
		context.TODO(),
		"34a080c9-b17d-4187-ad80-5af20266e535",
	)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _published = resend
    .templates
    .publish("34a080c9-b17d-4187-ad80-5af20266e535")
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.templates.model.PublishTemplateResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        PublishTemplateResponseSuccess data = resend.templates().publish("34a080c9-b17d-4187-ad80-5af20266e535");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.TemplatePublishAsync( new Guid( "34a080c9-b17d-4187-ad80-5af20266e535" ) );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/templates/34a080c9-b17d-4187-ad80-5af20266e535/publish' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend templates publish 34a080c9-b17d-4187-ad80-5af20266e535
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "template",
  "id": "34a080c9-b17d-4187-ad80-5af20266e535"
}
```
