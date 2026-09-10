> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Configure a custom Return Path

> Learn how to configure a custom Return Path for your verified domain in Resend.

By default, Resend uses the `send` subdomain for the Return-Path address.

<Info>
  Domains that show `CNAME` records for sending use your Return-Path subdomain
  for one record and an `r`-prefixed sibling for the other. With a Return-Path
  of `outbound`, you'll be shown records for both `outbound.example.com` and
  `routbound.example.com`, and both need to be added for the domain to fully
  verify.
</Info>

You can provide a custom Return-Path address when you [add a new domain in the Dashboard](/docs/add-a-domain) under **Advanced options**, or by setting the optional `custom_return_path` parameter when [creating or updating a domain via the API](/docs/api-reference/domains/create-domain) or with [a domains CLI command](/docs/cli#domains).

<img alt="Custom Return Path" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-custom-return-path.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=569a75fc160aad18116efc93bcebe148" width="3360" height="2100" data-path="images/dashboard-domains-resend-custom-return-path.png" />

For the API, optionally pass the custom return path parameter.

<CodeGroup>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  resend.domains.create({ name: 'example.com', customReturnPath: 'outbound' });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->domains->create([
    'name' => 'example.com',
    'custom_return_path' => 'outbound'
  ]);
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  params: resend.Domains.CreateParams = {
    "name": "example.com",
    "custom_return_path": "outbound"
  }

  resend.Domains.create(params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  Resend.api_key = ENV["RESEND_API_KEY"]

  params = {
    name: "example.com",
    custom_return_path: "outbound"
  }
  domain = Resend::Domains.create(params)
  puts domain
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v3"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	params := &resend.CreateDomainRequest{
  		Name:             "example.com",
  		CustomReturnPath: "outbound",
  	}

  	domain, err := client.Domains.Create(params)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{types::CreateDomainOptions, Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _domain = resend
      .domains
      .add(CreateDomainOptions::new("example.com").with_custom_return_path("outbound"))
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;

  public class Main {
      public static void main(String[] args) {
          Resend resend = new Resend("re_xxxxxxxxx");

          CreateDomainOptions params = CreateDomainOptions
                  .builder()
                  .name("example.com")
                  .customReturnPath("outbound")
                  .build();

          CreateDomainResponse domain = resend.domains().create(params);
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.DomainAddAsync( new DomainAddData {
     DomainName = "example.com",
     CustomReturnPath = "outbound"
  } );
  Console.WriteLine( "Domain Id={0}", resp.Content.Id );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/domains' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "name": "example.com",
    "custom_return_path": "outbound"
  }'
  ```
</CodeGroup>

Custom return paths must adhere to the following rules:

* Must be 63 characters or less.
* Must start with a letter, and end with a letter or number.
* Must contain only letters, numbers, and hyphens.

Avoid setting values that could undermine credibility (e.g. `testing`), as they may be exposed to recipients in some email clients.
