> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Remove Suppression

> Remove a single suppression by ID or email.

## Path Parameters

<ParamField path="suppression" type="email | id" required>
  The Suppression ID or email address.
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  // Remove by suppression id
  const { data, error } = await resend.suppressions.remove(
    'e169aa45-1ecf-4183-9955-b1499d5701d3',
  );

  // Remove by email
  const { data, error } = await resend.suppressions.remove(
    'steve.wozniak@example.com',
  );
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  // Remove by suppression id
  $resend->suppressions->remove(
    'e169aa45-1ecf-4183-9955-b1499d5701d3'
  );

  // Remove by email
  $resend->suppressions->remove(
    'steve.wozniak@example.com'
  );
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  # Remove by suppression id
  resend.Suppressions.remove("e169aa45-1ecf-4183-9955-b1499d5701d3")

  # Remove by email
  resend.Suppressions.remove("steve.wozniak@example.com")
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  # Remove by suppression id
  Resend::Suppressions.remove("e169aa45-1ecf-4183-9955-b1499d5701d3")

  # Remove by email
  Resend::Suppressions.remove("steve.wozniak@example.com")
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v3"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	// Remove by suppression id
  	client.Suppressions.Remove("e169aa45-1ecf-4183-9955-b1499d5701d3")

  	// Remove by email
  	client.Suppressions.Remove("steve.wozniak@example.com")
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    // Remove by suppression id
    let _data = resend
      .suppressions
      .remove("e169aa45-1ecf-4183-9955-b1499d5701d3")
      .await?;

    // Remove by email
    let _data = resend
      .suppressions
      .remove("steve.wozniak@example.com")
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;

  public class Main {
      public static void main(String[] args) {
          Resend resend = new Resend("re_xxxxxxxxx");

          // Remove by suppression id
          resend.suppressions().remove("e169aa45-1ecf-4183-9955-b1499d5701d3");

          // Remove by email
          resend.suppressions().remove("steve.wozniak@example.com");
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

  // Remove by suppression id
  await resend.SuppressionRemoveAsync( "e169aa45-1ecf-4183-9955-b1499d5701d3" );

  // Remove by email
  await resend.SuppressionRemoveAsync( "steve.wozniak@example.com" );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  # Remove by suppression id
  curl -X DELETE 'https://api.resend.com/suppressions/e169aa45-1ecf-4183-9955-b1499d5701d3' \
       -H 'Authorization: Bearer re_xxxxxxxxx'

  # Remove by email
  curl -X DELETE 'https://api.resend.com/suppressions/steve.wozniak@example.com' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  # Remove by suppression id
  resend suppressions delete e169aa45-1ecf-4183-9955-b1499d5701d3

  # Remove by email
  resend suppressions delete steve.wozniak@example.com
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "suppression",
    "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
    "deleted": true
  }
  ```
</ResponseExample>
