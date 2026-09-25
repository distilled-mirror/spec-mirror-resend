> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Clicked Links

> Retrieve the links clicked in a broadcast.

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

Retrieve every link clicked in a broadcast, ranked by total clicks. Results are
paginated with cursors. See [Pagination](/docs/api-reference/pagination) for how
`after` and `before` work.

<Info>
  Responses are cached for up to 15 minutes, so requesting the same page again
  may return slightly stale data within that window.
</Info>

## Path Parameters

<ResendParamField path="broadcast_id" type="string" required>
  The broadcast ID.
</ResendParamField>

## Query Parameters

<ResendParamField query="limit" type="number">
  Number of links to return. Between `1` and `100`. Defaults to `20`.
</ResendParamField>

<ResendParamField query="after" type="string">
  Cursor to fetch the page after this link. Cannot be used with `before`.
</ResendParamField>

<ResendParamField query="before" type="string">
  Cursor to fetch the page before this link. Cannot be used with `after`.
</ResendParamField>

## Response Fields

<ParamField body="object" type="string">
  Always `list`.
</ParamField>

<ParamField body="has_more" type="boolean">
  Whether more links exist beyond this page.
</ParamField>

<ParamField body="data" type="array">
  The clicked links, ordered by total clicks, descending.

  <Expandable defaultOpen="true" title="properties">
    <ParamField body="id" type="string">
      An opaque cursor for this row, used only for pagination. It does not
      identify any entity in Resend.
    </ParamField>

    <ParamField body="url" type="string">
      The URL that was clicked.
    </ParamField>

    <ParamField body="clicks" type="number">
      Total clicks on this link, including repeat clicks by the same
      recipient.
    </ParamField>

    <ParamField body="unique_clicks" type="number">
      The number of distinct recipients who clicked this link.
    </ParamField>
  </Expandable>
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.broadcasts.clickedLinks(
    '559ac32e-9ef5-46fb-82a1-b76b840c0f7b',
    { limit: 20 },
  );
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->broadcasts->clickedLinks->list('559ac32e-9ef5-46fb-82a1-b76b840c0f7b',[
    'limit' => 20
  ]);
  ```

  ```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  resend.Broadcasts.clicked_links(
      id="559ac32e-9ef5-46fb-82a1-b76b840c0f7b",
      params={"limit": 20},
  )
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  Resend::Broadcasts.clicked_links("559ac32e-9ef5-46fb-82a1-b76b840c0f7b", { limit: 20 })
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v4"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	client.Broadcasts.ClickedLinks("559ac32e-9ef5-46fb-82a1-b76b840c0f7b")
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{Resend, Result, list_opts::ListOptions};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _links = resend
      .broadcasts
      .clicked_links("559ac32e-9ef5-46fb-82a1-b76b840c0f7b", ListOptions::default())
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.Resend;
  import com.resend.services.broadcasts.model.ListBroadcastClickedLinksResponseSuccess;

  Resend resend = new Resend("re_xxxxxxxxx");

  ListBroadcastClickedLinksResponseSuccess data = resend.broadcasts().clickedLinks("559ac32e-9ef5-46fb-82a1-b76b840c0f7b");
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.BroadcastClickedLinksAsync( new Guid( "559ac32e-9ef5-46fb-82a1-b76b840c0f7b" ) );
  Console.WriteLine( "Nr Links={0}", resp.Content.Data.Count );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/broadcasts/559ac32e-9ef5-46fb-82a1-b76b840c0f7b/clicked-links?limit=20' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend broadcasts clicked-links 559ac32e-9ef5-46fb-82a1-b76b840c0f7b --limit 20
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "list",
    "has_more": true,
    "data": [
      {
        "id": "b2Zmc2V0OjA",
        "url": "https://resend.com/pricing",
        "clicks": 42,
        "unique_clicks": 30
      },
      {
        "id": "b2Zmc2V0OjE",
        "url": "https://resend.com/docs",
        "clicks": 17,
        "unique_clicks": 15
      }
    ]
  }
  ```
</ResponseExample>
