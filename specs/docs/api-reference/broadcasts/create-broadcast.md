> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Broadcast

> Create a new broadcast to send to your contacts.

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

<ResendParamField body="segment_id" type="string" required>
  The ID of the segment you want to send to.

  <Info>
    Audiences are now called Segments. Follow the [Migration
    Guide](/docs/dashboard/segments/migrating-from-audiences-to-segments).
  </Info>
</ResendParamField>

<ParamField body="from" type="string" required>
  Sender email address.

  To include a friendly name, pass the sender as `Name <email@example.com>`, for example `Acme <onboarding@example.dev>`.
</ParamField>

<ParamField body="subject" type="string" required>
  Email subject.
</ParamField>

<ResendParamField body="reply_to" type="string | string[]">
  Reply-to email address. For multiple addresses, send as an array of strings.
</ResendParamField>

<ParamField body="html" type="string">
  The HTML version of the message. You can include Contact Properties in the
  body of the Broadcast. Learn more about [Contact
  Properties](/docs/dashboard/audiences/contacts).
</ParamField>

<ParamField body="text" type="string">
  The plain text version of the message. You can include Contact Properties in the body of the Broadcast. Learn more about [Contact Properties](/docs/dashboard/audiences/contacts).

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
  Optional. Omit it to send to every subscribed contact in the segment, without
  checking topic preferences.
</ResendParamField>

<ParamField body="send" type="boolean">
  Send the broadcast immediately after creation. Defaults to `false`.

  <Info>
    When set to `true`, the broadcast will be sent or scheduled (if `scheduled_at` is provided) without requiring a separate call to the [Send Broadcast](/docs/api-reference/broadcasts/send-broadcast) endpoint.
  </Info>
</ParamField>

<ResendParamField body="scheduled_at" type="string">
  Schedule the broadcast to be sent later. The date should be in natural language (e.g.: `in 1 min`) or ISO 8601 format (e.g: `2026-08-05T11:52:01.858Z`).

  <Warning>
    This parameter requires `send` to be set to `true`.
  </Warning>
</ResendParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  // Create a draft broadcast
  const { data, error } = await resend.broadcasts.create({
    segmentId: '78261eea-8f8b-4381-83c6-79fa7120f1cf',
    from: 'Acme <onboarding@resend.dev>',
    subject: 'hello world',
    html: 'Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}',
  });

  // Create and send immediately
  const { data: sent, error: sendError } = await resend.broadcasts.create({
    segmentId: '78261eea-8f8b-4381-83c6-79fa7120f1cf',
    from: 'Acme <onboarding@resend.dev>',
    subject: 'hello world',
    html: 'Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}',
    send: true,
  });

  // Create and schedule
  const { data: scheduled, error: scheduleError } =
    await resend.broadcasts.create({
      segmentId: '78261eea-8f8b-4381-83c6-79fa7120f1cf',
      from: 'Acme <onboarding@resend.dev>',
      subject: 'hello world',
      html: 'Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}',
      send: true,
      scheduledAt: 'in 1 hour',
    });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  // Create a draft broadcast
  $resend->broadcasts->create([
    'segment_id' => '78261eea-8f8b-4381-83c6-79fa7120f1cf',
    'from' => 'Acme <onboarding@resend.dev>',
    'subject' => 'hello world',
    'html' => 'Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}',
  ]);

  // Create and send immediately
  $resend->broadcasts->create([
    'segment_id' => '78261eea-8f8b-4381-83c6-79fa7120f1cf',
    'from' => 'Acme <onboarding@resend.dev>',
    'subject' => 'hello world',
    'html' => 'Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}',
    'send' => true,
  ]);

  // Create and schedule
  $resend->broadcasts->create([
    'segment_id' => '78261eea-8f8b-4381-83c6-79fa7120f1cf',
    'from' => 'Acme <onboarding@resend.dev>',
    'subject' => 'hello world',
    'html' => 'Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}',
    'send' => true,
    'scheduled_at' => 'in 1 hour',
  ]);
  ```

  ```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  # Create a draft broadcast
  params: resend.Broadcasts.CreateParams = {
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "Hello, world!",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
  }
  resend.Broadcasts.create(params)

  # Create and send immediately
  params: resend.Broadcasts.CreateParams = {
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "Hello, world!",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
    "send": True,
  }
  resend.Broadcasts.create(params)

  # Create and schedule
  params: resend.Broadcasts.CreateParams = {
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "Hello, world!",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
    "send": True,
    "scheduled_at": "in 1 hour",
  }
  resend.Broadcasts.create(params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  # Create a draft broadcast
  params = {
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "hello world",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
  }
  Resend::Broadcasts.create(params)

  # Create and send immediately
  params = {
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "Hello, world!",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
    "send": true,
  }
  Resend::Broadcasts.create(params)

  # Create and schedule
  params = {
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "Hello, world!",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
    "send": true,
    "scheduled_at": "in 1 hour",
  }
  Resend::Broadcasts.create(params)

  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v4"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	// Create a draft broadcast
  	params := &resend.CreateBroadcastRequest{
  		SegmentId: "78261eea-8f8b-4381-83c6-79fa7120f1cf",
  		From:      "Acme <onboarding@resend.dev>",
  		Html:      "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
  		Subject:   "Hello, world!",
  	}
  	client.Broadcasts.Create(params)

  	// Create and send immediately
  	params = &resend.CreateBroadcastRequest{
  		SegmentId: "78261eea-8f8b-4381-83c6-79fa7120f1cf",
  		From:      "Acme <onboarding@resend.dev>",
  		Subject:   "Hello, world!",
  		Html:      "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
  		Send:      true,
  	}
  	client.Broadcasts.Create(params)

  	// Create and schedule
  	params = &resend.CreateBroadcastRequest{
  		SegmentId:   "78261eea-8f8b-4381-83c6-79fa7120f1cf",
  		From:        "Acme <onboarding@resend.dev>",
  		Subject:     "Hello, world!",
  		Html:        "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
  		Send:        true,
  		ScheduledAt: "in 1 hour",
  	}
  	client.Broadcasts.Create(params)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{types::CreateBroadcastOptions, Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let segment_id = "78261eea-8f8b-4381-83c6-79fa7120f1cf";
    let from = "Acme <onboarding@resend.dev>";
    let subject = "hello world";
    let html = "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}";

    let opts = CreateBroadcastOptions::new(segment_id, from, subject).with_html(html);

    // Create a draft broadcast
    let _broadcast = resend.broadcasts.create(opts.clone()).await?;

    // Create and send immediately
    let _broadcast = resend
      .broadcasts
      .create(opts.clone().with_send(true))
      .await?;

    // Create and schedule
    let _broadcast = resend
      .broadcasts
      .create(opts.with_send(true).with_scheduled_at("in 1 hour"))
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.Resend;
  import com.resend.services.broadcasts.model.CreateBroadcastOptions;
  import com.resend.services.broadcasts.model.CreateBroadcastResponseSuccess;

  Resend resend = new Resend("re_xxxxxxxxx");

  // Create a draft broadcast
  CreateBroadcastOptions params = CreateBroadcastOptions.builder()
      .segmentId("78261eea-8f8b-4381-83c6-79fa7120f1cf")
      .from("Acme <onboarding@resend.dev>")
      .subject("hello world")
      .html("Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}")
      .build();
  CreateBroadcastResponseSuccess data = resend.broadcasts().create(params);

  // Create and send immediately
  CreateBroadcastOptions sendParams = CreateBroadcastOptions.builder()
      .segmentId("78261eea-8f8b-4381-83c6-79fa7120f1cf")
      .from("Acme <onboarding@resend.dev>")
      .subject("hello world")
      .html("Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}")
      .send(true)
      .build();
  CreateBroadcastResponseSuccess sent = resend.broadcasts().create(sendParams);

  // Create and schedule
  CreateBroadcastOptions scheduleParams = CreateBroadcastOptions.builder()
      .segmentId("78261eea-8f8b-4381-83c6-79fa7120f1cf")
      .from("Acme <onboarding@resend.dev>")
      .subject("hello world")
      .html("Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}")
      .send(true)
      .scheduledAt("in 1 hour")
      .build();
  CreateBroadcastResponseSuccess scheduled = resend.broadcasts().create(scheduleParams);
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  // Create a draft broadcast
  var resp = await resend.BroadcastAddAsync(
      new BroadcastData()
      {
          DisplayName = "Example Broadcast",
          SegmentId = new Guid( "78261eea-8f8b-4381-83c6-79fa7120f1cf" ),
          From = "Acme <onboarding@resend.dev>",
          Subject = "Hello, world!",
          HtmlBody = "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
      }
  );

  Console.WriteLine( "Broadcast Id={0}", resp.Content );

  // Create and send immediately
  var sent = await resend.BroadcastAddAsync(
      new BroadcastData()
      {
          DisplayName = "Example Broadcast",
          SegmentId = new Guid( "78261eea-8f8b-4381-83c6-79fa7120f1cf" ),
          From = "Acme <onboarding@resend.dev>",
          Subject = "Hello, world!",
          HtmlBody = "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
          SendAfterAdd = true,
      }
  );

  Console.WriteLine( "Broadcast Id={0}", sent.Content );

  // Create and schedule
  var scheduled = await resend.BroadcastAddAsync(
      new BroadcastData()
      {
          DisplayName = "Example Broadcast",
          SegmentId = new Guid( "78261eea-8f8b-4381-83c6-79fa7120f1cf" ),
          From = "Acme <onboarding@resend.dev>",
          Subject = "Hello, world!",
          HtmlBody = "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
          SendAfterAdd = true,
          MomentSchedule = DateTime.UtcNow.AddHours( 1 ),
      }
  );

  Console.WriteLine( "Broadcast Id={0}", scheduled.Content );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  # Create a draft broadcast
  curl -X POST 'https://api.resend.com/broadcasts' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'
  {
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "hello world",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}"
  }'

  # Create and send immediately
  curl -X POST 'https://api.resend.com/broadcasts' \
   -H 'Authorization: Bearer re_xxxxxxxxx' \
   -H 'Content-Type: application/json' \
   -d $'
  {
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "hello world",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
    "send": true
  }'

  # Create and schedule
  curl -X POST 'https://api.resend.com/broadcasts' \
   -H 'Authorization: Bearer re_xxxxxxxxx' \
   -H 'Content-Type: application/json' \
   -d $'
  {
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "hello world",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
    "send": true,
    "scheduled_at": "in 1 hour"
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  # Create a draft broadcast
  resend broadcasts create \
    --from "Acme <onboarding@resend.dev>" \
    --subject "hello world" \
    --segment-id 78261eea-8f8b-4381-83c6-79fa7120f1cf \
    --html "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}"

  # Create and send immediately
  resend broadcasts create \
    --from "Acme <onboarding@resend.dev>" \
    --subject "hello world" \
    --segment-id 78261eea-8f8b-4381-83c6-79fa7120f1cf \
    --html "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}" \
    --send

  # Create and schedule
  resend broadcasts create \
    --from "Acme <onboarding@resend.dev>" \
    --subject "hello world" \
    --segment-id 78261eea-8f8b-4381-83c6-79fa7120f1cf \
    --html "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}" \
    --send \
    --scheduled-at "in 1 hour"
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
