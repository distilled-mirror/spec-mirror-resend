> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send Draft

> Send an existing draft from the inbox address.

Sends the draft from the inbox address.

The draft needs a `to` recipient and `html` or `text`. A draft that is not a
reply also needs a `subject`. Otherwise, the request returns a `422`. A reply
draft without a subject uses the thread subject with a `Re:` prefix. The whole
email can be at most 40 MB. A draft that was already sent returns a `409`.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

The Draft ID.

## Body Parameters

The request body is optional and takes only `headers`. Without headers, send no
body.

**headers** `object | null`

Custom headers to add to the email. You cannot set `In-Reply-To`,
`References`, or `Reply-To`.

## Headers

**Idempotency-Key** `string`

Add an idempotency key to prevent duplicated emails.

* Should be **unique per API request**
* Idempotency keys expire after **24 hours**
* Have a maximum length of **256 characters**
* A retry with the same key returns the first successful response, with the
  `idempotent-replayed: true` header
* A failed request is not stored, so you can retry it with the same key
* Reusing the key with a different body, or while the first request is still
  running, returns a `409`

[Learn more](https://resend.com/docs/dashboard/emails/idempotency-keys.md)

## Response Fields

**id** `string`

The ID of the sent email. Use it with the [emails
endpoints](https://resend.com/docs/api-reference/emails/retrieve-email.md).

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.drafts.send({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  draftId: 'c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->drafts->send(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  'c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32'
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Drafts.send(
    inbox_id="b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    draft_id="c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  draft_id: "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32"
}

Resend::Inboxes::Drafts.send(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Drafts.Send(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
		nil,
	)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{
  types::{SendInboxDraftOptions},
  Resend, Result,
};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _sent = resend
    .inboxes
    .send_draft(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
      SendInboxDraftOptions::new(),
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.SendInboxDraftResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        SendInboxDraftResponseSuccess data = resend.inboxes().drafts().send(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxDraftSendAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32" )
);
Console.WriteLine( "Email Id={0}", resp.Content );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/drafts/c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32/send' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes drafts send b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "id": "6a0c8e58-3d9e-4f7a-8b14-2e3f4a5b6c71"
}
```
