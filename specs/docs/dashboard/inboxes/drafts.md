> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Inbox Drafts

> Learn how to create, update, and send draft emails in the inbox.

A draft is an unsent email in an inbox. A draft can start a new conversation, or be a reply to an email in an existing thread. Drafts are shared with your team, so anyone can pick up a draft, edit it and send it.

## Create a draft

### Using the dashboard

**1. Open an inbox.**

Select an inbox from the [Inboxes dashboard](https://resend.com/inboxes).

**2. Click the **Compose** button.**

You can also press <kbd>C</kbd>.

**3. Enter the recipients, subject and message.**

Click **Cc** or **Bcc** to add more recipients. You can add up to 50
recipients in total.

The draft saves automatically as you write, so there is no save button. You can minimize the composer and return to it later from the **Drafts** folder.

To reply to or forward an email in a thread, use the **Reply**, **Reply all** or **Forward** buttons while viewing the thread. The reply opens inline beneath the email and is also saved as a draft as you write.

### Using the API

Omit `thread_id` to create a draft for a new conversation.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.drafts.create({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  to: ['ada@example.com'],
  subject: 'Refund for order 1041',
  html: '<p>Refund issued for order 1041.</p>',
  text: 'Refund issued for order 1041.',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->drafts->create('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1', [
  'to' => ['ada@example.com'],
  'subject' => 'Refund for order 1041',
  'html' => '<p>Refund issued for order 1041.</p>',
  'text' => 'Refund issued for order 1041.',
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Drafts.CreateParams = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "to": ["ada@example.com"],
  "subject": "Refund for order 1041",
  "html": "<p>Refund issued for order 1041.</p>",
  "text": "Refund issued for order 1041.",
}

resend.Inboxes.Drafts.create(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "to": ["ada@example.com"],
  "subject": "Refund for order 1041",
  "html": "<p>Refund issued for order 1041.</p>",
  "text": "Refund issued for order 1041.",
}

Resend::Inboxes::Drafts.create(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.CreateInboxDraftRequest{
		To:      []string{"ada@example.com"},
		Subject: "Refund for order 1041",
		Html:    "<p>Refund issued for order 1041.</p>",
		Text:    "Refund issued for order 1041.",
	}

	client.Inboxes.Drafts.Create("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{types::CreateInboxDraftOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let draft = CreateInboxDraftOptions::new()
    .with_to(["ada@example.com"])
    .with_subject("Refund for order 1041")
    .with_html("<p>Refund issued for order 1041.</p>")
    .with_text("Refund issued for order 1041.");

  let _draft = resend
    .inboxes
    .create_draft("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", draft)
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.CreateInboxDraftOptions;
import com.resend.services.inboxes.model.CreateInboxDraftResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        CreateInboxDraftOptions params = CreateInboxDraftOptions.builder()
                .to("ada@example.com")
                .subject("Refund for order 1041")
                .html("<p>Refund issued for order 1041.</p>")
                .text("Refund issued for order 1041.")
                .build();

        CreateInboxDraftResponseSuccess data = resend.inboxes().drafts().create("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxDraftCreateAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new InboxDraftCreateData()
    {
        To = "ada@example.com",
        Subject = "Refund for order 1041",
        HtmlBody = "<p>Refund issued for order 1041.</p>",
        TextBody = "Refund issued for order 1041.",
    }
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/drafts' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "to": ["ada@example.com"],
  "subject": "Refund for order 1041",
  "html": "<p>Refund issued for order 1041.</p>",
  "text": "Refund issued for order 1041."
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes drafts create \
  --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --to ada@example.com \
  --subject "Refund for order 1041" \
  --html "<p>Refund issued for order 1041.</p>" \
  --text "Refund issued for order 1041."
```

To create a reply draft, pass `thread_id` and `reply_to_email_id` together. If you leave out `to`, it is set to the author of the email you are replying to, or its `Reply-To` address. If the inbox sent that email, `to` is set to that email's recipients instead. `cc` and `bcc` are never filled in. If you leave out `subject`, the draft is sent with the subject of the thread, prefixed with `Re:`.

An email can have only one unsent reply draft. Creating a second one returns the existing draft.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.drafts.create({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  replyToEmailId: '5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60',
  subject: 'Re: Refund for order 1041',
  text: 'Refund issued for order 1041.',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->drafts->create('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1', [
  'thread_id' => '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  'reply_to_email_id' => '5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60',
  'subject' => 'Re: Refund for order 1041',
  'text' => 'Refund issued for order 1041.',
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Drafts.CreateParams = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "thread_id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  "reply_to_email_id": "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
  "subject": "Re: Refund for order 1041",
  "text": "Refund issued for order 1041.",
}

resend.Inboxes.Drafts.create(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "thread_id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  "reply_to_email_id": "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
  "subject": "Re: Refund for order 1041",
  "text": "Refund issued for order 1041.",
}

Resend::Inboxes::Drafts.create(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.CreateInboxDraftRequest{
		ThreadId:       "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
		ReplyToEmailId: "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
		Subject:        "Re: Refund for order 1041",
		Text:           "Refund issued for order 1041.",
	}

	client.Inboxes.Drafts.Create("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{types::CreateInboxDraftOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let draft = CreateInboxDraftOptions::reply(
    "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
    "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
  )
  .with_subject("Re: Refund for order 1041")
  .with_text("Refund issued for order 1041.");

  let _draft = resend
    .inboxes
    .create_draft("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", draft)
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.CreateInboxDraftOptions;
import com.resend.services.inboxes.model.CreateInboxDraftResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        CreateInboxDraftOptions params = CreateInboxDraftOptions.builder()
                .threadId("4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12")
                .replyToEmailId("5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60")
                .subject("Re: Refund for order 1041")
                .text("Refund issued for order 1041.")
                .build();

        CreateInboxDraftResponseSuccess data = resend.inboxes().drafts().create("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxDraftCreateAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new InboxDraftCreateData()
    {
        ThreadId = new Guid( "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12" ),
        ReplyToEmailId = new Guid( "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60" ),
        Subject = "Re: Refund for order 1041",
        TextBody = "Refund issued for order 1041.",
    }
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/drafts' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "thread_id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  "reply_to_email_id": "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
  "subject": "Re: Refund for order 1041",
  "text": "Refund issued for order 1041."
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes drafts create \
  --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --thread-id 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12 \
  --reply-to-email-id 5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60 \
  --subject "Re: Refund for order 1041" \
  --text "Refund issued for order 1041."
```

## Attachments

In the composer, click **Attach files** or drag files onto the message. Attachment content can total up to 25 MB per draft. Images dropped into the body of the message are inserted inline.

Via the API, pass files in the `attachments` array as Base64 encoded `content`.

## Write with AI

Type <kbd>/</kbd> in the body of a message and choose **Start from a prompt...** to have AI write the message for you. Describe what you want to say, and the message is written in the tone of voice set for the [inbox agent](/docs/dashboard/inboxes/agent), using the rest of the thread as context. Once there is content in the message you can prompt again to change it.

## View drafts

Select the **Drafts** folder in an inbox to see all of its unsent drafts. Select a draft to continue editing it.

You can also [list drafts](/docs/api-reference/inboxes/list-drafts) via the API, SDKs, or CLI. Drafts are returned most recently updated first.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.drafts.list({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->drafts->list('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1');
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Drafts.list("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Inboxes::Drafts.list({ "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" })
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Drafts.List("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", nil)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{list_opts::ListOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _drafts = resend
    .inboxes
    .list_drafts("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", ListOptions::default())
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.ListInboxDraftsResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        ListInboxDraftsResponseSuccess data = resend.inboxes().drafts().list("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxDraftListAsync( new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ) );
Console.WriteLine( "Nr Drafts={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/drafts' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes drafts list --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1
```

## Update a draft

In the Dashboard, open the draft and edit it. Changes are saved automatically.

You can also [update a draft](/docs/api-reference/inboxes/update-draft) via the API, SDKs, or CLI. Fields you leave out stay as they are, except for `html` and `text`: sending either one replaces both.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.drafts.update({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  draftId: 'c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32',
  subject: 'Refund issued for order 1041',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->drafts->update(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  'c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32',
  [
    'subject' => 'Refund issued for order 1041',
  ]
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Drafts.UpdateParams = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "id": "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
  "subject": "Refund issued for order 1041",
}

resend.Inboxes.Drafts.update(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "draft_id": "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
  "subject": "Refund issued for order 1041",
}

Resend::Inboxes::Drafts.update(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	subject := "Refund issued for order 1041"

	params := &resend.UpdateInboxDraftRequest{
		Subject: &subject,
	}

	client.Inboxes.Drafts.Update(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
		params,
	)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{types::UpdateInboxDraftOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let update = UpdateInboxDraftOptions::new().with_subject("Refund issued for order 1041");

  let _draft = resend
    .inboxes
    .update_draft(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
      update,
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.UpdateInboxDraftOptions;
import com.resend.services.inboxes.model.UpdateInboxDraftResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        UpdateInboxDraftOptions params = UpdateInboxDraftOptions.builder()
                .subject("Refund issued for order 1041")
                .build();

        UpdateInboxDraftResponseSuccess data = resend.inboxes().drafts().update(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
                params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxDraftUpdateAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32" ),
    new InboxDraftUpdateData()
    {
        Subject = "Refund issued for order 1041",
    }
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X PATCH 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/drafts/c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "subject": "Refund issued for order 1041"
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes drafts update \
  --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --draft-id c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32 \
  --subject "Refund issued for order 1041"
```

## Send a draft

In the Dashboard, click **Send** or press <kbd>⌘</kbd> + <kbd>Enter</kbd>. The email is sent from the inbox address, along with any attachments saved on the draft.

You can also [send a draft](/docs/api-reference/inboxes/send-draft) via the API, SDKs, or CLI. The draft must have at least one recipient in `to`. A reply draft without a subject is sent with the subject of the thread, prefixed with `Re:`.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.drafts.send({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  draftId: 'c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->drafts->send(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  'c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32'
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Drafts.send(
  inbox_id="b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  draft_id="c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "draft_id": "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
}

Resend::Inboxes::Drafts.send(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Drafts.Send(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
		nil,
	)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{types::SendInboxDraftOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _email = resend
    .inboxes
    .send_draft(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
      SendInboxDraftOptions::new(),
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.SendInboxDraftResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        SendInboxDraftResponseSuccess data = resend.inboxes().drafts().send(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxDraftSendAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32" )
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/drafts/c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32/send' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes drafts send \
  --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --draft-id c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32
```

## Drafts from the inbox agent

If the [inbox agent](/docs/dashboard/inboxes/agent) is allowed to draft replies or forward threads, it creates drafts for you to review. The agent never sends a draft itself. When you open the thread, the draft appears in the reply composer with a badge showing it was drafted by the agent. Edit it if needed, then send it.

## Discard a draft

In the composer, click the trash icon to discard the draft. In the **Drafts** folder, hover over a draft and click **Discard draft**, or select several drafts and click **Discard**. Each discard shows a notification with an **Undo** button.

You can also [delete a draft](/docs/api-reference/inboxes/delete-draft) via the API, SDKs, or CLI.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.drafts.remove({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  draftId: 'c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->drafts->remove(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  'c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32'
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Drafts.remove(
  inbox_id="b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  draft_id="c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "draft_id": "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
}

Resend::Inboxes::Drafts.remove(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Drafts.Remove(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
	)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _deleted = resend
    .inboxes
    .delete_draft(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.RemoveInboxDraftResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        RemoveInboxDraftResponseSuccess data = resend.inboxes().drafts().remove(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxDraftDeleteAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32" )
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X DELETE 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/drafts/c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes drafts delete \
  --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --draft-id c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32 \
  --yes
```

## API Reference

For complete API documentation, see the [Inbox Drafts API reference](/docs/api-reference/inboxes/create-draft).
