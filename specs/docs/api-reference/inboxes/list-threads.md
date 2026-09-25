> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Threads

> Retrieve the threads in one folder of an inbox.

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

  [Get early access](https://resend.com/help?type=report\&message=I+would+like+early+access+to+Inboxes.\&priority=low) if you're interested in testing this feature.

  <span />

  Once you have access, upgrade your Resend SDK to use the new methods:

  <CodeGroup>
    ```bash Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install resend@6.28.1-preview-inboxes.1
    ```

    ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install -g resend-cli@2.22.0-preview-inboxes.2
    ```
  </CodeGroup>
</Warning>

A thread is a conversation within an inbox, made up of one or more messages.

## Path Parameters

<ResendParamField path="inbox_id" type="string" required>
  The Inbox ID.
</ResendParamField>

## Query Parameters

<ParamField query="folder" type="string" default="inbox">
  The folder to list: `inbox`, `archive`, `spam`, `sent`, or `trash`.
</ParamField>

<ParamField query="query" type="string">
  Case-insensitive substring matched against the thread subject and its label
  names. Max length is `256` characters.
</ParamField>

<ParamField query="label" type="string[]">
  Label IDs to filter by.
</ParamField>

<ParamField query="limit" type="number">
  Number of threads to return. Default is `20`, maximum is `100`, minimum is
  `1`.
</ParamField>

<ParamField query="after" type="string">
  The ID of the last thread on the current page. Returns the next, older page.
</ParamField>

<ParamField query="before" type="string">
  The ID of the first thread on the current page. Returns the previous, newer
  page.
</ParamField>

## Folders

Every thread sits in exactly one folder within its inbox.

| Folder    | Meaning                                                      |
| --------- | ------------------------------------------------------------ |
| `inbox`   | The default. The thread holds at least one received message. |
| `archive` | The thread was archived.                                     |
| `spam`    | The thread was marked as spam.                               |
| `trash`   | The thread is scheduled for deletion in 30 days.             |
| `sent`    | Threads whose messages are all outbound.                     |

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
  The threads in the folder, most recently active first.

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
  </Expandable>
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.inboxes.threads.list({
    inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  });
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend inboxes threads list --inbox_id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "list",
    "has_more": true,
    "data": [
      {
        "id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
        "subject": "Refund for order 1041",
        "from": "Ada Lovelace <ada@example.org>",
        "to": ["support@example.com"],
        "cc": [],
        "bcc": [],
        "labels": [
          {
            "id": "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
            "name": "Urgent",
            "color": "crimson"
          }
        ],
        "message_count": 2,
        "has_attachment": true,
        "has_draft": false,
        "read": false,
        "received_at": "2026-08-05T14:03:11.229Z"
      }
    ]
  }
  ```
</ResponseExample>
