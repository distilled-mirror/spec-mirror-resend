> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send Email

> Trigger templated emails in your Automations.

This automation step triggers a [Template](https://resend.com/docs/dashboard/templates/introduction.md) email to be sent to the contact.

## How it works

> [tab] Using the dashboard
>
> After adding a [trigger](https://resend.com/docs/dashboard/automations/trigger.md), create a new step to **Send an email**.
>
> ![Add Send Email Action](https://mintcdn.com/resend/ePnINhGLisYSJsWT/images/automations-steps-email.png?fit=max\&auto=format\&n=ePnINhGLisYSJsWT\&q=85\&s=98e94d53506699d565747e510702ad53)
>
> Select a published template, then configure the sender address.
>
> ![Send Email Action Sender Settings](https://mintcdn.com/resend/3_DkZ6MFMzztlC_E/images/automations-steps-email-settings.png?fit=max\&auto=format\&n=3_DkZ6MFMzztlC_E\&q=85\&s=312f80d13ca502ae8de7e7bffd31e251)
>
> Optionally, select a [Topic](#send-with-a-topic) to skip this step for contacts who opted out of it.
>
> *The subject always comes from the Template. To send a different subject, set `subject` when creating the step via the [API](#configuration).*

> [tab] Using the API
>
> Add a `send_email` step to your Automation's `steps` array.
>
> ```ts Node.js {13-21} theme={"theme":{"light":"github-light","dark":"vesper"}}
> import { Resend } from 'resend';
>
> const resend = new Resend('re_xxxxxxxxx');
>
> const { data, error } = await resend.automations.create({
>   name: 'Welcome series',
>   steps: [
>     {
>       key: 'start',
>       type: 'trigger',
>       config: { eventName: 'user.created' },
>     },
>     {
>       key: 'welcome',
>       type: 'send_email',
>       config: {
>         template: {
>           id: '044db673-fff6-420f-a566-f6aba05d60e7',
>         },
>       },
>     },
>   ],
>   connections: [{ from: 'start', to: 'welcome' }],
> });
> ```
>
> ```php PHP {11-19} theme={"theme":{"light":"github-light","dark":"vesper"}}
> $resend = Resend::client('re_xxxxxxxxx');
>
> $resend->automations->create([
>   'name' => 'Welcome series',
>   'steps' => [
>     [
>       'key' => 'start',
>       'type' => 'trigger',
>       'config' => ['event_name' => 'user.created'],
>     ],
>     [
>       'key' => 'welcome',
>       'type' => 'send_email',
>       'config' => [
>         'template' => [
>           'id' => '044db673-fff6-420f-a566-f6aba05d60e7',
>         ],
>       ],
>     ],
>   ],
>   'connections' => [['from' => 'start', 'to' => 'welcome']],
> ]);
> ```
>
> ```python Python {13-21} theme={"theme":{"light":"github-light","dark":"vesper"}}
> import resend
>
> resend.api_key = "re_xxxxxxxxx"
>
> params: resend.Automations.CreateParams = {
>   "name": "Welcome series",
>   "steps": [
>     {
>       "key": "start",
>       "type": "trigger",
>       "config": {"event_name": "user.created"},
>     },
>     {
>       "key": "welcome",
>       "type": "send_email",
>       "config": {
>         "template": {
>           "id": "044db673-fff6-420f-a566-f6aba05d60e7",
>         },
>       },
>     },
>   ],
>   "connections": [{"from": "start", "to": "welcome"}],
> }
>
> resend.Automations.create(params)
> ```
>
> ```ruby Ruby {13-21} theme={"theme":{"light":"github-light","dark":"vesper"}}
> require "resend"
>
> Resend.api_key = "re_xxxxxxxxx"
>
> params = {
>   name: "Welcome series",
>   steps: [
>     {
>       key: "start",
>       type: "trigger",
>       config: { event_name: "user.created" },
>     },
>     {
>       key: "welcome",
>       type: "send_email",
>       config: {
>         template: {
>           id: "044db673-fff6-420f-a566-f6aba05d60e7",
>         },
>       },
>     },
>   ],
>   connections: [{ from: "start", to: "welcome" }],
> }
>
> Resend::Automations.create(params)
> ```
>
> ```go Go {18-26} theme={"theme":{"light":"github-light","dark":"vesper"}}
> package main
>
> import "github.com/resend/resend-go/v4"
>
> func main() {
> 	client := resend.NewClient("re_xxxxxxxxx")
>
> 	params := &resend.CreateAutomationRequest{
> 		Name: "Welcome series",
> 		Steps: []resend.AutomationStep{
> 			{
> 				Key:  "start",
> 				Type: resend.AutomationStepTypeTrigger,
> 				Config: map[string]any{
> 					"event_name": "user.created",
> 				},
> 			},
> 			{
> 				Key:  "welcome",
> 				Type: resend.AutomationStepTypeSendEmail,
> 				Config: map[string]any{
> 					"template": map[string]any{
> 						"id": "044db673-fff6-420f-a566-f6aba05d60e7",
> 					},
> 				},
> 			},
> 		},
> 		Connections: []resend.AutomationConnection{
> 			{From: "start", To: "welcome"},
> 		},
> 	}
>
> 	client.Automations.Create(params)
> }
> ```
>
> ```rust Rust {22-27} theme={"theme":{"light":"github-light","dark":"vesper"}}
> use resend_rs::{
>   types::{
>     AutomationStatus, AutomationTemplate, Connection, CreateAutomationOptions, SendEmailStepConfig,
>     Step, TriggerStepConfig,
>   },
>   Resend, Result,
> };
>
> #[tokio::main]
> async fn main() -> Result<()> {
>   let resend = Resend::new("re_xxxxxxxxx");
>
>   let opts = CreateAutomationOptions {
>     name: "Welcome series".to_owned(),
>     steps: vec![
>       Step::Trigger {
>         key: "start".to_owned(),
>         config: TriggerStepConfig {
>           event_name: "user.created".to_owned(),
>         },
>       },
>       Step::SendEmail {
>         key: "welcome".to_owned(),
>         config: SendEmailStepConfig::new(AutomationTemplate::new(
>           "044db673-fff6-420f-a566-f6aba05d60e7",
>         )),
>       },
>     ],
>     connections: vec![Connection::new("start", "welcome")],
>     status: AutomationStatus::Disabled,
>   };
>   let _automation = resend.automations.create(opts).await?;
>
>   Ok(())
> }
> ```
>
> ```java Java {21-29} theme={"theme":{"light":"github-light","dark":"vesper"}}
> import com.resend.*;
> import com.resend.core.exception.ResendException;
> import com.resend.services.automations.model.AutomationConnection;
> import com.resend.services.automations.model.AutomationStep;
> import com.resend.services.automations.model.CreateAutomationOptions;
> import com.resend.services.automations.model.CreateAutomationResponseSuccess;
> import java.util.Map;
>
> public class Main {
>     public static void main(String[] args) throws ResendException {
>         Resend resend = new Resend("re_xxxxxxxxx");
>
>         CreateAutomationOptions options = CreateAutomationOptions.builder()
>                 .name("Welcome series")
>                 .steps(
>                     AutomationStep.trigger("start")
>                         .eventName("user.created")
>                         .build(),
>                     AutomationStep.sendEmail("welcome")
>                         .template("044db673-fff6-420f-a566-f6aba05d60e7")
>                         .templateVariable("name", Map.of("var", "event.firstName"))
>                         .build()
>                 )
>                 .connections(
>                     AutomationConnection.builder()
>                         .from("start")
>                         .to("welcome")
>                         .build()
>                 )
>                 .build();
>
>         CreateAutomationResponseSuccess data = resend.automations().create(options);
>     }
> }
> ```
>
> ```csharp .NET {7-14,22} theme={"theme":{"light":"github-light","dark":"vesper"}}
> using Resend;
> using System.Text.Json;
>
> IResend resend = ResendClient.Create( "re_xxxxxxxxx" );
>
> var startConfig = JsonSerializer.SerializeToElement( new { event_name = "user.created" } );
> var welcomeConfig = JsonSerializer.SerializeToElement( new
> {
>     template = new
>     {
>         id = "044db673-fff6-420f-a566-f6aba05d60e7",
>         variables = new { name = new { @var = "event.firstName" } },
>     },
>     subject = "Welcome to Acme!",
>     from = "Acme <hello@example.com>",
>     reply_to = "support@example.com",
> } );
>
> var resp = await resend.AutomationCreateAsync( new AutomationCreateData()
> {
>     Name = "Welcome series",
>     Steps = new List<AutomationStepData>
>     {
>         new AutomationStepData { Ref = "start", Type = "trigger", Config = startConfig },
>         new AutomationStepData { Ref = "welcome", Type = "send_email", Config = welcomeConfig },
>     },
>     Connections = new List<AutomationEdge>
>     {
>         new AutomationEdge { From = "start", To = "welcome", EdgeType = "default" },
>     },
> } );
> ```
>
> ```bash cURL {10-17} theme={"theme":{"light":"github-light","dark":"vesper"}}
> curl -X POST 'https://api.resend.com/automations' \
>      -H 'Authorization: Bearer re_xxxxxxxxx' \
>      -H 'Content-Type: application/json' \
>      -d '{
>   "name": "Welcome series",
>   "steps": [{
>     "key": "start",
>     "type": "trigger",
>     "config": { "event_name": "user.created" }
>   }, {
>     "key": "welcome",
>     "type": "send_email",
>     "config": {
>       "template": {
>         "id": "044db673-fff6-420f-a566-f6aba05d60e7"
>       }
>     }
>   }],
>   "connections": [
>     { "from": "start", "to": "welcome" }
>   ]
> }'
> ```
>
> ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
> resend automations create --name "Welcome series" --file ./automation.json
> ```

> [!NOTE]
>
> Only `published` templates are available to be used in an Automation.

## Template variables

Use the `variables` field to pass data into your template. Each value is a static string, passed as-is, or a reference with `{ "var": "<path>" }`:

* `event.*` is a field from the event that triggered the Automation, such as `event.firstName`.
* `contact.*` is a field from the contact, such as `contact.properties.company`.
* `wait_events.<event_name>.*` is a field from an event a previous [wait for event](https://resend.com/docs/dashboard/automations/wait-for-event.md#use-the-received-event-in-later-steps) step received, such as `wait_events.feedback.received.response`. If the Automation waited for that event more than once, this is the most recent one before this step.

```json {7-14} theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "welcome",
  "type": "send_email",
  "config": {
    "template": {
      "id": "044db673-fff6-420f-a566-f6aba05d60e7",
      "variables": {
        "firstName": { "var": "event.firstName" },
        "orderNumber": { "var": "event.orderId" },
        "total": { "var": "event.amount" },
        "company": { "var": "contact.properties.company" },
        "feedback": { "var": "wait_events.feedback.received.response" },
        "supportEmail": "help@example.com"
      }
    }
  }
}
```

Template variables must be present in your referenced template and the key names must match exactly with the template variable names.

### Use contact properties in a Template

A Template only reads the variables the step maps. It can't read contact placeholders like `{{{contact.first_name}}}` or `{{{contact.first_name|there}}}`, which work in [Broadcasts](https://resend.com/docs/dashboard/broadcasts/editor.md#personalize-your-content) only. A Template that uses them fails when the step sends it, and the run's `status_reason` is `inline_fallback` or `template_render_failed`.

To greet the contact by name:

1. In the Template, add a [variable](https://resend.com/docs/dashboard/templates/template-variables.md) such as `USER_FIRST_NAME`, with `there` as its fallback value, and write `Hi {{{USER_FIRST_NAME}}}`. Resend uses the fallback when the contact has no first name set.
2. In the step, map the variable to the contact property:

```json {7-9} theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "welcome",
  "type": "send_email",
  "config": {
    "template": {
      "id": "044db673-fff6-420f-a566-f6aba05d60e7",
      "variables": {
        "USER_FIRST_NAME": { "var": "contact.first_name" }
      }
    }
  }
}
```

Built-in properties map as `contact.first_name`, `contact.last_name`, and `contact.email`. A custom property needs the `properties.` prefix: a Broadcast's `{{{contact.company}}}` becomes `{ "var": "contact.properties.company" }`.

Use a variable name that isn't [reserved](https://resend.com/docs/dashboard/templates/template-variables.md#create-custom-variables). `FIRST_NAME` is reserved, which is why the example uses `USER_FIRST_NAME`.

For more help working with variables, see the [Template documentation](https://resend.com/docs/dashboard/templates/template-variables.md).

## Send with a Topic

Set `topic_id` to send the email only to contacts subscribed to a [Topic](https://resend.com/docs/dashboard/contacts/manage-topics.md). This lets contacts opt out of one kind of Automation email, like product tips, while still receiving others.

```json {8} theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "tips",
  "type": "send_email",
  "config": {
    "template": {
      "id": "044db673-fff6-420f-a566-f6aba05d60e7"
    },
    "topic_id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e"
  }
}
```

When the step runs, Resend checks the contact's subscription to the Topic:

* **Opted in**: the email is sent.
* **Opted out**: the step is [skipped](https://resend.com/docs/dashboard/automations/runs.md#skipped-steps) and no email is sent. The Automation continues to the next step.
* **No preference**: the Topic's default subscription decides. The email is sent if the default is `opt_in`, and the step is skipped if it's `opt_out`.

The Topic must exist in your team. If it doesn't, the API rejects the request with a `422` error.

> [!WARNING]
>
> If you delete a Topic that a `send_email` step uses, the step keeps the
> deleted Topic's ID and fails every time it runs. Pick another Topic for the
> step or remove it before deleting the Topic.

## Unsubscribe behavior

Resend does not automatically add an unsubscribe link to emails sent from a `send_email` step. To let contacts opt out, add `{{{RESEND_UNSUBSCRIBE_URL}}}` to the [Template](https://resend.com/docs/dashboard/templates/introduction.md) used by the step.

> [!NOTE]
>
> `{{{RESEND_UNSUBSCRIBE_URL}}}` must be added to the Template itself, not the step's `config`. If the Template doesn't include this variable, contacts have no way to unsubscribe from within the email.

When the Template includes `{{{RESEND_UNSUBSCRIBE_URL}}}`, Resend handles unsubscribes as follows, with or without a Topic:

* **Global unsubscribe always wins.** A contact who is [unsubscribed](https://resend.com/docs/dashboard/contacts/managing-unsubscribe-list.md#subscription-statuses) never receives Automation emails, even if they have opted in to the step's Topic.
* **The unsubscribe link opens your preference page.** It works the same as the [Broadcast unsubscribe link](https://resend.com/docs/dashboard/broadcasts/editor.md#broadcast-unsubscribe-link).
* **One-click unsubscribe is global.** Resend also adds `List-Unsubscribe` and `List-Unsubscribe-Post` headers, which inbox providers like Gmail show as an unsubscribe button. Using that button unsubscribes the contact from all Broadcasts and Automation emails, not only the step's Topic.

See [when to use an unsubscribe link](https://resend.com/docs/knowledge-base/should-i-add-an-unsubscribe-link.md) to decide whether your Automation emails need one.

## Configuration

**config.template** `object` *required*

The published template to send. Provide `id` and optionally `variables`.

**properties**

**config.template.id** `string` *required*

The ID or alias of the template to send.

**config.template.variables** `object`

A key-value map of template variables. Each value can be a static string or a variable reference object (`{ "var": "event.fieldName" }`) that resolves dynamically from the `event.*`, `contact.*`, or `wait_events.*` namespaces.

**config.from** `string`

The sender email address.

If provided, this value will override the template's default value.

**config.subject** `string`

The email subject line.

If provided, this value will override the template's default value.

**config.reply\_to** `string`

Reply-to email address.

If provided, this value will override the template's default value.

**config.topic\_id** `string`

The ID of the [Topic](https://resend.com/docs/dashboard/contacts/manage-topics.md) this email belongs
to. Contacts not subscribed to the Topic skip this step. See [Send with a
Topic](https://resend.com/docs/dashboard/automations/send-email.md#send-with-a-topic).

```json theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "key": "welcome",
  "type": "send_email",
  "config": {
    "template": {
      "id": "062f8ef4-fbfa-44f1-b5e0-ff8e1e8ffa96",
      "variables": {
        "name": { "var": "event.firstName" }
      }
    },
    "from": "hello@example.com",
    "subject": "Welcome!",
    "reply_to": "support@example.com",
    "topic_id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e"
  }
}
```
