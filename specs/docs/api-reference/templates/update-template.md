> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Template

> Update a template.

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

## Path Parameters

<ParamField body="id | alias" type="string">
  The ID or alias of the template to duplicate.
</ParamField>

## Body Parameters

<ParamField body="name" type="string">
  The name of the template.
</ParamField>

<ParamField body="html" type="string">
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

  const { data, error } = await resend.templates.update(
    '34a080c9-b17d-4187-ad80-5af20266e535',
    {
      name: 'order-confirmation',
      html: '<p>Total: {{{PRICE}}}</p><p>Name: {{{PRODUCT}}}</p>',
    },
  );
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->templates->update('34a080c9-b17d-4187-ad80-5af20266e535', [
    'name' => 'order-confirmation',
    'html' => '<p>Total: {{{PRICE}}}</p><p>Name: {{{PRODUCT}}}</p>',
  ]);
  ```

  ```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  resend.Templates.update({
      "id": "34a080c9-b17d-4187-ad80-5af20266e535",
      "name": "order-confirmation",
      "html": "<p>Total: {{{PRICE}}}</p><p>Name: {{{PRODUCT}}}</p>",
  })
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  Resend::Templates.update("34a080c9-b17d-4187-ad80-5af20266e535", {
    name: "order-confirmation",
    html: "<p>Total: {{{PRICE}}}</p><p>Name: {{{PRODUCT}}}</p>"
  })
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import (
  	"context"

  	"github.com/resend/resend-go/v4"
  )

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	client.Templates.UpdateWithContext(context.TODO(), "34a080c9-b17d-4187-ad80-5af20266e535", &resend.UpdateTemplateRequest{
  		Name: "order-confirmation",
  		Html: "<p>Total: {{{PRICE}}}</p><p>Name: {{{PRODUCT}}}</p>",
  	})
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{
    types::UpdateTemplateOptions,
    Resend, Result,
  };

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let name = "order-confirmation";
    let html = "<p>Total: {{{PRICE}}}</p><p>Name: {{{PRODUCT}}}</p>";

    let update = UpdateTemplateOptions::new(name, html);

    let _template = resend
      .templates
      .update("34a080c9-b17d-4187-ad80-5af20266e535", update)
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.Resend;
  import com.resend.core.exception.ResendException;
  import com.resend.services.templates.model.UpdateTemplateOptions;
  import com.resend.services.templates.model.UpdateTemplateResponseSuccess;

  public class Main {
      public static void main(String[] args) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          UpdateTemplateOptions params = UpdateTemplateOptions.builder()
                  .name("order-confirmation")
                  .html("<p>Total: {{{PRICE}}}</p><p>Name: {{{PRODUCT}}}</p>")
                  .build();

          UpdateTemplateResponseSuccess data = resend.templates().update("34a080c9-b17d-4187-ad80-5af20266e535", params);
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  await resend.TemplateUpdateAsync(
      templateId: new Guid( "e169aa45-1ecf-4183-9955-b1499d5701d3" ),
      new TemplateData()
      {
          HtmlBody = "<p>Total: {{{PRICE}}}</p><p>Name: {{{PRODUCT}}}</p>",
      }
  );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X PATCH 'https://api.resend.com/templates/34a080c9-b17d-4187-ad80-5af20266e535' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "name": "order-confirmation",
    "html": "<p>Total: {{{PRICE}}}</p><p>Name: {{{PRODUCT}}}</p>"
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend templates update 34a080c9-b17d-4187-ad80-5af20266e535 \
    --name order-confirmation \
    --html "<p>Total: {{{PRICE}}}</p><p>Name: {{{PRODUCT}}}</p>"
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "template",
    "id": "34a080c9-b17d-4187-ad80-5af20266e535"
  }
  ```
</ResponseExample>
