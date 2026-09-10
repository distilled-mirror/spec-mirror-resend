> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Compose and send Broadcasts with the API

> Send marketing emails using the Broadcasts API.

Resend's [no-code Broadcast editor](/docs/dashboard/broadcasts/editor) allows all members of your team to write and send email campaigns directly in the Resend Dashboard, without having to ask for help from developers.

To programmatically create, update, and send Broadcasts, you can use the [Broadcast API](/docs/api-reference/broadcasts/create-broadcast). There are also API endpoints to list, retrieve, and delete Broadcasts, allowing you to manage your marketing campaigns directly from your application.

## Create Broadcasts

The [`create()` method](/docs/api-reference/broadcasts/create-broadcast) takes the same sending properties that can be set in the Editor composer. This allows developers to also create drafts without sending, schedule sending for a time in the future, [personalize with dynamic content data](/docs/dashboard/broadcasts/editor#personalize-your-content), and more.

Set the `send` property to `true` to send immediately or to schedule the Broadcast, or leave `false` (the default) to create a draft:

<CodeGroup>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  // Create a draft Broadcast
  const { data, error } = await resend.broadcasts.create({
    segmentId: '78261eea-8f8b-4381-83c6-79fa7120f1cf',
    from: 'Acme <onboarding@resend.dev>',
    subject: 'hello world',
    html: 'Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}',
  });

  // Create and send immediately
  const { data, error } = await resend.broadcasts.create({
    segmentId: '78261eea-8f8b-4381-83c6-79fa7120f1cf',
    from: 'Acme <onboarding@resend.dev>',
    subject: 'hello world',
    html: 'Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}',
    send: true,
  });

  // Create and schedule
  const { data, error } = await resend.broadcasts.create({
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

  // Create a draft Broadcast
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

  // Create a draft Broadcast
  params: resend.Broadcasts.CreateParams = {
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "Hello, world!",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
  }
  resend.Broadcasts.create(params)

  // Create and send immediately
  params: resend.Broadcasts.CreateParams = {
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "Hello, world!",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
    "send": true,
  }
  resend.Broadcasts.create(params)

  // Create and schedule
  params: resend.Broadcasts.CreateParams = {
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "Hello, world!",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
    "send": true,
    "scheduled_at": "in 1 hour",
  }
  resend.Broadcasts.create(params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  // Create a draft Broadcast
  params = {
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "hello world",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
  }
  Resend::Broadcasts.create(params)

  // Create and send immediately
  params = {
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "Hello, world!",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
    "send": true,
  }
  Resend::Broadcasts.create(params)

  // Create and schedule
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

  import "github.com/resend/resend-go/v3"

  // Create a draft Broadcast
  params := &resend.CreateBroadcastRequest{
    SegmentId: "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    From:       "Acme <onboarding@resend.dev>",
    Html:       "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
    Subject:    "Hello, world!",
  }
  broadcast, _ := client.Broadcasts.Create(params)

  // Create and send immediately
  params = {
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "Hello, world!",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
    "send": true,
  }
  broadcast, _ := client.Broadcasts.Create(params)

  // Create and schedule
  params = {
    "segment_id": "78261eea-8f8b-4381-83c6-79fa7120f1cf",
    "from": "Acme <onboarding@resend.dev>",
    "subject": "Hello, world!",
    "html": "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
    "send": true,
    "scheduled_at": "in 1 hour",
  }
  broadcast, _ := client.Broadcasts.Create(params)
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

    // Create a draft Broadcast
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
  Resend resend = new Resend("re_xxxxxxxxx");

  // Create a draft Broadcast
  CreateBroadcastOptions params = CreateBroadcastOptions.builder()
      .segmentId("78261eea-8f8b-4381-83c6-79fa7120f1cf")
      .from("Acme <onboarding@resend.dev>")
      .subject("hello world")
      .html("Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}")
      .build();
  CreateBroadcastResponseSuccess data = resend.broadcasts().create(params);

  // Create and send immediately
  CreateBroadcastOptions params = CreateBroadcastOptions.builder()
      .segmentId("78261eea-8f8b-4381-83c6-79fa7120f1cf")
      .from("Acme <onboarding@resend.dev>")
      .subject("hello world")
      .html("Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}")
      .send(true)
      .build();
  CreateBroadcastResponseSuccess data = resend.broadcasts().create(params);

  // Create and schedule
  CreateBroadcastOptions params = CreateBroadcastOptions.builder()
      .segmentId("78261eea-8f8b-4381-83c6-79fa7120f1cf")
      .from("Acme <onboarding@resend.dev>")
      .subject("hello world")
      .html("Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}")
      .send(true)
      .scheduledAt("in 1 hour")
      .build();
  CreateBroadcastResponseSuccess data = resend.broadcasts().create(params);
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  // Create a draft Broadcast
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
  var resp = await resend.BroadcastAddAsync(
      new BroadcastData()
      {
          DisplayName = "Example Broadcast",
          SegmentId = new Guid( "78261eea-8f8b-4381-83c6-79fa7120f1cf" ),
          From = "Acme <onboarding@resend.dev>",
          Subject = "Hello, world!",
          HtmlBody = "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
          Send = true,
      }
  );

  Console.WriteLine( "Broadcast Id={0}", resp.Content );

  // Create and schedule
  var resp = await resend.BroadcastAddAsync(
      new BroadcastData()
      {
          DisplayName = "Example Broadcast",
          SegmentId = new Guid( "78261eea-8f8b-4381-83c6-79fa7120f1cf" ),
          From = "Acme <onboarding@resend.dev>",
          Subject = "Hello, world!",
          HtmlBody = "Hi {{{contact.first_name|there}}}, you can unsubscribe here: {{{RESEND_UNSUBSCRIBE_URL}}}",
          Send = true,
          ScheduledAt = DateTime.UtcNow.AddHours( 1 ),
      }
  );

  Console.WriteLine( "Broadcast Id={0}", resp.Content );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  # Create a draft Broadcast
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
  # Create a draft Broadcast
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
</CodeGroup>

## Send Broadcasts

Use the [`send()` method](/docs/api-reference/broadcasts/send-broadcast) to send or schedule an existing API-created Broadcast by ID. Broadcasts created using the Dashboard Broadcast editor cannot be sent with this endpoint.

<CodeGroup>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.broadcasts.send(
    '559ac32e-9ef5-46fb-82a1-b76b840c0f7b',
    {
      scheduledAt: 'in 1 min',
    },
  );
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->broadcasts->send('559ac32e-9ef5-46fb-82a1-b76b840c0f7b', [
    'scheduled_at' => 'in 1 min',
  ]);
  ```

  ```py Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  params: resend.Broadcasts.SendParams = {
    "broadcast_id": "559ac32e-9ef5-46fb-82a1-b76b840c0f7b",
    "scheduled_at": "in 1 min"
  }
  resend.Broadcasts.send(params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  params = {
    broadcast_id: "559ac32e-9ef5-46fb-82a1-b76b840c0f7b",
    scheduled_at: "in 1 min"
  }
  Resend::Broadcasts.send(params)
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v3"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	sendParams := &resend.SendBroadcastRequest{
  		BroadcastId: "559ac32e-9ef5-46fb-82a1-b76b840c0f7b",
  		ScheduledAt: "in 1 min",
  	}

  	client.Broadcasts.Send(sendParams)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{types::SendBroadcastOptions, Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let opts =
      SendBroadcastOptions::new("559ac32e-9ef5-46fb-82a1-b76b840c0f7b").with_scheduled_at("in 1 min");

    let _broadcast = resend.broadcasts.send(opts).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  Resend resend = new Resend("re_xxxxxxxxx");

  SendBroadcastOptions params = SendBroadcastOptions.builder()
      .scheduledAt("in 1 min")
      .build();

  SendBroadcastResponseSuccess data = resend.broadcasts().send(params,
      "498ee8e4-7aa2-4eb5-9f04-4194848049d1");
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  // Send now
  await resend.BroadcastSendAsync( new Guid( "559ac32e-9ef5-46fb-82a1-b76b840c0f7b" ) );

  // Send in 5 mins
  await resend.BroadcastScheduleAsync(
      new Guid( "559ac32e-9ef5-46fb-82a1-b76b840c0f7b" ),
      DateTime.UtcNow.AddMinutes( 5 ) );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/broadcasts/559ac32e-9ef5-46fb-82a1-b76b840c0f7b/send' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "scheduled_at": "in 1 min"
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend broadcasts send 559ac32e-9ef5-46fb-82a1-b76b840c0f7b --scheduled-at "in 1 min"
  ```
</CodeGroup>

## Other ways to send

You can also send and manage Broadcasts using [Resend CLI commands](/docs/cli#broadcasts) and [AI building tools](/docs/ai-onboarding).

## API Reference

For complete API documentation, see the [Broadcasts API reference](/docs/api-reference/broadcasts/create-broadcast).
