> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Templates

> List all templates.

By default, the API will return the most recent 20 templates. You can optionally use the `limit` parameter to return a different number of templates or control the pagination of the results with the `after` or `before` parameters.

## Query Parameters

**limit** `number`

Number of templates to retrieve.
<ul><li>Default value: `20`</li>
<li>Maximum value: `100`</li>
<li>Minimum value: `1`</li></ul>

**after** `string`

The ID *after* which we'll retrieve more templates (for pagination).
This ID will *not* be included in the returned list. Cannot be
used with the
`before` parameter.
**before** `string`

The ID *before* which we'll retrieve more templates (for
pagination). This ID will *not* be included in the returned list.
Cannot be used with the `after` parameter.

> [!NOTE]
>
> You can only use either `after` or `before`
> parameter, not both. See our
> [pagination guide](https://resend.com/docs/api-reference/pagination.md) for more
> information.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.templates.list({
  limit: 2,
  after: '34a080c9-b17d-4187-ad80-5af20266e535',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->templates->list([
  'limit' => 2,
  'after' => '34a080c9-b17d-4187-ad80-5af20266e535'
]);
```

```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Templates.list({
    "limit": 2,
    "after": "34a080c9-b17d-4187-ad80-5af20266e535",
})
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Templates.list(
  limit: 2,
  after: "34a080c9-b17d-4187-ad80-5af20266e535"
)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import (
	"context"

	"github.com/resend/resend-go/v4"
)

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	limit := 2
	after := "34a080c9-b17d-4187-ad80-5af20266e535"

	client.Templates.ListWithContext(context.TODO(), &resend.ListOptions{
		Limit: &limit,
		After: &after,
	})
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{list_opts::ListOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let list_opts = ListOptions::default()
    .with_limit(2)
    .list_after("34a080c9-b17d-4187-ad80-5af20266e535");

  let _list = resend.templates.list(list_opts).await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.core.net.ListParams;
import com.resend.services.templates.model.ListTemplatesResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        ListParams params = ListParams.builder()
            .limit(2)
            .after("34a080c9-b17d-4187-ad80-5af20266e535")
            .build();

        ListTemplatesResponseSuccess data = resend.templates().list(params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.TemplateListAsync();
Console.WriteLine( "Nr Templates={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/templates?limit=2&after=34a080c9-b17d-4187-ad80-5af20266e535' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend templates list
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "data": [
    {
      "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
      "name": "reset-password",
      "status": "draft",
      "published_at": null,
      "created_at": "2026-10-06 23:47:56.678+00",
      "updated_at": "2026-10-06 23:47:56.678+00",
      "alias": "reset-password"
    },
    {
      "id": "b7f9c2e1-1234-4abc-9def-567890abcdef",
      "name": "welcome-message",
      "status": "published",
      "published_at": "2026-10-06 23:47:56.678+00",
      "created_at": "2026-10-06 23:47:56.678+00",
      "updated_at": "2026-10-06 23:47:56.678+00",
      "alias": "welcome-message"
    }
  ],
  "has_more": false
}
```
