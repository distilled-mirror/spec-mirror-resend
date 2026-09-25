> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Version History

> Edit Templates safely in production environments with version history.

Templates in production require a workflow that lets you make changes safely without disrupting active emails. As you build your Template, your entire team can collaborate on the content and design in real-time with full version history.

## Draft vs Published

Templates start in a draft state and must be published before they can be used to send emails.

This separation allows you to:

* Test Templates thoroughly before going live
* Make changes without affecting active emails
* Maintain version control over your email content

Once you [publish a Template](/docs/dashboard/templates/create-template#publish-a-template), this published version will be used to send emails until you publish again. You can continue to work on a production Template in draft state without affecting the published version, and the editor will automatically save your progress.

<CodeGroup>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  // Create template
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  await resend.templates.create({
    name: 'order-confirmation',
    from: 'Resend Store <store@resend.com>',
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

  // Publish template
  await resend.templates.publish('template_id');

  // Or create and publish a template in one step
  const { data, error } = await resend.templates
    .create({
      name: 'order-confirmation',
      html: '<p>Thanks for your order!</p>',
    })
    .publish();
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  // Create template
  $resend->templates->create([
    'name' => 'order-confirmation',
    'from' => 'Resend Store <store@resend.com>',
    'subject' => 'Thanks for your order!',
      'html' => "<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>",
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

  // Publish template
  $resend->templates->publish('template_id');
  ```

  ```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  # Create template
  params: resend.Templates.CreateParams = {
    "name": "order-confirmation",
    "from": "Resend Store <store@resend.com>",
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
      },
    ]
  }

  resend.Templates.create(params)

  # Publish template
  resend.Templates.publish('template_id');
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  # Create template
  params = {
    "name": 'order-confirmation',
    "from": 'Resend Store <store@resend.com>',
    "subject": 'Thanks for your order!',
    "html": "<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>",
    "variables": [{
        "key": 'PRODUCT',
        "type": 'string',
        "fallback_value": 'item'
      },
      {
        "key": 'PRICE',
        "type": 'number',
        "fallback_value": 20
      }
    ]
  }

  Resend::Templates.create(params)

  # Publish template
  Resend::Templates.publish('template_id');
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  import "github.com/resend/resend-go/v4"

  client := resend.NewClient("re_xxxxxxxxx")

  // Create template
  params := &resend.CreateTemplateRequest{
    Name: "order-confirmation",
    From: "Resend Store <store@resend.com>",
    Subject: "Thanks for your order!",
    Html: "<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>",
    Variables: []*resend.TemplateVariable{
      {
        Key: "PRODUCT",
        Type: "string",
        FallbackValue: "item",
      },
      {
        Key: "PRICE",
        Type: "number",
        FallbackValue: 20,
      },
    },
  }

  template, _ := client.Templates.Create(params)

  // Publish template
  client.Templates.Publish(template.Id)
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{
    types::{CreateTemplateOptions, Variable, VariableType},
    Resend, Result,
  };

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    // Create template
    let name = "order-confirmation";
    let from = "Resend Store <store@resend.com>";
    let subject = "Thanks for your order!";
    let html = "<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>";

    let variables = [
      Variable::new("PRODUCT", VariableType::String).with_fallback("item"),
      Variable::new("PRICE", VariableType::Number).with_fallback(20),
    ];

    let opts = CreateTemplateOptions::new(name, html)
      .with_from(from)
      .with_subject(subject)
      .with_variables(&variables);

    let template = resend.templates.create(opts).await?;

    // Publish template
    resend.templates.publish(&template.id).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;
  import com.resend.services.templates.model.CreateTemplateOptions;
  import com.resend.services.templates.model.CreateTemplateResponseSuccess;
  import com.resend.services.templates.model.Variable;
  import com.resend.services.templates.model.VariableType;
  import java.util.Arrays;
  import java.util.List;

  Resend resend = new Resend("re_xxxxxxxxx");

  // Create template
  List<Variable> variables = Arrays.asList(
    new Variable("PRODUCT", VariableType.STRING, "item"),
    new Variable("PRICE", VariableType.NUMBER, 20)
  );

  CreateTemplateOptions params = CreateTemplateOptions.builder()
    .name("order-confirmation")
    .from("Resend Store <store@resend.com>")
    .subject("Thanks for your order!")
    .html("<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>")
    .variables(variables)
    .build();

  CreateTemplateResponseSuccess data = resend.templates().create(params);

  // Publish template
  resend.templates().publish(data.getId());
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create("re_xxxxxxxxx");

  // Create template
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
      From = "Resend Store <store@resend.com>",
      Subject = "Thanks for your order!",
      HtmlBody = @"
        <p>Name: {{{PRODUCT}}}</p>
        <p>Total: {{{PRICE}}}</p>
      ",
      Variables = variables,
    }
  );

  // Publish template
  await resend.TemplatePublishAsync(resp.Content);

  Console.WriteLine($"Template Id={resp.Content}");
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  # Create template
  curl -X POST 'https://api.resend.com/templates' \
   -H 'Authorization: Bearer re_xxxxxxxxx' \
   -H 'Content-Type: application/json' \
   -d $'{
    "name": "order-confirmation",
    "from": "Resend Store <store@resend.com>",
    "subject": "Thanks for your order!",
    "html": "<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>",
    "variables": [
      {
        "key": "PRODUCT",
        "type": "string",
        "fallbackValue": "item"
      },
      {
        "key": "PRICE",
        "type": "number",
        "fallbackValue": 20
      }
    ]
  }'

  # Publish template
  curl -X POST 'https://api.resend.com/templates/{template_id}/publish' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json'
  ```
</CodeGroup>

After you publish a Template, you can freely work on it through the editor or update it [via the Templates API](/docs/api-reference/templates/update-template) without affecting the published version. This allows you to test and validate new edits before sending them to users.

## Version History

Each Template contains a version history that helps you track changes your team has made over time. You can view the version history by clicking the three dots in the top right corner of the Template editor and selecting **Version History**.

As you work on a Template in the editor, your changes are saved as a draft, although you can also manually save drafts by pressing <kbd>Cmd</kbd> + <kbd>S</kbd> (Mac) or <kbd>Ctrl</kbd> + <kbd>S</kbd> (Windows). Only after publishing again will the changes be reflected in emails using the Template.

Through the version history, you can preview each version, who made them, and when they were made. You can also revert to a previous version if needed.

<video src="https://mintcdn.com/resend/8sUIFX1U2gAd2pqE/images/templates-version-history.mp4?fit=max&auto=format&n=8sUIFX1U2gAd2pqE&q=85&s=31b1f60d7873113f5dcc7c84928118d2" autoPlay muted loop data-path="images/templates-version-history.mp4" />

Reverting creates a new draft based on the selected version's content, without affecting the published Template.

## Edit a Template

You can work on a new draft version of your published Template, update the design and messaging, then test it thoroughly before publishing it again.

Your email sending will continue to use the current published version until you're ready to make the switch, without the need to create a new separate Template or risk leaking information like your new logo.

This behavior is also useful to avoid breaking changes when you need to edit a Template that's in production. Add or remove variables, update the design, and more without affecting your existing emails or raising validation errors.

## API reference

For complete API documentation, see the [updating Templates API reference](/docs/api-reference/templates/update-template).
