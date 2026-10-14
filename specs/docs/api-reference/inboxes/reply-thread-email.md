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
    ```bash Node.js theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install resend@6.32.1-preview-inboxes.6
    ```

    ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}} theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install -g resend-cli@2.22.0-preview-inboxes.9
    ```
  </CodeGroup>
</Warning>

Replies from the inbox address. `to` is taken from the message you reply to:
its author, or its `Reply-To` address if it has one. When the inbox sent that
message, the reply goes to the message's original `to` recipients. Add more
recipients with `cc` and `bcc`. The total number of recipients can't exceed 50,
counted after `reply_all` adds everyone on the message.

At least one of `html` or `text` is required.

The reply is threaded for the recipient. `In-Reply-To` is set to the
`Message-ID` of the message you reply to, and `References` to that message's
`References` followed by its `Message-ID`. These headers can't be set or
overridden.

## Path Parameters

<ResendParamField path="inbox_id" type="string" required>
  The Inbox ID.
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
  strings. Not copied from the message you reply to unless `reply_all` is
  `true`, which merges these addresses with the copied ones, without duplicates.
</ParamField>

<ParamField body="bcc" type="string | string[]">
  BCC recipient email address. For multiple addresses, send as an array of
  strings. Not copied from the message you reply to.
</ParamField>

<ParamField body="html" type="string">
  The HTML body.
</ParamField>

<ParamField body="text" type="string">
  The plain-text body.
</ParamField>

<ParamField body="subject" type="string">
  The subject of the reply. When omitted, the thread subject is used, prefixed
  with `Re:` if it isn't already. Max 2000 characters.
</ParamField>

<ParamField body="reply_all" type="boolean" default="false">
  Reply to everyone on the original message, not only its author. The reply goes
  to the author, or its `Reply-To` address if it has one, and to the message's
  `to` and `cc` recipients, excluding the inbox's own address. `bcc` recipients
  are never copied.
</ParamField>

<ParamField body="attachments" type="array">
  Filename and content of attachments (max 25MB of content per message). A
  `path` is fetched when the email is sent and does not count toward that limit.

  [See examples](/docs/dashboard/emails/attachments)

  <Expandable defaultOpen="true" title="properties">
    <ParamField body="content" type="buffer | string">
      Content of an attached file, passed as a buffer or Base64 string.
    </ParamField>

    <ParamField body="filename" type="string">
      Name of attached file.
    </ParamField>

    <ParamField body="path" type="string">
      Path where the attachment file is hosted
    </ParamField>

    <ResendParamField body="content_type" type="string">
      Content type for the attachment.
    </ResendParamField>

    <ResendParamField body="content_id" type="string">
      You can embed images using the content id parameter for the attachment. To show the image, you need to include the ID in the `src` attribute of the `img` tag (e.g., `<img src="cid:...">`) of your HTML. [Learn about inline images](/docs/dashboard/emails/embed-inline-images).
    </ResendParamField>
  </Expandable>
</ParamField>

<ParamField body="headers" type="object">
  Custom headers to add to the email. `In-Reply-To`, `References`, and
  `Reply-To` can't be set and return `422`.
</ParamField>

## Headers

<ParamField header="Idempotency-Key" type="string">
  Add an idempotency key to prevent duplicated emails.

  * Should be **unique per API request**
  * Idempotency keys expire after **24 hours**
  * Have a maximum length of **256 characters**

  [Learn more](/docs/dashboard/emails/idempotency-keys)
</ParamField>

## Response Fields

<ParamField body="id" type="string">
  The ID of the queued outbound email.
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
  resend inboxes threads emails reply \
    --inbox_id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
    --thread_id 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12 \
    --email_id 5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60 \
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
