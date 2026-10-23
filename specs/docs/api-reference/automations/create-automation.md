> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Automation

> Create a new automation to automate email sequences.

## Body Parameters

**name** `string` *required*

The name of the automation.

**status** `string`

The status of the automation. Possible values are `enabled` or `disabled`.
Defaults to `disabled`.

**steps** `Step[]`

The steps that compose the automation graph. Must be provided together with
`connections`. See [Step
Properties](/docs/dashboard/automations/steps.md#step-properties) for full object
definition.

**connections** `Connection[]`

The connections between steps in the automation graph. Must be provided
together with `steps`. See [Connection
Properties](/docs/dashboard/automations/connections.md#connection-properties) for full
object definition.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.automations.create({
  name: 'Welcome series',
  status: 'disabled',
  steps: [
    {
      key: 'start',
      type: 'trigger',
      config: { eventName: 'user.created' },
    },
    {
      key: 'welcome',
      type: 'send_email',
      config: {
        template: { id: '34a080c9-b17d-4187-ad80-5af20266e535' },
      },
    },
  ],
  connections: [{ from: 'start', to: 'welcome' }],
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->automations->create([
  'name' => 'Welcome series',
  'status' => 'disabled',
  'steps' => [
    [
      'key' => 'start',
      'type' => 'trigger',
      'config' => ['event_name' => 'user.created'],
    ],
    [
      'key' => 'welcome',
      'type' => 'send_email',
      'config' => [
        'template' => ['id' => '34a080c9-b17d-4187-ad80-5af20266e535'],
      ],
    ],
  ],
  'connections' => [['from' => 'start', 'to' => 'welcome']],
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Automations.CreateParams = {
  "name": "Welcome series",
  "status": "disabled",
  "steps": [
    {
      "key": "start",
      "type": "trigger",
      "config": {"event_name": "user.created"},
    },
    {
      "key": "welcome",
      "type": "send_email",
      "config": {
        "template": {"id": "34a080c9-b17d-4187-ad80-5af20266e535"},
      },
    },
  ],
  "connections": [{"from": "start", "to": "welcome"}],
}

resend.Automations.create(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  name: "Welcome series",
  status: "disabled",
  steps: [
    {
      key: "start",
      type: "trigger",
      config: { event_name: "user.created" },
    },
    {
      key: "welcome",
      type: "send_email",
      config: {
        template: { id: "34a080c9-b17d-4187-ad80-5af20266e535" },
      },
    },
  ],
  connections: [{ from: "start", to: "welcome" }],
}

Resend::Automations.create(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.CreateAutomationRequest{
		Name:   "Welcome series",
		Status: resend.AutomationStatusDisabled,
		Steps: []resend.AutomationStep{
			{
				Key:  "start",
				Type: resend.AutomationStepTypeTrigger,
				Config: map[string]any{
					"event_name": "user.created",
				},
			},
			{
				Key:  "welcome",
				Type: resend.AutomationStepTypeSendEmail,
				Config: map[string]any{
					"template": map[string]any{
						"id": "34a080c9-b17d-4187-ad80-5af20266e535",
					},
				},
			},
		},
		Connections: []resend.AutomationConnection{
			{From: "start", To: "welcome"},
		},
	}

	client.Automations.Create(params)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{
  types::{
    AutomationStatus, AutomationTemplate, Connection, CreateAutomationOptions, SendEmailStepConfig,
    Step, TriggerStepConfig,
  },
  Resend, Result,
};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let opts = CreateAutomationOptions {
    name: "Welcome series".to_owned(),
    status: AutomationStatus::Disabled,
    steps: vec![
      Step::Trigger {
        key: "start".to_owned(),
        config: TriggerStepConfig {
          event_name: "user.created".to_owned(),
        },
      },
      Step::SendEmail {
        key: "welcome".to_owned(),
        config: SendEmailStepConfig::new(AutomationTemplate::new(
          "34a080c9-b17d-4187-ad80-5af20266e535",
        )),
      },
    ],
    connections: vec![Connection::new("start", "welcome")],
  };
  let _automation = resend.automations.create(opts).await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.automations.model.AutomationConnection;
import com.resend.services.automations.model.AutomationStatus;
import com.resend.services.automations.model.AutomationStep;
import com.resend.services.automations.model.CreateAutomationOptions;
import com.resend.services.automations.model.CreateAutomationResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        CreateAutomationOptions options = CreateAutomationOptions.builder()
                .name("Welcome series")
                .status(AutomationStatus.DISABLED)
                .steps(
                    AutomationStep.trigger("start")
                        .eventName("user.created")
                        .build(),
                    AutomationStep.sendEmail("welcome")
                        .template("34a080c9-b17d-4187-ad80-5af20266e535")
                        .build()
                )
                .connections(
                    AutomationConnection.builder()
                        .from("start")
                        .to("welcome")
                        .build()
                )
                .build();

        CreateAutomationResponseSuccess response = resend.automations().create(options);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;
using System.Text.Json;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

var startConfig = JsonSerializer.SerializeToElement( new { event_name = "user.created" } );
var welcomeConfig = JsonSerializer.SerializeToElement( new { template = new { id = "34a080c9-b17d-4187-ad80-5af20266e535" } } );

var resp = await resend.AutomationCreateAsync( new AutomationCreateData()
{
    Name = "Welcome series",
    Status = "disabled",
    Steps = new List<AutomationStepData>
    {
        new AutomationStepData { Ref = "start", Type = "trigger", Config = startConfig },
        new AutomationStepData { Ref = "welcome", Type = "send_email", Config = welcomeConfig },
    },
    Connections = new List<AutomationEdge>
    {
        new AutomationEdge { From = "start", To = "welcome" },
    },
} );
Console.WriteLine( "AutomationId={0}", resp.Content );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/automations' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d '{
  "name": "Welcome series",
  "steps": [
    {
      "key": "start",
      "type": "trigger",
      "config": { "event_name": "user.created" }
    },
    {
      "key": "welcome",
      "type": "send_email",
      "config": {
        "template": { "id": "34a080c9-b17d-4187-ad80-5af20266e535" }
      }
    }
  ],
  "connections": [
    { "from": "start", "to": "welcome" }
  ]
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend automations create --name "Welcome series" --file ./automation.json
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "automation",
  "id": "c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd"
}
```
