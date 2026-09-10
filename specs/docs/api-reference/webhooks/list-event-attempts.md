> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Attempts

> Retrieve the delivery attempts for a single webhook event.

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

## Path Parameters

<ResendParamField path="webhook_id" type="string" required>
  The Webhook ID.
</ResendParamField>

<ResendParamField path="event_id" type="string" required>
  The Webhook Event ID.
</ResendParamField>

## Query Parameters

<ParamField query="limit" type="number">
  Number of attempts to return. Between `1` and `100`. Defaults to `20`.
</ParamField>

<ParamField query="after" type="string">
  The attempt ID to fetch the next page after.

  The `before` parameter is not supported for this endpoint.
</ParamField>

## Response Fields

<ParamField body="object" type="string">
  Always `list`.
</ParamField>

<ParamField body="has_more" type="boolean">
  Whether more attempts exist beyond this page.
</ParamField>

<ParamField body="data" type="array">
  The delivery attempts for this event, most recent first.

  <Expandable defaultOpen="true" title="properties">
    <ParamField body="id" type="string">
      The attempt ID.
    </ParamField>

    <ParamField body="http_status_code" type="number">
      The HTTP status code your endpoint returned for this attempt.
    </ParamField>

    <ParamField body="response" type="string">
      The response body your endpoint returned for this attempt.
    </ParamField>

    <ParamField body="sent_at" type="string">
      When this attempt was sent.
    </ParamField>
  </Expandable>
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.webhooks.events.attempts.list({
    eventId: 'msg_1srOrx2ZWZBpBUvZwXKQmoEYga2',
    webhookId: '4dd369bc-aa82-4ff3-97de-514ae3000ee0',
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $attempts = $resend->webhooks->events->attempts->list(
      '4dd369bc-aa82-4ff3-97de-514ae3000ee0',
      'msg_1srOrx2ZWZBpBUvZwXKQmoEYga2'
  );
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = 're_xxxxxxxxx'

  attempts = resend.Webhooks.list_event_attempts(
      webhook_id='4dd369bc-aa82-4ff3-97de-514ae3000ee0',
      event_id='msg_1srOrx2ZWZBpBUvZwXKQmoEYga2',
  )
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require 'resend'

  Resend.api_key = 're_xxxxxxxxx'

  attempts = Resend::Webhooks.list_event_attempts(
    '4dd369bc-aa82-4ff3-97de-514ae3000ee0',
    'msg_1srOrx2ZWZBpBUvZwXKQmoEYga2'
  )
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v4"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	client.Webhooks.ListEventAttempts(
  		"4dd369bc-aa82-4ff3-97de-514ae3000ee0",
  		"msg_1srOrx2ZWZBpBUvZwXKQmoEYga2",
  	)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{list_opts::ListOptions, Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _attempts = resend
      .webhooks
      .list_event_attempts(
        "4dd369bc-aa82-4ff3-97de-514ae3000ee0",
        "msg_1srOrx2ZWZBpBUvZwXKQmoEYga2",
        ListOptions::default(),
      )
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;
  import com.resend.core.exception.ResendException;
  import com.resend.services.webhooks.model.ListWebhookEventAttemptsResponseSuccess;

  public class Main {
      public static void main(String[] args) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          ListWebhookEventAttemptsResponseSuccess attempts = resend.webhooks().listEventAttempts(
              "4dd369bc-aa82-4ff3-97de-514ae3000ee0",
              "msg_1srOrx2ZWZBpBUvZwXKQmoEYga2"
          );
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.WebhookEventAttemptListAsync(
      new Guid( "4dd369bc-aa82-4ff3-97de-514ae3000ee0" ),
      "msg_1srOrx2ZWZBpBUvZwXKQmoEYga2"
  );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/webhooks/4dd369bc-aa82-4ff3-97de-514ae3000ee0/events/msg_1srOrx2ZWZBpBUvZwXKQmoEYga2/attempts' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "list",
    "has_more": false,
    "data": [
      {
        "id": "atmpt_1srOrx2ZWZBpBUvZwXKQmoEYga2",
        "http_status_code": 200,
        "response": "{\"ok\":true}",
        "sent_at": "2026-08-22T15:33:12.000Z"
      },
      {
        "id": "atmpt_2ZbUCwvGmIT4mLIN6d3Yz0Ainbd",
        "http_status_code": 500,
        "response": "Internal Server Error",
        "sent_at": "2026-08-22T15:28:05.000Z"
      }
    ]
  }
  ```
</ResponseExample>
