> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Inbox

> Create an inbox to send, receive and organize email.

An inbox sends and receives email at an address on one of your domains, such as
`support@example.com`.

Without `forwarding`, the domain must have receiving enabled, with DKIM and SPF
verified and the inbound MX record verified or pending. With `forwarding` set to
`true`, the domain needs only DKIM and SPF verified. Otherwise, the request
returns a `422`. An address that is already in use
returns a `409`. A team at the inbox limit of its plan gets a `403`.

## Body Parameters

The inbox email address on one of your verified domains. The part before the
`@` can contain only letters, numbers, and `.`, `_`, `%`, and `-`, up to 64
characters. It cannot start or end with `.` or have two `.` in a row. To call
an inbox with a `%` in its address, use the Inbox ID in the path.

**name** `string`

Internal name for the inbox. Recipients do not see it. Max 64 characters.
Defaults to `email_address`.

The name recipients see when mail is sent from this inbox. Use a plain name,
without `:`, `<`, `>`, or line breaks. Max 78 characters. An email address in
the name must be on one of your verified domains.

**forwarding** `boolean` (default: false)

When `true`, Resend provisions a receiving address so you can receive mail
without adding an MX record. Read it from `receiving_address` with [Get
Inbox](/docs/api-reference/inboxes/get-inbox.md).

## Response Fields

**object** `string`

Always `inbox`.

**id** `string`

The ID of the inbox.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.create({
  emailAddress: 'support@example.com',
  name: 'Customer Support',
  fromName: 'Ada from Support',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->create([
  'email_address' => 'support@example.com',
  'name' => 'Customer Support',
  'from_name' => 'Ada from Support',
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.CreateParams = {
    "email_address": "support@example.com",
    "name": "Customer Support",
    "from_name": "Ada from Support",
}

resend.Inboxes.create(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  email_address: "support@example.com",
  name: "Customer Support",
  from_name: "Ada from Support"
}

Resend::Inboxes.create(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.CreateInboxRequest{
		EmailAddress: "support@example.com",
		Name:         "Customer Support",
		FromName:     "Ada from Support",
	}

	client.Inboxes.Create(params)
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{
  types::{CreateInboxOptions},
  Resend, Result,
};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let opts = CreateInboxOptions::new("support@example.com")
    .with_name("Customer Support")
    .with_from_name("Ada from Support");

  let _inbox = resend.inboxes.create(opts).await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.CreateInboxOptions;
import com.resend.services.inboxes.model.CreateInboxResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        CreateInboxOptions params = CreateInboxOptions.builder()
                .emailAddress("support@example.com")
                .name("Customer Support")
                .fromName("Ada from Support")
                .build();

        CreateInboxResponseSuccess data = resend.inboxes().create(params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxCreateAsync( new InboxCreateData()
{
    EmailAddress = "support@example.com",
    Name = "Customer Support",
    FromName = "Ada from Support",
} );
Console.WriteLine( "Inbox Id={0}", resp.Content );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/inboxes' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "email_address": "support@example.com",
  "name": "Customer Support",
  "from_name": "Ada from Support"
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes create \
  --email-address support@example.com \
  --name "Customer Support" \
  --from-name "Ada from Support"
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "inbox",
  "id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1"
}
```
