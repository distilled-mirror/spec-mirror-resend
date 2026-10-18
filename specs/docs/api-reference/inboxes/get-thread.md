> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Retrieve Thread

> Retrieve a thread summary.

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

The response is the thread summary. Messages are listed separately with [List
Thread Emails](/docs/api-reference/inboxes/list-thread-emails).

## Path Parameters

<ResendParamField path="inbox_id" type="string" required>
  The Inbox ID or the inbox email address, such as `support@example.com`.
</ResendParamField>

<ResendParamField path="thread_id" type="string" required>
  The Thread ID.
</ResendParamField>

## Response Fields

<ParamField body="object" type="string">
  Always `inbox_thread`.
</ParamField>

<ParamField body="id" type="string">
  The ID of the thread.
</ParamField>

<ParamField body="subject" type="string | null">
  The subject of the thread.
</ParamField>

<ParamField body="folder" type="string">
  The folder the thread lives in. Every thread sits in exactly one folder within
  its inbox. You can move a thread to `inbox`, `archive`, `spam`, or `trash`.
  `sent` is assigned automatically.

  * `inbox`: The default. The thread holds at least one received message.
  * `archive`: The thread was archived.
  * `spam`: The thread was marked as spam.
  * `trash`: The thread is scheduled for deletion in 30 days.
  * `sent`: Threads whose messages are all outbound.
</ParamField>

<ParamField body="labels" type="array">
  The labels attached to the thread.

  <Expandable title="properties">
    <ParamField body="id" type="string">
      The ID of the label.
    </ParamField>

    <ParamField body="name" type="string">
      The name of the label.
    </ParamField>

    <ParamField body="color" type="string">
      The color of the label as an uppercase `#RRGGBB` hex code.
    </ParamField>
  </Expandable>
</ParamField>

<ParamField body="read" type="boolean">
  True only when every message in the thread is read.
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.inboxes.threads.get({
    inboxId: 'b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1',
    threadId: '4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12',
  });
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X GET 'https://api.resend.com/inboxes/b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1/threads/4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend inboxes threads get b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1 4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "inbox_thread",
    "id": "4d8e2a1c-9b3f-4c6d-8a21-3e5f7c9c0d12",
    "subject": "Refund for order 1041",
    "folder": "inbox",
    "labels": [
      {
        "id": "7f9c1d2e-4a6b-4c3d-8e15-9b0a7c6d5e34",
        "name": "Urgent",
        "color": "#E93D82"
      }
    ],
    "read": false
  }
  ```
</ResponseExample>
