> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Enable Forge

> Put a domain's sending and receiving on Resend Forge.

This endpoint returns the DNS records Forge needs. Add them to your DNS and call
[Verify Domain](https://resend.com/docs/api-reference/domains/verify-domain.md) with `scope: ["forge"]`,
then poll [Retrieve Domain](https://resend.com/docs/api-reference/domains/get-domain.md) until each of
these records has the `status` `verified`.
Calling this endpoint again returns the current state.

* **Sending:** a Forge `SPF` record of type `CNAME`.
* **Receiving:** when the domain also receives email, Forge moves receiving
  too. The `Receiving` record of type `MX` gets a new value and the `status`
  `pending`. Replace your current `MX` record with it.

> [!NOTE]
>
> The domain keeps sending through its current records while the Forge record
> verifies, so there is no interruption.

> [!NOTE]
>
> The domain must be a sending domain. Receive-only domains, domains on a
> dedicated IP, and domains with legacy DomainKeys Identified Mail (DKIM) get a
> `forge_unavailable` error.

## Path Parameters

The Domain ID.

## Body Parameters

The subdomain label for the Forge return path, for example `forge` on
`example.com` produces a `CNAME` record for `forge.example.com`. It must start
with a letter and end with a letter or digit. It can contain only letters,
digits, and hyphens, and be 63 characters or less. It's stored lowercased.
When omitted, Resend picks a label that is free in your DNS. It can't equal
the domain's current return path, and the chosen host must not already have
DNS records, and either case gets a `return_path_unavailable` error. It can't
be changed afterwards.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.domains.forge.enable({
  id: 'd91cd9bd-1176-453e-8fc1-35364d380206',
  customReturnPath: 'forge',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->domains->forge->enable('d91cd9bd-1176-453e-8fc1-35364d380206', [
  'custom_return_path' => 'forge',
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Domains.Forge.EnableParams = {
    "id": "d91cd9bd-1176-453e-8fc1-35364d380206",
    "custom_return_path": "forge",
}

resend.Domains.Forge.enable(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

domain = Resend::Domains::Forge.enable(
  id: "d91cd9bd-1176-453e-8fc1-35364d380206",
  custom_return_path: "forge"
)
puts domain
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.EnableDomainForgeRequest{
		CustomReturnPath: "forge",
	}

	client.DomainForge.Enable("d91cd9bd-1176-453e-8fc1-35364d380206", params)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{types::EnableForgeOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let options = EnableForgeOptions::new().with_custom_return_path("forge");

  let _domain = resend
    .domains
    .enable_forge("d91cd9bd-1176-453e-8fc1-35364d380206", options)
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.domains.model.Domain;
import com.resend.services.domains.model.EnableForgeOptions;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        EnableForgeOptions params = EnableForgeOptions
                .builder()
                .customReturnPath("forge").build();

        Domain domain = resend.domains().forge()
                .enable("d91cd9bd-1176-453e-8fc1-35364d380206", params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.DomainForgeEnableAsync(
    new Guid( "d91cd9bd-1176-453e-8fc1-35364d380206" ),
    "forge" );
Console.WriteLine( "Domain Id={0}", resp.Content.Id );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/domains/d91cd9bd-1176-453e-8fc1-35364d380206/forge' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d '{"custom_return_path": "forge"}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend domains forge enable d91cd9bd-1176-453e-8fc1-35364d380206 --custom-return-path forge
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "domain",
  "id": "d91cd9bd-1176-453e-8fc1-35364d380206",
  "name": "example.com",
  "created_at": "2023-04-26T20:21:26.347412+00:00",
  "status": "partially_verified",
  "capabilities": {
    "sending": "enabled",
    "receiving": "disabled"
  },
  "records": [
    {
      "record": "DKIM",
      "name": "resend._domainkey",
      "value": "p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC...",
      "type": "TXT",
      "status": "verified",
      "ttl": "Auto"
    },
    {
      "record": "SPF",
      "name": "send",
      "type": "MX",
      "ttl": "Auto",
      "status": "verified",
      "value": "feedback-smtp.us-east-1.amazonses.com",
      "priority": 10
    },
    {
      "record": "SPF",
      "name": "send",
      "value": "v=spf1 include:amazonses.com ~all",
      "type": "TXT",
      "ttl": "Auto",
      "status": "verified"
    },
    {
      "record": "SPF",
      "name": "forge",
      "value": "send.forge.rmta.net",
      "type": "CNAME",
      "status": "pending",
      "ttl": "Auto"
    }
  ],
  "region": "us-east-1",
  "open_tracking": false,
  "click_tracking": false
}
```
