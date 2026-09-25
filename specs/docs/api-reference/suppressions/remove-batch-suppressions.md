> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Remove Batch Suppressions

> Remove up to 100 suppressions from the suppression list at once.

## Body Parameters

Provide either `emails` or `ids`, but not both.

<ParamField body="emails" type="array">
  The email addresses to remove from the suppression list. Must contain between
  1 and 100 email addresses.
</ParamField>

<ParamField body="ids" type="array">
  The suppression IDs to remove from the suppression list. Must contain between
  1 and 100 IDs.
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.suppressions.batch.remove({
    ids: ['e169aa45-1ecf-4183-9955-b1499d5701d3'],
    // or: emails: ['steve.wozniak@example.com', 'susan.kare@example.com'],
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  // Remove by suppression ids
  $resend->suppressions->batch->remove([
    'ids' => ['e169aa45-1ecf-4183-9955-b1499d5701d3'],
  ]);

  // Remove by emails
  $resend->suppressions->batch->remove([
    'emails' => ['steve.wozniak@example.com', 'susan.kare@example.com'],
  ]);
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  # Remove by suppression ids
  ids_params: resend.Suppressions.Batch.RemoveParams = {
    "ids": ["e169aa45-1ecf-4183-9955-b1499d5701d3"],
  }

  resend.Suppressions.Batch.remove(ids_params)

  # Remove by emails
  emails_params: resend.Suppressions.Batch.RemoveParams = {
    "emails": ["steve.wozniak@example.com", "susan.kare@example.com"],
  }

  resend.Suppressions.Batch.remove(emails_params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  # Remove by suppression ids
  Resend::Suppressions::Batch.remove(
    ids: ["e169aa45-1ecf-4183-9955-b1499d5701d3"]
  )

  # Remove by emails
  Resend::Suppressions::Batch.remove(
    emails: ["steve.wozniak@example.com", "susan.kare@example.com"]
  )
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v4"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	// Remove by suppression ids
  	client.Suppressions.Batch.Remove(&resend.BatchRemoveSuppressionsRequest{
  		Ids: []string{"e169aa45-1ecf-4183-9955-b1499d5701d3"},
  	})

  	// Remove by emails
  	client.Suppressions.Batch.Remove(&resend.BatchRemoveSuppressionsRequest{
  		Emails: []string{"steve.wozniak@example.com", "susan.kare@example.com"},
  	})
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{Resend, Result, types::BatchRemoveSuppressionOptions};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    // Remove by email
    let opt_emails = BatchRemoveSuppressionOptions::new()
      .add_emails(vec!["steve.wozniak@example.com", "susan.kare@example.com"]);
    let _data = resend.suppressions.batch_remove(opt_emails).await?;

    // Remove by id
    let opt_ids =
      BatchRemoveSuppressionOptions::new().add_ids(vec!["e169aa45-1ecf-4183-9955-b1499d5701d3"]);

    let _data = resend.suppressions.batch_remove(opt_ids).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.Resend;
  import com.resend.core.exception.ResendException;
  import com.resend.services.suppressions.model.RemoveSuppressionsOptions;
  import java.util.List;

  public class Main {
      public static void main(String[] args) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          // Remove by suppression ids
          RemoveSuppressionsOptions byIds = RemoveSuppressionsOptions.builder()
                  .ids(List.of("e169aa45-1ecf-4183-9955-b1499d5701d3"))
                  .build();

          resend.suppressions().batch().remove(byIds);

          // Remove by emails
          RemoveSuppressionsOptions byEmails = RemoveSuppressionsOptions.builder()
                  .emails(List.of("steve.wozniak@example.com", "susan.kare@example.com"))
                  .build();

          resend.suppressions().batch().remove(byEmails);
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

  // Remove by suppression ids
  await resend.SuppressionBatchRemoveAsync( new[]
  {
      new Guid( "e169aa45-1ecf-4183-9955-b1499d5701d3" ),
  } );

  // Remove by emails
  await resend.SuppressionBatchRemoveAsync( new[]
  {
      "steve.wozniak@example.com",
      "susan.kare@example.com",
  } );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  # Remove by suppression ids
  curl -X POST 'https://api.resend.com/suppressions/batch/remove' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "ids": ["e169aa45-1ecf-4183-9955-b1499d5701d3"]
  }'

  # Remove by emails
  curl -X POST 'https://api.resend.com/suppressions/batch/remove' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "emails": ["steve.wozniak@example.com", "susan.kare@example.com"]
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  # Remove by email
  resend suppressions batch remove --file suppressions.json

  # Remove by id
  resend suppressions batch remove --file suppression-ids.json --ids
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "data": [
      {
        "object": "suppression",
        "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
        "deleted": true
      }
    ]
  }
  ```
</ResponseExample>
