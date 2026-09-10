> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Template

> Create a new template with optional variables.

export const ResendParamField = ({children, body, path, ...props}) => {
  const [lang, setLang] = useState(() => {
    return localStorage.getItem('code') || '"Node.js"';
  });
  useEffect(() => {
    const onStorage = event => {
      const key = event.detail.key;
      if (key === 'code') {
        setLang(event.detail.value);
      }
    };
    document.addEventListener('mintlify-localstorage', onStorage);
    return () => {
      document.removeEventListener('mintlify-localstorage', onStorage);
    };
  }, []);
  const toCamelCase = str => typeof str === 'string' ? str.replace(/[_-](\w)/g, (_, c) => c.toUpperCase()) : str;
  const resolvedBody = useMemo(() => {
    const value = JSON.parse(lang);
    return value === 'Node.js' ? toCamelCase(body) : body;
  }, [body, lang]);
  const resolvedPath = useMemo(() => {
    const value = JSON.parse(lang);
    return value === 'Node.js' ? toCamelCase(path) : path;
  }, [path, lang]);
  return <ParamField body={resolvedBody} path={resolvedPath} {...props}>
      {children}
    </ParamField>;
};

## Body Parameters

<ParamField body="name" type="string" required>
  The name of the template.
</ParamField>

<ParamField body="html" type="string" required>
  The HTML version of the template.
</ParamField>

<ParamField body="alias" type="string">
  The alias of the template.
</ParamField>

<ParamField body="from" type="string">
  Sender email address.

  To include a friendly name, use the format `"Your Name <sender@domain.com>"`.

  If provided, this value can be overridden when sending an email using the template.
</ParamField>

<ParamField body="subject" type="string">
  Default email subject.

  This value can be overridden when sending an email using the template.
</ParamField>

<ResendParamField body="reply_to" type="string | string[]">
  Default Reply-to email address. For multiple addresses, send as an array of strings.

  This value can be overridden when sending an email using the template.
</ResendParamField>

<ParamField body="text" type="string">
  The plain text version of the message.

  <Info>
    If not provided, the HTML will be used to generate a plain text version. You can opt out of this behavior by setting value to an empty string.
  </Info>
</ParamField>

<ParamField body="react" type="React.ReactNode">
  The React component used to write the template. *Only available in the Node.js
  SDK.*
</ParamField>

<ParamField body="variables" type="array">
  The array of variables used in the template. Each template may contain up to 50 variables.

  Each variable is an object with the following properties:

  <Expandable defaultOpen title="properties">
    <ParamField body="key" type="string" required>
      The key of the variable. We recommend capitalizing the key (e.g. `PRODUCT_NAME`). The following variable names are reserved and cannot be used:
      `FIRST_NAME`, `LAST_NAME`, `EMAIL`, `RESEND_UNSUBSCRIBE_URL`, `contact`, and `this`.
    </ParamField>

    <ParamField body="type" type="'string' | 'number'" required>
      The type of the variable.

      Can be `'string'` or `'number'`
    </ParamField>

    <ResendParamField body="fallback_value" type="string | number">
      The fallback value of the variable. The value must match the type of the variable.

      If no fallback value is provided, you must provide a value for the variable when sending an email using the template.
    </ResendParamField>
  </Expandable>

  <Info>
    Before you can use a template, you must publish it first. To publish a
    template, use the [Templates dashboard](https://resend.com/templates) or
    [publish template API](/docs/api-reference/templates/publish-template).

    [Learn more about Templates](/docs/dashboard/templates/introduction).
  </Info>
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.templates.create({
    name: 'order-confirmation',
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
        fallbackValue: 25,
      }
    ],
  });

  // Or create and publish a template in one step
  await resend.templates.create({ ... }).publish();
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->templates->create([
    'name' => 'order-confirmation',
    'html' => '<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>',
    'variables' => [
      [
        'key' => 'PRODUCT',
        'type' => 'string',
        'fallback_value' => 'item',
      ],
      [
        'key' => 'PRICE',
        'type' => 'number',
        'fallback_value' => 25,
      ]
    ],
  ]);
  ```

  ```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  resend.Templates.create({
      "name": "order-confirmation",
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
              "fallback_value": 25,
          }
      ],
  })
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  Resend::Templates.create(
    name: "order-confirmation",
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
        fallback_value: 25
      }
    ]
  )
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import (
  	"context"

  	"github.com/resend/resend-go/v3"
  )

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	client.Templates.CreateWithContext(context.TODO(), &resend.CreateTemplateRequest{
  		Name: "order-confirmation",
  		Html: "<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>",
  		Variables: []*resend.TemplateVariable{
  			{
  				Key:           "PRODUCT",
  				Type:          resend.VariableTypeString,
  				FallbackValue: "item",
  			},
  			{
  				Key:           "PRICE",
  				Type:          resend.VariableTypeNumber,
  				FallbackValue: 25,
  			},
  		},
  	})
  }
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
    let html = "<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>";

    let variables = [
      Variable::new("PRODUCT", VariableType::String).with_fallback("item"),
      Variable::new("PRICE", VariableType::Number).with_fallback(25)
    ];

    let opts = CreateTemplateOptions::new(name, html).with_variables(&variables);
    let template = resend.templates.create(opts).await?;

    let _published = resend.templates.publish(&template.id).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;

  public class Main {
      public static void main(String[] args) {
          Resend resend = new Resend("re_xxxxxxxxx");

          CreateTemplateOptions params = CreateTemplateOptions.builder()
                  .name("order-confirmation")
                  .html("<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>")
                  .addVariable(new Variable("PRODUCT", VariableType.STRING, "item"))
                  .addVariable(new Variable("PRICE", VariableType.NUMBER, 25))
                  .build();

          CreateTemplateResponseSuccess data = resend.templates().create(params);
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create("re_xxxxxxxxx");

  var variables = new List<TemplateVariable>()
  {
    new TemplateVariable() {
      Key = "PRODUCT",
      Type = TemplateVariableType.String,
      Default = "item",
    },
    new TemplateVariable() {
      Key = "PRICE",
      Type = TemplateVariableType.Number,
      Default = 25,
    }
  };

  var resp = await resend.TemplateCreateAsync(
    new TemplateData()
    {
      Name = "welcome-email",
      HtmlBody = "<strong>Hey, {{{PRODUCT}}}, you are {{{PRICE}}} years old.</strong>",
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
        "fallback_value": 25
      }
    ]
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend templates create \
    --name order-confirmation \
    --html "<p>Name: {{{PRODUCT}}}</p><p>Total: {{{PRICE}}}</p>" \
    --var PRODUCT:string:item \
    --var PRICE:number:25
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "id": "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794",
    "object": "template"
  }
  ```
</ResponseExample>
