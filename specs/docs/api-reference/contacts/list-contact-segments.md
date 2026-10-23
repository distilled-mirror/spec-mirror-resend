> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Contact Segments

> Retrieve a list of segments that a contact is part of.

## Path Parameters

Either `id` or `email` must be provided.

**id** `string`

The Contact ID.

**email** `string`

The Contact Email.

## Query Parameters

Note that the `limit` parameter is *optional*. If
you do not provide a `limit`, all segments will be returned
in a single response.

**limit** `number`

Number of segments to retrieve.
<ul><li>Maximum value: `100`</li>
<li>Minimum value: `1`</li></ul>

**after** `string`

The ID *after* which we'll retrieve more segments (for pagination).
This ID will *not* be included in the returned list. Cannot be
used with the
`before` parameter.
**before** `string`

The ID *before* which we'll retrieve more segments (for
pagination). This ID will *not* be included in the returned list.
Cannot be used with the `after` parameter.

> [!NOTE]
>
> You can only use either `after` or `before`
> parameter, not both. See our
> [pagination guide](/docs/api-reference/pagination.md) for more
> information.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.contacts.segments.list({
  contactId: 'e169aa45-1ecf-4183-9955-b1499d5701d3',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->contacts->segments->list(
  contactId: 'e169aa45-1ecf-4183-9955-b1499d5701d3'
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = 're_xxxxxxxxx'

params: resend.Contacts.Segments.ListParams = {
    "contact_id": 'e169aa45-1ecf-4183-9955-b1499d5701d3',
}

segments = resend.Contacts.Segments.list(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require 'resend'

Resend.api_key = 're_xxxxxxxxx'

segments = Resend::Contacts::Segments.list(
  contact_id: 'e169aa45-1ecf-4183-9955-b1499d5701d3'
)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	listParams := &resend.ListContactSegmentsRequest{
		ContactId: "479e3145-dd38-476b-932c-529ceb705947",
	}

	client.Contacts.Segments.List(listParams)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result, list_opts::ListOptions};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _contacts = resend
    .contacts
    .list_contact_segment(
      "e169aa45-1ecf-4183-9955-b1499d5701d3",
      ListOptions::default()
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;

public class Main {
  public static void main(String[] args) throws ResendException {
    Resend resend = new Resend("re_xxxxxxxxx");

    resend.contacts().segments().list("e169aa45-1ecf-4183-9955-b1499d5701d3");
  }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.ContactListSegmentsAsync( new Guid( "e169aa45-1ecf-4183-9955-b1499d5701d3" ));
Console.WriteLine( "Nr Segments={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/contacts/e169aa45-1ecf-4183-9955-b1499d5701d3/segments' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend contacts segments e169aa45-1ecf-4183-9955-b1499d5701d3
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "data": [
    {
      "id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
      "name": "Registered Users",
      "created_at": "2026-10-06 22:59:55.977+00"
    }
  ],
  "has_more": false
}
```
