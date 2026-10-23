> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Broadcast

> Update a broadcast to send to your contacts.

## Path Parameters

The ID of the broadcast you want to update.

## Body Parameters

The ID of the segment you want to send to.

> [!NOTE]
>
> Audiences are now called Segments. Follow the [Migration
> Guide](/docs/dashboard/segments/migrating-from-audiences-to-segments.md).

**from** `string`

Sender email address.

To include a friendly name, use the format `"Your Name <sender@domain.com>"`.

**subject** `string`

Email subject.

Reply-to email address. For multiple addresses, send as an array of strings.

**html** `string`

The HTML version of the message.

**text** `string`

The plain text version of the message.

> [!NOTE]
>
> If not provided, the HTML will be used to generate a plain text version. You
> can opt out of this behavior by setting value to an empty string.

**react** `React.ReactNode`

The React component used to write the message. *Only available in the Node.js
SDK.*

**name** `string`

The friendly name of the broadcast. Only used for internal reference.

The topic ID that the broadcast will be scoped to.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.broadcasts.update(
  '49a3999c-0ce1-4ea6-ab68-afcd6dc2e794',
  {
    html: 'Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}',
  },
);
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->broadcasts->update('49a3999c-0ce1-4ea6-ab68-afcd6dc2e794', [
  'html' => 'Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}',
]);
```

```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Broadcasts.UpdateParams = {
  "broadcast_id": "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794",
  "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}"
}

resend.Broadcasts.update(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "broadcast_id": "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794",
  "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
}
Resend::Broadcasts.update(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.UpdateBroadcastRequest{
		BroadcastId: "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794",
		Html:        "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
	}

	client.Broadcasts.Update(params)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{types::UpdateBroadcastOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let id = "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794";
  let html = "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}";

  let opts = UpdateBroadcastOptions::new().with_html(html);

  let _broadcast = resend.broadcasts.update(id, opts).await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.services.broadcasts.model.UpdateBroadcastOptions;
import com.resend.services.broadcasts.model.UpdateBroadcastResponseSuccess;

Resend resend = new Resend("re_xxxxxxxxx");

UpdateBroadcastOptions params = UpdateBroadcastOptions.builder()
    .id("49a3999c-0ce1-4ea6-ab68-afcd6dc2e794")
    .html("Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}")
    .build();

UpdateBroadcastResponseSuccess data = resend.broadcasts().update(params);
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.BroadcastUpdateAsync(
    new Guid( "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794" ),
    new BroadcastUpdateData()
    {
        HtmlBody = "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
    }
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X PATCH 'https://api.resend.com/broadcasts/49a3999c-0ce1-4ea6-ab68-afcd6dc2e794' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}"
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend broadcasts update 49a3999c-0ce1-4ea6-ab68-afcd6dc2e794 \
  --html "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}"
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "broadcast",
  "id": "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794"
}
```
