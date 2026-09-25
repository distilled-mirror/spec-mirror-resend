> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Using Templates

> Learn how to use Templates to send transactional emails.

## Email Templates

With Templates, you can define the structure and layout of a message once, then reuse it for multiple emails.

Use Templates for [transactional emails](/docs/email-types#send-transactional-emails) you send often, like:

* Login/Auth
* Onboarding
* Ecommerce
* Notifications
* Automations

## Template Features

With Resend's Template features, you can:

* Compose with Resend's [no-code Template editor](/docs/dashboard/templates/template-editor).
* Edit and update Templates with access to full [version history](/docs/dashboard/templates/version-history).
* Include [custom variables](/docs/dashboard/templates/template-variables) to personalize content.

You can even [embed the React Email editor](/docs/knowledge-base/embed-react-email-editor) in your own application to let your users create their own transactional emails from Templates and ship HTML-ready email content directly to Resend.

## Choose your infrastructure

To [create transactional email Templates](/docs/dashboard/templates/create-template), you can use a variety of tools:

* [Editor](/docs/dashboard/templates/template-editor): create using Resend's no-code editor
* [SDKs](/docs/sdks): create with an SDK built for your language
* [Integrations](/docs/integrations): create with a framework or tool you already use
* [API](/docs/api-reference/templates/create-template): create with raw cURL calls
* [CLI](/docs/cli#emails): create templates from the terminal
* [MCP](/docs/mcp-server): create through your agent with MCP
* [React Email](/docs/knowledge-base/template-emails-with-react-email): create from a React Email Template file
* [HTML](/docs/dashboard/templates/create-template#add-a-template-from-an-existing-file): create from an HTML file

## Send Emails with Templates

When you send a transactional email from your application, you can reference a [published Template](/docs/dashboard/templates/create-template#publish-a-template) to use as your content instead of passing the HTML directly.

Specify the Template ID and include any [Template variables](/docs/dashboard/templates/template-variables) in your API endpoint or CLI command. Resend will replace the Template variables with the actual variables specified in your code.

<CodeGroup>
  ```ts Node.js {8-14} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  await resend.emails.send({
    from: 'Acme <onboarding@resend.dev>',
    to: 'delivered@resend.dev',
    template: {
      id: 'order-confirmation',
      variables: {
        PRODUCT: 'Vintage Macintosh',
        PRICE: 499,
      },
    },
  });
  ```

  ```php PHP {7-12} theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->emails->send([
    'from' => 'Acme <onboarding@resend.dev>',
    'to' => ['delivered@resend.dev'],
    'subject' => 'hello world',
    'template'=> [
      'id' => 'f3b9756c-f4f4-44da-bc00-9f7903c8a83f',
      'variables' => [
        'PRODUCT' => 'Vintage Macintosh',
        'PRICE' => 499,
      ]
    ]
  ]);
  ```

  ```python Python {8-14} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  resend.Emails.send({
    "from": "Acme <onboarding@resend.dev>",
    "to": "delivered@resend.dev",
    "template": {
      "id": "order-confirmation",
      "variables": {
        "PRODUCT": "Vintage Macintosh",
        "PRICE": 499
      }
    }
  })
  ```

  ```ruby Ruby {8-14} theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  Resend::Emails.send({
    from: "Acme <onboarding@resend.dev>",
    to: "delivered@resend.dev",
    template: {
      id: "order-confirmation",
      variables: {
        PRODUCT: "Vintage Macintosh",
        PRICE: 499
      }
    }
  })
  ```

  ```go Go {8-14} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import "github.com/resend/resend-go/v4"

  client := resend.NewClient("re_xxxxxxxxx")

  params := &resend.SendEmailRequest{
    From: "Acme <onboarding@resend.dev>",
    To: []string{"delivered@resend.dev"},
    Template: &resend.EmailTemplate{
      Id: "order-confirmation",
      Variables: map[string]interface{}{
        "PRODUCT": "Vintage Macintosh",
        "PRICE": 499,
      },
    },
  }

  client.Emails.Send(params)
  ```

  ```rust Rust {11-13,20} theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{
    json,
    types::{CreateEmailBaseOptions, EmailTemplate},
    Resend, Result,
  };

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let template = EmailTemplate::new("order-confirmation")
      .with_variable("PRODUCT", json!("Vintage Macintosh"))
      .with_variable("PRICE", json!(499));

    let email = CreateEmailBaseOptions::new(
      "Acme <onboarding@resend.dev>",
      ["delivered@resend.dev"],
      "hello world",
    )
    .with_template(template);

    let _email = resend.emails.send(email).await?;

    Ok(())
  }
  ```

  ```java Java {11-13,18-21} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;
  import com.resend.services.emails.model.CreateEmailOptions;
  import com.resend.services.emails.model.CreateEmailResponse;
  import com.resend.services.emails.model.Template;
  import java.util.Arrays;
  import java.util.HashMap;
  import java.util.Map;

  Resend resend = new Resend("re_xxxxxxxxx");

  Map<String, Object> variables = new HashMap<>();
  variables.put("PRODUCT", "Vintage Macintosh");
  variables.put("PRICE", 499);

  CreateEmailOptions params = CreateEmailOptions.builder()
    .from("Acme <onboarding@resend.dev>")
    .to(Arrays.asList("customer@email.com"))
    .template(Template.builder()
      .id("order-confirmation")
      .variables(variables)
      .build())
    .build();

  CreateEmailResponse data = resend.emails().send(params);
  ```

  ```csharp .NET {5-9,17-20} theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create("re_xxxxxxxxx");

  var variables = new Dictionary<string, object>
  {
    { "PRODUCT", "Vintage Macintosh" },
    { "PRICE", 499 }
  };

  var resp = await resend.EmailSendAsync(
    new EmailMessage()
    {
      From = "Acme <onboarding@resend.dev>",
      To = new[] { "delivered@resend.dev" },
      Template = new EmailMessageTemplate()
      {
        TemplateId = "b6d24b8e-af0b-4c3c-be0c-359bbd97381e",
        Variables = variables
      }
    }
  );

  Console.WriteLine($"Email Id={resp.Content}");
  ```

  ```bash cURL {7-13} theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/emails' \
    -H 'Authorization: Bearer re_xxxxxxxxx' \
    -H 'Content-Type: application/json' \
    -d $'{
      "from": "Acme <onboarding@resend.dev>",
      "to": "delivered@resend.dev",
      "template": {
        "id": "order-confirmation",
        "variables": {
          "PRODUCT": "Vintage Macintosh",
          "PRICE": 499
        }
      }
  }'
  ```
</CodeGroup>

## Related Guides

See how to use Resend's email Template features.

<CardGroup>
  <Card title="Create Templates" icon="cards-blank" href="/docs/dashboard/templates/create-template" />

  <Card title="Editor" icon="pencil" href="/docs/dashboard/templates/template-editor" />

  <Card title="Template variables" icon="swap" href="/docs/dashboard/templates/template-variables" />

  <Card title="Version history" icon="code-compare" href="/docs/dashboard/templates/version-history" />

  <Card title="React Email Templates" icon="react" href="/docs/knowledge-base/template-emails-with-react-email" />

  <Card title="Embed Email Editor" icon="picture-in-picture" href="/docs/knowledge-base/embed-react-email-editor" />
</CardGroup>
