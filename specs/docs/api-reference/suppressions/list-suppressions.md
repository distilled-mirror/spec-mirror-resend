> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Suppressions

> Show all suppressions.

## Query Parameters

**limit** `number`

Number of suppressions to retrieve.
<ul><li>Default value: `20`</li>
<li>Maximum value: `100`</li>
<li>Minimum value: `1`</li></ul>

**after** `string`

The ID *after* which we'll retrieve more suppressions (for pagination).
This ID will *not* be included in the returned list. Cannot be
used with the
`before` parameter.
**before** `string`

The ID *before* which we'll retrieve more suppressions (for
pagination). This ID will *not* be included in the returned list.
Cannot be used with the `after` parameter.

> [!NOTE]
>
> You can only use either `after` or `before`
> parameter, not both. See our
> [pagination guide](/docs/api-reference/pagination) for more
> information.

**origin** `bounce | complaint | manual`

Filter suppressions by origin.

Possible values:

* `bounce`: emails suppressed automatically after a bounce
* `complaint`: emails suppressed due to a user complaint
* `manual`: emails suppressed by your team manually

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.suppressions.list();
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->suppressions->list();
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Suppressions.list()
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Suppressions.list
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Suppressions.List(&resend.ListSuppressionsOptions{})
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result, list_opts::ListOptions};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _data = resend.suppressions.list(ListOptions::default()).await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        resend.suppressions().list();
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

await resend.SuppressionListAsync();
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/suppressions' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend suppressions list
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "has_more": false,
  "data": [
    {
      "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
      "email": "steve.wozniak@example.com",
      "origin": "manual",
      "source_id": null,
      "created_at": "2026-10-06 23:47:56.678+00"
    },
    {
      "id": "520784e2-887d-4c25-b53c-4ad46ad38100",
      "email": "susan.kare@example.com",
      "origin": "bounce",
      "source_id": "4ef9a417-02e9-4d39-ad75-9611e0fcc33c",
      "created_at": "2026-10-07 08:12:03.412+00"
    }
  ]
}

// The `source_id` in the response references the email that triggered the suppression. For suppressions with a `manual` origin, `source_id` is `null`.
```
