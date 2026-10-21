> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Agent Settings

> Update the agent settings for an inbox.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

## Body Parameters

Send at least one of `instructions`, `tone`, or `actions`. Omitted fields keep
their current value.

**instructions** `string | null`

Instructions the agent follows when handling the inbox's threads. 1 to 4000
characters. Whitespace at the start and end does not count. Send `null` to
clear them.

**tone** `'concise_professional' | 'concise_casual' | 'expanded_professional' | 'expanded_casual' | null`

Tone the agent writes in. Send `null` to clear it.

* `concise_professional`: Brief responses in a professional tone.
* `concise_casual`: Brief responses in a casual tone.
* `expanded_professional`: Detailed responses in a professional tone.
* `expanded_casual`: Detailed responses in a casual tone.

**actions** `string[]`

Actions the agent is allowed to take. The list replaces the current actions.
Send an empty array to disable all actions.

* `draft_reply`: Draft a reply.
* `forward_thread`: Forward a thread.
* `add_labels`: Add labels to a thread.
* `assign_thread`: Assign a thread.
* `mark_as_spam`: Mark a thread as spam.
* `archive`: Archive a thread.
* `move_to_trash`: Move a thread to the trash.

## Response Fields

**object** `string`

Always `inbox_agent`.

**id** `string`

The ID of the agent.

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
  inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  instructions: "Answer refund questions yourself. Escalate legal threats.",
  tone: "concise_professional",
  actions: ["draft_reply", "add_labels"]
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
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{
  types::{InboxAgentAction, InboxAgentTone, UpdateInboxAgentOptions},
  Resend, Result,
};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let opts = UpdateInboxAgentOptions::new()
    .with_instructions("Answer refund questions yourself. Escalate legal threats.")
    .with_tone(InboxAgentTone::ConciseProfessional)
    .with_actions([InboxAgentAction::DraftReply, InboxAgentAction::AddLabels]);

  let _agent = resend
    .inboxes
    .update_agent("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", opts)
    .await?;

  Ok(())
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxAgentUpdateAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new InboxAgentUpdateData()
    {
        Instructions = "Answer refund questions yourself. Escalate legal threats.",
        Tone = InboxAgentTone.ConciseProfessional,
        Actions = [ InboxAgentAction.DraftReply, InboxAgentAction.AddLabels ],
    }
);
Console.WriteLine( "Agent Id={0}", resp.Content );
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
resend inboxes agent update b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --instructions "Answer refund questions yourself. Escalate legal threats." \
  --tone concise_professional \
  --actions draft_reply,add_labels
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "inbox_agent",
  "id": "a1f84a4e-6f2b-4f0a-9c1d-8a2e5b3c7d90"
}
```
