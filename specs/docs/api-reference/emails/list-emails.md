> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Sent Emails

> Retrieve a list of emails sent by your team.

You can list all emails sent by your team. The list returns references to individual emails. If needed, you can use the `id` of an email to retrieve the email HTML to plain text using the [Retrieve Email](/docs/api-reference/emails/retrieve-email) endpoint or the [Retrieve Attachments](/docs/api-reference/emails/list-email-attachments) endpoint to get an email's attachments.

> [!NOTE]
>
> This endpoint only returns emails sent by your team. If you need to list
> emails received by your domain, use the [List Received
> Emails](/docs/api-reference/emails/list-received-emails) endpoint.

## Query Parameters

**limit** `number`

Number of emails to retrieve.
<ul><li>Default value: `20`</li>
<li>Maximum value: `100`</li>
<li>Minimum value: `1`</li></ul>

**after** `string`

The ID *after* which we'll retrieve more emails (for pagination).
This ID will *not* be included in the returned list. Cannot be
used with the
`before` parameter.
**before** `string`

The ID *before* which we'll retrieve more emails (for
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

const { data, error } = await resend.emails.list();
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->emails->list();
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"
resend.Emails.list()
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

emails = Resend::Emails.list
puts emails
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import (
	"context"

	"github.com/resend/resend-go/v4"
)

func main() {
	ctx := context.TODO()
	client := resend.NewClient("re_xxxxxxxxx")

	paginatedResp, err := client.Emails.ListWithOptions(ctx, nil)
	if err != nil {
		panic(err)
	}

	if paginatedResp.HasMore {
		opts := &resend.ListOptions{
			After: &paginatedResp.Data[len(paginatedResp.Data)-1].Id,
		}
		client.Emails.ListWithOptions(ctx, opts)
	}
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{list_opts::ListOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _emails = resend.emails.list(ListOptions::default()).await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.emails.model.ListEmailsResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        ListEmailsResponseSuccess emails = resend.emails().list();
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.EmailListAsync();
Console.WriteLine( "Count={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/emails' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend emails list
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "has_more": false,
  "data": [
    {
      "id": "4ef9a417-02e9-4d39-ad75-9611e0fcc33c",
      "message_id": "<111-222-333@email.example.com>",
      "to": ["delivered@resend.dev"],
      "from": "Acme <onboarding@resend.dev>",
      "created_at": "2026-04-03 22:13:42.674981+00",
      "subject": "Hello World",
      "bcc": null,
      "cc": null,
      "reply_to": null,
      "last_event": "delivered",
      "scheduled_at": null
    },
    {
      "id": "3a9f8c2b-1e5d-4f8a-9c7b-2d6e5f8a9c7b",
      "message_id": "<444-555-666@email.example.com>",
      "to": ["user@example.com"],
      "from": "Acme <onboarding@resend.dev>",
      "created_at": "2026-04-03 21:45:12.345678+00",
      "subject": "Welcome to Acme",
      "bcc": null,
      "cc": null,
      "reply_to": null,
      "last_event": "opened",
      "scheduled_at": null
    }
  ]
}
```
