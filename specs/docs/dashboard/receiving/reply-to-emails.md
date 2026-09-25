> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Reply to Receiving Emails

> Reply to Receiving emails in the same thread.

Email clients thread emails by using the `message_id` metadata.

If you want to reply to an email, add the `In-Reply-To` header set to the `message_id` of the received email. To signal the threading, set the subject to start with `Re:` so that email clients can group the replies together.

## Get the message ID

The `message_id` is included in the [webhook event](/docs/webhooks/emails/received) payload when an email is received:

```json {5} theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "type": "email.received",
  "data": {
    "email_id": "56761188-7520-42d8-8898-ff6fc54ce618",
    "message_id": "<111-222-333@email.example.com>",
    "subject": "Sending this example",
    "from": "Acme <onboarding@resend.dev>",
    "to": ["delivered@resend.dev"]
  }
}
```

Use the `message_id` value from `event.data.message_id` as the `In-Reply-To` header when sending your reply.

## Send a reply in thread

Here's how you can reply in thread using each SDK:

<CodeGroup>
  ```ts Node.js {14} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend, type EmailReceivedEvent } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  export async function replyToEmail(event: EmailReceivedEvent) {
    const messageId = event.data.message_id;

    const { data, error } = await resend.emails.send({
      from: 'Acme <onboarding@resend.dev>',
      to: ['delivered@resend.dev'],
      subject: `Re: ${event.data.subject}`,
      html: '<p>Thanks for your email!</p>',
      headers: {
        'In-Reply-To': messageId,
      },
    });
  }
  ```

  ```php PHP {13} theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $event = json_decode(file_get_contents('php://input'), true);

  $messageId = $event['data']['message_id'];

  $data = $resend->emails->send([
      'from' => 'Acme <onboarding@resend.dev>',
      'to' => ['delivered@resend.dev'],
      'subject' => "Re: {$event['data']['subject']}",
      'html' => '<p>Thanks for your email!</p>',
      'headers' => [
          'In-Reply-To' => $messageId,
      ],
  ]);
  ```

  ```python Python {14} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  def handle_email_received(event: resend.EmailReceivedEvent):
      message_id = event["data"]["message_id"]

      params: resend.Emails.SendParams = {
          "from": "Acme <onboarding@resend.dev>",
          "to": ["delivered@resend.dev"],
          "subject": f"Re: {event['data']['subject']}",
          "html": "<p>Thanks for your email!</p>",
          "headers": {
              "In-Reply-To": message_id,
          },
      }

      email = resend.Emails.send(params)
  ```

  ```rb Ruby {13} theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  message_id = event["data"]["message_id"]

  params = {
      from: "Acme <onboarding@resend.dev>",
      to: ["delivered@resend.dev"],
      subject: "Re: #{event['data']['subject']}",
      html: "<p>Thanks for your email!</p>",
      headers: {
          "In-Reply-To": message_id,
      },
  }

  sent = Resend::Emails.send(params)
  ```

  ```go Go {29} theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import (
  	"fmt"
  	"context"

  	"github.com/resend/resend-go/v4"
  )

  func main() {
      ctx := context.TODO()
      client := resend.NewClient("re_xxxxxxxxx")

      var event struct {
          Data struct {
              MessageId string `json:"message_id"`
              Subject   string `json:"subject"`
          } `json:"data"`
      }

      messageId := event.Data.MessageId

      params := &resend.SendEmailRequest{
          From:    "Acme <onboarding@resend.dev>",
          To:      []string{"delivered@resend.dev"},
          Subject: fmt.Sprintf("Re: %s", event.Data.Subject),
          Html:    "<p>Thanks for your email!</p>",
          Headers: map[string]string{
              "In-Reply-To": messageId,
          },
      }

      sent, err := client.Emails.SendWithContext(ctx, params)

      if err != nil {
          panic(err)
      }
      fmt.Println(sent.Id)
  }
  ```

  ```rust Rust {17} theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::events::EmailEvent;
  use resend_rs::types::CreateEmailBaseOptions;
  use resend_rs::{Resend, Result};

  async fn reply(event: EmailEvent) -> Result<()> {
      let resend = Resend::new("re_xxxxxxxxx");

      let message_id = &event.data.message_id;
      let subject = format!("Re: {}", event.data.subject);

      let email = CreateEmailBaseOptions::new(
          "Acme <onboarding@resend.dev>",
          ["delivered@resend.dev"],
          &subject,
      )
      .with_html("<p>Thanks for your email!</p>")
      .with_header("In-Reply-To", message_id);

      let _email = resend.emails.send(email).await?;

      Ok(())
  }
  ```

  ```java Java {20} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;
  import com.resend.core.exception.ResendException;
  import com.resend.services.emails.model.CreateEmailOptions;
  import com.resend.services.emails.model.CreateEmailResponse;
  import com.resend.services.receiving.model.ReceivedEmail;
  import java.util.Map;

  public class Main {
      public static void reply(ReceivedEmail event) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          String messageId = event.getMessageId();

          CreateEmailOptions params = CreateEmailOptions.builder()
                  .from("Acme <onboarding@resend.dev>")
                  .to("delivered@resend.dev")
                  .subject("Re: " + event.getSubject())
                  .html("<p>Thanks for your email!</p>")
                  .headers(Map.of(
                      "In-Reply-To", messageId
                  ))
                  .build();

          CreateEmailResponse data = resend.emails().send(params);
      }
  }
  ```

  ```csharp .NET {18} theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;
  using System.Collections.Generic;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  async Task ReplyAsync(ReceivedEmail eventData)
  {
      var messageId = eventData.MessageId;

      var message = new EmailMessage()
      {
          From = "Acme <onboarding@resend.dev>",
          To = "delivered@resend.dev",
          Subject = $"Re: {eventData.Subject}",
          HtmlBody = "<p>Thanks for your email!</p>",
          Headers = new Dictionary<string, string>()
          {
              { "In-Reply-To", messageId },
          },
      };

      var resp = await resend.EmailSendAsync(message);
  }
  ```

  ```bash cURL {10} theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/emails' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "from": "Acme <onboarding@resend.dev>",
    "to": ["delivered@resend.dev"],
    "subject": "Re: Sending this example",
    "html": "<p>Thanks for your email!</p>",
    "headers": {
      "In-Reply-To": "<111-222-333@email.example.com>"
    }
  }'
  ```

  ```bash CLI {6} theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend emails send \
    --from "Acme <onboarding@resend.dev>" \
    --to delivered@resend.dev \
    --subject "Re: Sending this example" \
    --html "<p>Thanks for your email!</p>" \
    --headers "In-Reply-To=<111-222-333@email.example.com>"
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use axum::{
      extract::State,
      response::{IntoResponse, Json, Response},
  };
  use resend_rs::{types::CreateEmailBaseOptions, Resend};
  use serde::Serialize;
  use std::sync::Arc;

  struct AppState {
      resend: Resend,
  }

  #[derive(Serialize)]
  struct Empty {}

  async fn example(
      State(state): State<Arc<AppState>>,
      Json(event): Json<resend_rs::events::EmailEvent>,
  ) -> Response {
      if matches!(
          event.r#type,
          resend_rs::events::EmailEventType::EmailReceived
      ) {
          let email = CreateEmailBaseOptions::new(
              "Acme <onboarding@resend.dev>",
              vec!["delivered@resend.dev"],
              format!("Re: {}", event.data.subject),
          )
          .with_html("<p>Thanks for your email!</p>")
          .with_header("In-Reply-To", &event.data.message_id);

          let data = state.resend.emails.send(email).await.unwrap();
          Json(data).into_response()
      } else {
          Json(Empty {}).into_response()
      }
  }
  ```
</CodeGroup>

## Replying multiple times in a thread

If you're replying multiple times within the same thread, make sure to also append
the previous `message_id`s to the `References` header, separated by spaces.
This helps email clients maintain the correct threading structure.

<CodeGroup>
  ```ts Node.js {14-15} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend, type EmailReceivedEvent } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  export async function replyInThread(event: EmailReceivedEvent) {
    const previousReferences = ['<msg_id1@domain.com>', '<msg_id2@domain.com>'];

    const { data, error } = await resend.emails.send({
      from: 'Acme <onboarding@resend.dev>',
      to: ['delivered@resend.dev'],
      subject: `Re: ${event.data.subject}`,
      html: '<p>Thanks for your email!</p>',
      headers: {
        'In-Reply-To': event.data.message_id,
        'References': [...previousReferences, event.data.message_id].join(' '),
      },
    });
  }
  ```

  ```php PHP {13-14} theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $event = json_decode(file_get_contents('php://input'), true);

  $previousReferences = ['<msg_id1@domain.com>', '<msg_id2@domain.com>'];

  $data = $resend->emails->send([
      'from' => 'Acme <onboarding@resend.dev>',
      'to' => ['delivered@resend.dev'],
      'subject' => "Re: {$event['data']['subject']}",
      'html' => '<p>Thanks for your email!</p>',
      'headers' => [
          'In-Reply-To' => $event['data']['message_id'],
          'References' => implode(' ', [...$previousReferences, $event['data']['message_id']]),
      ],
  ]);
  ```

  ```python Python {14-15} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  def handle_email_received(event: resend.EmailReceivedEvent):
      previous_references = ["<msg_id1@domain.com>", "<msg_id2@domain.com>"]

      params: resend.Emails.SendParams = {
          "from": "Acme <onboarding@resend.dev>",
          "to": ["delivered@resend.dev"],
          "subject": f"Re: {event['data']['subject']}",
          "html": "<p>Thanks for your email!</p>",
          "headers": {
              "In-Reply-To": event["data"]["message_id"],
              "References": " ".join([*previous_references, event["data"]["message_id"]]),
          },
      }

      email = resend.Emails.send(params)
  ```

  ```rb Ruby {13-14} theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  previous_references = ["<msg_id1@domain.com>", "<msg_id2@domain.com>"]

  params = {
      from: "Acme <onboarding@resend.dev>",
      to: ["delivered@resend.dev"],
      subject: "Re: #{event['data']['subject']}",
      html: "<p>Thanks for your email!</p>",
      headers: {
          "In-Reply-To": event["data"]["message_id"],
          "References": [*previous_references, event["data"]["message_id"]].join(" "),
      },
  }

  sent = Resend::Emails.send(params)
  ```

  ```go Go {32-33} theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import (
  	"context"
  	"fmt"
  	"strings"

  	"github.com/resend/resend-go/v4"
  )

  func main() {
      ctx := context.TODO()
      client := resend.NewClient("re_xxxxxxxxx")

      var event struct {
          Data struct {
              MessageId string `json:"message_id"`
              Subject   string `json:"subject"`
          } `json:"data"`
      }

      previousReferences := []string{"<msg_id1@domain.com>", "<msg_id2@domain.com>"}

      allReferences := append(previousReferences, event.Data.MessageId)

      params := &resend.SendEmailRequest{
          From:    "Acme <onboarding@resend.dev>",
          To:      []string{"delivered@resend.dev"},
          Subject: fmt.Sprintf("Re: %s", event.Data.Subject),
          Html:    "<p>Thanks for your email!</p>",
          Headers: map[string]string{
              "In-Reply-To": event.Data.MessageId,
              "References":  strings.Join(allReferences, " "),
          },
      }

      sent, err := client.Emails.SendWithContext(ctx, params)

      if err != nil {
          panic(err)
      }
      fmt.Println(sent.Id)
  }
  ```

  ```rust Rust {19-20} theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::events::EmailEvent;
  use resend_rs::types::CreateEmailBaseOptions;
  use resend_rs::{Resend, Result};

  async fn reply(resend: &Resend, event: EmailEvent) -> Result<()> {
      let subject = format!("Re: {}", event.data.subject);
      let previous_references = vec!["<msg_id1@domain.com>", "<msg_id2@domain.com>"];

      let all_references = [previous_references, vec![event.data.message_id.as_str()]]
          .concat()
          .join(" ");

      let email = CreateEmailBaseOptions::new(
          "Acme <onboarding@resend.dev>",
          ["delivered@resend.dev"],
          &subject,
      )
      .with_html("<p>Thanks for your email!</p>")
      .with_header("In-Reply-To", &event.data.message_id)
      .with_header("References", &all_references);

      let _email = resend.emails.send(email).await?;

      Ok(())
  }
  ```

  ```java Java {25-26} theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;
  import com.resend.core.exception.ResendException;
  import com.resend.services.emails.model.CreateEmailOptions;
  import com.resend.services.emails.model.CreateEmailResponse;
  import com.resend.services.receiving.model.ReceivedEmail;
  import java.util.ArrayList;
  import java.util.List;
  import java.util.Map;

  public class Main {
      public static void reply(ReceivedEmail event) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          List<String> previousReferences = List.of("<msg_id1@domain.com>", "<msg_id2@domain.com>");

          List<String> allReferences = new ArrayList<>(previousReferences);
          allReferences.add(event.getMessageId());

          CreateEmailOptions params = CreateEmailOptions.builder()
                  .from("Acme <onboarding@resend.dev>")
                  .to("delivered@resend.dev")
                  .subject("Re: " + event.getSubject())
                  .html("<p>Thanks for your email!</p>")
                  .headers(Map.of(
                      "In-Reply-To", event.getMessageId(),
                      "References", String.join(" ", allReferences)
                  ))
                  .build();

          CreateEmailResponse data = resend.emails().send(params);
      }
  }
  ```

  ```csharp .NET {18-19} theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  async Task ReplyAsync(ReceivedEmail eventData)
  {
      var previousReferences = new List<string> { "<msg_id1@domain.com>", "<msg_id2@domain.com>" };
      previousReferences.Add(eventData.MessageId);

      var message = new EmailMessage()
      {
          From = "Acme <onboarding@resend.dev>",
          To = "delivered@resend.dev",
          Subject = $"Re: {eventData.Subject}",
          HtmlBody = "<p>Thanks for your email!</p>",
          Headers = new Dictionary<string, string>()
          {
              { "In-Reply-To", eventData.MessageId },
              { "References", string.Join(" ", previousReferences) },
          },
      };

      var resp = await resend.EmailSendAsync(message);
  }
  ```

  ```bash cURL {10-11} theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/emails' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "from": "Acme <onboarding@resend.dev>",
    "to": ["delivered@resend.dev"],
    "subject": "Re: Sending this example",
    "html": "<p>Thanks for your email!</p>",
    "headers": {
      "In-Reply-To": "<111-222-333@email.example.com>",
      "References": "<msg_id1@domain.com> <msg_id2@domain.com> <111-222-333@email.example.com>"
    }
  }'
  ```

  ```bash CLI {6-7} theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend emails send \
    --from "Acme <onboarding@resend.dev>" \
    --to delivered@resend.dev \
    --subject "Re: Sending this example" \
    --html "<p>Thanks for your email!</p>" \
    --headers "In-Reply-To=<111-222-333@email.example.com>" \
      "References=<msg_id1@domain.com> <msg_id2@domain.com> <111-222-333@email.example.com>"
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{events::EmailEvent, types::CreateEmailBaseOptions, Resend};

  async fn reply(resend: &Resend, event: EmailEvent) {
      let previous_references = [
          "<msg_id1@domain.com>",
          "<msg_id2@domain.com>",
          &event.data.message_id,
      ];

      let email = CreateEmailBaseOptions::new(
          "Acme <onboarding@resend.dev>",
          vec!["delivered@resend.dev"],
          format!("Re: {}", event.data.subject),
      )
      .with_html("<p>Thanks for your email!</p>")
      .with_header("In-Reply-To", &event.data.message_id)
      .with_header("References", &previous_references.join(" "));

      let data = resend.emails.send(email).await.unwrap();
  }
  ```
</CodeGroup>
