> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Inbox Agent

> Learn how to configure and use the built-in Inbox agent.

Every inbox has a built-in agent that can triage incoming email for you. You describe how the inbox should be handled, choose which actions the agent is allowed to take, and the agent acts on each new email that arrives.

## How the agent works

When a new email arrives in an inbox, the agent reads it alongside your instructions and decides which of its enabled actions to take, if any. The agent runs once the inbox has instructions and at least one enabled action.

The agent does not act on threads in the spam folder, and it skips emails that need no action.

> [!NOTE]
>
> The agent never sends email on its own. Replies and forwards are saved as
> [drafts](/docs/dashboard/inboxes/drafts.md) for a member of your team to review and
> send.

## Configure the agent

### Using the dashboard

**1. Open an inbox and click the **Settings** button.**

**2. Select the **Customize** tab.**

If the inbox is empty, you can also click **Set up agent**.

**3. Write your **Instructions**.**

Describe how the agent should handle email in this inbox, in up to 4,000
characters. Click the suggestion button for an example to start from.

**4. Choose the **Available actions**.**

Select the actions the agent is allowed to take, or choose **All actions**.

**5. Set the **Tone of voice**.**

Choose how concise or expanded, and how professional or casual, the agent's
writing should be. The preview shows how replies will sound.

Changes are saved automatically as you make them.

### Using the API

You can also [update the agent settings](/docs/api-reference/inboxes/update-agent.md) via the API, SDKs, or CLI. Fields you leave out keep their current value, and `actions` replaces the whole set of actions. The `tone` is one of `concise_professional`, `concise_casual`, `expanded_professional`, or `expanded_casual`.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.agent.update({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  instructions: 'Answer refund questions yourself. Escalate legal threats.',
  tone: 'concise_professional',
  actions: ['draft_reply', 'add_labels'],
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->agent->update('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1', [
  'instructions' => 'Answer refund questions yourself. Escalate legal threats.',
  'tone' => 'concise_professional',
  'actions' => ['draft_reply', 'add_labels'],
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Agent.UpdateParams = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "instructions": "Answer refund questions yourself. Escalate legal threats.",
  "tone": "concise_professional",
  "actions": ["draft_reply", "add_labels"],
}

resend.Inboxes.Agent.update(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "instructions": "Answer refund questions yourself. Escalate legal threats.",
  "tone": "concise_professional",
  "actions": ["draft_reply", "add_labels"],
}

Resend::Inboxes::Agent.update(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	instructions := "Answer refund questions yourself. Escalate legal threats."
	tone := resend.InboxAgentToneConciseProfessional

	params := &resend.UpdateInboxAgentRequest{
		Instructions: &instructions,
		Tone:         &tone,
		Actions: []resend.InboxAgentAction{
			resend.InboxAgentActionDraftReply,
			resend.InboxAgentActionAddLabels,
		},
	}

	client.Inboxes.Agent.Update("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{types::{InboxAgentAction, InboxAgentTone, UpdateInboxAgentOptions}, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let update = UpdateInboxAgentOptions::new()
    .with_instructions("Answer refund questions yourself. Escalate legal threats.")
    .with_tone(InboxAgentTone::ConciseProfessional)
    .with_actions([InboxAgentAction::DraftReply, InboxAgentAction::AddLabels]);

  let _agent = resend
    .inboxes
    .update_agent("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", update)
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.InboxAgentAction;
import com.resend.services.inboxes.model.UpdateInboxAgentOptions;
import com.resend.services.inboxes.model.UpdateInboxAgentResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        UpdateInboxAgentOptions params = UpdateInboxAgentOptions.builder()
                .instructions("Answer refund questions yourself. Escalate legal threats.")
                .tone("concise_professional")
                .actions(InboxAgentAction.DRAFT_REPLY, InboxAgentAction.ADD_LABELS)
                .build();

        UpdateInboxAgentResponseSuccess data = resend.inboxes().agent().update("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxAgentUpdateAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new InboxAgentUpdateData()
    {
        Instructions = "Answer refund questions yourself. Escalate legal threats.",
        Tone = InboxAgentTone.ConciseProfessional,
        Actions = new List<InboxAgentAction>
        {
            InboxAgentAction.DraftReply,
            InboxAgentAction.AddLabels,
        },
    }
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X PATCH 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/agent' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "instructions": "Answer refund questions yourself. Escalate legal threats.",
  "tone": "concise_professional",
  "actions": ["draft_reply", "add_labels"]
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes agent update \
  --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --instructions "Answer refund questions yourself. Escalate legal threats." \
  --tone concise_professional \
  --actions draft_reply add_labels
```

To see the current settings, [retrieve the agent settings](/docs/api-reference/inboxes/get-agent.md).

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

Resend::Inboxes::Agent.get({ "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" })
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Agent.Get("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
}
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

        GetInboxAgentResponseSuccess data = resend.inboxes().agent().get("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1");
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
resend inboxes agent get --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1
```

## Actions

The available actions are:

| Dashboard name | API value | What the agent does |
| - | - | - |
| Draft replies | `draft_reply` | Writes a reply as a draft for you to review and send. |
| Forward threads | `forward_thread` | Writes a forward as a draft for you to review and send. |
| Add labels | `add_labels` | Applies existing [labels](/docs/dashboard/inboxes/labels.md) to the thread. |
| Assign threads to teammates | `assign_thread` | Assigns the thread to a member of your team. |
| Mark as spam | `mark_as_spam` | Moves the thread to the spam folder. |
| Archive | `archive` | Moves the thread to the archive folder. |
| Move to trash | `move_to_trash` | Moves the thread to the trash folder. |

A few rules keep the agent's actions safe:

* **Drafts are never overwritten.** If a thread already has a draft, the agent leaves it alone and does not draft a reply or forward.
* **Forwards only go to addresses in your instructions.** Write out the full email address the agent should forward to. Naming a domain or a person is not enough.
* **Assignments need a clear match.** Name the teammate by email address or name in your instructions. If the name matches nobody, or more than one person, the thread is not assigned.
* **Labels must already exist.** The agent applies your existing labels but does not create new ones. [Create the labels](/docs/dashboard/inboxes/labels.md#create-a-label) you want it to use first.

## Writing instructions

Clear, specific instructions get the best results. Tell the agent what kinds of email to expect, and what to do with each. For example:

```text theme={"theme":{"light":"github-light","dark":"vesper"}}
This inbox receives support requests for our online store.

- Label anything about billing or refunds with "Billing".
- Label anything that mentions a legal threat with "Urgent" and assign it to ada@example.com.
- Draft replies to questions about order status, pointing them to https://example.com/orders.
- Forward partnership enquiries to partners@example.com.
- Archive newsletters and automated notifications.
```

## Review the agent's work

The agent's work shows up directly in the inbox. Threads it labels, assigns or moves appear with those changes applied, and you can undo any of them by [organizing the thread](/docs/dashboard/inboxes/threads.md#organize-threads) yourself.

When you open a thread that the agent drafted a reply or forward for, the draft opens in the reply composer with a badge showing it was drafted by the agent. Edit the draft if needed, then click **Send**, or discard it.

## Disable the agent

To stop the agent from acting on new email, remove all of its available actions or clear its instructions. Via the API, send an empty `actions` array.

## API Reference

For complete API documentation, see the [Inbox Agent API reference](/docs/api-reference/inboxes/get-agent.md).
