> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Webhook

> Update an existing webhook configuration.

## Path Parameters

The Webhook ID.

## Body Parameters

**endpoint** `string`

The URL where webhook events will be sent.

**events** `string[]`

Array of event types to subscribe to.

See [event types](https://resend.com/docs/webhooks/event-types.md) for available options.

**status** `string`

The webhook status. Can be either `enabled` or `disabled`.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.webhooks.update(
  '430eed87-632a-4ea6-90db-0aace67ec228',
  {
    endpoint: 'https://new-webhook.example.com/handler',
    events: ['email.sent', 'email.delivered'],
    status: 'enabled',
  },
);
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->webhooks->update('430eed87-632a-4ea6-90db-0aace67ec228', [
  'endpoint' => 'https://new-webhook.example.com/handler',
  'events' => ['email.sent', 'email.delivered'],
  'status' => 'enabled',
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = 're_xxxxxxxxx'

params: resend.Webhooks.UpdateParams = {
    "webhook_id": "430eed87-632a-4ea6-90db-0aace67ec228",
    "endpoint": "https://new-webhook.example.com/handler",
    "events": ["email.sent", "email.delivered"],
    "status": "enabled",
}

webhook = resend.Webhooks.update(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require 'resend'

Resend.api_key = 're_xxxxxxxxx'

params = {
  webhook_id: '430eed87-632a-4ea6-90db-0aace67ec228',
  endpoint: 'https://new-webhook.example.com/handler',
  events: ['email.sent', 'email.delivered'],
  status: 'enabled'
}

webhook = Resend::Webhooks.update(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	endpoint := "https://new-webhook.example.com/handler"
	status := "enabled"
	params := &resend.UpdateWebhookRequest{
		Endpoint: &endpoint,
		Events:   []string{"email.sent", "email.delivered"},
		Status:   &status,
	}

	client.Webhooks.Update("430eed87-632a-4ea6-90db-0aace67ec228", params)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{
  events::EmailEventType::{EmailDelivered, EmailSent},
  types::{UpdateWebhookOptions, WebhookStatus},
  Resend, Result,
};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let events = [EmailSent, EmailDelivered];
  let opts = UpdateWebhookOptions::default()
    .with_endpoint("https://new-webhook.example.com/handler")
    .with_events(events)
    .with_status(WebhookStatus::Enabled);

  let _webhook = resend
    .webhooks
    .update("430eed87-632a-4ea6-90db-0aace67ec228", opts)
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.webhooks.model.UpdateWebhookOptions;
import com.resend.services.webhooks.model.UpdateWebhookResponseSuccess;
import com.resend.services.webhooks.model.WebhookStatus;
import static com.resend.services.webhooks.model.WebhookEvent.*;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        UpdateWebhookOptions options = UpdateWebhookOptions.builder()
            .endpoint("https://new-webhook.example.com/handler")
            .events(EMAIL_SENT, EMAIL_DELIVERED)
            .status(WebhookStatus.ENABLED)
            .build();

        UpdateWebhookResponseSuccess response = resend.webhooks()
            .update("430eed87-632a-4ea6-90db-0aace67ec228", options);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.WebhookUpdateAsync(
    new Guid( "430eed87-632a-4ea6-90db-0aace67ec228" ),
    new WebhookData()
    {
      EndpointUrl = "https://new-webhook.example.com/handler",
      Events = [ WebhookEventType.EmailSent ],
      Status = WebhookStatus.Disabled,
    }
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X PATCH 'https://api.resend.com/webhooks/430eed87-632a-4ea6-90db-0aace67ec228' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d '{
  "endpoint": "https://new-webhook.example.com/handler",
  "events": ["email.sent", "email.delivered"],
  "status": "enabled"
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend webhooks update 430eed87-632a-4ea6-90db-0aace67ec228 \
  --endpoint https://new-webhook.example.com/handler \
  --events email.sent email.delivered \
  --status enabled
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "webhook",
  "id": "430eed87-632a-4ea6-90db-0aace67ec228"
}
```
