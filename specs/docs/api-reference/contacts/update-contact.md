> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Contact

> Update an existing contact.

## Path Parameters

Either `id` or `email` must be provided.

**id** `string`

The Contact ID.

**email** `string`

The Contact Email.

## Body Parameters

The first name of the contact.

The last name of the contact.

**unsubscribed** `boolean`

The Contact's global subscription status. If set to `true`, the contact will
be unsubscribed from all Broadcasts.

**properties** `object`

A map of custom property keys and values to update.

**custom properties**

**key** `string` *required*

The property key.

**value** `string | number | boolean | null` *required*

The property value. Use `null` to clear the property value.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.contacts.update({
  id: 'e169aa45-1ecf-4183-9955-b1499d5701d3',
  // or: email: 'acme@example.com',
  unsubscribed: true,
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

// Update by contact id
$resend->contacts->update(
  idOrEmail: 'e169aa45-1ecf-4183-9955-b1499d5701d3',
  parameters: [
    'unsubscribed' => true
  ]
);

// Update by contact email
$resend->contacts->update(
  idOrEmail: 'acme@example.com',
  parameters: [
    'unsubscribed' => true
  ]
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

# Update by contact id
params: resend.Contacts.UpdateParams = {
  "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
  "unsubscribed": True,
}

resend.Contacts.update(params)

# Update by contact email
params: resend.Contacts.UpdateParams = {
  "email": "acme@example.com",
  "unsubscribed": True,
}

resend.Contacts.update(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

# Update by contact id
params = {
  "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
  "unsubscribed": true,
}

Resend::Contacts.update(params)

# Update by contact email
params = {
  "email": "acme@example.com",
  "unsubscribed": true,
}

Resend::Contacts.update(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	// Update by contact id
	params := &resend.UpdateContactRequest{
		Id:           "e169aa45-1ecf-4183-9955-b1499d5701d3",
		Unsubscribed: true,
	}

	client.Contacts.Update(params)

	// Update by contact email
	params = &resend.UpdateContactRequest{
		Email:        "acme@example.com",
		Unsubscribed: true,
	}

	client.Contacts.Update(params)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{types::ContactChanges, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let changes = ContactChanges::new().with_unsubscribed(true);

  // Update by contact id
  let _contact = resend
    .contacts
    .update("e169aa45-1ecf-4183-9955-b1499d5701d3", changes.clone())
    .await?;

  // Update by contact email
  let _contact = resend
    .contacts
    .update("acme@example.com", changes)
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.contacts.model.UpdateContactOptions;
import com.resend.services.contacts.model.UpdateContactResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        UpdateContactOptions params = UpdateContactOptions.builder()
                .id("e169aa45-1ecf-4183-9955-b1499d5701d3") // or: .email("acme@example.com")
                .unsubscribed(true)
                .build();

        UpdateContactResponseSuccess data = resend.contacts().update(params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

// By Id
await resend.ContactUpdateAsync(
    contactId: new Guid( "e169aa45-1ecf-4183-9955-b1499d5701d3" ),
    new ContactData()
    {
        FirstName = "Stevie",
        LastName = "Wozniaks",
        IsUnsubscribed = true,
    }
);

// By Email
await resend.ContactUpdateByEmailAsync(
    "acme@example.com",
    new ContactData()
    {
        FirstName = "Stevie",
        LastName = "Wozniaks",
        IsUnsubscribed = true,
    }
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
# Update by contact id
curl -X PATCH 'https://api.resend.com/contacts/520784e2-887d-4c25-b53c-4ad46ad38100' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "unsubscribed": true
}'

# Update by contact email
curl -X PATCH 'https://api.resend.com/contacts/acme@example.com' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "unsubscribed": true
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
# Update by contact id
resend contacts update e169aa45-1ecf-4183-9955-b1499d5701d3 --unsubscribed

# Update by contact email
resend contacts update acme@example.com --unsubscribed
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "contact",
  "id": "479e3145-dd38-476b-932c-529ceb705947"
}
```
