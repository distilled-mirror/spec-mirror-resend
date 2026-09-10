> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Using Automations

> Automate emails with custom events.

Automations allow you to **create email steps** based on custom events from your application.

You can use Automations for use cases like:

* Welcome emails
* Drip campaigns
* Payment recovery
* Abandoned cart
* Trial expiration

Automations support `{{{RESEND_UNSUBSCRIBE_URL}}}` for compliance with non-transactional product and marketing messaging. See [Unsubscribe behavior](/docs/dashboard/automations/send-email#unsubscribe-behavior) for how to add it to a Send Email step, or read more about [when to use an unsubscribe link](/docs/knowledge-base/should-i-add-an-unsubscribe-link).

## How it works

To start executing an Automation, you need to:

<Steps>
  <Step title="Create Automation">
    Outline the sequence of steps to be executed.
  </Step>

  <Step title="Add Trigger">
    Define the event name that will trigger the Automation.
  </Step>

  <Step title="Define Steps">Configure the steps to be executed.</Step>

  <Step title="Send an Event">
    Trigger the Automation by sending an event from your application.
  </Step>

  <Step title="Monitor Runs">
    Track and debug your Automation executions using runs.
  </Step>
</Steps>

## Create an Automation

<Tabs>
  <Tab title="Using the dashboard">
    <Steps>
      <Step title="Create Automation">
        The [Automations page](https://resend.com/automations) shows all existing automations. You can search by name and filter by status (**All Statuses**, **Enabled**, or **Disabled**) to quickly find the automation you need.

        Click **Create automation** to start a new Automation.

        <img alt="Create Automation" src="https://mintcdn.com/resend/ePnINhGLisYSJsWT/images/automations-create.png?fit=max&auto=format&n=ePnINhGLisYSJsWT&q=85&s=14adc9d8a15b8c52b9b7acc361b966f2" width="4007" height="2216" data-path="images/automations-create.png" />
      </Step>

      <Step title="Add Trigger">
        A trigger is the first step that will run when the Automation is executed. You can use a [custom event](/docs/dashboard/automations/custom-events) like `user.created` or `onboarding.completed`, defining it inline or in the [Events page](https://resend.com/automations/events).

        <img alt="Add Trigger to Automation" src="https://mintcdn.com/resend/ePnINhGLisYSJsWT/images/automations-trigger.png?fit=max&auto=format&n=ePnINhGLisYSJsWT&q=85&s=1249bd18fbe832abb5b3ea0ecfe2b7ed" width="4008" height="2214" data-path="images/automations-trigger.png" />

        In this example, we will receive an event called `user.created` as a trigger.

        <img alt="Add Custom Event" src="https://mintcdn.com/resend/ePnINhGLisYSJsWT/images/automations-custom-event.png?fit=max&auto=format&n=ePnINhGLisYSJsWT&q=85&s=4e5b189cb756d8ca5a468746dac901a0" width="4008" height="2216" data-path="images/automations-custom-event.png" />

        See the [Trigger documentation](/docs/dashboard/automations/trigger) for more details.
      </Step>

      <Step title="Define Steps">
        Now, we need to define the [steps](/docs/dashboard/automations/steps) that will be executed.

        There are several step types you can add to your Automation:

        | Step type                                               | Description                                         |
        | ------------------------------------------------------- | --------------------------------------------------- |
        | [Condition](/docs/dashboard/automations/condition)           | Branches the workflow based on rules                |
        | [Delay](/docs/dashboard/automations/delay)                   | Pauses execution for a specified duration           |
        | [Wait for Event](/docs/dashboard/automations/wait-for-event) | Pauses execution until a specific event is received |
        | [Send Email](/docs/dashboard/automations/send-email)         | Sends an email using a template                     |
        | [Contact Update](/docs/dashboard/automations/contact-update) | Updates a contact's fields                          |
        | [Contact Delete](/docs/dashboard/automations/contact-delete) | Deletes the contact                                 |
        | [Add to Segment](/docs/dashboard/automations/add-to-segment) | Adds the contact to a segment                       |

        On this example, we will use the **Send Email** step.

        <img alt="Define Steps" src="https://mintcdn.com/resend/ePnINhGLisYSJsWT/images/automations-steps.png?fit=max&auto=format&n=ePnINhGLisYSJsWT&q=85&s=270948146f144b3a6108cd99c81d7a70" width="4008" height="2217" data-path="images/automations-steps.png" />

        Once you select that step, you will be able to select an existing template.

        <img alt="Add Send Email Step" src="https://mintcdn.com/resend/ePnINhGLisYSJsWT/images/automations-steps-email.png?fit=max&auto=format&n=ePnINhGLisYSJsWT&q=85&s=98e94d53506699d565747e510702ad53" width="4008" height="2216" data-path="images/automations-steps-email.png" />

        If you select a draft template, you can publish it directly from the Send Email node without leaving the workflow editor. Click the **Publish** button that appears when a draft template is selected.

        With the template selected, you will be able to configure the email subject and sender address.

        <img alt="Send Email Step Settings" src="https://mintcdn.com/resend/3_DkZ6MFMzztlC_E/images/automations-steps-email-settings.png?fit=max&auto=format&n=3_DkZ6MFMzztlC_E&q=85&s=312f80d13ca502ae8de7e7bffd31e251" width="4007" height="2216" data-path="images/automations-steps-email-settings.png" />

        Once you're done with the email, you can click on **Start** to enable the Automation.

        <img alt="Automation Enabled" src="https://mintcdn.com/resend/ePnINhGLisYSJsWT/images/automations-enabled.png?fit=max&auto=format&n=ePnINhGLisYSJsWT&q=85&s=09a441d2dce12d317b177fb9ede7dea0" width="4008" height="2216" data-path="images/automations-enabled.png" />

        <Note>
          While an Automation is enabled, its steps cannot be edited. To make changes,
          [duplicate the Automation](/docs/api-reference/automations/duplicate-automation),
          edit the copy, and switch over by stopping new runs on the original. In-flight
          runs will finish on the version they started with.
        </Note>
      </Step>

      <Step title="Send an Event">
        Now, we're ready to send an event to trigger the Automation.

        On your application, you can send an event to trigger the Automation by using the API.

        <CodeGroup>
          ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
          import { Resend } from 'resend';

          const resend = new Resend('re_xxxxxxxxx');

          // Trigger with a contact ID
          const { data, error } = await resend.events.send({
            event: 'user.created',
            contactId: '7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b',
            payload: {
              plan: 'pro',
            },
          });

          // Trigger with an email address
          const { data, error } = await resend.events.send({
            event: 'user.created',
            email: 'steve.wozniak@gmail.com',
            payload: {
              plan: 'pro',
            },
          });
          ```

          ```php PHP {6,13} theme={"theme":{"light":"github-light","dark":"vesper"}}
          $resend = Resend::client('re_xxxxxxxxx');

          // Trigger with a contact ID
          $resend->events->send([
            'event' => 'user.created',
            'contact_id' => '7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b',
            'payload' => ['plan' => 'pro'],
          ]);

          // Trigger with an email address
          $resend->events->send([
            'event' => 'user.created',
            'email' => 'steve.wozniak@gmail.com',
            'payload' => ['plan' => 'pro'],
          ]);
          ```

          ```python Python {8,19} theme={"theme":{"light":"github-light","dark":"vesper"}}
          import resend

          resend.api_key = "re_xxxxxxxxx"

          # Trigger with a contact ID
          params: resend.Events.SendParams = {
            "event": "user.created",
            "contact_id": "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b",
            "payload": {
              "plan": "pro",
            },
          }

          resend.Events.send(params)

          # Trigger with an email address
          params: resend.Events.SendParams = {
            "event": "user.created",
            "email": "steve.wozniak@gmail.com",
            "payload": {
              "plan": "pro",
            },
          }

          resend.Events.send(params)
          ```

          ```ruby Ruby {8,17} theme={"theme":{"light":"github-light","dark":"vesper"}}
          require "resend"

          Resend.api_key = "re_xxxxxxxxx"

          # Trigger with a contact ID
          params = {
            event: "user.created",
            contact_id: "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b",
            payload: {
              plan: "pro",
            },
          }

          Resend::Events.send(params)

          # Trigger with an email address
          params = {
            event: "user.created",
            email: "steve.wozniak@gmail.com",
            payload: {
              plan: "pro",
            },
          }

          Resend::Events.send(params)
          ```

          ```go Go {11,20} theme={"theme":{"light":"github-light","dark":"vesper"}}
          package main

          import "github.com/resend/resend-go/v3"

          func main() {
          	client := resend.NewClient("re_xxxxxxxxx")

          	// Trigger with a contact ID
          	client.Events.Send(&resend.SendEventRequest{
          		Event:     "user.created",
          		ContactId: "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b",
          		Payload: map[string]any{
          			"plan": "pro",
          		},
          	})

          	// Trigger with an email address
          	client.Events.Send(&resend.SendEventRequest{
          		Event: "user.created",
          		Email: "steve.wozniak@gmail.com",
          		Payload: map[string]any{
          			"plan": "pro",
          		},
          	})
          }
          ```

          ```rust Rust {10,19} theme={"theme":{"light":"github-light","dark":"vesper"}}
          use resend_rs::{types::SendEventOptions, Resend, Result};

          #[tokio::main]
          async fn main() -> Result<()> {
            let resend = Resend::new("re_xxxxxxxxx");

            // Trigger with a contact ID
            let _event = resend
              .events
              .send(SendEventOptions::new("user.created").contact_id(
                "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b",
              ).payload(serde_json::json!({
                "plan": "pro"
              })))
              .await?;

            // Trigger with an email address
            let _event = resend
              .events
              .send(SendEventOptions::new("user.created").email(
                "steve.wozniak@gmail.com",
              ).payload(serde_json::json!({
                "plan": "pro"
              })))
              .await?;

            Ok(())
          }
          ```

          ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
          import com.resend.*;

          public class Main {
              public static void main(String[] args) {
                  Resend resend = new Resend("re_xxxxxxxxx");

                  // Trigger with a contact ID
                  SendEventOptions params = SendEventOptions.builder()
                          .event("user.created")
                          .contactId("7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b")
                          .addPayload("plan", "pro")
                          .build();

                  SendEventResponseSuccess data = resend.events().send(params);

                  // Trigger with an email address
                  SendEventOptions params2 = SendEventOptions.builder()
                          .event("user.created")
                          .email("steve.wozniak@gmail.com")
                          .addPayload("plan", "pro")
                          .build();

                  SendEventResponseSuccess data2 = resend.events().send(params2);
              }
          }
          ```

          ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
          using Resend;
          using System.Text.Json;

          IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

          var payload = JsonSerializer.SerializeToElement( new { plan = "pro" } );

          // Trigger with a contact ID
          var resp = await resend.EventSendAsync( new EventSendData()
          {
              Event = "user.created",
              ContactId = new Guid( "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b" ),
              Payload = payload,
          } );
          Console.WriteLine( "Event={0}", resp.Content.Event );

          // Trigger with an email address
          await resend.EventSendAsync( new EventSendData()
          {
              Event = "user.created",
              Email = "steve.wozniak@gmail.com",
              Payload = payload,
          } );
          ```

          ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
          # Trigger with a contact ID
          curl -X POST 'https://api.resend.com/events/send' \
               -H 'Authorization: Bearer re_xxxxxxxxx' \
               -H 'Content-Type: application/json' \
               -d '{
            "event": "user.created",
            "contact_id": "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b",
            "payload": {
              "plan": "pro"
            }
          }'

          # Trigger with an email address
          curl -X POST 'https://api.resend.com/events/send' \
               -H 'Authorization: Bearer re_xxxxxxxxx' \
               -H 'Content-Type: application/json' \
               -d '{
            "event": "user.created",
            "email": "steve.wozniak@gmail.com",
            "payload": {
              "plan": "pro"
            }
          }'
          ```

          ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
          # Trigger with a contact ID
          resend events send \
            --event user.created \
            --contact-id 7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b \
            --payload '{"plan":"pro"}'

          # Trigger with an email address
          resend events send \
            --event user.created \
            --email steve.wozniak@gmail.com \
            --payload '{"plan":"pro"}'
          ```
        </CodeGroup>

        View the [API reference](/docs/api-reference/events/send-event) for more details.
      </Step>

      <Step title="Monitor Runs">
        After sending events, you can monitor your Automation executions through Runs. Each time an event triggers an Automation, a Run is created to track the execution.

        <img alt="Monitor Runs" src="https://mintcdn.com/resend/ePnINhGLisYSJsWT/images/automations-runs.png?fit=max&auto=format&n=ePnINhGLisYSJsWT&q=85&s=b15322c27ffd309ee310250f6fc6dedd" width="3411" height="1881" data-path="images/automations-runs.png" />

        Learn how to:

        * View Run statuses and execution details
        * Filter Runs by status (`running`, `completed`, `failed`, `cancelled`)
        * Debug failed Runs with step-level error information
        * Stop Automation Runs when needed

        See the [Runs documentation](/docs/dashboard/automations/runs) for more details.
      </Step>
    </Steps>
  </Tab>

  <Tab title="Using the API">
    <Steps>
      <Step title="Create Automation">
        When creating an Automation via the API, you can create an entire Automation flow with a single request. It accepts four parameters (status is optional and defaults to `disabled`):

        * `name`: The name of the Automation.
        * `status`: The status of the Automation.
        * `steps`: The [steps](/docs/dashboard/automations/steps) that compose the Automation graph.
        * `connections`: The [connections between steps](/docs/dashboard/automations/connections) in the Automation graph.

        <CodeGroup>
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

          import "github.com/resend/resend-go/v3"

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
          import com.resend.*;

          public class Main {
              public static void main(String[] args) {
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
        </CodeGroup>

        The trigger is defined as the first item in the `steps` array with `type: 'trigger'`. It requires you've created a custom event like `user.created` or `onboarding.completed`.

        For more help creating an Automation via the API, see the [Create Automation API reference](/docs/api-reference/automations/create-automation).
      </Step>

      <Step title="Send an Event">
        Trigger the Automation by sending an event from your application.

        <CodeGroup>
          ```ts Node.js {8,17} theme={"theme":{"light":"github-light","dark":"vesper"}}
          import { Resend } from 'resend';

          const resend = new Resend('re_xxxxxxxxx');

          // Trigger with a contact ID
          const { data, error } = await resend.events.send({
            event: 'user.created',
            contactId: '7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b',
            payload: {
              plan: 'pro',
            },
          });

          // Trigger with an email address
          const { data, error } = await resend.events.send({
            event: 'user.created',
            email: 'steve.wozniak@gmail.com',
            payload: {
              plan: 'pro',
            },
          });
          ```

          ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
          $resend = Resend::client('re_xxxxxxxxx');

          // Trigger with a contact ID
          $resend->events->send([
            'event' => 'user.created',
            'contact_id' => '7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b',
            'payload' => ['plan' => 'pro'],
          ]);

          // Trigger with an email address
          $resend->events->send([
            'event' => 'user.created',
            'email' => 'steve.wozniak@gmail.com',
            'payload' => ['plan' => 'pro'],
          ]);
          ```

          ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
          import resend

          resend.api_key = "re_xxxxxxxxx"

          # Trigger with a contact ID
          params: resend.Events.SendParams = {
            "event": "user.created",
            "contact_id": "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b",
            "payload": {
              "plan": "pro",
            },
          }

          resend.Events.send(params)

          # Trigger with an email address
          params: resend.Events.SendParams = {
            "event": "user.created",
            "email": "steve.wozniak@gmail.com",
            "payload": {
              "plan": "pro",
            },
          }

          resend.Events.send(params)
          ```

          ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
          require "resend"

          Resend.api_key = "re_xxxxxxxxx"

          # Trigger with a contact ID
          params = {
            event: "user.created",
            contact_id: "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b",
            payload: {
              plan: "pro",
            },
          }

          Resend::Events.send(params)

          # Trigger with an email address
          params = {
            event: "user.created",
            email: "steve.wozniak@gmail.com",
            payload: {
              plan: "pro",
            },
          }

          Resend::Events.send(params)
          ```

          ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
          package main

          import "github.com/resend/resend-go/v3"

          func main() {
          	client := resend.NewClient("re_xxxxxxxxx")

          	// Trigger with a contact ID
          	params := &resend.SendEventRequest{
          		Event:     "user.created",
          		ContactId: "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b",
          		Payload: map[string]any{
          			"plan": "pro",
          		},
          	}

          	client.Events.Send(params)

          	// Trigger with an email address
          	params = &resend.SendEventRequest{
          		Event: "user.created",
          		Email: "steve.wozniak@gmail.com",
          		Payload: map[string]any{
          			"plan": "pro",
          		},
          	}

          	client.Events.Send(params)
          }
          ```

          ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
          use resend_rs::{
            json,
            types::{ContactIdOrEmail, SendEventOptions},
            Resend, Result,
          };

          #[tokio::main]
          async fn main() -> Result<()> {
            let resend = Resend::new("re_xxxxxxxxx");

            let opts = SendEventOptions {
              event: "user.created".to_owned(),
              contact_id_or_email: ContactIdOrEmail::ContactId(
                "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b".to_owned(),
              ),
              payload: json!({
                "plan": "pro"
              }),
            };

            let opts = SendEventOptions {
              event: "user.created".to_owned(),
              contact_id_or_email: ContactIdOrEmail::Email("steve.wozniak@gmail.com".to_owned()),
              payload: json!({
                "plan": "pro"
              }),
            };

            let _event = resend.events.send(opts).await?;

            Ok(())
          }
          ```

          ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
          import com.resend.*;

          public class Main {
              public static void main(String[] args) {
                  Resend resend = new Resend("re_xxxxxxxxx");

                  // Trigger with a contact ID
                  SendEventOptions params = SendEventOptions.builder()
                          .event("user.created")
                          .contactId("7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b")
                          .addPayload("plan", "pro")
                          .build();

                  SendEventResponseSuccess data = resend.events().send(params);

                  // Trigger with an email address
                  SendEventOptions params = SendEventOptions.builder()
                          .event("user.created")
                          .email("steve.wozniak@gmail.com")
                          .addPayload("plan", "pro")
                          .build();

                  SendEventResponseSuccess data = resend.events().send(params);
              }
          }
          ```

          ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
          using Resend;
          using System.Text.Json;

          IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

          var payload = JsonSerializer.SerializeToElement( new { plan = "pro" } );

          // Trigger with a contact ID
          var resp = await resend.EventSendAsync( new EventSendData()
          {
              Event = "user.created",
              ContactId = new Guid( "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b" ),
              Payload = payload,
          } );
          Console.WriteLine( "Event={0}", resp.Content.Event );

          // Trigger with an email address
          await resend.EventSendAsync( new EventSendData()
          {
              Event = "user.created",
              Email = "steve.wozniak@gmail.com",
              Payload = payload,
          } );
          ```

          ```bash cURL {7,19} theme={"theme":{"light":"github-light","dark":"vesper"}}
          # Trigger with a contact ID
          curl -X POST 'https://api.resend.com/events/send' \
               -H 'Authorization: Bearer re_xxxxxxxxx' \
               -H 'Content-Type: application/json' \
               -d '{
            "event": "user.created",
            "contact_id": "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b",
            "payload": {
              "plan": "pro"
            }
          }'

          # Trigger with an email address
          curl -X POST 'https://api.resend.com/events/send' \
               -H 'Authorization: Bearer re_xxxxxxxxx' \
               -H 'Content-Type: application/json' \
               -d '{
            "event": "user.created",
            "email": "steve.wozniak@gmail.com",
            "payload": {
              "plan": "pro"
            }
          }'
          ```

          ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
          # Trigger with a contact ID
          resend events send \
            --event user.created \
            --contact-id 7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b \
            --payload '{"plan":"pro"}'

          # Trigger with an email address
          resend events send \
            --event user.created \
            --email steve.wozniak@gmail.com \
            --payload '{"plan":"pro"}'
          ```
        </CodeGroup>

        View the [Send Event API reference](/docs/api-reference/events/send-event) for more details.
      </Step>

      <Step title="Monitor Runs">
        After sending events, track your Automation executions through Runs.

        <CodeGroup>
          ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
          import { Resend } from 'resend';

          const resend = new Resend('re_xxxxxxxxx');

          const { data, error } = await resend.automations.runs.list({
            automationId: 'c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd',
          });
          ```

          ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
          $resend = Resend::client('re_xxxxxxxxx');

          $resend->automations->runs->list('c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd');
          ```

          ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
          import resend

          resend.api_key = "re_xxxxxxxxx"

          resend.Automations.Runs.list("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd")
          ```

          ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
          require "resend"

          Resend.api_key = "re_xxxxxxxxx"

          Resend::Automations::Runs.list("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd")
          ```

          ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
          package main

          import "github.com/resend/resend-go/v3"

          func main() {
          	client := resend.NewClient("re_xxxxxxxxx")

          	client.Automations.ListRuns("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd")
          }
          ```

          ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
          use resend_rs::{list_opts::ListOptions, Resend, Result};

          #[tokio::main]
          async fn main() -> Result<()> {
            let resend = Resend::new("re_xxxxxxxxx");

            let _automation = resend
              .automations
              .list_runs(
                "c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd",
                None,
                ListOptions::default(),
              )
              .await?;

            Ok(())
          }
          ```

          ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
          import com.resend.*;

          public class Main {
              public static void main(String[] args) {
                  Resend resend = new Resend("re_xxxxxxxxx");

                  ListAutomationRunsResponseSuccess data = resend.automations().listRuns("c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd");
              }
          }
          ```

          ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
          using Resend;

          IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

          var resp = await resend.AutomationRunListAsync( new Guid( "c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd" ) );
          Console.WriteLine( "Count={0}", resp.Content.Data.Count );
          ```

          ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
          curl -X GET 'https://api.resend.com/automations/c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd/runs' \
               -H 'Authorization: Bearer re_xxxxxxxxx'
          ```

          ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
          resend automations runs list c9b16d4f-ba6c-4e2e-b044-6bf4404e57fd
          ```
        </CodeGroup>

        You can filter Runs by status (`running`, `completed`, `failed`, `cancelled`).

        See the [Runs documentation](/docs/dashboard/automations/runs) and [List Runs API reference](/docs/api-reference/automations/list-automation-runs) for more details.
      </Step>
    </Steps>
  </Tab>
</Tabs>
