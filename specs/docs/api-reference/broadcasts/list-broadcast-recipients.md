> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Recipients

> Retrieve the recipients of a broadcast for a given event type.

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

Retrieve the recipients of a broadcast, filtered by a single event `type` (for
example everyone who `opened`, `clicked`, or `bounced`). Results are paginated
with cursors. See [Pagination](/docs/api-reference/pagination) for how `after` and
`before` work.

<Info>
  Responses are cached for up to 15 minutes, so requesting the same page again
  may return slightly stale data within that window.
</Info>

## Path Parameters

<ResendParamField path="broadcast_id" type="string" required>
  The broadcast ID.
</ResendParamField>

## Query Parameters

<ResendParamField query="type" type="string" required>
  The event to filter recipients by. One of `sent`, `delivered`, `opened`,
  `clicked`, `bounced`, `complained`, `unsubscribed`, or `suppressed`.
</ResendParamField>

<ResendParamField query="limit" type="number">
  Number of recipients to return. Between `1` and `100`. Defaults to `20`.
</ResendParamField>

<ResendParamField query="after" type="string">
  Cursor to fetch the page after this recipient. Cannot be used with `before`.
</ResendParamField>

<ResendParamField query="before" type="string">
  Cursor to fetch the page before this recipient. Cannot be used with `after`.
</ResendParamField>

<ResendParamField query="email" type="string">
  Filter recipients whose email contains this value.
</ResendParamField>

<ResendParamField query="bounce_type" type="string">
  Filter by bounce classification. One of `permanent`, `transient`, or
  `undetermined`. Can only be used with `type=bounced`.
</ResendParamField>

## Response Fields

<ParamField body="object" type="string">
  Always `list`.
</ParamField>

<ParamField body="has_more" type="boolean">
  Whether more recipients exist beyond this page.
</ParamField>

<ParamField body="data" type="array">
  The recipients matching the requested `type`.

  <Expandable defaultOpen="true" title="properties">
    <ParamField body="id" type="string">
      An opaque cursor for this row, used only for pagination. It does not
      identify any entity in Resend. Use `contact_id` to reference the contact.
    </ParamField>

    <ParamField body="contact_id" type="string | null">
      The matching contact's ID. `null` when the recipient's email no longer
      maps to a contact.
    </ParamField>

    <ParamField body="email" type="string">
      The recipient's email address.
    </ParamField>

    <ParamField body="count" type="number">
      How many times the recipient triggered the event. Only returned for
      `type=opened` and `type=clicked`.
    </ParamField>

    <ParamField body="bounce_type" type="string | null">
      The bounce classification: `permanent`, `transient`, or `undetermined`.
      Only returned for `type=bounced`.
    </ParamField>

    <ParamField body="clicked_links" type="array">
      The links this recipient clicked. Only returned for `type=clicked`.

      <Expandable title="properties">
        <ParamField body="url" type="string">
          The URL that was clicked.
        </ParamField>

        <ParamField body="clicks" type="number">
          How many times the recipient clicked this link.
        </ParamField>
      </Expandable>
    </ParamField>
  </Expandable>
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.broadcasts.recipients(
    '559ac32e-9ef5-46fb-82a1-b76b840c0f7b',
    { type: 'clicked', limit: 20 },
  );
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->broadcasts->recipients('559ac32e-9ef5-46fb-82a1-b76b840c0f7b', [
    'type' => 'clicked',
    'limit' => 20
  ]);
  ```

  ```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  resend.Broadcasts.recipients(
      "559ac32e-9ef5-46fb-82a1-b76b840c0f7b", {"type": "clicked", "limit": 20}
  )
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  Resend::Broadcasts.recipients(
    "559ac32e-9ef5-46fb-82a1-b76b840c0f7b",
    { type: "clicked", limit: 20 },
  )
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v3"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	limit := 20
  	client.Broadcasts.Recipients("559ac32e-9ef5-46fb-82a1-b76b840c0f7b", &resend.ListBroadcastRecipientsOptions{
  		Type:  resend.BroadcastRecipientEventTypeClicked,
  		Limit: &limit,
  	})
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{types::{BroadcastRecipientEventType, ListRecipientsOptions}, Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let list_opts = ListRecipientsOptions::new(BroadcastRecipientEventType::Clicked).with_limit(20);

    let _recipients = resend
      .broadcasts
      .recipients("559ac32e-9ef5-46fb-82a1-b76b840c0f7b", list_opts)
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  Resend resend = new Resend("re_xxxxxxxxx");

  ListBroadcastRecipientsResponseSuccess data = resend.broadcasts().recipients(
      "559ac32e-9ef5-46fb-82a1-b76b840c0f7b",
      ListBroadcastRecipientsParams.builder()
          .type(BroadcastRecipientEventType.CLICKED)
          .limit(20)
          .build());
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.BroadcastListRecipientsAsync(
      new Guid( "559ac32e-9ef5-46fb-82a1-b76b840c0f7b" ),
      BroadcastRecipientEventType.Clicked,
      new BroadcastListRecipientsQuery() { Limit = 20 } );
  Console.WriteLine( "Recipients={0}", resp.Content.Data.Count );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/broadcasts/559ac32e-9ef5-46fb-82a1-b76b840c0f7b/recipients?type=clicked&limit=20' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend broadcasts recipients 559ac32e-9ef5-46fb-82a1-b76b840c0f7b --type clicked --limit 20
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
        "contact_id": "e169aa45-1ecf-4183-9955-b1499d5701d3",
        "email": "carter@example.com",
        "count": 3,
        "clicked_links": [
          { "url": "https://resend.com/pricing", "clicks": 2 },
          { "url": "https://resend.com/docs", "clicks": 1 }
        ]
      },
      {
        "id": "b2Zmc2V0OjE",
        "contact_id": null,
        "email": "dana@example.com",
        "count": 1,
        "clicked_links": [{ "url": "https://resend.com/pricing", "clicks": 1 }]
      }
    ]
  }
  ```
</ResponseExample>
