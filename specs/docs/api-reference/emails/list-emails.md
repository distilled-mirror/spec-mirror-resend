> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Sent Emails

> Retrieve a list of emails sent by your team.

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

You can list all emails sent by your team. The list returns references to individual emails. If needed, you can use the `id` of an email to retrieve the email HTML to plain text using the [Retrieve Email](/docs/api-reference/emails/retrieve-email) endpoint or the [Retrieve Attachments](/docs/api-reference/emails/list-email-attachments) endpoint to get an email's attachments.

<Info>
  This endpoint only returns emails sent by your team. If you need to list
  emails received by your domain, use the [List Received
  Emails](/docs/api-reference/emails/list-received-emails) endpoint.
</Info>

<QueryParams type="emails" isRequired={true} />

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.emails.list();
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->emails->list();
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"
  resend.Emails.list()
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  Resend.api_key = "re_xxxxxxxxx"
  emails = Resend::Emails.list
  puts emails
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import (
  	"context"

  	"github.com/resend/resend-go/v3"
  )

  func main() {
  	ctx := context.TODO()
  	client := resend.NewClient("re_xxxxxxxxx")

  	paginatedResp, err := client.Emails.ListWithOptions(ctx, nil)
  	if err != nil {
  		panic(err)
  	}

  	if paginatedResp.HasMore {
  		opts := &resend.ListOptions{
  			After: &paginatedResp.Data[len(paginatedResp.Data)-1].ID,
  		}
  		client.Emails.ListWithOptions(ctx, opts)
  	}
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{list_opts::ListOptions, Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _emails = resend.emails.list(ListOptions::default()).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;

  public class Main {
      public static void main(String[] args) {
          Resend resend = new Resend("re_xxxxxxxxx");

          ListEmailsResponseSuccess emails = resend.emails().list();
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.EmailListAsync();
  Console.WriteLine( "Count={0}", resp.Content.Data.Count );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/emails' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend emails list
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "list",
    "has_more": false,
    "data": [
      {
        "id": "4ef9a417-02e9-4d39-ad75-9611e0fcc33c",
        "message_id": "<111-222-333@email.example.com>",
        "to": ["delivered@resend.dev"],
        "from": "Acme <onboarding@resend.dev>",
        "created_at": "2026-04-03 22:13:42.674981+00",
        "subject": "Hello World",
        "bcc": null,
        "cc": null,
        "reply_to": null,
        "last_event": "delivered",
        "scheduled_at": null
      },
      {
        "id": "3a9f8c2b-1e5d-4f8a-9c7b-2d6e5f8a9c7b",
        "message_id": "<444-555-666@email.example.com>",
        "to": ["user@example.com"],
        "from": "Acme <onboarding@resend.dev>",
        "created_at": "2026-04-03 21:45:12.345678+00",
        "subject": "Welcome to Acme",
        "bcc": null,
        "cc": null,
        "reply_to": null,
        "last_event": "opened",
        "scheduled_at": null
      }
    ]
  }
  ```
</ResponseExample>
