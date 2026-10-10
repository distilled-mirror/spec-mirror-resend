> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Inbox

> Create an inbox to send, receive and organize email.

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
    npm install resend@6.32.1-preview-inboxes.6
    ```

    ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
    npm install -g resend-cli@2.22.0-preview-inboxes.9
    ```
  </CodeGroup>
</Warning>

An inbox sends and receives email at an address on one of your domains, such as
`support@example.com`.

## Body Parameters

<ResendParamField body="email_address" type="string" required>
  The inbox email address on one of your domains. The domain must be verified to
  send email, and verified to receive email unless `forwarding` is `true`.
</ResendParamField>

<ParamField body="name" type="string">
  Internal name for the inbox. Recipients do not see it. Defaults to
  `email_address`.
</ParamField>

<ResendParamField body="from_name" type="string">
  The name recipients see when mail is sent from this inbox. A plain name, not
  a `Name <email>` address.
</ResendParamField>

<ParamField body="forwarding" type="boolean">
  When `true`, Resend provisions a receiving address so you can receive mail
  without adding an MX record. Read it from `receiving_address` with [Get
  Inbox](/docs/api-reference/inboxes/get-inbox). Defaults to `false`.
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.inboxes.create({
    emailAddress: 'support@example.com',
    name: 'Customer Support',
    fromName: 'Ada from Support',
  });
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/inboxes' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "email_address": "support@example.com",
    "name": "Customer Support",
    "from_name": "Ada from Support"
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend inboxes create \
    --email_address support@example.com \
    --name "Customer Support" \
    --from_name "Ada from Support"
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "inbox",
    "id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1"
  }
  ```
</ResponseExample>
