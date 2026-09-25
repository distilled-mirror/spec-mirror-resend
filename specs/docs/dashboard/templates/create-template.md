> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Create a Template

> Learn how to create a Template in the Resend Dashboard editor or with the API.

## Creating Templates

You can draft and publish reusable email Templates with Resend's no-code editor or programmatically.

Templates allow you to send your frequently used transactional emails without needing to include the entire HTML body content. You can also include [Template variables](/docs/dashboard/templates/template-variables) that will be replaced with personalized information when sending, such as a customer's first name.

You can create a new transactional email Template in several ways:

* [Dashboard editor](#add-a-template-in-the-dashboard)
* [API](#add-a-template-with-the-api)
* [CLI](/docs/cli#templates)
* [HTML file](#add-a-template-from-an-existing-file)
* [React Email](/docs/knowledge-base/template-emails-with-react-email)
* [Duplicate a Template](#duplicate-a-template)
* [Clone a Broadcast](#clone-a-broadcast)

A new Template must be [published](#publish-a-template) before it can be used to send emails.

## Add a Template in the Dashboard

To create and publish a new Template using the no-code editor:

<Steps>
  <Step title="Go to the Templates page in your Resend dashboard." />

  <Step title="Click Create template." />

  <Step title="Add sender info.">
    Choose any username at your [verified domain](/docs/add-a-domain) to send your email from.

    We suggest you choose a `from` name and address that assures the reader the email is coming from you, for example:

    * `My Company Name <company@email.example.com>`
  </Step>

  <Step title="Create a subject for your email." />

  <Step title="Optionally define other email fields.">
    Resend's no-code Template editor allows you to specify optional fields such as a different Reply-to address or preview text for email clients.
  </Step>

  <Step title="Write your email content.">
    You can use `/` commands in the Template editor for UI elements such as headings, lists, and images. You can also [compose your body text in Markdown](/docs/dashboard/templates/template-editor#markdown-support) and [add Template variables](/docs/dashboard/templates/template-variables) to personalize content.

    Alternatively, you can paste or drag in content from [an existing HTML or React Email file](#add-a-template-from-an-existing-file).
  </Step>

  <Step title="Use the sidebar to add custom styles.">
    When you select an element such as text, images, or the entire page, you will see contextual styling menu options in the page sidebar. Choose colors, sizes, layouts, and more in the sidebar or add your own global CSS styles directly in the editor.
  </Step>

  <Step title="Send yourself a test email.">
    Click `Test email` and add one or more email addresses to send a test email. You will see any Template variables and can update their default values before sending.

    <video src="https://mintcdn.com/resend/8sUIFX1U2gAd2pqE/images/templates-test-email.mp4?fit=max&auto=format&n=8sUIFX1U2gAd2pqE&q=85&s=9651888b2f1b914ffd64054a9fd3f342" autoPlay muted loop width="1512" height="926" data-path="images/templates-test-email.mp4" />
  </Step>

  <Step title="Publish your Template.">
    Click `Publish` to prompt Resend's review feature. This will check for any errors or concerns with your Template and allow you to catch common mistakes before publishing.
  </Step>

  <Step title="Slide to confirm.">
    When there are no errors, the "Slide to publish" element will be active. Slide the arrow to confirm that you are ready to publish your Template. Only published Templates can be used to send emails.

    Alternatively, exit the editor to leave your Template saved as a draft. It is automatically saved as you compose.
  </Step>
</Steps>

## Add a Template with the API

Programmatically create a Template from your application with the [Templates API](/docs/api-reference/templates/create-template). The payload can optionally include [variables to be used in the template](/docs/dashboard/templates/template-variables).

<CodeGroup>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  await resend.templates.create({
    name: 'order-confirmation',
    from: 'Resend Store <store@example.com>',
    subject: 'Thanks for your order!',
    html: '<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>',
    variables: [
      {
        key: 'PRODUCT',
        type: 'string',
        fallbackValue: 'item',
      },
      {
        key: 'PRICE',
        type: 'number',
        fallbackValue: 20,
      },
    ],
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->templates->create([
    'name' => 'order-confirmation',
    'from' => 'Resend Store <store@example.com>',
    'subject' => 'Thanks for your order!',
    'html' => '<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>',
    'variables' => [
      [
        'key' => 'PRODUCT',
        'type' => 'string',
        'fallback_value' => 'item'
      ],
      [
        'key' => 'PRICE',
        'type' => 'number',
        'fallback_value' => 49.99
      ]
    ]
  ]);
  ```

  ```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  params: resend.Templates.CreateParams = {
      "name": "order-confirmation",
      "from": "Resend Store <store@example.com>",
      "subject": "Thanks for your order!",
      "html": "<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>",
      "variables": [
          {
              "key": "PRODUCT",
              "type": "string",
              "fallback_value": "item",
          },
          {
              "key": "PRICE",
              "type": "number",
              "fallback_value": 20,
          },
      ],
  }

  resend.Templates.create(params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  Resend::Templates.create(
    name: "order-confirmation",
    from: "Resend Store <store@example.com>",
    subject: "Thanks for your order!",
    html: "<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>",
    variables: [
      {
        key: "PRODUCT",
        type: "string",
        fallback_value: "item"
      },
      {
        key: "PRICE",
        type: "number",
        fallback_value: 20
      }
    ]
  )
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  import "github.com/resend/resend-go/v4"

  client := resend.NewClient("re_xxxxxxxxx")

  client.Templates.Create(&resend.CreateTemplateRequest{
  	Name:    "order-confirmation",
  	From:    "Resend Store <store@example.com>",
  	Subject: "Thanks for your order!",
  	Html:    "<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>",
  	Variables: []*resend.TemplateVariable{
  		{
  			Key:           "PRODUCT",
  			Type:          resend.VariableTypeString,
  			FallbackValue: "item",
  		},
  		{
  			Key:           "PRICE",
  			Type:          resend.VariableTypeNumber,
  			FallbackValue: 20,
  		},
  	},
  })
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{
    types::{CreateTemplateOptions, Variable, VariableType},
    Resend, Result,
  };

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let name = "order-confirmation";
    let from = "Resend Store <store@example.com>";
    let subject = "Thanks for your order!";
    let html = "<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>";

    let variables = [
      Variable::new("PRODUCT", VariableType::String).with_fallback("item"),
      Variable::new("PRICE", VariableType::Number).with_fallback(20)
    ];

    let opts = CreateTemplateOptions::new(name, html)
      .with_from(from)
      .with_subject(subject)
      .with_variables(&variables);

    let template = resend.templates.create(opts).await?;

    let _published = resend.templates.publish(&template.id).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;
  import com.resend.core.exception.ResendException;
  import com.resend.services.templates.model.CreateTemplateOptions;
  import com.resend.services.templates.model.CreateTemplateResponseSuccess;
  import com.resend.services.templates.model.Variable;
  import com.resend.services.templates.model.VariableType;

  public class Main {
      public static void main(String[] args) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          CreateTemplateOptions params = CreateTemplateOptions.builder()
                  .name("order-confirmation")
                  .from("Resend Store <store@example.com>")
                  .subject("Thanks for your order!")
                  .html("<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>")
                  .addVariable(new Variable("PRODUCT", VariableType.STRING, "item"))
                  .addVariable(new Variable("PRICE", VariableType.NUMBER, 20))
                  .build();

          CreateTemplateResponseSuccess data = resend.templates().create(params);
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create("re_xxxxxxxxx");

  var variables = new List<TemplateVariable>
  {
    new TemplateVariable() {
      Key = "PRODUCT",
      Type = TemplateVariableType.String,
      Default = "item",
    },
    new TemplateVariable() {
      Key = "PRICE",
      Type = TemplateVariableType.Number,
      Default = 20,
    },
  };

  var resp = await resend.TemplateCreateAsync(
    new TemplateData()
    {
      Name = "order-confirmation",
      From = "Resend Store <store@example.com>",
      Subject = "Thanks for your order!",
      HtmlBody = "<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>",
      Variables = variables,
    }
  );

  Console.WriteLine($"Template Id={resp.Content}");
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/templates' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "name": "order-confirmation",
    "from": "Resend Store <store@example.com>",
    "subject": "Thanks for your order!",
    "html": "<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>",
    "variables": [
      {
        "key": "PRODUCT",
        "type": "string",
        "fallback_value": "item"
      },
      {
        "key": "PRICE",
        "type": "number",
        "fallback_value": 20
      }
    ]
  }'
  ```
</CodeGroup>

## Add a Template from an existing file

You can create a Template from existing resources such as an HTML or [React Email](https://react.email) file.

[Create a new Template in the Dashboard](#add-a-template-in-the-dashboard), then paste or drag in your HTML or React Email content.

<Note>
  When pasting React Email code, only imports from `@react-email/components` and
  `react` are supported. Local file imports (e.g., `./components/Logo`) and
  other third-party packages are not supported in the editor.
</Note>

## Duplicate a Template

You can duplicate an existing Template in the Dashboard, [via the Templates API](/docs/api-reference/templates/duplicate-template), or with a [Templates CLI command](/docs/cli#templates).

<img alt="Duplicate a template" src="https://mintcdn.com/resend/8sUIFX1U2gAd2pqE/images/templates-introduction-duplicate.png?fit=max&auto=format&n=8sUIFX1U2gAd2pqE&q=85&s=05d9c56edfa20ed9e03b3a83c01cd130" width="3024" height="1900" data-path="images/templates-introduction-duplicate.png" />

## Clone a Broadcast

You can turn any sent [Broadcast](/docs/dashboard/broadcasts/introduction) into a reusable Template. Cloning reuses a Broadcast's design and content as a starting point for transactional emails.

Locate your desired Broadcast in the [Broadcast dashboard](https://resend.com/broadcasts), click the more options button <span className="inline-block align-middle"><Icon icon="ellipsis" iconType="solid" /></span>, and choose **Clone as Template**.

## Publish a Template

By default, Templates are in a **draft** state. To use a Template to send emails, you must first **publish** it via the Dashboard, using the [Templates API](/docs/api-reference/templates/publish-template), or with a [Templates CLI command](/docs/cli#templates).

<img alt="Publish a template" src="https://mintcdn.com/resend/8sUIFX1U2gAd2pqE/images/templates-introduction-publish.png?fit=max&auto=format&n=8sUIFX1U2gAd2pqE&q=85&s=c39c711baf5719d8199ecdc3b2221480" width="3024" height="1900" data-path="images/templates-introduction-publish.png" />

For a more streamlined flow in your application, you can create and publish a Template in a single step.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.templates
  .create({
    name: 'order-confirmation',
    html: '<p>Thanks for your order!</p>',
  })
  .publish();
```

## Edit a Template

You can only send emails using the most recently published version of a Template. Once a Template is published, you can continue to edit it as a draft without impacting any emails sent using the Template.

To use an updated version of your Template, you must publish your Template again to create a new version for sending. Until you republish, any edits are only saved in draft form. After you publish a new version, your changes will then be reflected in any future emails using the Template.

[Learn more about editing Templates in production safely with version history](/docs/dashboard/templates/version-history).

## Delete a Template

You can delete a Template via the Dashboard by clicking on the **Delete** button, [via the Templates API](/docs/api-reference/templates/delete-template), or with a [Templates CLI command](/docs/cli#templates).

<img alt="Delete a template" src="https://mintcdn.com/resend/8sUIFX1U2gAd2pqE/images/templates-introduction-delete.png?fit=max&auto=format&n=8sUIFX1U2gAd2pqE&q=85&s=5e7bc7c5e86e28f831c1d133d7961d73" width="3024" height="1900" data-path="images/templates-introduction-delete.png" />

## API Reference

For complete API documentation, see the [Templates API reference](/docs/api-reference/templates/create-template) and the [`template` parameter of the Sending API](/docs/api-reference/emails/send-email#param-template).
