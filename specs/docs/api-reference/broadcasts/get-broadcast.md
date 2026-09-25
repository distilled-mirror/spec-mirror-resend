> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Retrieve Broadcast

> Retrieve a single broadcast.

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

You can retrieve broadcasts created via both this API and the Resend dashboard.

## Path Parameters

<ResendParamField path="broadcast_id" type="string" required>
  The broadcast ID.
</ResendParamField>

<Info>
  See all available `status` types in [the Broadcasts
  overview](/docs/dashboard/broadcasts/manage-broadcasts#understand-broadcast-statuses).
</Info>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.broadcasts.get(
    '559ac32e-9ef5-46fb-82a1-b76b840c0f7b',
  );
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->broadcasts->get('559ac32e-9ef5-46fb-82a1-b76b840c0f7b');
  ```

  ```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  resend.Broadcasts.get(id="559ac32e-9ef5-46fb-82a1-b76b840c0f7b")
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  Resend::Broadcasts.get("559ac32e-9ef5-46fb-82a1-b76b840c0f7b")
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v4"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	client.Broadcasts.Get("559ac32e-9ef5-46fb-82a1-b76b840c0f7b")
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _broadcast = resend
      .broadcasts
      .get("559ac32e-9ef5-46fb-82a1-b76b840c0f7b")
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.Resend;
  import com.resend.services.broadcasts.model.GetBroadcastResponseSuccess;

  Resend resend = new Resend("re_xxxxxxxxx");

  GetBroadcastResponseSuccess data = resend.broadcasts().get("559ac32e-9ef5-46fb-82a1-b76b840c0f7b");
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.BroadcastRetrieveAsync( new Guid( "559ac32e-9ef5-46fb-82a1-b76b840c0f7b" ) );
  Console.WriteLine( "Broadcast name={0}", resp.Content.DisplayName );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/broadcasts/559ac32e-9ef5-46fb-82a1-b76b840c0f7b' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend broadcasts get 559ac32e-9ef5-46fb-82a1-b76b840c0f7b
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "broadcast",
    "id": "559ac32e-9ef5-46fb-82a1-b76b840c0f7b",
    "name": "Announcements",
    "audience_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf", // now called segment_id
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "hello world",
    "reply_to": null,
    "preview_text": "Check out our latest announcements",
    "html": "<p>Hello {{{contact.first_name|there}}}!</p>",
    "text": "Hello {{{contact.first_name|there}}}!",
    "status": "draft",
    "created_at": "2026-12-01 19:32:22.980+00",
    "scheduled_at": null,
    "sent_at": null,
    "topic_id": "b6d24b8e-af0b-4c3c-be0c-359bbd97381e"
  }
  ```
</ResponseExample>
