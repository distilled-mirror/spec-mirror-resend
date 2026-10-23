> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Retrieve Agent Settings

> Retrieve the agent settings for an inbox.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

## Response Fields

**object** `string`

Always `inbox_agent`.

**instructions** `string | null`

Instructions the agent follows when handling the inbox's threads. `null` when
no instructions are set.

**tone** `'concise_professional' | 'concise_casual' | 'expanded_professional' | 'expanded_casual' | null`

Tone the agent writes in. `null` when no tone is set.

* `concise_professional`: Brief responses in a professional tone.
* `concise_casual`: Brief responses in a casual tone.
* `expanded_professional`: Detailed responses in a professional tone.
* `expanded_casual`: Detailed responses in a casual tone.

**actions** `string[]`

Actions the agent is allowed to take.

* `draft_reply`: Draft a reply.
* `forward_thread`: Forward a thread.
* `add_labels`: Add labels to a thread.
* `assign_thread`: Assign a thread.
* `mark_as_spam`: Mark a thread as spam.
* `archive`: Archive a thread.
* `move_to_trash`: Move a thread to the trash.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.agent.get({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->agent->get('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1');
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Agent.get("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Inboxes::Agent.get({ inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" })
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Agent.Get("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _agent = resend
    .inboxes
    .get_agent("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.GetInboxAgentResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        GetInboxAgentResponseSuccess data = resend.inboxes().agent()
                .get("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxAgentRetrieveAsync( new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ) );
Console.WriteLine( "Agent tone={0}", resp.Content.Tone );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/agent' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes agent get b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "inbox_agent",
  "instructions": "Answer refund questions yourself. Escalate legal threats.",
  "tone": "concise_professional",
  "actions": ["draft_reply", "add_labels"]
}
```
