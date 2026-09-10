> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Attachments

> Retrieve a list of attachments from a received email.

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

<QueryParams type="attachments" isRequired={false} />

## Path Parameters

<ParamField path="email_id" type="string" required>
  The Email ID.
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.emails.receiving.attachments.list({
    emailId: '4ef9a417-02e9-4d39-ad75-9611e0fcc33c',
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->emails->receiving->attachments->list(
    emailId: '4ef9a417-02e9-4d39-ad75-9611e0fcc33c'
  );
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = 're_xxxxxxxxx'

  attachments = resend.Emails.Receiving.Attachments.list(
    email_id='4ef9a417-02e9-4d39-ad75-9611e0fcc33c'
  )
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require 'resend'

  Resend.api_key = 're_xxxxxxxxx'

  attachments = Resend::Emails::Receiving::Attachments.list(
    email_id: '4ef9a417-02e9-4d39-ad75-9611e0fcc33c'
  )
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  import (
  	"context"

  	"github.com/resend/resend-go/v3"
  )

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	client.Emails.Receiving.ListAttachmentsWithContext(
  		context.TODO(),
  		"4ef9a417-02e9-4d39-ad75-9611e0fcc33c",
  	)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{list_opts::ListOptions, Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _email = resend
      .receiving
      .list_attachments(
        "4ef9a417-02e9-4d39-ad75-9611e0fcc33c",
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

      ListAttachmentsResponse response = resend.receiving().listAttachments(
        "4ef9a417-02e9-4d39-ad75-9611e0fcc33c"
      );
    }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.ReceivedEmailAttachmentListAsync( new Guid( "4ef9a417-02e9-4d39-ad75-9611e0fcc33c" ));
  Console.WriteLine( "Nr Attachments={0}", resp.Content.Data.Count );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/emails/receiving/4ef9a417-02e9-4d39-ad75-9611e0fcc33c/attachments' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend emails receiving attachments 4ef9a417-02e9-4d39-ad75-9611e0fcc33c
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "list",
    "has_more": false,
    "data": [
      {
        "id": "2a0c9ce0-3112-4728-976e-47ddcd16a318",
        "filename": "avatar.png",
        "size": 4096,
        "content_type": "image/png",
        "content_disposition": "inline",
        "content_id": "img001",
        "download_url": "https://inbound-cdn.resend.com/4ef9a417-02e9-4d39-ad75-9611e0fcc33c/attachments/2a0c9ce0-3112-4728-976e-47ddcd16a318?some-params=example&signature=sig-123",
        "expires_at": "2026-10-17T14:29:41.521Z"
      }
    ]
  }
  ```
</ResponseExample>
