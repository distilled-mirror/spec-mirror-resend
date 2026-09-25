> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Sender email addresses in Resend

> Learn how sending from an email address works on Resend.

Resend does not require you to “create an email address”, “set up a sender identity”, or “add a from-address” before sending.

Once a domain is verified in your Resend account, you can send from any email address at that domain.

<Info>
  The email address you send from does not need to exist in another system.
  However, we recommend using addresses that can receive replies.
</Info>

## How to add the sender address

You add the sender address in the `from` field when you send the email.

To include a friendly name, use the format `"Your Name <sender@example.com>"`.

<CodeGroup>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  await resend.emails.send({
    from: 'Acme <onboarding@example.com>',
    to: ['customer@example.com'],
    subject: 'Welcome to Acme',
    html: '<p>Thanks for signing up!</p>',
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->emails->send([
    'from' => 'Acme <onboarding@example.com>',
    'to' => ['customer@example.com'],
    'subject' => 'Welcome to Acme',
    'html' => '<p>Thanks for signing up!</p>'
  ]);
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  params: resend.Emails.SendParams = {
    "from": "Acme <onboarding@example.com>",
    "to": ["customer@example.com"],
    "subject": "Welcome to Acme",
    "html": "<p>Thanks for signing up!</p>"
  }

  email = resend.Emails.send(params)
  print(email)
  ```

  ```rb Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  params = {
    "from": "Acme <onboarding@example.com>",
    "to": ["customer@example.com"],
    "subject": "Welcome to Acme",
    "html": "<p>Thanks for signing up!</p>"
  }

  sent = Resend::Emails.send(params)
  puts sent
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import (
  	"context"
  	"fmt"

  	"github.com/resend/resend-go/v4"
  )

  func main() {
    ctx := context.TODO()
    client := resend.NewClient("re_xxxxxxxxx")

    params := &resend.SendEmailRequest{
        From:    "Acme <onboarding@example.com>",
        To:      []string{"customer@example.com"},
        Subject: "Welcome to Acme",
        Html:    "<p>Thanks for signing up!</p>",
    }

    sent, err := client.Emails.SendWithContext(ctx, params)

    if err != nil {
      panic(err)
    }
    fmt.Println(sent.Id)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::types::CreateEmailBaseOptions;
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let from = "Acme <onboarding@example.com>";
    let to = ["customer@example.com"];
    let subject = "Welcome to Acme";
    let html = "<p>Thanks for signing up!</p>";

    let email = CreateEmailBaseOptions::new(from, to, subject)
      .with_html(html);

    let _email = resend.emails.send(email).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;

  public class Main {
      public static void main(String[] args) {
          Resend resend = new Resend("re_xxxxxxxxx");

          CreateEmailOptions params = CreateEmailOptions.builder()
                  .from("Acme <onboarding@example.com>")
                  .to("customer@example.com")
                  .subject("Welcome to Acme")
                  .html("<p>Thanks for signing up!</p>")
                  .build();

          CreateEmailResponse data = resend.emails().send(params);
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.EmailSendAsync( new EmailMessage()
  {
      From = "Acme <onboarding@example.com>",
      To = "customer@example.com",
      Subject = "Welcome to Acme",
      HtmlBody = "<p>Thanks for signing up!</p>",
  } );
  Console.WriteLine( "Email Id={0}", resp.Content );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/emails' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "from": "Acme <onboarding@example.com>",
    "to": ["customer@example.com"],
    "subject": "Welcome to Acme",
    "html": "<p>Thanks for signing up!</p>"
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend emails send \
    --from "Acme <onboarding@example.com>" \
    --to customer@example.com \
    --subject "Welcome to Acme" \
    --html "<p>Thanks for signing up!</p>"
  ```
</CodeGroup>

In this example, `onboarding@example.com` is the sender address. As long as `example.com` is verified in Resend, you can use that address in `from` without creating it first.

## Common misconceptions

Some platforms require you to create, register, or pre-approve a sending address.\
Resend does not. After verifying your domain, you’re free to send from any address at that domain, such as `notifications@example.com` or `updates@example.com`. No extra setup, creation, or configuration of that address is needed.

## Getting started

To start sending emails with Resend:

1. [Sign up for a Resend account](https://resend.com/signup)
2. [Add and verify your domain](https://resend.com/domains)
3. [Create an API key](https://resend.com/api-keys)
4. Start sending emails immediately from any address at the domain you verified

If you're having trouble with domain verification or DNS records, see our [domain verification troubleshooting guide](/docs/knowledge-base/what-if-my-domain-is-not-verifying) or check our [DNS setup guides](/docs/knowledge-base/introduction) for your specific DNS provider.
