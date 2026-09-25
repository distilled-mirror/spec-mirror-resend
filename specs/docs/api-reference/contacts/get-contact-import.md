> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Retrieve Contact Import

> Retrieve a single contact import.

## Path Parameters

<ParamField path="id" type="string" required>
  The Contact Import ID.
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.contacts.imports.get(
    '479e3145-dd38-476b-932c-529ceb705947',
  );
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->contacts->imports->get('479e3145-dd38-476b-932c-529ceb705947');
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  resend.Contacts.Imports.get("479e3145-dd38-476b-932c-529ceb705947")
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  Resend::Contacts::Imports.get("479e3145-dd38-476b-932c-529ceb705947")
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v4"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	client.Contacts.Imports.Get("479e3145-dd38-476b-932c-529ceb705947")
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _data = resend
      .contacts
      .get_import("479e3145-dd38-476b-932c-529ceb705947")
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.Resend;
  import com.resend.services.contacts.model.GetContactImportResponseSuccess;

  public class Main {
      public static void main(String[] args) throws Exception {
          Resend resend = new Resend("re_xxxxxxxxx");

          GetContactImportResponseSuccess data = resend
                  .contacts()
                  .imports()
                  .get("479e3145-dd38-476b-932c-529ceb705947");
      }
  }
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/contacts/imports/479e3145-dd38-476b-932c-529ceb705947' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend contacts imports get 479e3145-dd38-476b-932c-529ceb705947
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "contact_import",
    "id": "479e3145-dd38-476b-932c-529ceb705947",
    "status": "completed",
    "created_at": "2026-05-15 18:32:37.823+00",
    "completed_at": "2026-05-15 18:33:42.916+00",
    "counts": {
      "total": 1200,
      "created": 800,
      "updated": 300,
      "skipped": 75,
      "failed": 25
    }
  }
  ```
</ResponseExample>
