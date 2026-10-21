> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Contact Imports

> Retrieve a list of contact imports.

## Query Parameters

**limit** `number`

Number of contact imports to retrieve.

<ul>
  <li>
    Default value: `10`
  </li>

  <li>
    Maximum value: `100`
  </li>

  <li>
    Minimum value: `1`
  </li>
</ul>

**after** `string`

The contact import ID *after* which we'll retrieve more contact
imports. This ID will *not* be included in the returned list. Cannot be
used with the `before` parameter.

**before** `string`

The contact import ID *before* which we'll retrieve more contact
imports. This ID will *not* be included in the returned list. Cannot be
used with the `after` parameter.

**status** `'queued' | 'in_progress' | 'completed' | 'failed'`

Filter contact imports by status.

> [!NOTE]
>
> You can only use either `after` or `before` parameter,
> not both. See our [pagination guide](/docs/api-reference/pagination) for
> more information.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.contacts.imports.list({
  limit: 10,
  status: 'completed',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->contacts->imports->list([
  'limit' => 10,
  'status' => 'completed',
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Contacts.Imports.ListParams = {
    "limit": 10,
    "status": "completed",
}

resend.Contacts.Imports.list(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Contacts::Imports.list(limit: 10, status: "completed")
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	limit := 10
	client.Contacts.Imports.List(&resend.ListContactImportsOptions{
		Limit:  &limit,
		Status: string(resend.ContactImportStatusCompleted),
	})
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result, Value, list_opts::ListOptions};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _data = resend
    .contacts
    .list_imports(
      ListOptions::default()
        .with_limit(10)
        .with_other("status", Value::String("completed".to_owned())),
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.services.contacts.model.ListContactImportsParams;
import com.resend.services.contacts.model.ListContactImportsResponseSuccess;

public class Main {
    public static void main(String[] args) throws Exception {
        Resend resend = new Resend("re_xxxxxxxxx");

        ListContactImportsParams params = ListContactImportsParams.builder()
                .limit(10)
                .status("completed")
                .build();

        ListContactImportsResponseSuccess data = resend.contacts().imports().list(params);
    }
}
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/contacts/imports?limit=10&status=completed' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend contacts imports list --limit 10 --status completed
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "has_more": false,
  "data": [
    {
      "object": "contact_import",
      "id": "479e3145-dd38-476b-932c-529ceb705947",
      "status": "completed",
      "created_at": "2026-05-15 18:32:37.823+00",
      "completed_at": "2026-05-15 18:33:42.916+00",
      "counts": {
        "total": 1200,
        "created": 800,
        "updated": 300,
        "skipped": 75,
        "failed": 25
      }
    }
  ]
}
```
