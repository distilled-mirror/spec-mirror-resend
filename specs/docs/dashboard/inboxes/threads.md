> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Managing Threads

> Learn how to read, organize, search, and respond to threads.

A thread is a conversation within an inbox. Emails sent and received in reply to each other are grouped into the same thread, so you can read, organize and respond to the whole conversation in one place.

## Folders

* `inbox`: The default. The thread holds at least one received message.
* `archive`: The thread was archived.
* `spam`: The thread was marked as spam.
* `trash`: The thread is scheduled for deletion in 30 days.
* `sent`: Threads whose messages are all outbound.

In the Dashboard, the folder switcher also shows a **Drafts** folder that lists your unsent [drafts](/docs/dashboard/inboxes/drafts). The **Inbox** folder shows a count of unread threads.

## View threads

Select an inbox from the [Inboxes dashboard](https://resend.com/inboxes) to see its threads, most recently active first. Use the folder switcher to change folders, or select a label in the left rail to see only the threads with that [label](/docs/dashboard/inboxes/labels).

Select a thread to open it and read every email in the conversation. Opening a thread marks it as read. Use the **Next email** and **Previous email** buttons, or the <kbd>↓</kbd> and <kbd>↑</kbd> keys, to move between threads.

You can also [list threads](/docs/api-reference/inboxes/list-threads) via the API, SDKs, or CLI, filtered by folder, label and read status.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.threads.list({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->threads->list('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1');
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Threads.list("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1")
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Inboxes::Threads.list({ "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" })
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Threads.List("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", nil)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{list_opts::ListOptions, types::ListInboxThreadsOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _threads = resend
    .inboxes
    .list_threads(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      ListInboxThreadsOptions::new(),
      ListOptions::default(),
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.ListInboxThreadsResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        ListInboxThreadsResponseSuccess data = resend.inboxes().threads().list("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxThreadListAsync( new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ) );
Console.WriteLine( "Nr Threads={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads list --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1
```

To read the emails in a thread, [list the thread emails](/docs/api-reference/inboxes/list-thread-emails). They are returned oldest first.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.threads.emails.list({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->threads->emails->list(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12'
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Threads.Emails.list(
  inbox_id="b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  thread_id="4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "thread_id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
}

Resend::Inboxes::Threads::Emails.list(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Threads.Emails.List(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
		nil,
	)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{list_opts::ListOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let _emails = resend
    .inboxes
    .list_thread_emails(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
      ListOptions::default(),
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.ListInboxThreadEmailsResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        ListInboxThreadEmailsResponseSuccess data = resend.inboxes().threads().emails().list(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxThreadEmailListAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12" )
);
Console.WriteLine( "Nr Emails={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X GET 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12/emails' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads emails list \
  --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --thread-id 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12
```

## Search threads

In the Dashboard, click the search icon or press <kbd>/</kbd> to search the inbox. Quick filters let you narrow results to emails **From me**, **Unread**, **Has attachments** or **Assigned to me**. You can also type search operators such as `from:`, `to:`, `label:`, `has:`, `is:`, `after:` and `before:`. Dates use the `YYYY-MM-DD` format.

You can also [search threads](/docs/api-reference/inboxes/search-threads) via the API, SDKs, or CLI by text, sender, recipient, attachments and date.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.threads.search({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  query: 'invoice -draft',
  from: ['isabella@example.com', 'carolina@example.com'],
  startDate: '2026-09-01',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->threads->search('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1', [
  'query' => 'invoice -draft',
  'from' => ['isabella@example.com', 'carolina@example.com'],
  'start_date' => '2026-09-01',
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Threads.SearchParams = {
  "query": "invoice -draft",
  "from": ["isabella@example.com", "carolina@example.com"],
  "start_date": "2026-09-01",
}

resend.Inboxes.Threads.search("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "query": "invoice -draft",
  "from": ["isabella@example.com", "carolina@example.com"],
  "start_date": "2026-09-01",
}

Resend::Inboxes::Threads.search(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.SearchInboxThreadsOptions{
		Query:     "invoice -draft",
		From:      []string{"isabella@example.com", "carolina@example.com"},
		StartDate: "2026-09-01",
	}

	client.Inboxes.Threads.Search("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{list_opts::ListOptions, types::SearchInboxThreadsOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let search = SearchInboxThreadsOptions::new()
    .with_query("invoice -draft")
    .with_from(["isabella@example.com", "carolina@example.com"])
    .with_start_date("2026-09-01");

  let _results = resend
    .inboxes
    .search_threads(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      search,
      ListOptions::default(),
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.SearchInboxThreadsParams;
import com.resend.services.inboxes.model.SearchInboxThreadsResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        SearchInboxThreadsParams params = SearchInboxThreadsParams.builder()
                .query("invoice -draft")
                .from("isabella@example.com", "carolina@example.com")
                .startDate("2026-09-01")
                .build();

        SearchInboxThreadsResponseSuccess data = resend.inboxes().threads().search("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

var resp = await resend.InboxThreadSearchAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new InboxThreadSearchQuery()
    {
        Query = "invoice -draft",
        From = new List<string> { "isabella@example.com", "carolina@example.com" },
        StartDate = "2026-09-01",
    }
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl --get 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/search' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     --data-urlencode 'query=invoice -draft' \
     --data-urlencode 'from=isabella@example.com,carolina@example.com' \
     --data-urlencode 'start_date=2026-09-01'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads search \
  --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --query "invoice -draft" \
  --from isabella@example.com carolina@example.com \
  --start-date 2026-09-01
```

> [!NOTE]
>
> Search can be up to about a minute behind new emails. To browse an inbox
> exactly as it is right now, list threads instead.

## Organize threads

You can act on a thread from the thread view, from the actions that appear when you hover over a thread in the list, or on many threads at once by selecting them and using the actions in the bar at the bottom of the list.

* **Mark as read** or **Mark as unread** changes the read status of every email in the thread.
* **Archive** moves the thread to the archive folder.
* **Report spam** moves the thread to the spam folder. From the spam folder, use **Report not spam** to move it back.
* **Delete** moves the thread to the trash. Threads in the trash are scheduled for deletion in 30 days.
* **Move to** moves the thread to another folder, or applies a [label](/docs/dashboard/inboxes/labels), and archives the thread.
* **Label as** adds or removes [labels](/docs/dashboard/inboxes/labels).

Each move shows a notification with an **Undo** button. To restore a thread from the archive, spam or trash, use **Move to** and choose **Inbox**.

You can also [update a thread](/docs/api-reference/inboxes/update-thread) via the API, SDKs, or CLI to mark it as read or unread, or move it to the `inbox`, `archive`, `spam` or `trash` folder.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.threads.update({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  read: true,
  folder: 'archive',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->threads->update(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  [
    'read' => true,
    'folder' => 'archive',
  ]
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Threads.UpdateParams = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  "read": True,
  "folder": "archive",
}

resend.Inboxes.Threads.update(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "thread_id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  "read": true,
  "folder": "archive",
}

Resend::Inboxes::Threads.update(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	read := true
	params := &resend.UpdateInboxThreadRequest{
		Read:   &read,
		Folder: resend.InboxMoveThreadFolderArchive,
	}

	client.Inboxes.Threads.Update(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
		params,
	)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{types::{UpdateInboxThreadFolder, UpdateInboxThreadOptions}, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let update = UpdateInboxThreadOptions::new()
    .with_read(true)
    .with_folder(UpdateInboxThreadFolder::Archive);

  let _thread = resend
    .inboxes
    .update_thread(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
      update,
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.MoveInboxThreadFolder;
import com.resend.services.inboxes.model.UpdateInboxThreadOptions;
import com.resend.services.inboxes.model.UpdateInboxThreadResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        UpdateInboxThreadOptions params = UpdateInboxThreadOptions.builder()
                .read(true)
                .folder(MoveInboxThreadFolder.ARCHIVE)
                .build();

        UpdateInboxThreadResponseSuccess data = resend.inboxes().threads().update(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
                params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxThreadUpdateAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12" ),
    new InboxThreadUpdateData()
    {
        IsRead = true,
        Folder = InboxMoveFolder.Archive,
    }
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X PATCH 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "read": true,
  "folder": "archive"
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads update \
  --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --thread-id 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12 \
  --read \
  --folder archive
```

## Delete a thread

Deleting a thread moves it to the trash and schedules it for deletion in 30 days. Until then, you can restore it by moving it back to another folder.

You can also [delete a thread](/docs/api-reference/inboxes/delete-thread) via the API, SDKs, or CLI.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.threads.remove({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->threads->remove(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12'
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Inboxes.Threads.remove(
  inbox_id="b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  thread_id="4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "thread_id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
}

Resend::Inboxes::Threads.remove(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	client.Inboxes.Threads.Remove(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
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
    .delete_thread(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.RemoveInboxThreadResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        RemoveInboxThreadResponseSuccess data = resend.inboxes().threads().remove(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12");
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxThreadDeleteAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12" )
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X DELETE 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12' \
     -H 'Authorization: Bearer re_xxxxxxxxx'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads delete \
  --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --thread-id 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12 \
  --yes
```

## Assign a thread

In the Dashboard, you can assign a thread to a member of your team so everyone knows who is handling it. Hover over a thread in the list and click **Assign thread**, or press <kbd>A</kbd>, then search for a teammate. Choose **Unassigned** to remove the assignment.

The [inbox agent](/docs/dashboard/inboxes/agent) can also assign threads based on your instructions.

## Reply and forward

While viewing a thread, use the **Reply**, **Reply all** or **Forward** buttons at the bottom of the thread, or the **More** menu on an individual email. The reply opens inline beneath the email and is saved as a [draft](/docs/dashboard/inboxes/drafts) as you write. Click **Send** or press <kbd>⌘</kbd> + <kbd>Enter</kbd> to send it.

Replies are sent from the inbox address and are threaded for the recipient. You can also [reply to](/docs/api-reference/inboxes/reply-thread-email) or [forward](/docs/api-reference/inboxes/forward-thread-email) an email via the API, SDKs, or CLI.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.threads.emails.reply({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  emailId: '5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60',
  text: 'Refund issued for order 1041.',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->threads->emails->reply(
  'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  '5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60',
  [
    'text' => 'Refund issued for order 1041.',
  ]
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Threads.Emails.ReplyParams = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "thread_id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  "email_id": "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
  "text": "Refund issued for order 1041.",
}

resend.Inboxes.Threads.Emails.reply(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  "inbox_id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  "thread_id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
  "email_id": "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
  "text": "Refund issued for order 1041.",
}

Resend::Inboxes::Threads::Emails.reply(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	params := &resend.ReplyInboxThreadEmailRequest{
		Text: "Refund issued for order 1041.",
	}

	client.Inboxes.Threads.Emails.Reply(
		"b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
		"4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
		"5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
		params,
	)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{types::ReplyInboxThreadEmailOptions, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let reply = ReplyInboxThreadEmailOptions::new().with_text("Refund issued for order 1041.");

  let _email = resend
    .inboxes
    .reply_thread_email(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
      "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
      reply,
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.Resend;
import com.resend.core.exception.ResendException;
import com.resend.services.inboxes.model.ReplyInboxThreadEmailOptions;
import com.resend.services.inboxes.model.ReplyInboxThreadEmailResponseSuccess;

public class Main {
    public static void main(String[] args) throws ResendException {
        Resend resend = new Resend("re_xxxxxxxxx");

        ReplyInboxThreadEmailOptions params = ReplyInboxThreadEmailOptions.builder()
                .text("Refund issued for order 1041.")
                .build();

        ReplyInboxThreadEmailResponseSuccess data = resend.inboxes().threads().emails().reply(
                "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
                "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
                "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
                params);
    }
}
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

await resend.InboxThreadEmailReplyAsync(
    new Guid( "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1" ),
    new Guid( "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12" ),
    new Guid( "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60" ),
    new InboxThreadEmailReplyData()
    {
        TextBody = "Refund issued for order 1041.",
    }
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12/emails/5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60/reply' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     -H 'Content-Type: application/json' \
     -d $'{
  "text": "Refund issued for order 1041."
}'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads emails reply \
  --inbox-id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --thread-id 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12 \
  --email-id 5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60 \
  --text "Refund issued for order 1041."
```

## Keyboard shortcuts

Press <kbd>?</kbd> in the Dashboard to see every keyboard shortcut. The most useful are:

| Shortcut | Action |
| - | - |
| <kbd>/</kbd> | Search emails |
| <kbd>C</kbd> | Compose |
| <kbd>↓</kbd> / <kbd>↑</kbd> | Next or previous email |
| <kbd>X</kbd> | Select email |
| <kbd>E</kbd> | Archive |
| <kbd>⇧</kbd> + <kbd>U</kbd> | Toggle read |
| <kbd>A</kbd> | Assign to |
| <kbd>L</kbd> | Label as |
| <kbd>V</kbd> | Move to |
| <kbd>!</kbd> | Report spam or not spam |
| <kbd>Backspace</kbd> | Move to trash |
| <kbd>Esc</kbd> | Go back or close composer |

## API Reference

For complete API documentation, see the [Inbox Threads API reference](/docs/api-reference/inboxes/list-threads).
