> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Events

> Retrieve a list of events.

## Query Parameters

**limit** `number`

Number of events to retrieve.
<ul><li>Default value: `20`</li>
<li>Maximum value: `100`</li>
<li>Minimum value: `1`</li></ul>

**after** `string`

The ID *after* which we'll retrieve more events (for pagination).
This ID will *not* be included in the returned list. Cannot be
used with the
`before` parameter.
**before** `string`

The ID *before* which we'll retrieve more events (for
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

const { data, error } = await resend.events.list();
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->events->list();
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Events.list()
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Events.list
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Events.List()
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result, list_opts::ListOptions};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _events = resend.events.list(ListOptions::default()).await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.events.model.ListEventsResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        ListEventsResponseSuccess data = resend.events().list();
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

var resp = await resend.EventListAsync();
Console.WriteLine( "Count={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/events' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend events list
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "has_more": false,
  "data": [
    {
      "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
      "name": "user.created",
      "schema": {
        "plan": "string"
      },
      "created_at": "2026-10-01 12:00:00.000000+00",
      "updated_at": "2026-10-01 12:00:00.000000+00"
    },
    {
      "id": "b2c3d4e5-f6a7-8901-bcde-f12345678901",
      "name": "user.upgraded",
      "schema": null,
      "created_at": "2026-09-15 08:30:00.000000+00",
      "updated_at": "2026-09-20 14:00:00.000000+00"
    }
  ]
}
```
