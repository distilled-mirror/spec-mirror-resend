> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Templates

> List all templates.

export const QueryParams = ({type, isRequired}) => {
  return <>
      <h2>Query Parameters</h2>

      {isRequired ? <ParamField query="limit" type="number">
          Number of {type} to retrieve.
          <ul>
            <li>
              Default value: <code>20</code>
            </li>
            <li>
              Maximum value: <code>100</code>
            </li>
            <li>
              Minimum value: <code>1</code>
            </li>
          </ul>
        </ParamField> : <>
          <p>
            Note that the <code>limit</code> parameter is <em>optional</em>. If
            you do not provide a <code>limit</code>, all {type} will be returned
            in a single response.
          </p>
          <ParamField query="limit" type="number">
            Number of {type} to retrieve.
            <ul>
              <li>
                Maximum value: <code>100</code>
              </li>
              <li>
                Minimum value: <code>1</code>
              </li>
            </ul>
          </ParamField>
        </>}

      <ParamField query="after" type="string">
        The ID <em>after</em> which we'll retrieve more {type} (for pagination).
        This ID will <em>not</em> be included in the returned list. Cannot be
        used with the
        <code>before</code> parameter.
      </ParamField>
      <ParamField query="before" type="string">
        The ID <em>before</em> which we'll retrieve more {type} (for
        pagination). This ID will <em>not</em> be included in the returned list.
        Cannot be used with the <code>after</code> parameter.
      </ParamField>
      <Info>
        You can only use either <code>after</code> or <code>before</code>{' '}
        parameter, not both. See our{' '}
        <a href="/docs/api-reference/pagination">pagination guide</a> for more
        information.
      </Info>
    </>;
};

By default, the API will return the most recent 20 templates. You can optionally use the `limit` parameter to return a different number of templates or control the pagination of the results with the `after` or `before` parameters.

<QueryParams type="templates" isRequired={true} />

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.templates.list({
    limit: 2,
    after: '34a080c9-b17d-4187-ad80-5af20266e535',
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->templates->list([
    'limit' => 2,
    'after' => '34a080c9-b17d-4187-ad80-5af20266e535'
  ]);
  ```

  ```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  resend.Templates.list({
      "limit": 2,
      "after": "34a080c9-b17d-4187-ad80-5af20266e535",
  })
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  Resend::Templates.list(
    limit: 2,
    after: "34a080c9-b17d-4187-ad80-5af20266e535"
  )
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  import (
  	"context"

  	"github.com/resend/resend-go/v3"
  )

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	client.Templates.ListWithContext(context.TODO(), &resend.ListOptions{
  		Limit: 2,
  		After: "34a080c9-b17d-4187-ad80-5af20266e535",
  	})
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{list_opts::ListOptions, Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let list_opts = ListOptions::default()
      .with_limit(2)
      .list_after("34a080c9-b17d-4187-ad80-5af20266e535");

    let _list = resend.templates.list(list_opts).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;

  public class Main {
      public static void main(String[] args) {
          Resend resend = new Resend("re_xxxxxxxxx");

          ListParams params = ListParams.builder()
              .limit(2)
              .after("34a080c9-b17d-4187-ad80-5af20266e535")
              .build();

          ListTemplatesResponseSuccess data = resend.templates().list(params);
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.TemplateListAsync();
  Console.WriteLine( "Nr Templates={0}", resp.Content.Data.Count );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/templates?limit=2&after=34a080c9-b17d-4187-ad80-5af20266e535' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend templates list
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "list",
    "data": [
      {
        "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
        "name": "reset-password",
        "status": "draft",
        "published_at": null,
        "created_at": "2026-10-06 23:47:56.678+00",
        "updated_at": "2026-10-06 23:47:56.678+00",
        "alias": "reset-password"
      },
      {
        "id": "b7f9c2e1-1234-4abc-9def-567890abcdef",
        "name": "welcome-message",
        "status": "published",
        "published_at": "2026-10-06 23:47:56.678+00",
        "created_at": "2026-10-06 23:47:56.678+00",
        "updated_at": "2026-10-06 23:47:56.678+00",
        "alias": "welcome-message"
      }
    ],
    "has_more": false
  }
  ```
</ResponseExample>
