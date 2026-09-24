> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Forward Thread Email

> Forward a message in an inbox thread to new recipients.

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
  number of users. The response shape might change before GA. [Get in
  touch](https://resend.com/help) if you're interested in testing this
  feature.

  <span />

  Once you have access, upgrade your Resend SDK to use the methods on this
  page:

  <CodeGroup>
    ```bash Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install resend@6.28.1-preview-inboxes.1
    ```

    ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install -g resend-cli@2.22.0-preview-inboxes.1
    ```
  </CodeGroup>
</Warning>

Forwards from the inbox address. `to` is required. The original message is
quoted under a forwarded-message banner.

## Path Parameters

<ResendParamField path="inbox_id" type="string" required>
  The Inbox ID.
</ResendParamField>

<ResendParamField path="thread_id" type="string" required>
  The Thread ID.
</ResendParamField>

<ResendParamField path="email_id" type="string" required>
  The Email ID of the message to forward, as returned in the thread's
  `messages[].id`.
</ResendParamField>

## Body Parameters

<ParamField body="to" type="string | string[]" required>
  Recipient email address. For multiple addresses, send as an array of strings.
  Max 50.
</ParamField>

<ParamField body="html" type="string">
  An HTML note sent above the quoted original.
</ParamField>

<ParamField body="text" type="string">
  A plain-text note sent above the quoted original.
</ParamField>

<ParamField body="subject" type="string">
  The subject of the forward. When omitted, the thread subject is used, prefixed
  with `Fwd:` if it isn't already.
</ParamField>

## Response Fields

<ParamField body="id" type="string">
  The ID of the queued outbound email.
</ParamField>

<ParamField body="email_id" type="string">
  The ID of the queued outbound email. Same value as `id`.
</ParamField>

<ParamField body="direction" type="string">
  Always `outbound`.
</ParamField>

<ParamField body="from" type="string">
  Sender email address.
</ParamField>

<ParamField body="to" type="string[]">
  The recipients of the message.
</ParamField>

<ParamField body="cc" type="string[]">
  The CC recipients of the message.
</ParamField>

<ParamField body="bcc" type="string[]">
  The BCC recipients of the message.
</ParamField>

<ParamField body="reply_to" type="string[]">
  Always an empty array.
</ParamField>

<ParamField body="subject" type="string">
  The subject of the sent forward.
</ParamField>

<ParamField body="message_id" type="string | null">
  Always `null`.
</ParamField>

<ParamField body="html" type="string">
  The HTML body, including the note and the quoted original.
</ParamField>

<ParamField body="text" type="string">
  The plain-text body, including the note and the quoted original.
</ParamField>

<ParamField body="attachments" type="array">
  The attachments on the message.

  <Expandable defaultOpen="true" title="properties">
    <ParamField body="id" type="string">
      The ID of the attachment.
    </ParamField>

    <ParamField body="filename" type="string | null">
      The filename of the attachment.
    </ParamField>

    <ParamField body="size" type="number | null">
      The size of the attachment in bytes.
    </ParamField>
  </Expandable>
</ParamField>

<ParamField body="read" type="boolean">
  Whether the message has been read.
</ParamField>

<ParamField body="received_at" type="string">
  ISO 8601 timestamp when the message was sent.
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.inboxes.threads.emails.forward({
    inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
    threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
    emailId: '5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60',
    to: ['colleague@example.org'],
    text: 'Flagging this refund request for you.',
  });
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12/emails/5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60/forward' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "to": ["colleague@example.org"],
    "text": "Flagging this refund request for you."
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend inboxes threads emails forward \
    --inbox_id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 \
    --thread_id 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12 \
    --email_id 5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60 \
    --to colleague@example.org \
    --text "Flagging this refund request for you."
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "id": "6a0c8e58-3d9e-4f7a-8b14-2e3f4a5b6c71",
    "email_id": "6a0c8e58-3d9e-4f7a-8b14-2e3f4a5b6c71",
    "direction": "outbound",
    "from": "support@example.com",
    "to": ["colleague@example.org"],
    "cc": [],
    "bcc": [],
    "reply_to": [],
    "subject": "Fwd: Refund for order 1041",
    "message_id": null,
    "html": "<div>Flagging this refund request for you.<br>\n<br>\n---------- Forwarded message ---------<br>\nFrom: Ada Lovelace &lt;ada@example.org&gt;<br>\nDate: Wed, Aug 5, 2026 at 2:03 PM<br>\nSubject: Refund for order 1041<br>\nTo: support@example.com<br>\n<br>\nCould I get a refund for order 1041?</div>",
    "text": "Flagging this refund request for you.\n\n---------- Forwarded message ---------\nFrom: Ada Lovelace <ada@example.org>\nDate: Wed, Aug 5, 2026 at 2:03 PM\nSubject: Refund for order 1041\nTo: support@example.com\n\nCould I get a refund for order 1041?",
    "attachments": [],
    "read": true,
    "received_at": "2026-08-05T14:12:04.110Z"
  }
  ```
</ResponseExample>
