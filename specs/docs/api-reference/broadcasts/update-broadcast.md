> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Broadcast

> Update a broadcast to send to your contacts.

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

<ResendParamField path="broadcast_id" type="string" required>
  The ID of the broadcast you want to update.
</ResendParamField>

## Body Parameters

<ResendParamField body="segment_id" type="string">
  The ID of the segment you want to send to.

  <Info>
    Audiences are now called Segments. Follow the [Migration
    Guide](/docs/dashboard/segments/migrating-from-audiences-to-segments).
  </Info>
</ResendParamField>

<ParamField body="from" type="string">
  Sender email address.

  To include a friendly name, use the format `"Your Name <sender@domain.com>"`.
</ParamField>

<ParamField body="subject" type="string">
  Email subject.
</ParamField>

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

<ParamField body="name" type="string">
  The friendly name of the broadcast. Only used for internal reference.
</ParamField>

<ResendParamField body="topic_id" type="string">
  The topic ID that the broadcast will be scoped to.
</ResendParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.broadcasts.update(
    '49a3999c-0ce1-4ea6-ab68-afcd6dc2e794',
    {
      html: 'Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}',
    },
  );
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->broadcasts->update('49a3999c-0ce1-4ea6-ab68-afcd6dc2e794', [
    'html' => 'Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}',
  ]);
  ```

  ```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  params: resend.Broadcasts.UpdateParams = {
    "id": "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}"
  }

  resend.Broadcasts.update(params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  params = {
    "id": "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
  }
  Resend::Broadcasts.update(params)
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v3"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	params := &resend.UpdateBroadcastRequest{
  		Id:   "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794",
  		Html: "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
  	}

  	client.Broadcasts.Update(params)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{types::UpdateBroadcastOptions, Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let id = "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794";
    let html = "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}";

    let opts = UpdateBroadcastOptions::new().with_html(html);

    let _broadcast = resend.broadcasts.update(id, opts).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  Resend resend = new Resend("re_xxxxxxxxx");

  UpdateBroadcastOptions params = UpdateBroadcastOptions.builder()
      .id("49a3999c-0ce1-4ea6-ab68-afcd6dc2e794")
      .html("Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}")
      .build();

  UpdateBroadcastResponseSuccess data = resend.broadcasts().update(params);
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.BroadcastUpdateAsync(
      new Guid( "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794" ),
      new BroadcastUpdateData()
      {
          HtmlBody = "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
      }
  );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X PATCH 'https://api.resend.com/broadcasts/49a3999c-0ce1-4ea6-ab68-afcd6dc2e794' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}"
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend broadcasts update 49a3999c-0ce1-4ea6-ab68-afcd6dc2e794 \
    --html "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}"
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "broadcast",
    "id": "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794"
  }
  ```
</ResponseExample>
