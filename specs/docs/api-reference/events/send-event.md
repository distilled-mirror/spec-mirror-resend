> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Send Event

> Send a named event to trigger matching automations.

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

## Body Parameters

<ParamField body="event" type="string" required>
  The name of the event to trigger. Must match the event name configured in an
  automation trigger step.
</ParamField>

Either `contact_id` or `email` must be provided, but not both.

<ResendParamField body="contact_id" type="string">
  The contact ID (UUID) to associate with this event. Exactly one of
  `contact_id` or `email` must be provided.
</ResendParamField>

<ParamField body="email" type="string">
  The email address to associate with this event. Exactly one of `contact_id` or
  `email` must be provided. If no contact with this email exists in your
  Audience, one will be created automatically when the automation runs.
</ParamField>

<ParamField body="payload" type="object">
  An optional object containing custom data to pass to the automation. This data
  can be used in template variables and conditions. If the event has a schema
  defined, the payload values will be validated and coerced to match the schema
  types.
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  // Trigger with a contact ID
  const { data, error } = await resend.events.send({
    event: 'user.created',
    contactId: '7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b',
    payload: {
      plan: 'pro',
    },
  });

  // Trigger with an email address
  const { data, error } = await resend.events.send({
    event: 'user.created',
    email: 'steve.wozniak@gmail.com',
    payload: {
      plan: 'pro',
    },
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  // Trigger with a contact ID
  $resend->events->send([
    'event' => 'user.created',
    'contact_id' => '7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b',
    'payload' => ['plan' => 'pro'],
  ]);

  // Trigger with an email address
  $resend->events->send([
    'event' => 'user.created',
    'email' => 'steve.wozniak@gmail.com',
    'payload' => ['plan' => 'pro'],
  ]);
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  # Trigger with a contact ID
  params: resend.Events.SendParams = {
    "event": "user.created",
    "contact_id": "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b",
    "payload": {
      "plan": "pro",
    },
  }

  resend.Events.send(params)

  # Trigger with an email address
  params: resend.Events.SendParams = {
    "event": "user.created",
    "email": "steve.wozniak@gmail.com",
    "payload": {
      "plan": "pro",
    },
  }

  resend.Events.send(params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  # Trigger with a contact ID
  params = {
    event: "user.created",
    contact_id: "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b",
    payload: {
      plan: "pro",
    },
  }

  Resend::Events.send(params)

  # Trigger with an email address
  params = {
    event: "user.created",
    email: "steve.wozniak@gmail.com",
    payload: {
      plan: "pro",
    },
  }

  Resend::Events.send(params)
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v3"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	// Trigger with a contact ID
  	params := &resend.SendEventRequest{
  		Event:     "user.created",
  		ContactId: "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b",
  		Payload: map[string]any{
  			"plan": "pro",
  		},
  	}

  	client.Events.Send(params)

  	// Trigger with an email address
  	params = &resend.SendEventRequest{
  		Event: "user.created",
  		Email: "steve.wozniak@gmail.com",
  		Payload: map[string]any{
  			"plan": "pro",
  		},
  	}

  	client.Events.Send(params)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{
    json,
    types::{ContactIdOrEmail, SendEventOptions},
    Resend, Result,
  };

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let opts = SendEventOptions {
      event: "user.created".to_owned(),
      contact_id_or_email: ContactIdOrEmail::ContactId(
        "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b".to_owned(),
      ),
      payload: json!({
        "plan": "pro"
      }),
    };

    let opts = SendEventOptions {
      event: "user.created".to_owned(),
      contact_id_or_email: ContactIdOrEmail::Email("steve.wozniak@gmail.com".to_owned()),
      payload: json!({
        "plan": "pro"
      }),
    };

    let _event = resend.events.send(opts).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;

  public class Main {
      public static void main(String[] args) {
          Resend resend = new Resend("re_xxxxxxxxx");

          // Trigger with a contact ID
          SendEventOptions params = SendEventOptions.builder()
                  .event("user.created")
                  .contactId("7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b")
                  .addPayload("plan", "pro")
                  .build();

          SendEventResponseSuccess data = resend.events().send(params);

          // Trigger with an email address
          SendEventOptions params = SendEventOptions.builder()
                  .event("user.created")
                  .email("steve.wozniak@gmail.com")
                  .addPayload("plan", "pro")
                  .build();

          SendEventResponseSuccess data = resend.events().send(params);
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;
  using System.Text.Json;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

  var payload = JsonSerializer.SerializeToElement( new { plan = "pro" } );

  // Trigger with a contact ID
  var resp = await resend.EventSendAsync( new EventSendData()
  {
      Event = "user.created",
      ContactId = new Guid( "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b" ),
      Payload = payload,
  } );
  Console.WriteLine( "Event={0}", resp.Content.Event );

  // Trigger with an email address
  await resend.EventSendAsync( new EventSendData()
  {
      Event = "user.created",
      Email = "steve.wozniak@gmail.com",
      Payload = payload,
  } );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  # Trigger with a contact ID
  curl -X POST 'https://api.resend.com/events/send' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d '{
    "event": "user.created",
    "contact_id": "7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b",
    "payload": {
      "plan": "pro"
    }
  }'

  # Trigger with an email address
  curl -X POST 'https://api.resend.com/events/send' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d '{
    "event": "user.created",
    "email": "steve.wozniak@gmail.com",
    "payload": {
      "plan": "pro"
    }
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  # Trigger with a contact ID
  resend events send \
    --event user.created \
    --contact-id 7f2e4a3b-dfbc-4e9a-8b2c-5f3a1d6e7c8b \
    --payload '{"plan":"pro"}'

  # Trigger with an email address
  resend events send \
    --event user.created \
    --email steve.wozniak@gmail.com \
    --payload '{"plan":"pro"}'
  ```
</RequestExample>

<Note>
  Successful requests return **202 Accepted** with the JSON body below.
</Note>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "event",
    "event": "user.created"
  }
  ```
</ResponseExample>
