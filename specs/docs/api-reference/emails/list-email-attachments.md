> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Attachments

> Retrieve a list of attachments from a sent email.

## Query Parameters

Note that the `limit` parameter is *optional*. If
you do not provide a `limit`, all attachments will be returned
in a single response.

**limit** `number`

Number of attachments to retrieve.
<ul><li>Maximum value: `100`</li>
<li>Minimum value: `1`</li></ul>

**after** `string`

The ID *after* which we'll retrieve more attachments (for pagination).
This ID will *not* be included in the returned list. Cannot be
used with the
`before` parameter.
**before** `string`

The ID *before* which we'll retrieve more attachments (for
pagination). This ID will *not* be included in the returned list.
Cannot be used with the `after` parameter.

> [!NOTE]
>
> You can only use either `after` or `before`
> parameter, not both. See our
> [pagination guide](/docs/api-reference/pagination) for more
> information.

## Path Parameters

**email\_id** `string` *required*

The Email ID.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.emails.attachments.list({
  emailId: '4ef9a417-02e9-4d39-ad75-9611e0fcc33c',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->emails->attachments->list(
  emailId: '4ef9a417-02e9-4d39-ad75-9611e0fcc33c'
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = 're_xxxxxxxxx'

attachments = resend.Emails.Attachments.list(
  email_id='4ef9a417-02e9-4d39-ad75-9611e0fcc33c'
)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require 'resend'

Resend.api_key = 're_xxxxxxxxx'

Resend::Emails::Attachments.list(
  email_id: "4ef9a417-02e9-4d39-ad75-9611e0fcc33c"
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

	client.Emails.ListAttachmentsWithContext(
		context.TODO(),
		"4ef9a417-02e9-4d39-ad75-9611e0fcc33c",
	)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{list_opts::ListOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _email = resend
    .emails
    .list_attachments(
      "4ef9a417-02e9-4d39-ad75-9611e0fcc33c",
      ListOptions::default(),
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.emails.model.ListAttachmentsResponse;

public class Main {
  public static void main(String[] args) throws ResendException {
    Resend resend = new Resend("re_xxxxxxxxx");

    ListAttachmentsResponse response = resend.emails().listAttachments(
      "4ef9a417-02e9-4d39-ad75-9611e0fcc33c"
    );
  }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.EmailAttachmentListAsync( new Guid( "4ef9a417-02e9-4d39-ad75-9611e0fcc33c" ));
Console.WriteLine( "Nr Attachments={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/emails/4ef9a417-02e9-4d39-ad75-9611e0fcc33c/attachments' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend emails attachments 4ef9a417-02e9-4d39-ad75-9611e0fcc33c
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "has_more": false,
  "data": [
    {
      "id": "2a0c9ce0-3112-4728-976e-47ddcd16a318",
      "filename": "avatar.png",
      "size": 4096,
      "content_type": "image/png",
      "content_disposition": "inline",
      "content_id": "img001",
      "download_url": "https://outbound-cdn.resend.com/4ef9a417-02e9-4d39-ad75-9611e0fcc33c/attachments/2a0c9ce0-3112-4728-976e-47ddcd16a318?some-params=example&signature=sig-123",
      "expires_at": "2026-10-17T14:29:41.521Z"
    }
  ]
}
```
