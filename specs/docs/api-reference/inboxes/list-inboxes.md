> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Inboxes

> Retrieve a list of inboxes for the team.

Inboxes are returned newest first. Results are paginated with cursors. See
[Pagination](https://resend.com/docs/api-reference/pagination.md) for how `after` and `before` work. The
cursors take an inbox ID. A value that is not a UUID returns a `422`, and an
unknown ID returns a `404`.

The list items carry fewer fields than a single inbox. [Retrieve an
inbox](https://resend.com/docs/api-reference/inboxes/get-inbox.md) to get all its fields.

## Query Parameters

**limit** `number`

Number of inboxes to retrieve.
<ul><li>Default value: `20`</li>
<li>Maximum value: `100`</li>
<li>Minimum value: `1`</li></ul>

**after** `string`

The ID *after* which we'll retrieve more inboxes (for pagination).
This ID will *not* be included in the returned list. Cannot be
used with the
`before` parameter.
**before** `string`

The ID *before* which we'll retrieve more inboxes (for
pagination). This ID will *not* be included in the returned list.
Cannot be used with the `after` parameter.

> [!NOTE]
>
> You can only use either `after` or `before`
> parameter, not both. See our
> [pagination guide](https://resend.com/docs/api-reference/pagination.md) for more
> information.

## Response Fields

**object** `string`

Always `list`.

**has\_more** `boolean`

Whether more inboxes exist beyond this page.

**data** `array`

The inboxes on this page.

**properties**

**id** `string`

The ID of the inbox.

**name** `string | null`

Internal name for the inbox. Recipients do not see it.

**email\_address** `string`

The address of the inbox.

**from\_name** `string | null`

The name recipients see when mail is sent from this inbox. `null` when
not set.

**unread** `number`

The number of unread threads in the Inbox folder.

**last\_received** `string | null`

ISO 8601 timestamp of the newest received email in the Inbox folder.
`null` when the folder has no received email.

**created\_at** `string`

ISO 8601 timestamp when the inbox was created.

**updated\_at** `string`

ISO 8601 timestamp when the inbox was updated.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.list();
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->list();
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.list()
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Inboxes.list
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.List(nil)
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result, list_opts::ListOptions};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _inboxes = resend.inboxes.list(ListOptions::default()).await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.ListInboxesResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        ListInboxesResponseSuccess data = resend.inboxes().list();
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxListAsync();
Console.WriteLine( "Nr Inboxes={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/inboxes' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes list
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "has_more": false,
  "data": [
    {
      "id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "name": "Customer Support",
      "email_address": "support@example.com",
      "from_name": "Ada from Support",
      "unread": 3,
      "last_received": "2026-08-05T14:03:11.229Z",
      "created_at": "2026-08-01T09:12:44.512Z",
      "updated_at": "2026-08-03T16:20:05.004Z"
    },
    {
      "id": "1c5e0f3a-6b21-4d9a-8e77-5c0a9d8b4e12",
      "name": "billing@example.com",
      "email_address": "billing@example.com",
      "from_name": null,
      "unread": 0,
      "last_received": null,
      "created_at": "2026-07-20T11:00:00.000Z",
      "updated_at": "2026-07-20T11:00:00.318Z"
    }
  ]
}
```
