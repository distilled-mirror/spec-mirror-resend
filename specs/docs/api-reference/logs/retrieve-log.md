> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Retrieve Log

> Retrieve a single API request log.

## Path Parameters

<ParamField path="log_id" type="string" required>
  The Log ID.
</ParamField>

<Info>
  The `request_body` and `response_body` fields vary depending on the original
  API request that was logged.
</Info>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.logs.get(
    '37e4414c-5e25-4dbc-a071-43552a4bd53b',
  );
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->logs->get('37e4414c-5e25-4dbc-a071-43552a4bd53b');
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  resend.Logs.get("37e4414c-5e25-4dbc-a071-43552a4bd53b")
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  Resend.api_key = "re_xxxxxxxxx"

  log = Resend::Logs.get("37e4414c-5e25-4dbc-a071-43552a4bd53b")
  puts log
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v3"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	client.Logs.Get("37e4414c-5e25-4dbc-a071-43552a4bd53b")
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _logs = resend
      .logs
      .get("37e4414c-5e25-4dbc-a071-43552a4bd53b")
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;

  public class Main {
      public static void main(String[] args) {
          Resend resend = new Resend("re_xxxxxxxxx");

          resend.logs().get("37e4414c-5e25-4dbc-a071-43552a4bd53b");
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.LogRetrieveAsync( new Guid( "37e4414c-5e25-4dbc-a071-43552a4bd53b" ) );
  Console.WriteLine( "Endpoint={0}", resp.Content.Endpoint );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/logs/37e4414c-5e25-4dbc-a071-43552a4bd53b' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend logs get 37e4414c-5e25-4dbc-a071-43552a4bd53b
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "log",
    "id": "37e4414c-5e25-4dbc-a071-43552a4bd53b",
    "created_at": "2026-03-30 13:43:54.622865+00",
    "endpoint": "/emails",
    "method": "POST",
    "response_status": 200,
    "user_agent": "resend-node:6.0.3",
    "request_body": {
      "from": "Acme <onboarding@resend.dev>",
      "to": ["delivered@resend.dev"],
      "subject": "Hello World"
    },
    "response_body": {
      "id": "4ef9a417-02e9-4d39-ad75-9611e0fcc33c"
    }
  }
  ```
</ResponseExample>
