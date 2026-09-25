> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Retrieve Suppression

> Retrieve a single suppression by ID or email.

A suppression can be retrieved either by its ID or by the suppressed email
address.

## Path Parameters

<ParamField path="suppression" type="email | id" required>
  The Suppression ID or email address.
</ParamField>

The `source_id` in the response references the email that triggered the
suppression. For suppressions with a `manual` origin, `source_id` is `null`.

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.suppressions.get(
    'e169aa45-1ecf-4183-9955-b1499d5701d3', // or: 'steve.wozniak@example.com'
  );
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  // Retrieve by suppression id
  $resend->suppressions->get(
    'e169aa45-1ecf-4183-9955-b1499d5701d3'
  );

  // Retrieve by email
  $resend->suppressions->get(
    'steve.wozniak@example.com'
  );
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  # Retrieve by suppression id
  resend.Suppressions.get("e169aa45-1ecf-4183-9955-b1499d5701d3")

  # Retrieve by email
  resend.Suppressions.get("steve.wozniak@example.com")
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  # Retrieve by suppression id
  Resend::Suppressions.get("e169aa45-1ecf-4183-9955-b1499d5701d3")

  # Retrieve by email
  Resend::Suppressions.get("steve.wozniak@example.com")
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v4"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	// Retrieve by suppression id
  	client.Suppressions.Get("e169aa45-1ecf-4183-9955-b1499d5701d3")

  	// Retrieve by email
  	client.Suppressions.Get("steve.wozniak@example.com")
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _data = resend
      .suppressions
      .get("e169aa45-1ecf-4183-9955-b1499d5701d3")
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.Resend;
  import com.resend.core.exception.ResendException;

  public class Main {
      public static void main(String[] args) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          // Retrieve by suppression id
          resend.suppressions().get("e169aa45-1ecf-4183-9955-b1499d5701d3");

          // Retrieve by email
          resend.suppressions().get("steve.wozniak@example.com");
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

  // Retrieve by suppression id
  await resend.SuppressionRetrieveAsync( "e169aa45-1ecf-4183-9955-b1499d5701d3" );

  // Retrieve by email
  await resend.SuppressionRetrieveAsync( "steve.wozniak@example.com" );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  # Retrieve by suppression id
  curl -X GET 'https://api.resend.com/suppressions/e169aa45-1ecf-4183-9955-b1499d5701d3' \
       -H 'Authorization: Bearer re_xxxxxxxxx'

  # Retrieve by email
  curl -X GET 'https://api.resend.com/suppressions/steve.wozniak@example.com' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  # Retrieve by suppression id
  resend suppressions get e169aa45-1ecf-4183-9955-b1499d5701d3

  # Retrieve by email
  resend suppressions get steve.wozniak@example.com
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "suppression",
    "id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
    "email": "steve.wozniak@example.com",
    "origin": "bounce",
    "source_id": "4ef9a417-02e9-4d39-ad75-9611e0fcc33c",
    "created_at": "2026-10-06 23:47:56.678+00"
  }
  ```
</ResponseExample>
