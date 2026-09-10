> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Contact Delete

> Remove a contact from your audience in an Automation.

This step removes the contact that triggered the Automation from its [Audience](/docs/dashboard/audiences/introduction). Once deleted, the contact will no longer receive emails from that audience and any remaining steps in the Automation run are skipped.

Common use cases:

* **Compliance**: Delete contacts as part of a data-removal workflow.
* **Churn**: Remove a contact, when a user stops using your service.
* **Unsubscribe flows**: Automatically remove contacts who opt out.

## How it works

<Tabs>
  <Tab title="Using the dashboard">
    Include the **Delete contact** step to your Automation.

    <img alt="Automation Contact Delete" src="https://mintcdn.com/resend/GClVSBUDv2Z8C3Ae/images/automations-contact-delete.png?fit=max&auto=format&n=GClVSBUDv2Z8C3Ae&q=85&s=57ab7ffaa985a85df04deab53f9dc27a" width="4008" height="2216" data-path="images/automations-contact-delete.png" />

    No configuration required. It is ready as soon as you add it.
  </Tab>

  <Tab title="Using the API">
    Add a `contact_delete` step to your Automation's `steps` array.

    <CodeGroup>
      ```ts Node.js {13-17} theme={"theme":{"light":"github-light","dark":"vesper"}}
      import { Resend } from 'resend';

      const resend = new Resend('re_xxxxxxxxx');

      const { data, error } = await resend.automations.create({
        name: 'Remove churned users',
        steps: [
          {
            key: 'start',
            type: 'trigger',
            config: { eventName: 'user.deleted' },
          },
          {
            key: 'remove',
            type: 'contact_delete',
            config: {},
          },
        ],
        connections: [{ from: 'start', to: 'remove', type: 'default' }],
      });
      ```

      ```php PHP {11-15} theme={"theme":{"light":"github-light","dark":"vesper"}}
      $resend = Resend::client('re_xxxxxxxxx');

      $resend->automations->create([
        'name' => 'Remove churned users',
        'steps' => [
          [
            'key' => 'start',
            'type' => 'trigger',
            'config' => ['event_name' => 'user.deleted'],
          ],
          [
            'key' => 'remove',
            'type' => 'contact_delete',
            'config' => [],
          ],
        ],
        'connections' => [['from' => 'start', 'to' => 'remove', 'type' => 'default']],
      ]);
      ```

      ```python Python {13-17} theme={"theme":{"light":"github-light","dark":"vesper"}}
      import resend

      resend.api_key = "re_xxxxxxxxx"

      params: resend.Automations.CreateParams = {
        "name": "Remove churned users",
        "steps": [
          {
            "key": "start",
            "type": "trigger",
            "config": {"event_name": "user.deleted"},
          },
          {
            "key": "remove",
            "type": "contact_delete",
            "config": {},
          },
        ],
        "connections": [{"from": "start", "to": "remove", "type": "default"}],
      }

      resend.Automations.create(params)
      ```

      ```ruby Ruby {13-17} theme={"theme":{"light":"github-light","dark":"vesper"}}
      require "resend"

      Resend.api_key = "re_xxxxxxxxx"

      params = {
        name: "Remove churned users",
        steps: [
          {
            key: "start",
            type: "trigger",
            config: { event_name: "user.deleted" },
          },
          {
            key: "remove",
            type: "contact_delete",
            config: {},
          },
        ],
        connections: [{ from: "start", to: "remove", type: "default" }],
      }

      Resend::Automations.create(params)
      ```

      ```go Go {18-22} theme={"theme":{"light":"github-light","dark":"vesper"}}
      package main

      import "github.com/resend/resend-go/v3"

      func main() {
      	client := resend.NewClient("re_xxxxxxxxx")

      	params := &resend.CreateAutomationRequest{
      		Name: "Remove churned users",
      		Steps: []resend.AutomationStep{
      			{
      				Key:  "start",
      				Type: resend.AutomationStepTypeTrigger,
      				Config: map[string]any{
      					"event_name": "user.deleted",
      				},
      			},
      			{
      				Key:    "remove",
      				Type:   resend.AutomationStepTypeContactDelete,
      				Config: map[string]any{},
      			},
      		},
      		Connections: []resend.AutomationConnection{
      			{From: "start", To: "remove", Type: resend.AutomationConnectionTypeDefault},
      		},
      	}

      	client.Automations.Create(params)
      }
      ```

      ```rust Rust {22-25} theme={"theme":{"light":"github-light","dark":"vesper"}}
      use resend_rs::{
        json,
        types::{
          AutomationStatus, Connection, ConnectionType, CreateAutomationOptions, Step, TriggerStepConfig,
        },
        Resend, Result,
      };

      #[tokio::main]
      async fn main() -> Result<()> {
        let resend = Resend::new("re_xxxxxxxxx");

        let opts = CreateAutomationOptions {
          name: "Remove churned users".to_owned(),
          steps: vec![
            Step::Trigger {
              key: "start".to_owned(),
              config: TriggerStepConfig {
                event_name: "user.deleted".to_owned(),
              },
            },
            Step::ContactDelete {
              key: "remove".to_owned(),
              config: json!("{}"),
            },
          ],
          connections: vec![Connection::new("start", "remove").with_type(ConnectionType::Default)],
          status: AutomationStatus::Disabled,
        };
        let _automation = resend.automations.create(opts).await?;

        Ok(())
      }
      ```

      ```java Java {14-17} theme={"theme":{"light":"github-light","dark":"vesper"}}
      import com.resend.*;

      public class Main {
          public static void main(String[] args) {
              Resend resend = new Resend("re_xxxxxxxxx");

              CreateAutomationOptions options = CreateAutomationOptions.builder()
                      .name("Remove churned users")
                      .steps(
                          AutomationStep.trigger("start")
                              .eventName("user.deleted")
                              .build(),
                          AutomationStep.contactDelete("remove")
                              .build()
                      )
                      .connections(
                          AutomationConnection.builder()
                              .from("start")
                              .to("remove")
                              .type(ConnectionType.DEFAULT)
                              .build()
                      )
                      .build();

              CreateAutomationResponseSuccess data = resend.automations().create(options);
          }
      }
      ```

      ```csharp .NET {7,15} theme={"theme":{"light":"github-light","dark":"vesper"}}
      using Resend;
      using System.Text.Json;

      IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

      var startConfig = JsonSerializer.SerializeToElement( new { event_name = "user.deleted" } );
      var removeConfig = JsonSerializer.SerializeToElement( new { } );

      var resp = await resend.AutomationCreateAsync( new AutomationCreateData()
      {
          Name = "Remove churned users",
          Steps = new List<AutomationStepData>
          {
              new AutomationStepData { Ref = "start", Type = "trigger", Config = startConfig },
              new AutomationStepData { Ref = "remove", Type = "contact_delete", Config = removeConfig },
          },
          Connections = new List<AutomationEdge>
          {
              new AutomationEdge { From = "start", To = "remove", EdgeType = "default" },
          },
      } );
      ```

      ```bash cURL {10-14} theme={"theme":{"light":"github-light","dark":"vesper"}}
      curl -X POST 'https://api.resend.com/automations' \
           -H 'Authorization: Bearer re_xxxxxxxxx' \
           -H 'Content-Type: application/json' \
           -d '{
        "name": "Remove churned users",
        "steps": [{
          "key": "start",
          "type": "trigger",
          "config": { "event_name": "user.deleted" }
        }, {
          "key": "remove",
          "type": "contact_delete",
          "config": {}
        }],
        "connections": [
          { "from": "start", "to": "remove", "type": "default" }
        ]
      }'
      ```

      ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
      resend automations create --name "Remove churned users" --file ./automation.json
      ```
    </CodeGroup>

    The `config` object is empty, so no additional fields are required.
  </Tab>
</Tabs>

<Warning>
  Deleting a contact is **permanent**. The contact and all of its properties are
  removed from the audience. If the contact needs to be re-added later, it must
  be created again.
</Warning>

## Configuration

```json Example theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "remove_contact",
  "type": "contact_delete",
  "config": {}
}
```
