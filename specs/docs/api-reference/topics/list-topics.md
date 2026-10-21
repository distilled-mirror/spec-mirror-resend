> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Topics

> Retrieve a list of topics for the authenticated user.

## Query Parameters

**limit** `number`

Number of topics to retrieve.
<ul><li>Default value: `20`</li>
<li>Maximum value: `100`</li>
<li>Minimum value: `1`</li></ul>

**after** `string`

The ID *after* which we'll retrieve more topics (for pagination).
This ID will *not* be included in the returned list. Cannot be
used with the
`before` parameter.
**before** `string`

The ID *before* which we'll retrieve more topics (for
pagination). This ID will *not* be included in the returned list.
Cannot be used with the `after` parameter.

> [!NOTE]
>
> You can only use either `after` or `before`
> parameter, not both. See our
> [pagination guide](/docs/api-reference/pagination) for more
> information.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.topics.list();
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->topics->list();
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Topics.list()
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Topics.list()
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import (
	"context"

	"github.com/resend/resend-go/v4"
)

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Topics.ListWithContext(context.TODO(), nil)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{list_opts::ListOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _list = resend.topics.list(ListOptions::default()).await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.topics.model.ListTopicsResponseSuccess;

public class Main {
  public static void main(String[] args) throws ResendException {
    Resend resend = new Resend("re_xxxxxxxxx");

    ListTopicsResponseSuccess response = resend.topics().list();
  }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.TopicListAsync();
Console.WriteLine( "Nr Topics={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/topics' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend topics list
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "has_more": false,
  "data": [
    {
      "id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e",
      "name": "Weekly Newsletter",
      "description": "Weekly newsletter for our subscribers",
      "default_subscription": "opt_in",
      "visibility": "public",
      "created_at": "2026-04-08 00:11:13.110779+00"
    }
  ]
}
```
