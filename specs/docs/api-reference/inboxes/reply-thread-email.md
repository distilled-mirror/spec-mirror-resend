> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Reply to Thread Email

> Send a reply to a message in an inbox thread.

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
    npm install resend@6.33.0
    ```

    ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install -g resend-cli@2.25.0
    ```
  </CodeGroup>
</Warning>

Sends a reply from the inbox address right away, with no stored draft. The `to`
recipients come from the message you reply to:

* For a message the inbox received, the reply goes to its `Reply-To` addresses,
  or to its sender when it has no `Reply-To`.
* For a message the inbox sent, the reply goes to that message's `to`
  recipients.

Set `reply_all` to also copy the other recipients of the message.

At least one of `html` or `text` must contain more than whitespace.

The reply is threaded for the recipient. `In-Reply-To` is set to the
`Message-ID` of the message you reply to, and `References` to that message's
`References` followed by its `Message-ID`. These headers can't be set or
overridden.

## Path Parameters

<ResendParamField path="inbox_id" type="string" required>
  The Inbox ID. An email address is not accepted.
</ResendParamField>

<ResendParamField path="thread_id" type="string" required>
  The Thread ID.
</ResendParamField>

<ResendParamField path="email_id" type="string" required>
  The Email ID of the message to reply to, as returned by [List Thread
  Emails](/docs/api-reference/inboxes/list-thread-emails) in `data[].id`.
</ResendParamField>

## Body Parameters

<ParamField body="cc" type="string | string[]">
  CC recipient email address. For multiple addresses, send as an array of
  strings. Without `reply_all`, the reply copies only these addresses. With
  `reply_all`, these addresses are merged with the copied recipients, without
  duplicates. `cc` and `bcc` combined must be fewer than 50 addresses. After the
  `to` recipients are added, the reply cannot exceed 50 recipients.
</ParamField>

<ParamField body="bcc" type="string | string[]">
  BCC recipient email address. For multiple addresses, send as an array of
  strings. BCC recipients of the original message are never copied.
</ParamField>

<ParamField body="html" type="string">
  The HTML body of the reply.
</ParamField>

<ParamField body="text" type="string">
  The plain-text body of the reply.
</ParamField>

<ParamField body="subject" type="string">
  The subject of the reply. Max 2000 characters. Cannot contain a line break.
  When omitted, the thread subject is used, prefixed with `Re:` if it does not
  already start with it.
</ParamField>

<ResendParamField body="reply_all" type="boolean" default="false">
  Reply to everyone on the original message. For a message the inbox received,
  the reply goes to its `Reply-To` addresses, or to its sender when it has none.
  It copies the other addresses of its `To` header and its `cc` recipients in
  `cc`. For a message the inbox sent, the reply goes to that message's
  `Reply-To` addresses when they are not the inbox address, otherwise to its
  `to` recipients. It copies its `cc` recipients. The inbox address is always
  excluded, and duplicates are removed.
</ResendParamField>

<ParamField body="attachments" type="array">
  Files to attach, as on [Send Email](/docs/api-reference/emails/send-email). Each one
  needs `content` or `path`. Up to 10 files. The `content` of all files can total
  at most 25 MB. A `path` file counts toward the 10 files only, because it is
  fetched when the email is sent. An empty file, a blocked file type, or a
  `path` that is not an `http` or `https` URL, or that points to `localhost`,
  returns a `422`.

  <Expandable defaultOpen title="properties">
    <ParamField body="content" type="buffer | string">
      Content of an attached file, passed as a buffer or Base64 string.
    </ParamField>

    <ParamField body="filename" type="string">
      Name of attached file.
    </ParamField>

    <ParamField body="path" type="string">
      Path where the attachment file is hosted.
    </ParamField>

    <ResendParamField body="content_type" type="string">
      Content type for the attachment. When not set, it is derived from the
      `filename`.
    </ResendParamField>

    <ResendParamField body="content_id" type="string">
      Content ID for embedding inline images with a `cid:` reference in the
      `html`. [Learn about inline images](/docs/dashboard/emails/embed-inline-images).
    </ResendParamField>
  </Expandable>
</ParamField>

<ParamField body="headers" type="object">
  Custom headers to add to the email. Resend sets the `In-Reply-To`,
  `References`, and `Reply-To` headers, so you cannot set them here. Sending one
  of them, in any letter case, returns a `422`. A header name cannot be empty,
  and names and values cannot contain line breaks or null characters, or the
  request returns a `422`.
</ParamField>

## Headers

<ParamField header="Idempotency-Key" type="string">
  Add an idempotency key to prevent duplicated emails.

  * Should be **unique per API request**
  * Idempotency keys expire after **24 hours**
  * Have a maximum length of **256 characters**
  * A retry with the same key returns the first successful response, with the
    `idempotent-replayed: true` header
  * A failed request is not stored, so you can retry it with the same key
  * Reusing the key with a different body, or while the first request is still
    running, returns a `409`

  [Learn more](/docs/dashboard/emails/idempotency-keys)
</ParamField>

## Response Fields

<ParamField body="id" type="string">
  The ID of the sent email. Use it with the [emails
  endpoints](/docs/api-reference/emails/retrieve-email).
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.inboxes.threads.emails.reply({
    inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
    threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
    emailId: '5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60',
    cc: ['billing@example.com'],
    bcc: ['records@example.com'],
    html: '<p>Refund issued for order 1041.</p>',
    text: 'Refund issued for order 1041.',
    attachments: [
      {
        path: 'https://resend.com/static/sample/invoice.pdf',
        filename: 'invoice.pdf',
      },
    ],
  });
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12/emails/5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60/reply' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "cc": ["billing@example.com"],
    "bcc": ["records@example.com"],
    "html": "<p>Refund issued for order 1041.</p>",
    "text": "Refund issued for order 1041.",
    "attachments": [
      {
        "path": "https://resend.com/static/sample/invoice.pdf",
        "filename": "invoice.pdf"
      }
    ]
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend inboxes threads emails reply b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12 5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60 \
    --html "<p>Refund issued for order 1041.</p>" \
    --text "Refund issued for order 1041."
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "id": "6a0c8e58-3d9e-4f7a-8b14-2e3f4a5b6c71"
  }
  ```
</ResponseExample>
