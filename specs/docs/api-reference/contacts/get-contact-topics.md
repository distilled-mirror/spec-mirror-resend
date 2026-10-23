> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Retrieve Contact Topics

> Retrieve a list of topics subscriptions for a contact.

## Path Parameters

Either `id` or `email` must be provided.

**id** `string`

The Contact ID.

**email** `string`

The Contact Email.

## Query Parameters

Note that the `limit` parameter is *optional*. If
you do not provide a `limit`, all topics will be returned
in a single response.

**limit** `number`

Number of topics to retrieve.
<ul><li>Maximum value: `100`</li>
<li>Minimum value: `1`</li></ul>

**after** `string`

The ID *after* which we'll retrieve more topics (for pagination).
This ID will *not* be included in the returned list. Cannot be
used with the
`before` parameter.
**before** `string`

The ID *before* which we'll retrieve more topics (for
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

const { data, error } = await resend.contacts.topics.list({
  id: 'e169aa45-1ecf-4183-9955-b1499d5701d3',
  // or: email: 'steve.wozniak@gmail.com',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

// Get by contact id
$resend->contacts->topics->get('e169aa45-1ecf-4183-9955-b1499d5701d3');

// Get by contact email
$resend->contacts->topics->get('steve.wozniak@gmail.com');
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = 're_xxxxxxxxx'

# Get by contact id
topics = resend.Contacts.Topics.list(contact_id='e169aa45-1ecf-4183-9955-b1499d5701d3')

# Get by contact email
topics = resend.Contacts.Topics.list(email='steve.wozniak@gmail.com')
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

# Get by contact id
contact_topics = Resend::Contacts::Topics.list(id: "e169aa45-1ecf-4183-9955-b1499d5701d3")

# Get by contact email
contact_topics = Resend::Contacts::Topics.list(email: "steve.wozniak@gmail.com")
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

	// Get by contact id
	topics, err := client.Contacts.Topics.ListWithContext(ctx, "e169aa45-1ecf-4183-9955-b1499d5701d3")
	if err != nil {
		panic(err)
	}
	fmt.Println(topics)

	// Get by contact email
	topics, err = client.Contacts.Topics.ListWithContext(ctx, "steve.wozniak@gmail.com")
	if err != nil {
		panic(err)
	}
	fmt.Println(topics)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{list_opts::ListOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _topics = resend
    .contacts
    .get_contact_topics(
      "e169aa45-1ecf-4183-9955-b1499d5701d3",
      ListOptions::default(),
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;

public class Main {
  public static void main(String[] args) throws ResendException {
    Resend resend = new Resend("re_xxxxxxxxx");

    // Get by contact id
    resend.contacts().topics().list("e169aa45-1ecf-4183-9955-b1499d5701d3");

    // Get by contact email
    resend.contacts().topics().list("steve.wozniak@gmail.com");
  }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.ContactListTopicsAsync( new Guid( "e169aa45-1ecf-4183-9955-b1499d5701d3" ));
Console.WriteLine( "Nr Topics={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
// Get by contact id
curl -X GET 'https://api.resend.com/contacts/e169aa45-1ecf-4183-9955-b1499d5701d3/topics' \
     -H 'Authorization: Bearer re_xxxxxxxxx'

// Get by contact email
curl -X GET 'https://api.resend.com/contacts/steve.wozniak@gmail.com/topics' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
# Get by contact id
resend contacts topics e169aa45-1ecf-4183-9955-b1499d5701d3

# Get by contact email
resend contacts topics steve.wozniak@gmail.com
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "has_more": false,
  "data": [
    {
      "id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e",
      "name": "Product Updates",
      "description": "New features, and latest announcements.",
      "subscription": "opt_in"
    }
  ]
}
```
