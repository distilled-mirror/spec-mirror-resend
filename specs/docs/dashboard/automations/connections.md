> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Connections

> Connections between steps in Automation workflows.

## How it works

Connections are the code definitions for the links between steps in the Automation graph and are defined and retrieved using the API.

If creating an Automation via the API, define connections as an array of objects.

<CodeGroup>
  ```ts Node.js {10, 15, 22} theme={"theme":{"light":"github-light","dark":"vesper"}}
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

  ```php PHP {8,13,20} theme={"theme":{"light":"github-light","dark":"vesper"}}
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

  ```python Python {10, 15, 22} theme={"theme":{"light":"github-light","dark":"vesper"}}
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

  ```ruby Ruby {10, 15, 22} theme={"theme":{"light":"github-light","dark":"vesper"}}
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

  ```go Go {13, 20, 30} theme={"theme":{"light":"github-light","dark":"vesper"}}
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

  ```rust Rust {18, 24, 30} theme={"theme":{"light":"github-light","dark":"vesper"}}
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

  ```java Java {17,22,26-29} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;
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

          CreateAutomationResponseSuccess data = resend.automations().create(options);
      }
  }
  ```

  ```csharp .NET {15,16,20} theme={"theme":{"light":"github-light","dark":"vesper"}}
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
  ```

  ```bash cURL {8,13,20-22} theme={"theme":{"light":"github-light","dark":"vesper"}}
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
</CodeGroup>

When retrieving Automations, the API returns the connections as an array.

<CodeGroup>
  ```json Response {10,15,22-28} theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "automation",
    "id": "c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd",
    "name": "Welcome series",
    "status": "disabled",
    "created_at": "2026-10-01 12:00:00.000000+00",
    "updated_at": "2026-10-01 12:00:00.000000+00",
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
      {
        "from": "start",
        "to": "welcome",
        "type": "default"
      }
    ]
  }
  ```
</CodeGroup>

## Connection properties

Connections define the links between steps in the automation graph.

<ParamField body="from" type="string" required>
  This is the `key` of the origin step.
</ParamField>

<ParamField body="to" type="string" required>
  This is the `key` of the destination step.
</ParamField>

<ParamField body="type" type="string">
  The type of connection between the origin and destination steps. Most
  automations use the default connection type.

  Use a non-default `type` only when the origin step can branch to multiple
  destinations:

  * For `wait_for_event`, use `event_received` or `timeout`.
  * For `condition`, use `condition_met` or `condition_not_met`.

  Possible values:

  * `default`
  * `condition_met`
  * `condition_not_met`
  * `timeout`
  * `event_received`
</ParamField>

```json Example theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "from": "start",
  "to": "welcome",
  "type": "default"
}
```
