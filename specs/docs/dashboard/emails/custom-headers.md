> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Custom Headers

> Customize how emails are sent with your own headers.

Email headers are typically hidden from the end user but are crucial for deliverability. They include information about the sender, receiver, timestamp, and more.

Resend already includes all the necessary headers for you, but now you can also add your own custom headers.

This is a fairly advanced feature, but it can be useful for a few things:

* Prevent threading on Gmail with the **`X-Entity-Ref-ID`** header ([Example](https://github.com/resend/resend-examples/tree/main/nextjs-resend-examples/typescript/src/app/prevent-threading))
* Include a shortcut for users to unsubscribe with the **`List-Unsubscribe`** header

Here's how you can add custom headers to your emails:

<CodeGroup>
  ```ts Node.js {11} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  await resend.emails.send({
    from: 'Acme <onboarding@resend.dev>',
    to: ['delivered@resend.dev'],
    subject: 'hello world',
    html: '<p>it works!</p>',
    headers: {
      'X-Entity-Ref-ID': 'xxx_xxxx',
    },
  });
  ```

  ```php PHP {9} theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->emails->send([
    'from' => 'Acme <onboarding@resend.dev>',
    'to' => ['delivered@resend.dev'],
    'subject' => 'hello world',
    'html' => '<p>it works!</p>',
    'headers' => [
      'X-Entity-Ref-ID' => 'xxx_xxxx',
    ]
  ]);
  ```

  ```python Python {11} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  params: resend.Emails.SendParams = {
    "from": "onboarding@resend.dev",
    "to": ["delivered@resend.dev"],
    "subject": "hi",
    "html": "<p>it works!</p>",
    "headers": {
      "X-Entity-Ref-ID": "xxx_xxxx"
    }
  }

  email = resend.Emails.send(params)
  print(email)
  ```

  ```rb Ruby {11} theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  params = {
    "from": "Acme <onboarding@resend.dev>",
    "to": ["delivered@resend.dev"],
    "subject": "hello world",
    "html": "<p>it works!</p>",
    "headers": {
      "X-Entity-Ref-ID": "123"
    },
  }

  sent = Resend::Emails.send(params)
  puts sent
  ```

  ```go Go {20} theme={"theme":{"light":"github-light","dark":"vesper"}}
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
        From:        "Acme <onboarding@resend.dev>",
        To:          []string{"delivered@resend.dev"},
        Subject:     "hello world",
        Html:        "<p>it works!</p>",
        Headers:     map[string]string{
          "X-Entity-Ref-ID": "xxx_xxxx",
        },
    }

    sent, err := client.Emails.SendWithContext(ctx, params)

    if err != nil {
      panic(err)
    }
    fmt.Println(sent.Id)
  }
  ```

  ```rust Rust {14} theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::types::{Attachment, CreateEmailBaseOptions, Tag};
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let from = "Acme <onboarding@resend.dev>";
    let to = ["delivered@resend.dev"];
    let subject = "hello world";

    let email = CreateEmailBaseOptions::new(from, to, subject)
      .with_html("<p>it works!</p>")
      .with_header("X-Entity-Ref-ID", "xxx_xxxx");

    let _email = resend.emails.send(email).await?;

    Ok(())
  }
  ```

  ```java Java {17} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;
  import com.resend.core.exception.ResendException;
  import com.resend.services.emails.model.CreateEmailOptions;
  import com.resend.services.emails.model.CreateEmailResponse;
  import java.util.Map;

  public class Main {
      public static void main(String[] args) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          CreateEmailOptions params = CreateEmailOptions.builder()
                  .from("Acme <onboarding@resend.dev>")
                  .to("delivered@resend.dev")
                  .subject("hello world")
                  .html("<p>it works!</p>")
                  .headers(Map.of(
                      "X-Entity-Ref-ID", "xxx_xxxx"
                  ))
                  .build();

          CreateEmailResponse data = resend.emails().send(params);
      }
  }
  ```

  ```csharp .NET {12-15} theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;
  using System.Collections.Generic;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var message = new EmailMessage()
  {
      From = "Acme <onboarding@resend.dev>",
      To = "delivered@resend.dev",
      Subject = "hello world",
      HtmlBody = "<p>it works!</p>",
      Headers = new Dictionary<string, string>()
      {
          { "X-Entity-Ref-ID", "xxx_xxxx" },
      },
  };

  var resp = await resend.EmailSendAsync( message );
  Console.WriteLine( "Email Id={0}", resp.Content );
  ```

  ```bash cURL {10} theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/emails' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "from": "Acme <onboarding@resend.dev>",
    "to": ["delivered@resend.dev"],
    "subject": "hello world",
    "html": "<p>it works!</p>",
    "headers": {
      "X-Entity-Ref-ID": "xxx_xxxx"
    }
  }'
  ```

  ```bash CLI {6} theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend emails send \
    --from "Acme <onboarding@resend.dev>" \
    --to delivered@resend.dev \
    --subject "hello world" \
    --html "<p>it works!</p>" \
    --headers "X-Entity-Ref-ID=xxx_xxxx"
  ```
</CodeGroup>
