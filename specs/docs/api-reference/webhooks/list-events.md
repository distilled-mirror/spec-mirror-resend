> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Events

> Retrieve a list of events delivered to a webhook.

## Path Parameters

The Webhook ID.

## Query Parameters

**limit** `number`

Number of events to return. Between `1` and `100`. Defaults to `20`.

**after** `string`

The event ID to fetch the next page after.

The `before` parameter is not supported for this endpoint.

## Response Fields

**object** `string`

Always `list`.

**has\_more** `boolean`

Whether more events exist beyond this page.

**data** `array`

The events delivered to this webhook, most recent first.

**properties**

**id** `string`

The event ID. Use this to [retrieve its details](/docs/api-reference/webhooks/get-event.md)
or [list its attempts](/docs/api-reference/webhooks/list-event-attempts.md).

**type** `string`

The event type, for example `email.sent`.

**created\_at** `string`

When the event was created.

**status** `string`

Delivery status of the event to this webhook: `success`, `failed`,
`attempting`, or `pending`.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.webhooks.events.list({
  webhookId: '4dd369bc-aa82-4ff3-97de-514ae3000ee0',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$events = $resend->webhooks->events->list(
    '4dd369bc-aa82-4ff3-97de-514ae3000ee0'
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = 're_xxxxxxxxx'

events = resend.Webhooks.list_events(
    webhook_id='4dd369bc-aa82-4ff3-97de-514ae3000ee0'
)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require 'resend'

Resend.api_key = 're_xxxxxxxxx'

events = Resend::Webhooks.list_events('4dd369bc-aa82-4ff3-97de-514ae3000ee0')
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Webhooks.ListEvents("4dd369bc-aa82-4ff3-97de-514ae3000ee0")
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{list_opts::ListOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _events = resend
    .webhooks
    .list_events(
      "4dd369bc-aa82-4ff3-97de-514ae3000ee0",
      ListOptions::default(),
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.webhooks.model.ListWebhookEventsResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        ListWebhookEventsResponseSuccess events = resend.webhooks().listEvents(
            "4dd369bc-aa82-4ff3-97de-514ae3000ee0"
        );
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.WebhookEventListAsync(
    new Guid( "4dd369bc-aa82-4ff3-97de-514ae3000ee0" )
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/webhooks/4dd369bc-aa82-4ff3-97de-514ae3000ee0/events' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "has_more": false,
  "data": [
    {
      "id": "msg_1srOsB4mXhCqCVwAxYRNnpFZhb3",
      "type": "email.delivered",
      "created_at": "2026-08-22T15:28:00.000Z",
      "status": "failed"
    },
    {
      "id": "msg_1srOrx2ZWZBpBUvZwXKQmoEYga2",
      "type": "email.sent",
      "created_at": "2026-08-22T15:27:42.000Z",
      "status": "success"
    }
  ]
}
```
