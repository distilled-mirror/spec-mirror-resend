> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Retrieve Template

> Retrieve a template by ID.

## Path Parameters

<ParamField body="id | alias" type="string">
  The ID or alias of the template to retrieve.
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.templates.get(
    '34a080c9-b17d-4187-ad80-5af20266e535',
  );
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->templates->get('34a080c9-b17d-4187-ad80-5af20266e535');
  ```

  ```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  resend.Templates.get("34a080c9-b17d-4187-ad80-5af20266e535")
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  Resend::Templates.get("34a080c9-b17d-4187-ad80-5af20266e535")
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import (
  	"context"

  	"github.com/resend/resend-go/v4"
  )

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	client.Templates.GetWithContext(
  		context.TODO(),
  		"34a080c9-b17d-4187-ad80-5af20266e535",
  	)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _template = resend
      .templates
      .get("34a080c9-b17d-4187-ad80-5af20266e535")
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.Resend;
  import com.resend.core.exception.ResendException;
  import com.resend.services.templates.model.GetTemplateResponseSuccess;

  public class Main {
      public static void main(String[] args) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          GetTemplateResponseSuccess data = resend.templates().get("34a080c9-b17d-4187-ad80-5af20266e535");
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var res = await resend.TemplateRetrieveAsync( new Guid( "34a080c9-b17d-4187-ad80-5af20266e535" ) );
  Console.WriteLine( "Template Name={0}", res.Content.Name );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/templates/34a080c9-b17d-4187-ad80-5af20266e535' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend templates get 34a080c9-b17d-4187-ad80-5af20266e535
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "template",
    "id": "34a080c9-b17d-4187-ad80-5af20266e535",
    "current_version_id": "b2693018-7abb-4b4b-b4cb-aadf72dc06bd",
    "alias": "reset-password",
    "name": "reset-password",
    "created_at": "2026-10-06 23:47:56.678+00",
    "updated_at": "2026-10-06 23:47:56.678+00",
    "status": "published",
    "published_at": "2026-10-06 23:47:56.678+00",
    "from": "John Doe <john.doe@example.com>",
    "subject": "Hello, world!",
    "reply_to": null,
    "html": "<h1>Hello, world!</h1>",
    "text": "Hello, world!",
    "variables": [
      {
        "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
        "key": "user_name",
        "type": "string",
        "fallback_value": "John Doe",
        "created_at": "2026-10-06 23:47:56.678+00",
        "updated_at": "2026-10-06 23:47:56.678+00"
      }
    ],
    "has_unpublished_versions": true
  }
  ```
</ResponseExample>
