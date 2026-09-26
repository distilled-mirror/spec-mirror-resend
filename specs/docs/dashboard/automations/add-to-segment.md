> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Add to Segment

> Include contacts to a segment as part of your Automation.

This step adds the current contact to a specified [Segment](/docs/dashboard/segments/introduction) when reached in the Automation flow.

Common use cases:

* **Cohorts**: Add contacts to a cohort segment after a specific event.
* **Lifecycle**: Segment contacts as they progress through onboarding.
* **Engagement**: Group contacts who completed a specific action.

## How it works

<Tabs>
  <Tab title="Using the dashboard">
    Define a **Add to segment** step and select the segment from the dropdown.

    <img alt="Automation Add to Segment" src="https://mintcdn.com/resend/C4ZmHxGOgdpKqZkf/images/automations-add-to-segment.png?fit=max&auto=format&n=C4ZmHxGOgdpKqZkf&q=85&s=4f48bf99d7854095810c5510a8605c99" width="4009" height="2216" data-path="images/automations-add-to-segment.png" />
  </Tab>

  <Tab title="Using the API">
    The `add_to_segment` step accepts a single `segment_id` field.

    <CodeGroup>
      ```ts Node.js {13-19} theme={"theme":{"light":"github-light","dark":"vesper"}}
      import { Resend } from 'resend';

      const resend = new Resend('re_xxxxxxxxx');

      const { data, error } = await resend.automations.create({
        name: 'Tag VIP Users',
        steps: [
          {
            key: 'start',
            type: 'trigger',
            config: { eventName: 'purchase.completed' },
          },
          {
            key: 'vip_users',
            type: 'add_to_segment',
            config: {
              segmentId: '83a1e324-26dc-47eb-9b28-ba8b6d1fe808',
            },
          },
        ],
        connections: [{ from: 'start', to: 'vip_users', type: 'default' }],
      });
      ```

      ```php PHP {11-17} theme={"theme":{"light":"github-light","dark":"vesper"}}
      $resend = Resend::client('re_xxxxxxxxx');

      $resend->automations->create([
        'name' => 'Tag VIP Users',
        'steps' => [
          [
            'key' => 'start',
            'type' => 'trigger',
            'config' => ['event_name' => 'purchase.completed'],
          ],
          [
            'key' => 'vip_users',
            'type' => 'add_to_segment',
            'config' => [
              'segment_id' => '83a1e324-26dc-47eb-9b28-ba8b6d1fe808',
            ],
          ],
        ],
        'connections' => [['from' => 'start', 'to' => 'vip_users', 'type' => 'default']],
      ]);
      ```

      ```python Python {13-19} theme={"theme":{"light":"github-light","dark":"vesper"}}
      import resend

      resend.api_key = "re_xxxxxxxxx"

      params: resend.Automations.CreateParams = {
        "name": "Tag VIP Users",
        "steps": [
          {
            "key": "start",
            "type": "trigger",
            "config": {"event_name": "purchase.completed"},
          },
          {
            "key": "vip_users",
            "type": "add_to_segment",
            "config": {
              "segment_id": "83a1e324-26dc-47eb-9b28-ba8b6d1fe808",
            },
          },
        ],
        "connections": [{"from": "start", "to": "vip_users", "type": "default"}],
      }

      resend.Automations.create(params)
      ```

      ```ruby Ruby {13-19} theme={"theme":{"light":"github-light","dark":"vesper"}}
      require "resend"

      Resend.api_key = "re_xxxxxxxxx"

      params = {
        name: "Tag VIP Users",
        steps: [
          {
            key: "start",
            type: "trigger",
            config: { event_name: "purchase.completed" },
          },
          {
            key: "vip_users",
            type: "add_to_segment",
            config: {
              segment_id: "83a1e324-26dc-47eb-9b28-ba8b6d1fe808",
            },
          },
        ],
        connections: [{ from: "start", to: "vip_users", type: "default" }],
      }

      Resend::Automations.create(params)
      ```

      ```go Go {18-24} theme={"theme":{"light":"github-light","dark":"vesper"}}
      package main

      import "github.com/resend/resend-go/v4"

      func main() {
      	client := resend.NewClient("re_xxxxxxxxx")

      	params := &resend.CreateAutomationRequest{
      		Name: "Tag VIP Users",
      		Steps: []resend.AutomationStep{
      			{
      				Key:  "start",
      				Type: resend.AutomationStepTypeTrigger,
      				Config: map[string]any{
      					"event_name": "purchase.completed",
      				},
      			},
      			{
      				Key:  "vip_users",
      				Type: resend.AutomationStepTypeAddToSegment,
      				Config: map[string]any{
      					"segment_id": "83a1e324-26dc-47eb-9b28-ba8b6d1fe808",
      				},
      			},
      		},
      		Connections: []resend.AutomationConnection{
      			{From: "start", To: "vip_users", Type: resend.AutomationConnectionTypeDefault},
      		},
      	}

      	client.Automations.Create(params)
      }
      ```

      ```rust Rust {22-27} theme={"theme":{"light":"github-light","dark":"vesper"}}
      use resend_rs::{
        types::{
          AddToSegmentStepConfig, AutomationStatus, Connection, ConnectionType, CreateAutomationOptions,
          Step, TriggerStepConfig,
        },
        Resend, Result,
      };

      #[tokio::main]
      async fn main() -> Result<()> {
        let resend = Resend::new("re_xxxxxxxxx");

        let opts = CreateAutomationOptions {
          name: "Tag VIP Users".to_owned(),
          steps: vec![
            Step::Trigger {
              key: "start".to_owned(),
              config: TriggerStepConfig {
                event_name: "purchase.completed".to_owned(),
              },
            },
            Step::AddToSegment {
              key: "vip_users".to_owned(),
              config: AddToSegmentStepConfig {
                segment_id: "83a1e324-26dc-47eb-9b28-ba8b6d1fe808".to_owned(),
              },
            },
          ],
          connections: vec![Connection::new("start", "vip_users").with_type(ConnectionType::Default)],
          status: AutomationStatus::Disabled,
        };
        let _automation = resend.automations.create(opts).await?;

        Ok(())
      }
      ```

      ```java Java {20-24} theme={"theme":{"light":"github-light","dark":"vesper"}}
      import com.resend.*;
      import com.resend.core.exception.ResendException;
      import com.resend.services.automations.model.AutomationConnection;
      import com.resend.services.automations.model.AutomationStep;
      import com.resend.services.automations.model.ConnectionType;
      import com.resend.services.automations.model.CreateAutomationOptions;
      import com.resend.services.automations.model.CreateAutomationResponseSuccess;

      public class Main {
          public static void main(String[] args) throws ResendException {
              Resend resend = new Resend("re_xxxxxxxxx");

              CreateAutomationOptions options = CreateAutomationOptions.builder()
                      .name("Tag VIP Users")
                      .steps(
                          AutomationStep.trigger("start")
                              .eventName("purchase.completed")
                              .build(),
                          AutomationStep.addToSegment("vip_users")
                              .segmentId("83a1e324-26dc-47eb-9b28-ba8b6d1fe808")
                              .build()
                      )
                      .connections(
                          AutomationConnection.builder()
                              .from("start")
                              .to("vip_users")
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

      var startConfig = JsonSerializer.SerializeToElement( new { event_name = "purchase.completed" } );
      var segmentConfig = JsonSerializer.SerializeToElement( new { segment_id = "83a1e324-26dc-47eb-9b28-ba8b6d1fe808" } );

      var resp = await resend.AutomationCreateAsync( new AutomationCreateData()
      {
          Name = "Tag VIP Users",
          Steps = new List<AutomationStepData>
          {
              new AutomationStepData { Ref = "start", Type = "trigger", Config = startConfig },
              new AutomationStepData { Ref = "vip_users", Type = "add_to_segment", Config = segmentConfig },
          },
          Connections = new List<AutomationEdge>
          {
              new AutomationEdge { From = "start", To = "vip_users", EdgeType = "default" },
          },
      } );
      ```

      ```bash cURL {10-14} theme={"theme":{"light":"github-light","dark":"vesper"}}
      curl -X POST 'https://api.resend.com/automations' \
           -H 'Authorization: Bearer re_xxxxxxxxx' \
           -H 'Content-Type: application/json' \
           -d '{
        "name": "Tag VIP Users",
        "steps": [{
          "key": "start",
          "type": "trigger",
          "config": { "event_name": "purchase.completed" }
        }, {
          "key": "vip_users",
          "type": "add_to_segment",
          "config": { "segment_id": "83a1e324-26dc-47eb-9b28-ba8b6d1fe808" }
        }],
        "connections": [
          { "from": "start", "to": "vip_users", "type": "default" }
        ]
      }'
      ```

      ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
      resend automations create --name "Tag VIP Users" --file ./automation.json
      ```
    </CodeGroup>
  </Tab>
</Tabs>

## Configuration

<ParamField body="config.segment_id" type="string" required>
  The ID of the segment to add the contact to.
</ParamField>

```json Example theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "add_to_vip",
  "type": "add_to_segment",
  "config": {
    "segment_id": "83a1e324-26dc-47eb-9b28-ba8b6d1fe808"
  }
}
```
