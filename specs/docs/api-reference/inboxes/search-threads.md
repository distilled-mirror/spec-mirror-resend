> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Search Threads

> Find threads in an inbox by text, people, attachments, and dates.

Search finds threads by the text of their emails, who sent or received them,
whether they have attachments, and their dates.

## Path Parameters

The Inbox ID or the inbox email address, such as `support@example.com`.

## Query Parameters

**query** `string`

Free text to search for in the subject, body, sender, recipients, and
attachment names. Max 256 characters and 32 words.

**from** `string`

Comma-separated senders. Up to `20` values.

**to** `string`

Comma-separated recipients. Up to `20` values.

**cc** `string`

Comma-separated CC recipients. Up to `20` values.

**bcc** `string`

Comma-separated BCC recipients. Up to `20` values.

**has\_attachment** `boolean`

`true` matches emails with an attachment. `false` matches emails without one.

**start\_date** `string`

Matches emails sent on or after this date. Accepts a date like `2026-09-01` or
an ISO 8601 timestamp, in UTC unless the timestamp has an offset.

**end\_date** `string`

Matches emails sent on or before this date. Same formats as `start_date`. A
date covers that whole day, so `start_date=2026-09-01&end_date=2026-09-30`
covers all of September.

**folders** `string`

Comma-separated folders to search. Defaults to `inbox`, or to
`inbox,archive,sent` when `labels` is set.

* `inbox`: The default. The thread holds at least one received message.
* `archive`: The thread was archived.
* `spam`: The thread was marked as spam.
* `trash`: The thread is scheduled for deletion in 30 days.
* `sent`: Threads whose messages are all outbound.

**labels** `string`

Comma-separated label IDs. Returns threads with any of these labels. Up to
`50` IDs.

**read** `boolean`

`true` returns threads where every email is read. `false` returns threads with
at least one unread email.

**limit** `number`

Number of threads to return. Default is `20`, maximum is `100`, minimum is
`1`.

**after** `string`

The ID of the last thread on the current page. Returns the next, older page.
Must be a thread ID.

**before** `string`

The ID of the first thread on the current page. Returns the previous, newer
page. Cannot be combined with `after`. Must be a thread ID.

## How matching works

* `query` matches when every word appears somewhere in the email. A quoted
  phrase like `"late fee"` must appear word for word, and `-word` or
  `-"a phrase"` excludes emails that contain it. `query=invoice -draft` finds
  emails that mention `invoice` but not `draft`.
* A comma means any of: `from=isabella@example.com,carolina@example.com`
  matches emails from either. Different parameters combine, so a thread must
  match all of them.
* `folders`, `labels`, and `read` apply to the thread. `query`, `from`, `to`,
  `cc`, `bcc`, `has_attachment`, `start_date`, and `end_date` must all match
  the same email in the thread.
* When any of these email filters is set, the matching email must itself be in
  one of `folders`. For `sent`, that means an email the inbox sent.
* When more than 10,000 threads match, search covers the 10,000 with the
  newest matching email.

## Response Fields

**object** `string`

Always `list`.

**has\_more** `boolean`

Whether more threads exist beyond this page. Pass the last thread's `id` as
`after` to continue.

**data** `array`

The matching threads, most recently active first.

**properties**

**id** `string`

The ID of the thread.

**subject** `string | null`

The subject of the thread.

**from** `string | null`

Sender email address. Can include the display name.

**to** `string[]`

The recipients of the most recent message. For a received email, these
are the addresses it was delivered to, not the full `To` header.

**cc** `string[]`

The CC recipients of the most recent message.

**bcc** `string[]`

The BCC recipients of the most recent message. Always empty for a
received email.

**labels** `array`

The labels attached to the thread.

**properties**

**id** `string`

The ID of the label.

**name** `string`

The name of the label.

**color** `string`

The color of the label as an uppercase `#RRGGBB` hex code.

**email\_count** `number`

The number of emails in the thread.

**has\_attachment** `boolean`

Whether the most recent message in the thread has an attachment.

**has\_draft** `boolean`

Whether the thread has an unsent draft.

**read** `boolean`

True only when every message in the thread is read.

**received\_at** `string`

ISO 8601 timestamp when the thread was last active.

**folder** `string`

The folder the thread lives in. Every thread sits in exactly one folder
within its inbox. You can move a thread to `inbox`, `archive`, `spam`, or
`trash`. `sent` is assigned automatically.

* `inbox`: The default. The thread holds at least one received message.
* `archive`: The thread was archived.
* `spam`: The thread was marked as spam.
* `trash`: The thread is scheduled for deletion in 30 days.
* `sent`: Threads whose messages are all outbound.

**matched\_email\_id** `string | null`

Identifies the email in the thread that matched the search. When `query`
has words or phrases, it's the most relevant match. Otherwise, it's the
newest. [Retrieve Thread Email](/docs/api-reference/inboxes/get-thread-email),
reply, and forward accept it as `email_id`. It is the same `id` that
[List Thread Emails](/docs/api-reference/inboxes/list-thread-emails) returns.
`null` when the search index returns no matched email for the thread.

## Errors

Validation errors return `422` with the name `validation_error`.

| Status | Message | When |
| - | - | - |
| `422` | ``The `query` parameter must be at most 256 characters, but received 300.`` | `query` is longer than `256` characters. |
| `422` | ``The `query` parameter must contain at most 32 words, but received 40.`` | `query` has more than `32` words. |
| `422` | ``The `from` parameter must contain at most 20 values, but received 25.`` | `from`, `to`, `cc`, or `bcc` has more than `20` values. |
| `422` | ``The `start_date` must be a valid ISO 8601 date.`` | `start_date` or `end_date` isn't a date or timestamp. |
| `422` | ``The `start_date` must be on or before the `end_date`.`` | `end_date` is before `start_date`. |
| `422` | ``The `folders` value "drafts" must be one of: inbox, archive, spam, sent, trash.`` | `folders` has an unknown folder. |
| `422` | ``The `labels` value "billing" must be a valid UUID.`` | `labels` has a value that isn't a label ID. |
| `422` | ``The `labels` parameter must contain at most 50 label IDs, but received 60.`` | `labels` has more than `50` IDs. |
| `422` | `The pagination limit must be a number between 1 and 100. See https://resend.com/docs/api-reference/pagination for more information.` | `limit` is out of range. |
| `422` | ``The `read` parameter must be `true` or `false`.`` | `read` or `has_attachment` isn't `true` or `false`. |
| `422` | ``The `after` parameter must be a thread ID. To filter by date, use `GET /inboxes/:id/threads/search` with `start_date`.`` | `after` or `before` is a date. For `before`, the message names `end_date`. |
| `422` | ``You can only pass one of `before` or `after` for pagination. See https://resend.com/docs/api-reference/pagination for more information.`` | Both `after` and `before` are set. |
| `404` | `Inbox not found.` | The inbox doesn't exist. |
| `404` | `Label "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34" not found.` | A label ID in `labels` doesn't exist in the inbox. |
| `404` | `The pagination cursor references an object that does not exist. See https://resend.com/docs/api-reference/pagination for more information.` | The thread in `after` or `before` isn't in the results. |

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.inboxes.threads.search({
  inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  query: 'invoice -draft',
  from: ['isabella@example.com', 'carolina@example.com'],
  startDate: '2026-09-01',
  limit: 2,
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->inboxes->threads->search('b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1', [
  'query' => 'invoice -draft',
  'from' => ['isabella@example.com', 'carolina@example.com'],
  'start_date' => '2026-09-01',
  'limit' => 2,
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Inboxes.Threads.SearchParams = {
    "query": "invoice -draft",
    "from": ["isabella@example.com", "carolina@example.com"],
    "start_date": "2026-09-01",
    "limit": 2,
}

resend.Inboxes.Threads.search("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  inbox_id: "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
  query: "invoice -draft",
  from: ["isabella@example.com", "carolina@example.com"],
  start_date: "2026-09-01",
  limit: 2
}

Resend::Inboxes::Threads.search(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
	client := resend.NewClient("re_xxxxxxxxx")

	limit := 2
	options := &resend.SearchInboxThreadsOptions{
		Query:     "invoice -draft",
		From:      []string{"isabella@example.com", "carolina@example.com"},
		StartDate: "2026-09-01",
		Limit:     &limit,
	}

	client.Inboxes.Threads.Search("b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1", options)
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{
  list_opts::ListOptions,
  types::SearchInboxThreadsOptions,
  Resend, Result,
};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let search = SearchInboxThreadsOptions::new()
    .with_query("invoice -draft")
    .with_from(["isabella@example.com", "carolina@example.com"])
    .with_start_date("2026-09-01");

  let _threads = resend
    .inboxes
    .search_threads(
      "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
      search,
      ListOptions::default().with_limit(2),
    )
    .await?;

  Ok(())
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
        From = [ "isabella@example.com", "carolina@example.com" ],
        StartDate = "2026-09-01",
        Limit = 2,
    }
);
Console.WriteLine( "Nr Threads={0}", resp.Content.Data.Count );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl --get 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/search' \
     -H 'Authorization: Bearer re_xxxxxxxxx' \
     --data-urlencode 'query=invoice -draft' \
     --data-urlencode 'from=isabella@example.com,carolina@example.com' \
     --data-urlencode 'start_date=2026-09-01' \
     --data-urlencode 'limit=2'
```

```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
resend inboxes threads search b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
  --query "invoice -draft" \
  --from isabella@example.com carolina@example.com \
  --start-date 2026-09-01 \
  --limit 2
```

```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "object": "list",
  "has_more": true,
  "data": [
    {
      "id": "b1e7c9d2-5a4f-4c3e-8d2b-7f6a1e9c0b54",
      "subject": "September invoice",
      "from": "Isabella <isabella@example.com>",
      "to": ["billing@example.com"],
      "cc": [],
      "bcc": [],
      "labels": [
        {
          "id": "0c9e4b7a-3f2d-4a1c-b8e6-5d7f2a9c1e03",
          "name": "Billing",
          "color": "#46A758"
        }
      ],
      "email_count": 3,
      "has_attachment": true,
      "has_draft": false,
      "read": false,
      "received_at": "2026-09-24T14:12:08.000Z",
      "folder": "inbox",
      "matched_email_id": "e8a3f1c6-2b9d-4e5a-a7c4-9d1b6f3e2a80"
    },
    {
      "id": "7d2f8a3b-9c1e-4b6d-a5f2-3e8c0b7a9d16",
      "subject": "Re: Q3 renewal",
      "from": "Carolina <carolina@example.com>",
      "to": ["billing@example.com"],
      "cc": ["finance@example.com"],
      "bcc": [],
      "labels": [],
      "email_count": 5,
      "has_attachment": false,
      "has_draft": false,
      "read": true,
      "received_at": "2026-09-18T09:47:31.000Z",
      "folder": "inbox",
      "matched_email_id": "3c6b9e2d-7a1f-4d8c-b3e5-0f2a8d6c4b19"
    }
  ]
}
```
