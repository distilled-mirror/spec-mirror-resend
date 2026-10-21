> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Delete Domain

> Remove an existing domain.

> [!WARNING]
>
> Removing a domain with a configured [custom tracking subdomain](/docs/dashboard/domains/tracking)
> will also remove the Resend provisioned proxy, breaking any existing email links that use that subdomain.
>
> To keep links working, set up your own proxy pointing to Resend’s tracking DNS records before removing the domain.

## Path Parameters

The Domain ID.

```js Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.domains.remove(
  'd91cd9bd-1176-453e-8fc1-35364d380206',
);
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->domains->remove('d91cd9bd-1176-453e-8fc1-35364d380206');
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Domains.remove(domain_id="d91cd9bd-1176-453e-8fc1-35364d380206")
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Domains.remove("d91cd9bd-1176-453e-8fc1-35364d380206")
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Domains.Remove("d91cd9bd-1176-453e-8fc1-35364d380206")
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _deleted = resend
    .domains
    .delete("d91cd9bd-1176-453e-8fc1-35364d380206")
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.domains.model.RemoveDomainResponse;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        RemoveDomainResponse removed = resend.domains().remove("d91cd9bd-1176-453e-8fc1-35364d380206");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.DomainDeleteAsync( new Guid( "d91cd9bd-1176-453e-8fc1-35364d380206" ) );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X DELETE 'https://api.resend.com/domains/d91cd9bd-1176-453e-8fc1-35364d380206' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend domains delete d91cd9bd-1176-453e-8fc1-35364d380206
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "domain",
  "id": "d91cd9bd-1176-453e-8fc1-35364d380206",
  "deleted": true
}
```
