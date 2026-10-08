> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Search Threads

> Find threads in an inbox by text, people, attachments, and dates.

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

<Warning>
  Inboxes are currently in private beta and only available to a limited
  number of users. The response shape might change before GA.

  <span />

  [Get early access](https://resend.com/settings/labs) if you're interested in testing this feature.

  <span />

  Once you have access, upgrade your Resend SDK to use the new methods:

  <CodeGroup>
    ```bash Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install resend@6.32.1-preview-inboxes.4
    ```

    ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install -g resend-cli@2.22.0-preview-inboxes.6
    ```
  </CodeGroup>
</Warning>

Search finds threads by the text of their emails, who sent or received them,
whether they have attachments, and their dates. Results are ordered by
latest activity, newest first, and paginate like [List
Threads](/docs/api-reference/inboxes/list-threads).

Search can be up to about a minute behind new emails. To browse an inbox
exactly and up to date, use [List
Threads](/docs/api-reference/inboxes/list-threads).

## Path Parameters

<ResendParamField path="inbox_id" type="string" required>
  The Inbox ID.
</ResendParamField>

## Query Parameters

<ParamField query="query" type="string">
  Free text to search for in the subject, body, sender, recipients, and
  attachment names. Every word must match. Wrap words in double quotes to match
  an exact phrase, and start a word or quoted phrase with `-` to exclude it. Max
  length is `256` characters and `32` words.
</ParamField>

<ParamField query="from" type="string">
  Comma-separated senders. Each value matches part of the sender's address or
  name, case-insensitive. Returns threads matching any of them. Up to `20`
  values.
</ParamField>

<ParamField query="to" type="string">
  Comma-separated recipients, matched the same way as `from`. Up to `20` values.
</ParamField>

<ParamField query="cc" type="string">
  Comma-separated CC recipients, matched the same way as `from`. Up to `20`
  values.
</ParamField>

<ParamField query="bcc" type="string">
  Comma-separated BCC recipients, matched the same way as `from`. Up to `20`
  values.
</ParamField>

<ParamField query="has_attachment" type="boolean">
  `true` matches emails with an attachment. `false` matches emails without one.
</ParamField>

<ParamField query="start_date" type="string">
  Matches emails sent on or after this date. Accepts a date like `2026-09-01` or
  an ISO 8601 timestamp, in UTC unless the timestamp has an offset.
</ParamField>

<ParamField query="end_date" type="string">
  Matches emails sent on or before this date. Same formats as `start_date`. A
  date covers that whole day, so `start_date=2026-09-01&end_date=2026-09-30`
  covers all of September. A timestamp is used as given.
</ParamField>

<ParamField query="folders" type="string">
  Comma-separated folders to search: `inbox`, `archive`, `spam`, `sent`, or
  `trash`. A thread is returned when any of its emails is in one of them, so a
  thread in `inbox` with an email you sent matches both `inbox` and `sent`.
  Defaults to `inbox`, or `inbox,archive,sent` when `labels` is set. `spam` and
  `trash` are only included when you name them.
</ParamField>

<ParamField query="labels" type="string">
  Comma-separated label IDs. Returns threads with any of these labels. Up to
  `50` IDs. An ID that doesn't exist in the inbox returns a `404`.
</ParamField>

<ParamField query="read" type="boolean">
  `true` returns threads where every email is read. `false` returns threads with
  at least one unread email.
</ParamField>

<ParamField query="limit" type="number">
  Number of threads to return. Default is `20`, maximum is `100`, minimum is
  `1`.
</ParamField>

<ParamField query="after" type="string">
  The ID of the last thread on the current page. Returns the next, older page.
  Must be a thread ID.
</ParamField>

<ParamField query="before" type="string">
  The ID of the first thread on the current page. Returns the previous, newer
  page. Cannot be combined with `after`. Must be a thread ID.
</ParamField>

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
* When more than 10,000 threads match, search covers the 10,000 with the
  newest matching email.

## Folders

Every thread sits in exactly one folder within its inbox.

| Folder | Meaning |
| - | - |
| `inbox` | The default. The thread holds at least one received message. |
| `archive` | The thread was archived. |
| `spam` | The thread was marked as spam. |
| `trash` | The thread is scheduled for deletion in 30 days. |
| `sent` | Threads whose messages are all outbound. |

You can move a thread to `inbox`, `archive`, `spam`, or `trash`. `sent` is
assigned automatically.

## Response Fields

<ParamField body="object" type="string">
  Always `list`.
</ParamField>

<ParamField body="has_more" type="boolean">
  Whether more threads exist beyond this page. Pass the last thread's `id` as
  `after` to continue.
</ParamField>

<ParamField body="data" type="array">
  The matching threads, most recently active first.

  <Expandable defaultOpen="true" title="properties">
    <ParamField body="id" type="string">
      The ID of the thread.
    </ParamField>

    <ParamField body="subject" type="string | null">
      The subject of the thread.
    </ParamField>

    <ParamField body="from" type="string | null">
      Sender email address.
    </ParamField>

    <ParamField body="to" type="string[]">
      The recipients of the most recent message.
    </ParamField>

    <ParamField body="cc" type="string[]">
      The CC recipients of the most recent message.
    </ParamField>

    <ParamField body="bcc" type="string[]">
      The BCC recipients of the most recent message.
    </ParamField>

    <ParamField body="labels" type="array">
      The labels attached to the thread, each with an `id`, `name`, and
      `color`.
    </ParamField>

    <ParamField body="message_count" type="number">
      The number of messages in the thread.
    </ParamField>

    <ParamField body="has_attachment" type="boolean">
      Whether any message has an attachment.
    </ParamField>

    <ParamField body="has_draft" type="boolean">
      Whether the thread has an unsent draft.
    </ParamField>

    <ParamField body="read" type="boolean">
      True only when every message in the thread is read.
    </ParamField>

    <ParamField body="received_at" type="string">
      ISO 8601 timestamp when the thread was last active.
    </ParamField>

    <ParamField body="folder" type="string">
      The folder the thread lives in. One of `inbox`, `archive`, `spam`,
      `sent`, or `trash`.
    </ParamField>

    <ParamField body="matched_email_id" type="string | null">
      The ID of the email in the thread that matched the search. When `query`
      has words or phrases, it's the most relevant match. Otherwise, it's the
      newest. Pass it to [Retrieve Thread
      Email](/docs/api-reference/inboxes/get-thread-email) to read that email.
    </ParamField>

    <ParamField body="highlights" type="object">
      Where `query` matched the email in `matched_email_id`, as text fragments
      with each match wrapped in `**`. Keys are `subject`, `body`, `from`,
      `to`, `cc`, `bcc`, and `attachments`, each an array of strings, and only
      keys with a match are present. `{}` when there's no `query`.
    </ParamField>
  </Expandable>
</ParamField>

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

<RequestExample>
  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl --get 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/search' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       --data-urlencode 'query=invoice -draft' \
       --data-urlencode 'from=isabella@example.com,carolina@example.com' \
       --data-urlencode 'start_date=2026-09-01' \
       --data-urlencode 'limit=2'
  ```
</RequestExample>

<ResponseExample>
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
            "color": "grass"
          }
        ],
        "message_count": 3,
        "has_attachment": true,
        "has_draft": false,
        "read": false,
        "received_at": "2026-09-24T14:12:08.000Z",
        "folder": "inbox",
        "matched_email_id": "e8a3f1c6-2b9d-4e5a-a7c4-9d1b6f3e2a80",
        "highlights": {
          "subject": ["September **invoice**"],
          "body": ["Attached is the **invoice** for September, due on the 30th."],
          "attachments": ["**invoice**-2026-09.pdf"]
        }
      },
      {
        "id": "7d2f8a3b-9c1e-4b6d-a5f2-3e8c0b7a9d16",
        "subject": "Re: Q3 renewal",
        "from": "Carolina <carolina@example.com>",
        "to": ["billing@example.com"],
        "cc": ["finance@example.com"],
        "bcc": [],
        "labels": [],
        "message_count": 5,
        "has_attachment": false,
        "has_draft": false,
        "read": true,
        "received_at": "2026-09-18T09:47:31.000Z",
        "folder": "inbox",
        "matched_email_id": "3c6b9e2d-7a1f-4d8c-b3e5-0f2a8d6c4b19",
        "highlights": {
          "body": ["I'll send the **invoice** once the renewal is signed."]
        }
      }
    ]
  }
  ```
</ResponseExample>
