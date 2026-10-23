> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Managing Inboxes

> Learn how to rename, update and delete inboxes in Resend.

Once you have created an inbox, all members of your team can view the inbox, update it and delete it once it is no longer required.

## View an inbox

See the address, unread count, and the date of the last received email on the [Inboxes dashboard](https://resend.com/inboxes). You can also search for inboxes by name.

Select any individual inbox to view its threads and to make changes to it.

## Edit an inbox

While viewing an inbox, click on the **Settings** button to reconfigure your inbox.

The General settings allow you to change the inbox nickname, which is the name that you see within the Dashboard. You can also change the **Reply as** name, which is the name that people who receive emails from this inbox will see. This is the `from_name` field in the API.

You can also [update an inbox](/docs/api-reference/inboxes/update-inbox.md) via the API, SDKs, or CLI.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.update(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  { name: 'Customer Support', fromName: 'Ada from Support' },
);
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->update('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1', [
  'name' => 'Customer Support',
  'from_name' => 'Ada from Support',
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.UpdateParams = {
  "id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "name": "Customer Support",
  "from_name": "Ada from Support",
}

resend.Inboxes.update(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "name": "Customer Support",
  "from_name": "Ada from Support",
}

Resend::Inboxes.update(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	fromName := "Ada from Support"

	params := &resend.UpdateInboxRequest{
		Name:     "Customer Support",
		FromName: &fromName,
	}

	client.Inboxes.Update("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{types::UpdateInboxOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let update = UpdateInboxOptions::new()
    .with_name("Customer Support")
    .with_from_name("Ada from Support");

  let _inbox = resend
    .inboxes
    .update("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", update)
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.UpdateInboxOptions;
import com.resend.services.inboxes.model.UpdateInboxResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        UpdateInboxOptions params = UpdateInboxOptions.builder()
                .name("Customer Support")
                .fromName("Ada from Support")
                .build();

        UpdateInboxResponseSuccess data = resend.inboxes().update("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxUpdateAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new InboxUpdateData()
    {
        Name = "Customer Support",
        FromName = "Ada from Support",
    }
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X PATCH 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "name": "Customer Support",
  "from_name": "Ada from Support"
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes update b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --name "Customer Support" \
  --from-name "Ada from Support"
```

In the Dashboard, you can also update how you view threads in the inbox. You can choose from **Simple list** (the default), **Grouped list**, **Board**, **Swimlanes**, or **Cards and list**. Grouped and card views group threads by label. These view options are not available through the API.

![Choose an inbox view: Simple list, Grouped list, Board, Swimlanes, or Cards and list](https://mintcdn.com/resend/2wyYbavX_c3s0W4P/images/inbox-view.png?fit=max\&auto=format\&n=2wyYbavX_c3s0W4P\&q=85\&s=23b53f0365280fd5137099dd006c3667)

## Inbox agent

In the settings menu, under **Customize**, is the configuration for the built-in agent for this inbox. Each inbox has an agent that can take instructions, perform actions and draft responses. You can find more details about this agent in [Inbox Agent](/docs/dashboard/inboxes/agent.md).

## Inbox labels

In the settings menu, under **Labels**, you can add, edit and remove labels that can be used to organize threads. Find more details about how to use labels under [Inbox Labels](/docs/dashboard/inboxes/labels.md).

## Delete an inbox

In the Dashboard, you can delete an inbox either from the settings panel at the bottom of the general settings, or from the [list of inboxes](https://resend.com/inboxes). To delete an inbox:

**1. Click **Delete inbox****

**2. Enter the email address into the form to confirm**

**3. Delete the inbox**

You can also [delete an inbox](/docs/api-reference/inboxes/delete-inbox.md) via the API, SDKs, or CLI.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.remove(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
);
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->remove('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1');
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.remove("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Inboxes.remove("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Remove("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _deleted = resend
    .inboxes
    .delete("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.RemoveInboxResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        RemoveInboxResponseSuccess data = resend.inboxes().remove("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxDeleteAsync( new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ) );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X DELETE 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes delete b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 --yes
```

Deleting an inbox *cannot be undone* and severs the connection between the emails that were sent and received by an inbox.

Deleting an inbox removes its threads and the emails in them from the inbox. The individual emails can still be viewed in the [Emails dashboard](https://resend.com/emails). If your domain is configured to receive emails and trigger `email.received` webhooks, they will continue to fire too.

## API Reference

For complete API documentation, see the [Inboxes API reference](/docs/api-reference/inboxes/update-inbox.md).
