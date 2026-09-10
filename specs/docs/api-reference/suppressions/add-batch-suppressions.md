> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Add Batch Suppressions

> Add up to 100 email addresses to the suppression list at once.

## Body Parameters

<ParamField body="emails" type="array" required>
  The email addresses to suppress. Must contain between 1 and 100 email
  addresses.
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.suppressions.batch.add({
    emails: ['steve.wozniak@example.com', 'susan.kare@example.com'],
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->suppressions->batch->add([
    'emails' => ['steve.wozniak@example.com', 'susan.kare@example.com'],
  ]);
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  params: resend.Suppressions.Batch.AddParams = {
    "emails": ["steve.wozniak@example.com", "susan.kare@example.com"],
  }

  resend.Suppressions.Batch.add(params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  Resend::Suppressions::Batch.add(
    emails: ["steve.wozniak@example.com", "susan.kare@example.com"]
  )
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v3"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	params := &resend.BatchAddSuppressionsRequest{
  		Emails: []string{"steve.wozniak@example.com", "susan.kare@example.com"},
  	}

  	client.Suppressions.Batch.Add(params)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::types::BatchAddSuppressionOptions;
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let opts =
      BatchAddSuppressionOptions::from(vec!["steve.wozniak@example.com", "susan.kare@example.com"]);
    let _data = resend.suppressions.batch_add(opts).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;
  import com.resend.services.suppressions.model.AddSuppressionsOptions;
  import java.util.List;

  public class Main {
      public static void main(String[] args) {
          Resend resend = new Resend("re_xxxxxxxxx");

          AddSuppressionsOptions options = AddSuppressionsOptions.builder()
                  .emails(List.of("steve.wozniak@example.com", "susan.kare@example.com"))
                  .build();

          resend.suppressions().batch().add(options);
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

  var resp = await resend.SuppressionBatchAddAsync( new[]
  {
      "steve.wozniak@example.com",
      "susan.kare@example.com",
  } );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/suppressions/batch/add' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "emails": ["steve.wozniak@example.com", "susan.kare@example.com"]
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend suppressions batch add --file suppressions.json
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "data": [
      {
        "object": "suppression",
        "id": "e169aa45-1ecf-4183-9955-b1499d5701d3"
      },
      {
        "object": "suppression",
        "id": "520784e2-887d-4c25-b53c-4ad46ad38100"
      }
    ]
  }
  ```
</ResponseExample>
