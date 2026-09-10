> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Event

> Update an existing event schema.

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

<ResendParamField path="id" type="string" required>
  The event ID or name.
</ResendParamField>

## Body Parameters

<ParamField body="schema" type="object" required>
  The updated schema definition for the event payload. Must be an object with
  flat key/type pairs, or `null` to clear the schema. Supported types: `string`,
  `number`, `boolean`, `date`.
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.events.update('user.created', {
    schema: {
      plan: 'string',
      trial: 'boolean',
    },
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->events->update('user.created', [
    'schema' => [
      'plan' => 'string',
      'trial' => 'boolean',
    ],
  ]);
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  params: resend.Events.UpdateParams = {
    "identifier": "user.created",
    "schema": {
      "plan": "string",
      "trial": "boolean",
    },
  }

  resend.Events.update(params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  params = {
    identifier: "user.created",
    schema: {
      plan: "string",
      trial: "boolean",
    },
  }

  Resend::Events.update(params)
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v3"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	params := &resend.UpdateEventRequest{
  		Schema: map[string]string{
  			"plan":  resend.EventSchemaTypeString,
  			"trial": resend.EventSchemaTypeBoolean,
  		},
  	}

  	client.Events.Update("user.created", params)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{json, types::UpdateEventOptions, Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let opts = UpdateEventOptions {
      schema: json!({
        "plan": "string",
        "trial": "boolean",
      }),
    };

    let _event = resend.events.update("user.created", opts).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;

  public class Main {
      public static void main(String[] args) {
          Resend resend = new Resend("re_xxxxxxxxx");

          UpdateEventOptions params = UpdateEventOptions.builder()
                  .identifier("user.created")
                  .addSchema("plan", "string")
                  .addSchema("trial", "boolean")
                  .build();

          UpdateEventResponseSuccess data = resend.events().update(params);
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;
  using System.Text.Json;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

  var schema = JsonSerializer.SerializeToElement( new { plan = "string", trial = "boolean" } );

  var resp = await resend.EventUpdateAsync( "user.created", new EventUpdateData { Schema = schema } );
  Console.WriteLine( "EventId={0}", resp.Content );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X PATCH 'https://api.resend.com/events/user.created' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d '{
    "schema": {
      "plan": "string",
      "trial": "boolean"
    }
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend events update user.created --schema '{"plan":"string","trial":"boolean"}'
  ```
</RequestExample>

<Note>Successful updates return **200 OK** with the JSON body below.</Note>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "event",
    "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
  }
  ```
</ResponseExample>
