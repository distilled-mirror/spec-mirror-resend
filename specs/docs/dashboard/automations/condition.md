> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Condition

> Route contacts through different paths based on conditions.

A branch step evaluates a condition against event or contact data and routes the Automation down one of two paths: **condition met** or **condition not met**.

Common use cases:

* **Plan-based emails**: Send different content to free vs. paid users.
* **Engagement splits**: Take different actions based on user activity.
* **Personalization**: Tailor follow-ups based on event payload values.

## How it works

<Tabs>
  <Tab title="Using the dashboard">
    Add a **Condition** step and configure the condition using the editor.

    <img alt="Automation Branch" src="https://mintcdn.com/resend/x30lv_t_NKKbe7WS/images/automations-branch.png?fit=max&auto=format&n=x30lv_t_NKKbe7WS&q=85&s=0079e0e52cf7c13d7645a7467c531696" width="3360" height="2100" data-path="images/automations-branch.png" />
  </Tab>

  <Tab title="Using the API">
    The condition step accepts a `type` and the corresponding rule fields.

    <CodeGroup>
      ```ts Node.js {13-22} theme={"theme":{"light":"github-light","dark":"vesper"}}
      import { Resend } from 'resend';

      const resend = new Resend('re_xxxxxxxxx');

      const { data, error } = await resend.automations.create({
        name: 'Plan-based Welcome',
        steps: [
          {
            key: 'start',
            type: 'trigger',
            config: { eventName: 'user.created' },
          },
          {
            key: 'check_plan',
            type: 'condition',
            config: {
              type: 'rule',
              field: 'event.plan',
              operator: 'eq',
              value: 'pro',
            },
          },
          {
            key: 'send_pro_email',
            type: 'send_email',
            config: { template: { id: 'pro-welcome-template-id' } },
          },
          {
            key: 'send_free_email',
            type: 'send_email',
            config: { template: { id: 'free-welcome-template-id' } },
          },
        ],
        connections: [
          { from: 'start', to: 'check_plan', type: 'default' },
          { from: 'check_plan', to: 'send_pro_email', type: 'condition_met' },
          {
            from: 'check_plan',
            to: 'send_free_email',
            type: 'condition_not_met',
          },
        ],
      });
      ```

      ```php PHP {11-20} theme={"theme":{"light":"github-light","dark":"vesper"}}
      $resend = Resend::client('re_xxxxxxxxx');

      $resend->automations->create([
        'name' => 'Plan-based Welcome',
        'steps' => [
          [
            'key' => 'start',
            'type' => 'trigger',
            'config' => ['event_name' => 'user.created'],
          ],
          [
            'key' => 'check_plan',
            'type' => 'condition',
            'config' => [
              'type' => 'rule',
              'field' => 'event.plan',
              'operator' => 'eq',
              'value' => 'pro',
            ],
          ],
          [
            'key' => 'send_pro_email',
            'type' => 'send_email',
            'config' => ['template' => ['id' => 'pro-welcome-template-id']],
          ],
          [
            'key' => 'send_free_email',
            'type' => 'send_email',
            'config' => ['template' => ['id' => 'free-welcome-template-id']],
          ],
        ],
        'connections' => [
          ['from' => 'start', 'to' => 'check_plan', 'type' => 'default'],
          ['from' => 'check_plan', 'to' => 'send_pro_email', 'type' => 'condition_met'],
          ['from' => 'check_plan', 'to' => 'send_free_email', 'type' => 'condition_not_met'],
        ],
      ]);
      ```

      ```python Python {13-22} theme={"theme":{"light":"github-light","dark":"vesper"}}
      import resend

      resend.api_key = "re_xxxxxxxxx"

      params: resend.Automations.CreateParams = {
        "name": "Plan-based Welcome",
        "steps": [
          {
            "key": "start",
            "type": "trigger",
            "config": {"event_name": "user.created"},
          },
          {
            "key": "check_plan",
            "type": "condition",
            "config": {
              "type": "rule",
              "field": "event.plan",
              "operator": "eq",
              "value": "pro",
            },
          },
          {
            "key": "send_pro_email",
            "type": "send_email",
            "config": {"template": {"id": "pro-welcome-template-id"}},
          },
          {
            "key": "send_free_email",
            "type": "send_email",
            "config": {"template": {"id": "free-welcome-template-id"}},
          },
        ],
        "connections": [
          {"from": "start", "to": "check_plan", "type": "default"},
          {"from": "check_plan", "to": "send_pro_email", "type": "condition_met"},
          {"from": "check_plan", "to": "send_free_email", "type": "condition_not_met"},
        ],
      }

      resend.Automations.create(params)
      ```

      ```ruby Ruby {13-22} theme={"theme":{"light":"github-light","dark":"vesper"}}
      require "resend"

      Resend.api_key = "re_xxxxxxxxx"

      params = {
        name: "Plan-based Welcome",
        steps: [
          {
            key: "start",
            type: "trigger",
            config: { event_name: "user.created" },
          },
          {
            key: "check_plan",
            type: "condition",
            config: {
              type: "rule",
              field: "event.plan",
              operator: "eq",
              value: "pro",
            },
          },
          {
            key: "send_pro_email",
            type: "send_email",
            config: { template: { id: "pro-welcome-template-id" } },
          },
          {
            key: "send_free_email",
            type: "send_email",
            config: { template: { id: "free-welcome-template-id" } },
          },
        ],
        connections: [
          { from: "start", to: "check_plan", type: "default" },
          { from: "check_plan", to: "send_pro_email", type: "condition_met" },
          { from: "check_plan", to: "send_free_email", type: "condition_not_met" },
        ],
      }

      Resend::Automations.create(params)
      ```

      ```go Go {18-27} theme={"theme":{"light":"github-light","dark":"vesper"}}
      package main

      import "github.com/resend/resend-go/v4"

      func main() {
      	client := resend.NewClient("re_xxxxxxxxx")

      	params := &resend.CreateAutomationRequest{
      		Name: "Plan-based Welcome",
      		Steps: []resend.AutomationStep{
      			{
      				Key:  "start",
      				Type: resend.AutomationStepTypeTrigger,
      				Config: map[string]any{
      					"event_name": "user.created",
      				},
      			},
      			{
      				Key:  "check_plan",
      				Type: resend.AutomationStepTypeCondition,
      				Config: map[string]any{
      					"type":     "rule",
      					"field":    "event.plan",
      					"operator": "eq",
      					"value":    "pro",
      				},
      			},
      			{
      				Key:  "send_pro_email",
      				Type: resend.AutomationStepTypeSendEmail,
      				Config: map[string]any{
      					"template": map[string]any{"id": "pro-welcome-template-id"},
      				},
      			},
      			{
      				Key:  "send_free_email",
      				Type: resend.AutomationStepTypeSendEmail,
      				Config: map[string]any{
      					"template": map[string]any{"id": "free-welcome-template-id"},
      				},
      			},
      		},
      		Connections: []resend.AutomationConnection{
      			{From: "start", To: "check_plan", Type: resend.AutomationConnectionTypeDefault},
      			{From: "check_plan", To: "send_pro_email", Type: resend.AutomationConnectionTypeConditionMet},
      			{From: "check_plan", To: "send_free_email", Type: resend.AutomationConnectionTypeConditionNotMet},
      		},
      	}

      	client.Automations.Create(params)
      }
      ```

      ```rust Rust {23-31} theme={"theme":{"light":"github-light","dark":"vesper"}}
      use resend_rs::{
        json,
        types::{
          AutomationStatus, AutomationTemplate, Connection, ConnectionType, CreateAutomationOptions,
          SendEmailStepConfig, Step, TriggerStepConfig,
        },
        Resend, Result,
      };

      #[tokio::main]
      async fn main() -> Result<()> {
        let resend = Resend::new("re_xxxxxxxxx");

        let opts = CreateAutomationOptions {
          name: "Plan-based Welcome".to_owned(),
          steps: vec![
            Step::Trigger {
              key: "start".to_owned(),
              config: TriggerStepConfig {
                event_name: "user.created".to_owned(),
              },
            },
            Step::Condition {
              key: "check_plan".to_owned(),
              config: json!({
                "type": "rule",
                "field": "event.plan",
                "operator": "eq",
                "value": "pro",
              }),
            },
            Step::SendEmail {
              key: "send_pro_email".to_owned(),
              config: SendEmailStepConfig::new(AutomationTemplate::new("pro-welcome-template-id")),
            },
            Step::SendEmail {
              key: "send_free_email".to_owned(),
              config: SendEmailStepConfig::new(AutomationTemplate::new("free-welcome-template-id")),
            },
          ],
          connections: vec![
            Connection::new("start", "check_plan").with_type(ConnectionType::Default),
            Connection::new("check_plan", "send_pro_email").with_type(ConnectionType::ConditionMet),
            Connection::new("check_plan", "send_free_email").with_type(ConnectionType::ConditionNotMet),
          ],
          status: AutomationStatus::Disabled,
        };
        let _automation = resend.automations.create(opts).await?;

        Ok(())
      }
      ```

      ```java Java {22-29} theme={"theme":{"light":"github-light","dark":"vesper"}}
      import com.resend.*;
      import com.resend.core.exception.ResendException;
      import com.resend.services.automations.model.AutomationConnection;
      import com.resend.services.automations.model.AutomationStep;
      import com.resend.services.automations.model.ConditionOperator;
      import com.resend.services.automations.model.ConditionRule;
      import com.resend.services.automations.model.ConnectionType;
      import com.resend.services.automations.model.CreateAutomationOptions;
      import com.resend.services.automations.model.CreateAutomationResponseSuccess;

      public class Main {
          public static void main(String[] args) throws ResendException {
              Resend resend = new Resend("re_xxxxxxxxx");

              CreateAutomationOptions options = CreateAutomationOptions.builder()
                      .name("Plan-based Welcome")
                      .steps(
                          AutomationStep.trigger("start")
                              .eventName("user.created")
                              .build(),
                          AutomationStep.condition("check_plan")
                              .rule(ConditionRule.builder()
                                      .field("event.plan")
                                      .operator(ConditionOperator.EQ)
                                      .value("pro")
                                      .build())
                              .build(),
                          AutomationStep.sendEmail("send_pro_email")
                              .template("pro-welcome-template-id")
                              .build(),
                          AutomationStep.sendEmail("send_free_email")
                              .template("free-welcome-template-id")
                              .build()
                      )
                      .connections(
                          AutomationConnection.builder()
                              .from("start")
                              .to("check_plan")
                              .type(ConnectionType.DEFAULT)
                              .build(),
                          AutomationConnection.builder()
                              .from("check_plan")
                              .to("send_pro_email")
                              .type(ConnectionType.CONDITION_MET)
                              .build(),
                          AutomationConnection.builder()
                              .from("check_plan")
                              .to("send_free_email")
                              .type(ConnectionType.CONDITION_NOT_MET)
                              .build()
                      )
                      .build();

              CreateAutomationResponseSuccess data = resend.automations().create(options);
          }
      }
      ```

      ```csharp .NET {7-13,23} theme={"theme":{"light":"github-light","dark":"vesper"}}
      using Resend;
      using System.Text.Json;

      IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

      var startConfig = JsonSerializer.SerializeToElement( new { event_name = "user.created" } );
      var conditionConfig = JsonSerializer.SerializeToElement( new
      {
          type = "rule",
          field = "event.plan",
          @operator = "eq",
          value = "pro",
      } );
      var proEmailConfig = JsonSerializer.SerializeToElement( new { template = new { id = "pro-welcome-template-id" } } );
      var freeEmailConfig = JsonSerializer.SerializeToElement( new { template = new { id = "free-welcome-template-id" } } );

      var resp = await resend.AutomationCreateAsync( new AutomationCreateData()
      {
          Name = "Plan-based Welcome",
          Steps = new List<AutomationStepData>
          {
              new AutomationStepData { Ref = "start", Type = "trigger", Config = startConfig },
              new AutomationStepData { Ref = "check_plan", Type = "condition", Config = conditionConfig },
              new AutomationStepData { Ref = "send_pro_email", Type = "send_email", Config = proEmailConfig },
              new AutomationStepData { Ref = "send_free_email", Type = "send_email", Config = freeEmailConfig },
          },
          Connections = new List<AutomationEdge>
          {
              new AutomationEdge { From = "start", To = "check_plan", EdgeType = "default" },
              new AutomationEdge { From = "check_plan", To = "send_pro_email", EdgeType = "condition_met" },
              new AutomationEdge { From = "check_plan", To = "send_free_email", EdgeType = "condition_not_met" },
          },
      } );
      ```

      ```bash cURL {10-19} theme={"theme":{"light":"github-light","dark":"vesper"}}
      curl -X POST 'https://api.resend.com/automations' \
           -H 'Authorization: Bearer re_xxxxxxxxx' \
           -H 'Content-Type: application/json' \
           -d '{
        "name": "Plan-based Welcome",
        "steps": [{
          "key": "start",
          "type": "trigger",
          "config": { "event_name": "user.created" }
        }, {
          "key": "check_plan",
          "type": "condition",
          "config": {
            "type": "rule",
            "field": "event.plan",
            "operator": "eq",
            "value": "pro"
          }
        }, {
          "key": "send_pro_email",
          "type": "send_email",
          "config": { "template": { "id": "pro-welcome-template-id" } }
        }, {
          "key": "send_free_email",
          "type": "send_email",
          "config": { "template": { "id": "free-welcome-template-id" } }
        }],
        "connections": [
          { "from": "start", "to": "check_plan", "type": "default" },
          { "from": "check_plan", "to": "send_pro_email", "type": "condition_met" },
          { "from": "check_plan", "to": "send_free_email", "type": "condition_not_met" }
        ]
      }'
      ```

      ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
      resend automations create --name "Plan-based Welcome" --file ./automation.json
      ```
    </CodeGroup>
  </Tab>
</Tabs>

## Connection types

A condition step always produces two outgoing connections.

| Connection type     | Description                                 |
| ------------------- | ------------------------------------------- |
| `condition_met`     | Taken when the condition evaluates to true  |
| `condition_not_met` | Taken when the condition evaluates to false |

```json {4,9} theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "from": "check_plan",
  "to": "send_pro_email",
  "type": "condition_met"
},
{
  "from": "check_plan",
  "to": "send_free_email",
  "type": "condition_not_met"
}
```

## Configuration

<ParamField body="config.type" type="string" required>
  The type of condition node. Possible values:

  * `rule`
  * `and`
  * `or`
</ParamField>

For `rule` type:

<ParamField body="config.field" type="string" required>
  The field to evaluate. Must use the `event.` or `contact.` namespace prefix
  (e.g., `event.amount`, `contact.email`).
</ParamField>

<ParamField body="config.operator" type="string" required>
  The comparison operator. Possible values:

  * `eq`: equals
  * `neq`: not equals
  * `gt`: greater than
  * `gte`: greater than or equal to
  * `lt`: less than
  * `lte`: less than or equal to
  * `contains`: contains a given value
  * `starts_with`: starts with a given value
  * `ends_with`: ends with a given value
  * `exists`: field exists
  * `is_empty`: field is empty
</ParamField>

<ParamField body="config.value" type="string | number | boolean | null">
  The value to compare against. Not required for `exists` and `is_empty`
  operators.
</ParamField>

For `and` / `or` types:

<ParamField body="config.rules" type="object[]" required>
  An array of nested condition config objects. Must contain at least one item.
</ParamField>

Single rule example:

```json theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "check_plan",
  "type": "condition",
  "config": {
    "type": "rule",
    "field": "event.plan",
    "operator": "eq",
    "value": "pro"
  }
}
```

Use `and` or `or` to combine multiple rules into a single branch:

```json {5-19} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "check_plan_and_amount",
  "type": "condition",
  "config": {
    "type": "and",
    "rules": [
      {
        "type": "rule",
        "field": "event.plan",
        "operator": "eq",
        "value": "pro"
      },
      {
        "type": "rule",
        "field": "event.amount",
        "operator": "gte",
        "value": 100
      }
    ]
  }
}
```
