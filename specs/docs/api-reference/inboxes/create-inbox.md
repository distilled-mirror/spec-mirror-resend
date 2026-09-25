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

An inbox sends and receives email at an address on one of your domains, such as
`support@example.com`.

## Body Parameters

<ResendParamField body="email_address" type="string" required>
  The inbox email address on one of your domains. The domain must be verified to
  send email, and verified to receive email unless `forwarding` is `true`.
</ResendParamField>

<ParamField body="name" type="string">
  Internal name for the inbox. Recipients do not see it.
</ParamField>

<ResendParamField body="friendly_name" type="string">
  The name recipients see when mail is sent from this inbox. A plain name, not
  a `Name <email>` address.
</ResendParamField>

<ParamField body="forwarding" type="boolean">
  When `true`, Resend provisions a receiving address so you can receive mail
  without adding an MX record. Defaults to `false`.
</ParamField>

## Response Fields

<ParamField body="object" type="string">
  Always `inbox`.
</ParamField>

<ParamField body="id" type="string">
  The ID of the inbox.
</ParamField>

<ParamField body="name" type="string">
  Internal name for the inbox. Recipients do not see it.
</ParamField>

<ParamField body="email_address" type="string">
  The address of the inbox.
</ParamField>

<ParamField body="domain_id" type="string">
  The ID of the domain that owns the address.
</ParamField>

<ParamField body="forwarding_address" type="string | null">
  The address to forward mail to when forwarding is enabled. `null` otherwise.
</ParamField>

<ParamField body="friendly_name" type="string | null">
  The name recipients see when mail is sent from this inbox. A plain name, not
  a `Name <email>` address.
</ParamField>

<ParamField body="unread" type="number">
  The number of unread threads in the inbox.
</ParamField>

<ParamField body="created_at" type="string">
  ISO 8601 timestamp when the inbox was created.
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.inboxes.create({
    emailAddress: 'support@example.com',
    name: 'Customer Support',
    friendlyName: 'Ada from Support',
  });
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/inboxes' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "email_address": "support@example.com",
    "name": "Customer Support",
    "friendly_name": "Ada from Support"
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend inboxes create \
    --email_address support@example.com \
    --name "Customer Support" \
    --friendly_name "Ada from Support"
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "inbox",
    "id": "b3e2b2b6-3f0e-4c8e-9ad3-2f43a1e2c7f1",
    "name": "Customer Support",
    "email_address": "support@example.com",
    "domain_id": "d91cd9bd-1176-453e-8fc1-35364d380206",
    "forwarding_address": null,
    "friendly_name": "Ada from Support",
    "unread": 0,
    "created_at": "2026-08-05T14:03:11.229Z"
  }
  ```
</ResponseExample>
