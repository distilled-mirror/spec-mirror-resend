> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Broadcasts

> Retrieve a list of broadcast.

> [!NOTE]
>
> See all available `status` types in [the Broadcasts
> overview](https://resend.com/docs/dashboard/broadcasts/manage-broadcasts.md#understand-broadcast-statuses).

## Query Parameters

Note that the `limit` parameter is *optional*. If
you do not provide a `limit`, all broadcasts will be returned
in a single response.

**limit** `number`

Number of broadcasts to retrieve.
<ul><li>Maximum value: `100`</li>
<li>Minimum value: `1`</li></ul>

**after** `string`

The ID *after* which we'll retrieve more broadcasts (for pagination).
This ID will *not* be included in the returned list. Cannot be
used with the
`before` parameter.
**before** `string`

The ID *before* which we'll retrieve more broadcasts (for
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

const { data, error } = await resend.broadcasts.list();
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->broadcasts->list();
```

```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Broadcasts.list()
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Broadcasts.list()
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Broadcasts.List()
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result, list_opts::ListOptions};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _broadcasts = resend.broadcasts.list(ListOptions::default()).await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.services.broadcasts.model.ListBroadcastsResponseSuccess;

Resend resend = new Resend("re_xxxxxxxxx");

ListBroadcastsResponseSuccess data = resend.broadcasts().list();
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.BroadcastListAsync();
Console.WriteLine( "Nr Broadcasts={0}", resp.Content.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/broadcasts' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend broadcasts list
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "has_more": false,
  "data": [
    {
      "id": "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794",
      "name": "Announcements",
      "audience_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf", // now called segment_id
      "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
      "status": "draft",
      "created_at": "2026-11-01 15:13:31.723+00",
      "scheduled_at": null,
      "sent_at": null
    },
    {
      "id": "559ac32e-9ef5-46fb-82a1-b76b840c0f7b",
      "name": "Black Friday",
      "audience_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf", // now called segment_id
      "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
      "status": "sent",
      "created_at": "2026-12-01 19:32:22.980+00",
      "scheduled_at": "2026-12-02 19:32:22.980+00",
      "sent_at": "2026-12-02 19:32:22.980+00"
    }
  ]
}
```
