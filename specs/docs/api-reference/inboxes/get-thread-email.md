> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Retrieve Thread Email

> Retrieve a single message from a thread.

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

Returns one message of a thread. Each item from [List Thread
Emails](/docs/api-reference/inboxes/list-thread-emails) has this shape.

## Path Parameters

<ResendParamField path="inbox_id" type="string" required>
  The Inbox ID. An email address is not accepted.
</ResendParamField>

<ResendParamField path="thread_id" type="string" required>
  The Thread ID.
</ResendParamField>

<ResendParamField path="email_id" type="string" required>
  The Email ID, as returned by [List Thread
  Emails](/docs/api-reference/inboxes/list-thread-emails) in `data[].id`.
</ResendParamField>

## Response Fields

<ParamField body="id" type="string">
  The ID of the message.
</ParamField>

<ParamField body="direction" type="string">
  Whether the message was received by the inbox or sent from it. One of
  `inbound` or `outbound`. A message the inbox sent to itself is `inbound`, so a
  reply to it goes to its sender.
</ParamField>

<ParamField body="from" type="string">
  Sender email address. Includes the display name when the sender has one, in
  the format `Name <sender@domain.com>`.
</ParamField>

<ParamField body="to" type="string[]">
  The recipients of the message. For a received message, these are the addresses
  it was delivered to, not the full `To` header.
</ParamField>

<ParamField body="cc" type="string[]">
  The CC recipients of the message.
</ParamField>

<ParamField body="bcc" type="string[]">
  The BCC recipients of the message. Always empty for a received message.
</ParamField>

<ParamField body="reply_to" type="string[]">
  The Reply-To addresses.
</ParamField>

<ParamField body="subject" type="string | null">
  The subject of the message.
</ParamField>

<ParamField body="message_id" type="string | null">
  The Message-ID header of the message.
</ParamField>

<ParamField body="html" type="string | null">
  The HTML body.
</ParamField>

<ParamField body="text" type="string | null">
  The plain-text body.
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
  ISO 8601 timestamp when the inbox received the message, or when the inbox sent
  it.
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.inboxes.threads.emails.get({
    inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
    threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
    emailId: '5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60',
  });
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12/emails/5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend inboxes threads emails get b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12 5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "id": "5b1a9f47-2c8d-4e6f-9a03-1d2e3f4a5b60",
    "direction": "inbound",
    "from": "Ada Lovelace <ada@example.org>",
    "to": ["support@example.com"],
    "cc": [],
    "bcc": [],
    "reply_to": ["replies@example.org"],
    "subject": "Refund for order 1041",
    "message_id": "<1041@example.org>",
    "html": "<p>Could I get a refund for order 1041?</p>",
    "text": "Could I get a refund for order 1041?",
    "attachments": [
      {
        "id": "9d4f2b81-6c3a-4e7d-8b12-0a5c6d7e8f90",
        "filename": "receipt.pdf",
        "size": 20841
      }
    ],
    "read": false,
    "received_at": "2026-08-05T14:03:11.229Z"
  }
  ```
</ResponseExample>
