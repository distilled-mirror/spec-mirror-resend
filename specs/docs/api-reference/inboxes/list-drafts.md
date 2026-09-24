> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# List Drafts

> Retrieve the drafts on an inbox.

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

Unsent drafts, most recently updated first.

## Path Parameters

<ResendParamField path="inbox_id" type="string" required>
  The Inbox ID.
</ResendParamField>

## Query Parameters

<ParamField query="limit" type="number">
  Number of drafts to return. Default is `20`, maximum is `100`, minimum is `1`.
</ParamField>

<ParamField query="after" type="string">
  The ID of the last draft on the current page. Returns the next, older page.
</ParamField>

<ParamField query="before" type="string">
  The ID of the first draft on the current page. Returns the previous, newer
  page.
</ParamField>

## Response Fields

<ParamField body="object" type="string">
  Always `list`.
</ParamField>

<ParamField body="has_more" type="boolean">
  Whether more drafts exist beyond this page. Pass the last draft's `id` as
  `after` to continue.
</ParamField>

<ParamField body="data" type="array">
  The drafts on this page.

  <Expandable defaultOpen="true" title="properties">
    <ParamField body="id" type="string">
      The ID of the draft.
    </ParamField>

    <ParamField body="type" type="string">
      `standalone` for a new conversation, or `reply`.
    </ParamField>

    <ParamField body="to" type="string[] | null">
      Recipients.
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

    <ParamField body="snippet" type="string | null">
      A short preview of the body.
    </ParamField>

    <ParamField body="thread_id" type="string | null">
      The Thread ID when this draft is a reply. `null` otherwise.
    </ParamField>

    <ParamField body="reply_to_email_id" type="string | null">
      The Email ID being replied to. `null` otherwise.
    </ParamField>

    <ParamField body="updated_at" type="string">
      ISO 8601 timestamp when the draft was last saved.
    </ParamField>
  </Expandable>
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.inboxes.drafts.list({
    inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
  });
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/drafts' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend inboxes drafts list --inbox_id b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "list",
    "has_more": false,
    "data": [
      {
        "id": "c3a1e8b4-2d5f-4a7c-9e10-6b8d7f5a4c32",
        "type": "standalone",
        "to": ["ada@example.org"],
        "cc": [],
        "bcc": [],
        "subject": "Refund for order 1041",
        "snippet": "Refund issued for order 1041.",
        "thread_id": null,
        "reply_to_email_id": null,
        "updated_at": "2026-08-05T14:12:04.110Z"
      }
    ]
  }
  ```
</ResponseExample>
