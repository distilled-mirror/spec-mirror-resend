> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Creating Inboxes

> Learn how to create inboxes in Resend.

An inbox is an email address on a [verified domain](/docs/dashboard/domains/introduction.md). Once it exists, it can send email and collect replies in threads.

## Before you create an inbox

* [Add and verify a domain](/docs/dashboard/domains/introduction.md) for sending. The inbox address must use that domain.
* To receive email at the inbox, the domain also needs [receiving enabled with an MX record](/docs/dashboard/receiving/custom-domains.md#enabling-receiving-for-an-existing-domain). If you can't change the MX record, [set up forwarding](#forward-an-existing-address) instead.
* Inboxes are billed separately from the rest of your plan. When you create an inbox in the dashboard, Resend shows what applies to your account. See [pricing](https://resend.com/pricing#inboxes) for details.

## Create an inbox

### Using the dashboard

**1. Navigate to the Inboxes Dashboard page.**

The [Inboxes page](https://resend.com/inboxes) shows all of your existing
inboxes, and allows you to add new ones.

**2. Click the **Create inbox** button.**

![Create inbox](https://mintcdn.com/resend/2wyYbavX_c3s0W4P/images/inboxes-create.png?fit=max\&auto=format\&n=2wyYbavX_c3s0W4P\&q=85\&s=9a7716bb0de50e1a6efe64460fabac5b)

**3. Enter the address.**

Type the part before the `@`, for example `support`.

**4. Choose the domain from your list of verified domains.**

![Choose an address and domain](https://mintcdn.com/resend/2wyYbavX_c3s0W4P/images/inboxes-create-2.png?fit=max\&auto=format\&n=2wyYbavX_c3s0W4P\&q=85\&s=7041e9dcbb51c8031fc9553c171abf16)

**5. Start sending emails from your new inbox.**

![The new inbox is ready for you to compose your first
email.](https://mintcdn.com/resend/2wyYbavX_c3s0W4P/images/inboxes-create-3.png?fit=max\&auto=format\&n=2wyYbavX_c3s0W4P\&q=85\&s=f4a193c17e707a162a4558d2825a5008)

### Using the API

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
  "email_address": "support@example.com",
  "name": "Customer Support",
  "from_name": "Ada from Support",
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
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{types::CreateInboxOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let inbox = CreateInboxOptions::new("support@example.com")
    .with_name("Customer Support")
    .with_from_name("Ada from Support");

  let _inbox = resend.inboxes.create(inbox).await?;

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

await resend.InboxCreateAsync( new InboxCreateData()
{
    EmailAddress = "support@example.com",
    Name = "Customer Support",
    FromName = "Ada from Support",
} );
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

## Forward an existing address

If your domain is not verified for receiving emails you have two options. You can either [enable receiving for your domain with an MX record](/docs/dashboard/receiving/custom-domains.md#enabling-receiving-for-an-existing-domain) or set up forwarding. The Dashboard makes these options available to you.

If you are using the API and you can't add an MX record for the domain, set `forwarding` to `true` when creating the inbox. Resend provisions a receiving address for the inbox. [Retrieve the inbox](/docs/api-reference/inboxes/get-inbox.md) to read its `receiving_address`, then forward your existing mailbox to that address. Forwarded emails arrive in the inbox as threads.

> [!NOTE]
>
> Forwarding is useful when your domain's MX records already point at another
> mail provider and you don't want to change them.

## API Reference

For complete API documentation, see the [Inboxes API reference](/docs/api-reference/inboxes/create-inbox.md).
