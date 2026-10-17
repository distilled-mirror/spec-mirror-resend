> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Draft

> Update an unsent draft.

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

Updates the content of an unsent draft.

## Path Parameters

<ResendParamField path="inbox_id" type="string" required>
  The Inbox ID or the inbox email address, such as `support@example.com`.
</ResendParamField>

<ResendParamField path="draft_id" type="string" required>
  The Draft ID.
</ResendParamField>

## Body Parameters

<ParamField body="to" type="string | string[] | null">
  Recipients.
</ParamField>

<ParamField body="cc" type="string | string[] | null">
  CC recipients.
</ParamField>

<ParamField body="bcc" type="string | string[] | null">
  BCC recipients.
</ParamField>

<ParamField body="subject" type="string | null">
  The subject. Max 2000 characters.
</ParamField>

<ParamField body="html" type="string | null">
  The HTML body.
</ParamField>

<ParamField body="text" type="string | null">
  The plain-text body. Pass `null` to clear. Sending `html` or `text` replaces
  both, and the one you leave out is saved as `null`.
</ParamField>

<ParamField body="attachments" type="array | null">
  Files to store on the draft.

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
    "id": "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32"
  }
  ```
</ResponseExample>
