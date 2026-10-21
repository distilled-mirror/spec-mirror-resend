> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Delete Broadcast

> Remove an existing broadcast.

You can only delete Broadcasts that have not yet been sent (i.e., `draft` or `scheduled`). Deleting a `scheduled` Broadcast also cancels the scheduled delivery and the email will not be sent.

## Path Parameters

The broadcast ID.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.broadcasts.remove(
  '559ac32e-9ef5-46fb-82a1-b76b840c0f7b',
);
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->broadcasts->remove('559ac32e-9ef5-46fb-82a1-b76b840c0f7b');
```

```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Broadcasts.remove(id="559ac32e-9ef5-46fb-82a1-b76b840c0f7b")
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Broadcasts.remove("559ac32e-9ef5-46fb-82a1-b76b840c0f7b")
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Broadcasts.Remove("559ac32e-9ef5-46fb-82a1-b76b840c0f7b")
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _deleted = resend
    .broadcasts
    .delete("559ac32e-9ef5-46fb-82a1-b76b840c0f7b")
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.services.broadcasts.model.RemoveBroadcastResponseSuccess;

Resend resend = new Resend("re_xxxxxxxxx");

RemoveBroadcastResponseSuccess data = resend.broadcasts().remove("559ac32e-9ef5-46fb-82a1-b76b840c0f7b");
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.BroadcastDeleteAsync( new Guid( "559ac32e-9ef5-46fb-82a1-b76b840c0f7b" ) );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X DELETE 'https://api.resend.com/broadcasts/559ac32e-9ef5-46fb-82a1-b76b840c0f7b' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend broadcasts delete 559ac32e-9ef5-46fb-82a1-b76b840c0f7b
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "broadcast",
  "id": "559ac32e-9ef5-46fb-82a1-b76b840c0f7b",
  "deleted": true
}
```
