> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Retrieve Inbox

> Retrieve a single inbox by its ID or email address.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

## Response Fields

**object** `string`

Always `inbox`.

**id** `string`

The ID of the inbox.

**name** `string`

Internal name for the inbox. Recipients do not see it.

**email\_address** `string`

The address of the inbox.

**domain\_id** `string`

The ID of the domain that owns the address.

**receiving\_address** `string | null`

The address to forward mail to when forwarding is enabled. `null` otherwise.

**from\_name** `string | null`

The name recipients see when mail is sent from this inbox. `null` when not
set.

**unread** `number`

The number of unread threads in the Inbox folder.

**drafts** `number`

The number of unsent drafts.

**last\_received** `string | null`

ISO 8601 timestamp of the newest received email in the Inbox folder. `null`
when the folder has no received email.

**created\_at** `string`

ISO 8601 timestamp when the inbox was created.

**updated\_at** `string`

ISO 8601 timestamp when the inbox was updated.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.get(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
);
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->get('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1');
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.get("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Inboxes.get("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Get("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _inbox = resend
    .inboxes
    .get("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.GetInboxResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        GetInboxResponseSuccess data = resend.inboxes().get("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxRetrieveAsync( new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ) );
Console.WriteLine( "Inbox address={0}", resp.Content.EmailAddress );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes get b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "inbox",
  "id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "name": "Customer Support",
  "email_address": "support@example.com",
  "domain_id": "d91cd9bd-1176-453e-8fc1-35364d380206",
  "receiving_address": null,
  "from_name": "Ada from Support",
  "unread": 3,
  "drafts": 2,
  "last_received": "2026-08-05T14:03:11.229Z",
  "created_at": "2026-08-01T09:12:44.512Z",
  "updated_at": "2026-08-03T16:20:05.004Z"
}
```
