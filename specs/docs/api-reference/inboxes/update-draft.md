> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Draft

> Update fields on an existing draft.

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

Updates the content of an unsent draft. Send at least one of `to`, `cc`, `bcc`,
`subject`, `text`, `html`, or `attachments`. An empty body is rejected even when
the draft already has files. A body with none of these keys returns a `422`, even
when it has other keys.

Fields you leave out stay as they are. `html` and `text` are the exception:
sending either one replaces both, and the one you leave out is saved as `null`.
For `attachments`, a present array replaces every file on the draft, `[]` or
`null` removes them, and leaving the field out keeps them.

After the update, the draft must still contain at least one non-empty field.
Files already on the draft count toward that. The combined recipients cannot
exceed 50. A draft that was already sent, or that changed during the request,
returns a `409`.

## Path Parameters

<ResendParamField path="inbox_id" type="string" required>
  The Inbox ID. An email address is not accepted.
</ResendParamField>

<ResendParamField path="draft_id" type="string" required>
  The Draft ID.
</ResendParamField>

## Body Parameters

<ParamField body="to" type="string | string[] | null">
  Recipients. For multiple addresses, send an array of strings. Each value can
  include a friendly name. Pass `null` to clear.
</ParamField>

<ParamField body="cc" type="string | string[] | null">
  CC recipients. Pass `null` or `[]` to clear.
</ParamField>

<ParamField body="bcc" type="string | string[] | null">
  BCC recipients. Pass `null` or `[]` to clear.
</ParamField>

<ParamField body="subject" type="string | null">
  The subject. Max 2000 characters. Must not contain a line break. Pass `null`
  to clear.
</ParamField>

<ParamField body="html" type="string | null">
  The HTML body. Pass `null` to clear. Sending `html` or `text` replaces both,
  and the one you leave out is saved as `null`.
</ParamField>

<ParamField body="text" type="string | null">
  The plain-text body. Pass `null` to clear. Sending `html` or `text` replaces
  both, and the one you leave out is saved as `null`.
</ParamField>

<ParamField body="attachments" type="array | null">
  Files to store on the draft. Each one needs `content`, `filename`, and
  `content_type`. `path` and `content_id` return `422`. An empty file or a
  blocked file type, such as `.exe`, returns `422`. The files on a draft can
  total at most 25 MB. A present array
  replaces every file on the draft. `[]` or `null` removes them. Leave the field out to
  keep the current files.

  <Expandable defaultOpen="true" title="properties">
    <ParamField body="content" type="buffer | string" required>
      Content of an attached file, passed as a buffer or Base64 string.
    </ParamField>

    <ParamField body="filename" type="string" required>
      Name of attached file.
    </ParamField>

    <ResendParamField body="content_type" type="string" required>
      Content type for the attachment.
    </ResendParamField>
  </Expandable>
</ParamField>

## Response Fields

<ParamField body="object" type="string">
  Always `inbox_draft`.
</ParamField>

<ParamField body="id" type="string">
  The ID of the draft.
</ParamField>

<ParamField body="type" type="string">
  `reply` when the draft replies to an email in an existing thread. `standalone`
  when the draft starts a new thread.
</ParamField>

<ParamField body="to" type="string[] | null">
  Recipients. `null` or empty when no recipients are set.
</ParamField>

<ParamField body="cc" type="string[]">
  CC recipients.
</ParamField>

<ParamField body="bcc" type="string[]">
  BCC recipients.
</ParamField>

<ParamField body="subject" type="string | null">
  The subject.
</ParamField>

<ParamField body="html" type="string | null">
  The HTML body.
</ParamField>

<ParamField body="text" type="string | null">
  The plain-text body.
</ParamField>

<ParamField body="thread_id" type="string | null">
  The Thread ID when this draft is a reply. `null` otherwise.
</ParamField>

<ParamField body="reply_to_email_id" type="string | null">
  The Email ID being replied to. `null` otherwise.
</ParamField>

<ParamField body="email_id" type="string | null">
  The ID of the outbound email queued when the draft was sent. `null` until the
  draft is sent.
</ParamField>

<ParamField body="created_at" type="string">
  ISO 8601 timestamp when the draft was created.
</ParamField>

<ParamField body="updated_at" type="string">
  ISO 8601 timestamp when the draft was last saved.
</ParamField>

<ParamField body="attachments" type="array">
  The files saved on the draft.

  <Expandable defaultOpen="true" title="properties">
    <ParamField body="id" type="string">
      The ID of the attachment.
    </ParamField>

    <ParamField body="filename" type="string">
      The filename of the attachment.
    </ParamField>

    <ParamField body="content_type" type="string">
      The MIME type of the attachment, such as `application/pdf`.
    </ParamField>

    <ParamField body="size" type="number">
      The size of the attachment in bytes.
    </ParamField>
  </Expandable>
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.inboxes.drafts.update({
    inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
    draftId: 'c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32',
    subject: 'Refund issued for order 1041',
  });
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
  resend inboxes drafts update b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32 \
    --subject "Refund issued for order 1041"
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "inbox_draft",
    "id": "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
    "type": "standalone",
    "to": ["ada@example.org"],
    "cc": [],
    "bcc": [],
    "subject": "Refund issued for order 1041",
    "html": "<p>Refund issued for order 1041.</p>",
    "text": "Refund issued for order 1041.",
    "thread_id": null,
    "reply_to_email_id": null,
    "email_id": null,
    "created_at": "2026-08-05T14:12:04.110Z",
    "updated_at": "2026-08-05T14:13:22.004Z",
    "attachments": [
      {
        "id": "9d4f2b81-6c3a-4e7d-8b12-0a5c6d7e8f90",
        "filename": "receipt.pdf",
        "content_type": "application/pdf",
        "size": 5
      }
    ]
  }
  ```
</ResponseExample>
