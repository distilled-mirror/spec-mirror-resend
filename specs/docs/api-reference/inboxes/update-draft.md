> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Draft

> Update an unsent draft.

Updates the content of an unsent draft. A draft that was already sent returns
a `409`.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

The Draft ID.

## Body Parameters

Send at least one field. Omitted fields keep their current value. A request
with `html` or `text` replaces both, and the one you leave out is saved as
`null`. After the update, the draft must still have at least one non-empty
field, and `to`, `cc`, and `bcc` combined cannot exceed 50 recipients.

**to** `string | string[] | null`

Recipients. Send `null` or `[]` to clear them.

**cc** `string | string[] | null`

CC recipients. Send `null` or `[]` to clear them.

**bcc** `string | string[] | null`

BCC recipients. Send `null` or `[]` to clear them.

**subject** `string | null`

The subject. 1 to 2000 characters, with no line breaks. Send `null` to clear
it.

**html** `string | null`

The HTML body. Send `null` to clear it.

**text** `string | null`

The plain-text body. Send `null` to clear it.

**attachments** `array | null`

Files to store on the draft, up to 25 MB in total. Sending the field replaces
every attachment on the draft. Send `null` or `[]` to remove them all. Drafts
do not accept `path` or `content_id`.

**properties**

**content** `buffer | string` *required*

Content of an attached file, passed as a buffer or Base64 string.

**filename** `string` *required*

Name of attached file.

Content type for the attachment. Must be a valid MIME type, such as
`application/pdf`.

## Response Fields

**object** `string`

Always `inbox_draft`.

**id** `string`

The ID of the draft.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.drafts.update({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  draftId: 'c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32',
  subject: 'Refund issued for order 1041',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->drafts->update(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  'c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32',
  ['subject' => 'Refund issued for order 1041']
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Drafts.UpdateParams = {
    "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    "id": "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
    "subject": "Refund issued for order 1041",
}

resend.Inboxes.Drafts.update(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  draft_id: "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
  subject: "Refund issued for order 1041"
}

Resend::Inboxes::Drafts.update(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	subject := "Refund issued for order 1041"
	params := &resend.UpdateInboxDraftRequest{
		Subject: &subject,
	}

	client.Inboxes.Drafts.Update(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
		params,
	)
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{
  types::{UpdateInboxDraftOptions},
  Resend, Result,
};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let opts = UpdateInboxDraftOptions::new().with_subject("Refund issued for order 1041");

  let _draft = resend
    .inboxes
    .update_draft(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
      opts,
    )
    .await?;

  Ok(())
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxDraftUpdateAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32" ),
    new InboxDraftUpdateData()
    {
        Subject = "Refund issued for order 1041",
    }
);
Console.WriteLine( "Draft Id={0}", resp.Content );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X PATCH 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/drafts/c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "subject": "Refund issued for order 1041"
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes drafts update b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32 \
  --subject "Refund issued for order 1041"
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "inbox_draft",
  "id": "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32"
}
```
