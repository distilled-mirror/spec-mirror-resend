> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Segment Contacts

> Retrieve a list of contacts in a segment.

## Path Parameters

The Segment ID.

## Query Parameters

Note that the `limit` parameter is *optional*. If
you do not provide a `limit`, all contacts will be returned
in a single response.

**limit** `number`

Number of contacts to retrieve.
<ul><li>Maximum value: `100`</li>
<li>Minimum value: `1`</li></ul>

**after** `string`

The ID *after* which we'll retrieve more contacts (for pagination).
This ID will *not* be included in the returned list. Cannot be
used with the
`before` parameter.
**before** `string`

The ID *before* which we'll retrieve more contacts (for
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

const { data, error } = await resend.contacts.list({
  segmentId: '78261eea-8f8b-4381-83c6-79fa7120f1cf',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->contacts->list([
  'segment_id' => '78261eea-8f8b-4381-83c6-79fa7120f1cf',
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = 're_xxxxxxxxx'

contacts = resend.Contacts.list(segment_id='78261eea-8f8b-4381-83c6-79fa7120f1cf')
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require 'resend'

Resend.api_key = 're_xxxxxxxxx'

contacts = Resend::Contacts.list(segment_id: '78261eea-8f8b-4381-83c6-79fa7120f1cf')
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import (
	"context"
	"fmt"

	"github.com/resend/resend-go/v4"
)

func main() {
	ctx := context.TODO()
	client := resend.NewClient("re_xxxxxxxxx")

	contacts, err := client.Contacts.ListWithContext(ctx, &resend.ListContactsOptions{
		SegmentId: "78261eea-8f8b-4381-83c6-79fa7120f1cf",
	})
	if err != nil {
		panic(err)
	}
	fmt.Println(contacts)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{list_opts::ListOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _contacts = resend
    .segments
    .list_contacts(
      "78261eea-8f8b-4381-83c6-79fa7120f1cf",
      ListOptions::default(),
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.contacts.model.ListContactsResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        ListContactsResponseSuccess response = resend.contacts().list("78261eea-8f8b-4381-83c6-79fa7120f1cf");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.SegmentListContactsAsync( new Guid( "78261eea-8f8b-4381-83c6-79fa7120f1cf" ) );
Console.WriteLine( "Nr Contacts={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/segments/78261eea-8f8b-4381-83c6-79fa7120f1cf/contacts' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend segments contacts 78261eea-8f8b-4381-83c6-79fa7120f1cf
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "has_more": false,
  "data": [
    {
      "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
      "email": "steve.wozniak@gmail.com",
      "first_name": "Steve",
      "last_name": "Wozniak",
      "created_at": "2026-10-06 23:47:56.678+00",
      "unsubscribed": false
    }
  ]
}
```
