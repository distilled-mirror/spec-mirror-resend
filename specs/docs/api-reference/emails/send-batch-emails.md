> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send Batch Emails

> Trigger up to 100 batch emails at once.

export const ResendParamField = ({children, body, path, ...props}) => {
  const [lang, setLang] = useState(() => {
    return localStorage.getItem('code') || '"Node.js"';
  });
  useEffect(() => {
    const onStorage = event => {
      const key = event.detail.key;
      if (key === 'code') {
        setLang(event.detail.value);
      }
    };
    document.addEventListener('mintlify-localstorage', onStorage);
    return () => {
      document.removeEventListener('mintlify-localstorage', onStorage);
    };
  }, []);
  const toCamelCase = str => typeof str === 'string' ? str.replace(/[_-](\w)/g, (_, c) => c.toUpperCase()) : str;
  const resolvedBody = useMemo(() => {
    const value = JSON.parse(lang);
    return value === 'Node.js' ? toCamelCase(body) : body;
  }, [body, lang]);
  const resolvedPath = useMemo(() => {
    const value = JSON.parse(lang);
    return value === 'Node.js' ? toCamelCase(path) : path;
  }, [path, lang]);
  return <ParamField body={resolvedBody} path={resolvedPath} {...props}>
      {children}
    </ParamField>;
};

Instead of sending one email per HTTP request, Resend provides a batching endpoint that permits you to send up to 100 emails in a single API call.

## Body Parameters

<ParamField body="from" type="string" required>
  Sender email address.

  To include a friendly name, pass the sender as `Name <email@example.com>`, for example `Acme <onboarding@example.dev>`.
</ParamField>

<ParamField body="to" type="string | string[]" required>
  Recipient email address. For multiple addresses, send as an array of strings.
  Max 50.
</ParamField>

<ParamField body="subject" type="string" required>
  Email subject.
</ParamField>

<ParamField body="bcc" type="string | string[]">
  Bcc recipient email address. For multiple addresses, send as an array of
  strings.
</ParamField>

<ParamField body="cc" type="string | string[]">
  Cc recipient email address. For multiple addresses, send as an array of
  strings.
</ParamField>

<ResendParamField body="scheduled_at" type="string">
  Schedule email to be sent later. The date should be in natural language (e.g.: `in 1 min`) or ISO 8601 format (e.g:
  `2026-08-05T11:52:01.858Z`).

  [See examples](/docs/dashboard/emails/schedule-email)
</ResendParamField>

<ResendParamField body="reply_to" type="string | string[]">
  Reply-to email address. For multiple addresses, send as an array of strings.
</ResendParamField>

<ParamField body="html" type="string">
  The HTML version of the message.
</ParamField>

<ParamField body="text" type="string">
  The plain text version of the message.

  <Info>
    If not provided, the HTML will be used to generate a plain text version. You
    can opt out of this behavior by setting value to an empty string.
  </Info>
</ParamField>

<ParamField body="react" type="React.ReactNode">
  The React component used to write the message. *Only available in the Node.js
  SDK.*
</ParamField>

<ParamField body="headers" type="object">
  Custom headers to add to the email.
</ParamField>

<ResendParamField body="topic_id" type="string">
  The topic ID to receive the email.

  * If the recipient is a contact and has opted-in to the topic, the email is sent.
  * If the recipient is a contact and has opted-out of the topic, the email is not sent and will be marked as failed.
  * If the recipient is not a contact, the email is sent if the topic default subscription value is set to `opt-in`.

  <Note>Each email address (to, cc, bcc) is checked and handled separately.</Note>
</ResendParamField>

<ParamField body="tags" type="array">
  Custom data passed in key/value pairs.

  [See examples](/docs/dashboard/emails/tags).

  <Expandable defaultOpen title="properties">
    <ParamField body="name" type="string" required>
      The name of the email tag.

      It can only contain ASCII letters (a–z, A–Z), numbers (0–9), underscores (\_), or dashes (-).

      It can contain no more than 256 characters.
    </ParamField>

    <ParamField body="value" type="string" required>
      The value of the email tag.

      It can only contain ASCII letters (a–z, A–Z), numbers (0–9), underscores (\_), or dashes (-).

      It can contain no more than 256 characters.
    </ParamField>
  </Expandable>
</ParamField>

<ParamField body="template" type="object">
  To send using a template, provide a `template` object with:

  * `id`: the id *or* the alias of the published template
  * `variables`: an object with a key for each variable (if applicable)

  <Info>
    If a `template` is provided, you cannot send `html`, `text`, or `react` in the payload, otherwise the API will return a validation error.

    When sending a template, the payload for `from`, `subject`, and `reply_to` take precedence over the template's defaults for these fields. If the template does not provide a default value for these fields, you must provide them in the payload.
  </Info>
</ParamField>

<ParamField body="id" type="string" required>
  The id of the published email template. Required if `template` is provided. Only published templates can be used when sending emails.
</ParamField>

<ParamField body="variables" type="object">
  Template variables object with key/value pairs.

  ```ts theme={"theme":{"light":"github-light","dark":"vesper"}}
  variables: {
  	CTA: 'Sign up now',
  	CTA_LINK: 'https://example.com/signup'
  }
  ```

  When sending the template, the HTML will be parsed. If all the variables used in the template were provided, the email will be sent. If not, the call will throw a validation error.

  See the [errors reference](/docs/api-reference/errors) for more details or [learn more about templates](/docs/dashboard/templates/introduction).

  <Expandable defaultOpen title="properties">
    <ParamField body="key" type="string" required>
      The key of the variable.

      May only contain ASCII letters (a–z, A–Z), numbers (0–9), and underscores (\_). The following variable names are reserved and cannot be used: `FIRST_NAME`, `LAST_NAME`, `EMAIL`, `UNSUBSCRIBE_URL`.

      It can contain no more than 50 characters.
    </ParamField>

    <ParamField body="value" type="string | number" required>
      The value of the variable.

      Observe these technical limitations:

      * `string`: maximum length of 2,000 characters
      * `number`: not greater than 2^53 - 1
    </ParamField>
  </Expandable>
</ParamField>

## Headers

<ParamField header="Idempotency-Key" type="string">
  Add an idempotency key to prevent duplicated emails.

  * Should be **unique per API request**
  * Idempotency keys expire after **24 hours**
  * Have a maximum length of **256 characters**

  [Learn more about idempotency keys →](/docs/dashboard/emails/idempotency-keys)
</ParamField>

## Limitations

The `attachments` field is not supported yet.

## Response format

When the request succeeds, each entry in `data` corresponds to the email at the same index in the batch payload (0-based). The first email in your request will be the first entry in `data`, and so on.

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.batch.send([
    {
      from: 'Acme <onboarding@resend.dev>',
      to: ['foo@gmail.com'],
      subject: 'hello world',
      html: '<h1>it works!</h1>',
    },
    {
      from: 'Acme <onboarding@resend.dev>',
      to: ['bar@outlook.com'],
      subject: 'world hello',
      html: '<p>it works!</p>',
    },
  ]);
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->batch->send([
    [
      'from' => 'Acme <onboarding@resend.dev>',
      'to' => ['foo@gmail.com'],
      'subject' => 'hello world',
      'html' => '<h1>it works!</h1>',
    ],
    [
      'from' => 'Acme <onboarding@resend.dev>',
      'to' => ['bar@outlook.com'],
      'subject' => 'world hello',
      'html' => '<p>it works!</p>',
    ]
  ]);
  ```

  ```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend
  from typing import List

  resend.api_key = "re_xxxxxxxxx"

  params: List[resend.Emails.SendParams] = [
    {
      "from": "Acme <onboarding@resend.dev>",
      "to": ["foo@gmail.com"],
      "subject": "hello world",
      "html": "<h1>it works!</h1>",
    },
    {
      "from": "Acme <onboarding@resend.dev>",
      "to": ["bar@outlook.com"],
      "subject": "world hello",
      "html": "<p>it works!</p>",
    }
  ]

  resend.Batch.send(params)
  ```

  ```rb Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = 're_xxxxxxxxx'

  params = [
    {
      "from": "Acme <onboarding@resend.dev>",
      "to": ["foo@gmail.com"],
      "subject": "hello world",
      "html": "<h1>it works!</h1>",
    },
    {
      "from": "Acme <onboarding@resend.dev>",
      "to": ["bar@outlook.com"],
      "subject": "world hello",
      "html": "<p>it works!</p>",
    }
  ]

  Resend::Batch.send(params)
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

    var batchEmails = []*resend.SendEmailRequest{
      {
        From:    "Acme <onboarding@resend.dev>",
        To:      []string{"foo@gmail.com"},
        Subject: "hello world",
        Html:    "<h1>it works!</h1>",
      },
      {
        From:    "Acme <onboarding@resend.dev>",
        To:      []string{"bar@outlook.com"},
        Subject: "world hello",
        Html:    "<p>it works!</p>",
      },
    }

    sent, err := client.Batch.SendWithContext(ctx, batchEmails)

    if err != nil {
      panic(err)
    }
    fmt.Println(sent.Data)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::types::CreateEmailBaseOptions;
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let emails = vec![
      CreateEmailBaseOptions::new(
        "Acme <onboarding@resend.dev>",
        vec!["foo@gmail.com"],
        "hello world",
      )
      .with_html("<h1>it works!</h1>"),
      CreateEmailBaseOptions::new(
        "Acme <onboarding@resend.dev>",
        vec!["bar@outlook.com"],
        "world hello",
      )
      .with_html("<p>it works!</p>"),
    ];

    let _emails = resend.batch.send(emails).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.Resend;
  import com.resend.core.exception.ResendException;
  import com.resend.services.batch.model.CreateBatchEmailsResponse;
  import com.resend.services.emails.model.CreateEmailOptions;
  import java.util.Arrays;

  public class Main {
      public static void main(String[] args) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          CreateEmailOptions firstEmail = CreateEmailOptions.builder()
              .from("Acme <onboarding@resend.dev>")
              .to("foo@gmail.com")
              .subject("hello world")
              .html("<h1>it works!</h1>")
              .build();

          CreateEmailOptions secondEmail = CreateEmailOptions.builder()
              .from("Acme <onboarding@resend.dev>")
              .to("bar@outlook.com")
              .subject("world hello")
              .html("<p>it works!</p>")
              .build();

          CreateBatchEmailsResponse data = resend.batch().send(
              Arrays.asList(firstEmail, secondEmail)
          );
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var mail1 = new EmailMessage()
  {
      From = "Acme <onboarding@resend.dev>",
      To = "foo@gmail.com",
      Subject = "hello world",
      HtmlBody = "<p>it works!</p>",
  };

  var mail2 = new EmailMessage()
  {
      From = "Acme <onboarding@resend.dev>",
      To = "bar@outlook.com",
      Subject = "hello world",
      HtmlBody = "<p>it works!</p>",
  };

  var resp = await resend.EmailBatchAsync( [ mail1, mail2 ] );
  Console.WriteLine( "Nr Emails={0}", resp.Content.Count );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/emails/batch' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'[
    {
      "from": "Acme <onboarding@resend.dev>",
      "to": ["foo@gmail.com"],
      "subject": "hello world",
      "html": "<h1>it works!</h1>"
    },
    {
      "from": "Acme <onboarding@resend.dev>",
      "to": ["bar@outlook.com"],
      "subject": "world hello",
      "html": "<p>it works!</p>"
    }
  ]'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend emails batch --file ./path/to/emails.json
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "data": [
      {
        "id": "ae2014de-c168-4c61-8267-70d2662a1ce1"
      },
      {
        "id": "faccb7a5-8a28-4e9a-ac64-8da1cc3bc1cb"
      }
    ]
  }
  ```
</ResponseExample>
