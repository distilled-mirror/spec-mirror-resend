> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Attachments

> Send emails with attachments.

There are two ways to send attachments:

1. [From a remote file](#send-attachments-from-a-remote-file)
2. [From a local file](#send-attachments-from-a-local-file)

<Info>
  We currently do not support sending attachments [when using our batch
  endpoint](/docs/api-reference/emails/send-batch-emails).
</Info>

## Send attachments from a remote file

Include the `path` parameter to send attachments from a remote file. This parameter accepts a URL to the file you want to attach.

Define the file name that will be attached using the `filename` parameter.

<CodeGroup>
  ```ts Node.js {12-13} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  await resend.emails.send({
    from: 'Acme <onboarding@resend.dev>',
    to: ['delivered@resend.dev'],
    subject: 'Receipt for your payment',
    html: '<p>Thanks for the payment</p>',
    attachments: [
      {
        path: 'https://resend.com/static/sample/invoice.pdf',
        filename: 'invoice.pdf',
      },
    ],
  });
  ```

  ```php PHP {10-11} theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->emails->send([
    'from' => 'Acme <onboarding@resend.dev>',
    'to' => ['delivered@resend.dev'],
    'subject' => 'Receipt for your payment',
    'html' => '<p>Thanks for the payment</p>',
    'attachments' => [
      [
        'path' => 'https://resend.com/static/sample/invoice.pdf',
        'filename' => 'invoice.pdf'
      ]
    ]
  ]);
  ```

  ```python Python {6-7} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  attachment: resend.RemoteAttachment = {
    "path": "https://resend.com/static/sample/invoice.pdf",
    "filename": "invoice.pdf",
  }

  params: resend.Emails.SendParams = {
    "from": "Acme <onboarding@resend.dev>",
    "to": ["delivered@resend.dev"],
    "subject": "Receipt for your payment",
    "html": "<p>Thanks for the payment</p>",
    "attachments": [attachment],
  }

  resend.Emails.send(params)
  ```

  ```rb Ruby {12-13} theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  params = {
    "from": "Acme <onboarding@resend.dev>",
    "to": ["delivered@resend.dev"],
    "subject": "Receipt for your payment",
    "html": "<p>Thanks for the payment</p>",
    "attachments": [
      {
        "path": "https://resend.com/static/sample/invoice.pdf",
        "filename": 'invoice.pdf',
      }
    ]
  }

  Resend::Emails.send(params)
  ```

  ```go Go {15-16} theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import (
  	"context"
  	"fmt"

  	"github.com/resend/resend-go/v4"
  )

  func main() {
    ctx := context.TODO()
    client := resend.NewClient("re_xxxxxxxxx")

    attachment := &resend.Attachment{
      Path:  "https://resend.com/static/sample/invoice.pdf",
      Filename: "invoice.pdf",
    }

    params := &resend.SendEmailRequest{
        From:        "Acme <onboarding@resend.dev>",
        To:          []string{"delivered@resend.dev"},
        Subject:     "Receipt for your payment",
        Html:        "<p>Thanks for the payment</p>",
        Attachments: []*resend.Attachment{attachment},
    }

    sent, err := client.Emails.SendWithContext(ctx, params)

    if err != nil {
      panic(err)
    }
    fmt.Println(sent.Id)
  }
  ```

  ```rust Rust {12-13} theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::types::{CreateAttachment, CreateEmailBaseOptions};
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let from = "Acme <onboarding@resend.dev>";
    let to = ["delivered@resend.dev"];
    let subject = "Receipt for your payment";

    let path = "https://resend.com/static/sample/invoice.pdf";
    let filename = "invoice.pdf";

    let email = CreateEmailBaseOptions::new(from, to, subject)
      .with_html("<p>Thanks for the payment</p>")
      .with_attachment(CreateAttachment::from_path(path).with_filename(filename));

    let _email = resend.emails.send(email).await?;

    Ok(())
  }
  ```

  ```java Java {12-13} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;
  import com.resend.core.exception.ResendException;
  import com.resend.services.emails.model.Attachment;
  import com.resend.services.emails.model.CreateEmailOptions;
  import com.resend.services.emails.model.CreateEmailResponse;

  public class Main {
      public static void main(String[] args) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          Attachment att = Attachment.builder()
                  .path("https://resend.com/static/sample/invoice.pdf")
                  .fileName("invoice.pdf")
                  .build();

          CreateEmailOptions params = CreateEmailOptions.builder()
                  .from("Acme <onboarding@resend.dev>")
                  .to("delivered@resend.dev")
                  .subject("Receipt for your payment")
                  .html("<p>Thanks for the payment</p>")
                  .attachments(att)
                  .build();

          CreateEmailResponse data = resend.emails().send(params);
      }
  }
  ```

  ```csharp .NET {14-18} theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;
  using System.Collections.Generic;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var message = new EmailMessage()
  {
      From = "Acme <onboarding@resend.dev>",
      To = "delivered@resend.dev",
      Subject = "Receipt for your payment",
      HtmlBody = "<p>Thanks for the payment</p>",
  };

  message.Attachments = new List<EmailAttachment>();
  message.Attachments.Add( new EmailAttachment() {
    Filename = "invoice.pdf",
    Path = "https://resend.com/static/sample/invoice.pdf",
  } );

  var resp = await resend.EmailSendAsync( message );
  Console.WriteLine( "Email Id={0}", resp.Content );
  ```

  ```bash cURL {11-12} theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/emails' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "from": "Acme <onboarding@resend.dev>",
    "to": ["delivered@resend.dev"],
    "subject": "Receipt for your payment",
    "html": "<p>Thanks for the payment</p>",
    "attachments": [
      {
        "path": "https://resend.com/static/sample/invoice.pdf",
        "filename": "invoice.pdf"
      }
    ]
  }'
  ```
</CodeGroup>

## Send attachments from a local file

Include the `content` parameter to send attachments from a local file. This parameter accepts the Base64 encoded content of the file you want to attach.

Define the file name that will be attached using the `filename` parameter.

<CodeGroup>
  ```ts Node.js {16-17} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';
  import fs from 'fs';

  const resend = new Resend('re_xxxxxxxxx');

  const filepath = `${__dirname}/static/invoice.pdf`;
  const attachment = fs.readFileSync(filepath).toString('base64');

  await resend.emails.send({
    from: 'Acme <onboarding@resend.dev>',
    to: ['delivered@resend.dev'],
    subject: 'Receipt for your payment',
    text: '<p>Thanks for the payment</p>',
    attachments: [
      {
        content: attachment,
        filename: 'invoice.pdf',
      },
    ],
  });
  ```

  ```php PHP {12-13} theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $attachment = base64_encode(file_get_contents(__DIR__ . '/static/invoice.pdf'));

  $resend->emails->send([
    'from' => 'Acme <onboarding@resend.dev>',
    'to' => ['delivered@resend.dev'],
    'subject' => 'Receipt for your payment',
    'html' => '<p>Thanks for the payment</p>',
    'attachments' => [
      [
        'filename' => 'invoice.pdf',
        'content' => $attachment
      ]
    ]
  ]);
  ```

  ```python Python {10} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import os
  import resend

  resend.api_key = "re_xxxxxxxxx"

  f: bytes = open(
    os.path.join(os.path.dirname(__file__), "../static/invoice.pdf"), "rb"
  ).read()

  attachment: resend.Attachment = {"content": list(f), "filename": "invoice.pdf"}

  params: resend.Emails.SendParams = {
    "from": "Acme <onboarding@resend.dev>",
    "to": ["delivered@resend.dev"],
    "subject": "Receipt for your payment",
    "html": "<p>Thanks for the payment</p>",
    "attachments": [attachment],
  }

  resend.Emails.send(params)
  ```

  ```rb Ruby {14-15} theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  file = IO.read("invoice.pdf")

  params = {
    "from": "Acme <onboarding@resend.dev>",
    "to": ["delivered@resend.dev"],
    "subject": "Receipt for your payment",
    "html": "<p>Thanks for the payment</p>",
    "attachments": [
      {
        "content": file.bytes,
        "filename": 'invoice.pdf',
      }
    ]
  }

  Resend::Emails.send(params)
  ```

  ```go Go {22-23} theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import (
  	"context"
  	"fmt"
  	"os"

  	"github.com/resend/resend-go/v4"
  )

  func main() {
    ctx := context.TODO()
    client := resend.NewClient("re_xxxxxxxxx")

    pwd, _ := os.Getwd()
    f, err := os.ReadFile(pwd + "/static/invoice.pdf")
    if err != nil {
      panic(err)
    }

    attachment := &resend.Attachment{
      Content:  f,
      Filename: "invoice.pdf",
    }

    params := &resend.SendEmailRequest{
        From:        "Acme <onboarding@resend.dev>",
        To:          []string{"delivered@resend.dev"},
        Subject:     "Receipt for your payment",
        Html:        "<p>Thanks for the payment</p>",
        Attachments: []*resend.Attachment{attachment},
    }

    sent, err := client.Emails.SendWithContext(ctx, params)

    if err != nil {
      panic(err)
    }
    fmt.Println(sent.Id)
  }
  ```

  ```rust Rust {22} theme={"theme":{"light":"github-light","dark":"vesper"}}
  use std::fs::File;
  use std::io::Read;

  use resend_rs::types::{CreateAttachment, CreateEmailBaseOptions};
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let from = "Acme <onboarding@resend.dev>";
    let to = ["delivered@resend.dev"];
    let subject = "Receipt for your payment";

    let filename = "invoice.pdf";
    let mut f = File::open(filename).unwrap();
    let mut invoice = Vec::new();
    f.read_to_end(&mut invoice).unwrap();

    let email = CreateEmailBaseOptions::new(from, to, subject)
      .with_html("<p>Thanks for the payment</p>")
      .with_attachment(CreateAttachment::from_content(invoice).with_filename(filename));

    let _email = resend.emails.send(email).await?;

    Ok(())
  }
  ```

  ```java Java {12-13} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;
  import com.resend.core.exception.ResendException;
  import com.resend.services.emails.model.Attachment;
  import com.resend.services.emails.model.CreateEmailOptions;
  import com.resend.services.emails.model.CreateEmailResponse;

  public class Main {
      public static void main(String[] args) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          Attachment att = Attachment.builder()
                  .fileName("invoice.pdf")
                  .content("invoiceBuffer")
                  .build();

          CreateEmailOptions params = CreateEmailOptions.builder()
                  .from("Acme <onboarding@resend.dev>")
                  .to("delivered@resend.dev")
                  .subject("Receipt for your payment")
                  .html("<p>Thanks for the payment</p>")
                  .attachments(att)
                  .build();

          CreateEmailResponse data = resend.emails().send(params);
      }
  }
  ```

  ```csharp .NET {15-19} theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;
  using System.Collections.Generic;
  using System.IO;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var message = new EmailMessage()
  {
      From = "Acme <onboarding@resend.dev>",
      To = "delivered@resend.dev",
      Subject = "Receipt for your payment",
      HtmlBody = "<p>Thanks for the payment</p>",
  };

  message.Attachments = new List<EmailAttachment>();
  message.Attachments.Add( new EmailAttachment() {
    Filename = "invoice.pdf",
    Content = await File.ReadAllBytesAsync( "invoice.pdf" ),
  } );

  var resp = await resend.EmailSendAsync( message );
  Console.WriteLine( "Email Id={0}", resp.Content );
  ```

  ```bash cURL {11-12} theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/emails' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "from": "Acme <onboarding@resend.dev>",
    "to": ["delivered@resend.dev"],
    "subject": "Receipt for your payment",
    "html": "<p>Thanks for the payment</p>",
    "attachments": [
      {
        "content": "UmVzZW5kIGF0dGFjaG1lbnQgZXhhbXBsZS4gTmljZSBqb2Igc2VuZGluZyB0aGUgZW1haWwh%",
        "filename": "invoice.txt"
      }
    ]
  }'
  ```

  ```bash CLI {6} theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend emails send \
    --from "Acme <onboarding@resend.dev>" \
    --to delivered@resend.dev \
    --subject "Receipt for your payment" \
    --html "<p>Thanks for the payment</p>" \
    --attachment ./static/invoice.pdf
  ```
</CodeGroup>

## Embed Images using CID

You can optionally embed an image in the HTML body of the email. Both remote and local attachments are supported. All attachment requirements, options, and limitations apply to embedded inline images as well.

Embedding images requires two steps:

**1. Add the CID in the email HTML.**

Use the prefix `cid:` to reference the ID in the `src` attribute of an image tag in the HTML body of the email.

```html theme={"theme":{"light":"github-light","dark":"vesper"}}
<img src="cid:logo-image" />
```

**2. Reference the CID in the attachment**

The content id is an arbitrary string set by you, and must be less than 128 characters.

<CodeGroup>
  ```ts Node.js {9, 14} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  await resend.emails.send({
    from: 'Acme <onboarding@resend.dev>',
    to: ['delivered@resend.dev'],
    subject: 'Thank you for contacting us',
    html: '<p>Here is our <img src="cid:logo-image"/> inline logo</p>',
    attachments: [
      {
        path: 'https://resend.com/static/sample/logo.png',
        filename: 'logo.png',
        contentId: 'logo-image',
      },
    ],
  });
  ```

  ```php PHP {7,12} theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->emails->send([
    'from' => 'Acme <onboarding@resend.dev>',
    'to' => ['delivered@resend.dev'],
    'subject' => 'Thank you for contacting us',
    'html' => '<p>Here is our <img src="cid:logo-image"/> inline logo</p>',
    'attachments' => [
      [
        'path' => 'https://resend.com/static/sample/logo.png',
        'filename' => 'logo.png',
        'content_id' => 'logo-image',
      ]
    ]
  ]);
  ```

  ```python Python {8,15} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  attachment: resend.RemoteAttachment = {
    "path": "https://resend.com/static/sample/logo.png",
    "filename": "logo.png",
    "content_id": "logo-image",
  }

  params: resend.Emails.SendParams = {
    "from": "Acme <onboarding@resend.dev>",
    "to": ["delivered@resend.dev"],
    "subject": "Thank you for contacting us",
    "html": "<p>Here is our <img src=\"cid:logo-image\"/> inline logo</p>",
    "attachments": [attachment],
  }

  resend.Emails.send(params)
  ```

  ```rb Ruby {9, 14} theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  params = {
    "from": "Acme <onboarding@resend.dev>",
    "to": ["delivered@resend.dev"],
    "subject": "Thank you for contacting us",
    "html": "<p>Here is our <img src=\"cid:logo-image\"/> inline logo</p>",
    "attachments": [
      {
        "path": "https://resend.com/static/sample/logo.png",
        "filename": 'logo.png',
        "content_id": "logo-image",
      }
    ]
  }

  Resend::Emails.send(params)
  ```

  ```go Go {17, 24} theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import (
  	"context"
  	"fmt"

  	"github.com/resend/resend-go/v4"
  )

  func main() {
    ctx := context.TODO()
    client := resend.NewClient("re_xxxxxxxxx")

    attachment := &resend.Attachment{
      Path:  "https://resend.com/static/sample/logo.png",
      Filename: "logo.png",
      ContentId: "logo-image",
    }

    params := &resend.SendEmailRequest{
        From:        "Acme <onboarding@resend.dev>",
        To:          []string{"delivered@resend.dev"},
        Subject:     "Thank you for contacting us",
        Html:        "<p>Here is our <img src=\"cid:logo-image\"/> inline logo</p>",
        Attachments: []*resend.Attachment{attachment},
    }

    sent, err := client.Emails.SendWithContext(ctx, params)

    if err != nil {
      panic(err)
    }
    fmt.Println(sent.Id)
  }
  ```

  ```rust Rust {14, 17} theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::types::{CreateAttachment, CreateEmailBaseOptions};
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let from = "Acme <onboarding@resend.dev>";
    let to = ["delivered@resend.dev"];
    let subject = "Thank you for contacting us";

    let path = "https://resend.com/static/sample/logo.png";
    let filename = "logo.png";
    let content_id = "logo-image";

    let email = CreateEmailBaseOptions::new(from, to, subject)
      .with_html("<p>Here is our <img src=\"cid:logo-image\"/> inline logo</p>")
      .with_attachment(
        CreateAttachment::from_path(path)
          .with_filename(filename)
          .with_content_id(content_id),
      );

    let _email = resend.emails.send(email).await?;

    Ok(())
  }
  ```

  ```java Java {14, 21} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;
  import com.resend.core.exception.ResendException;
  import com.resend.services.emails.model.Attachment;
  import com.resend.services.emails.model.CreateEmailOptions;
  import com.resend.services.emails.model.CreateEmailResponse;

  public class Main {
      public static void main(String[] args) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          Attachment att = Attachment.builder()
                  .path("https://resend.com/static/sample/logo.png")
                  .fileName("logo.png")
                  .contentId("logo-image")
                  .build();

          CreateEmailOptions params = CreateEmailOptions.builder()
                  .from("Acme <onboarding@resend.dev>")
                  .to("delivered@resend.dev")
                  .subject("Thank you for contacting us")
                  .html("<p>Here is our <img src=\"cid:logo-image\"/> inline logo</p>")
                  .attachments(att)
                  .build();

          CreateEmailResponse data = resend.emails().send(params);
      }
  }
  ```

  ```csharp .NET {11, 18} theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;
  using System.Collections.Generic;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var message = new EmailMessage()
  {
      From = "Acme <onboarding@resend.dev>",
      To = "delivered@resend.dev",
      Subject = "Thank you for contacting us",
      HtmlBody = "<p>Here is our <img src=\"cid:logo-image\"/> inline logo</p>",
  };

  message.Attachments = new List<EmailAttachment>();
  message.Attachments.Add( new EmailAttachment() {
    Filename = "logo.png",
    Path = "https://resend.com/static/sample/logo.png",
    ContentId = "logo-image",
  } );

  var resp = await resend.EmailSendAsync( message );
  Console.WriteLine( "Email Id={0}", resp.Content );
  ```

  ```bash cURL {8,13} theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/emails' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "from": "Acme <onboarding@resend.dev>",
    "to": ["delivered@resend.dev"],
    "subject": "Thank you for contacting us",
    "html": "<p>Here is our <img src=\"cid:logo-image\"/> inline logo</p>",
    "attachments": [
      {
        "path": "https://resend.com/static/sample/logo.png",
        "filename": "logo.png",
        "content_id": "logo-image"
      }
    ]
  }'
  ```
</CodeGroup>

Learn more about [embedding images](/docs/dashboard/emails/embed-inline-images).

## View and Download Attachments

You can view and download attachments from sent emails from the dashboard or programmatically through the [Attachments API](/docs/api-reference/emails/list-email-attachments).

### From the dashboard

1. Go to [Emails](https://resend.com/emails).
2. Navigate to any email you sent with an attachment.
3. Click on the attachment to download it locally.

Attachments include the filename and an icon to help you identify the type of attachment. Each attachment type has a unique icon:

* Image
* PDF
* Spreadsheet
* Default (for unknown types)

### From the API

Use [List Attachments](/docs/api-reference/emails/list-email-attachments) to fetch all attachments for a sent email, or [Retrieve Attachment](/docs/api-reference/emails/retrieve-email-attachment) to fetch a single one. Both endpoints return a signed `download_url` that you can use to download the content.

## Attachment Limitations

* Emails can be no larger than 40MB (including attachments after Base64 encoding).
* Not all file types are supported. See the list of [unsupported file types](/docs/knowledge-base/what-attachment-types-are-not-supported).
* Emails with attachments cannot be sent using our [batching endpoint](/docs/api-reference/emails/send-batch-emails).

## Examples

### Attachments

<CardGroup>
  <Card title="Next.js (TypeScript)" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/nextjs-resend-examples/typescript/src/app/attachments">
    See the full source code.
  </Card>

  <Card title="Next.js (JavaScript)" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/nextjs-resend-examples/javascript/src/app/attachments">
    See the full source code.
  </Card>

  <Card title="PHP" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/attachments">
    See the full source code.
  </Card>

  <Card title="Laravel" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/laravel-resend-examples">
    See the full source code.
  </Card>

  <Card title="Python" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/python-resend-examples/examples">
    See the full source code.
  </Card>

  <Card title="Ruby" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/ruby-resend-examples/examples">
    See the full source code.
  </Card>
</CardGroup>

### Inline Images (CID)

<CardGroup>
  <Card title="Next.js (TypeScript)" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/nextjs-resend-examples/typescript/src/app/cid-attachments">
    See the full source code.
  </Card>

  <Card title="Next.js (JavaScript)" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/nextjs-resend-examples/javascript/src/app/cid-attachments">
    See the full source code.
  </Card>

  <Card title="PHP" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/php-resend-examples/src/attachments">
    See the full source code.
  </Card>

  <Card title="Laravel" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/laravel-resend-examples">
    See the full source code.
  </Card>

  <Card title="Python" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/python-resend-examples/examples">
    See the full source code.
  </Card>

  <Card title="Ruby" icon="arrow-up-right-from-square" href="https://github.com/resend/resend-examples/tree/main/ruby-resend-examples/examples">
    See the full source code.
  </Card>
</CardGroup>
