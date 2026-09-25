> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Rotate Signing Secret

> Generate a new signing secret for a webhook.

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

<Note>
  For 24 hours after the rotation, payloads are signed with both the new and the
  previous secret, so either one verifies them. After that, only the new secret
  does. Use that window to update the secret your application uses to [verify
  requests](/docs/webhooks/verify-webhooks-requests) without dropping events.
</Note>

## Path Parameters

<ResendParamField path="webhook_id" type="string" required>
  The Webhook ID.
</ResendParamField>

## Response Fields

<ParamField body="object" type="string">
  Always `webhook`.
</ParamField>

<ParamField body="id" type="string">
  The Webhook ID.
</ParamField>

<ParamField body="signing_secret" type="string">
  The new signing secret.
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.webhooks.rotateSigningSecret(
    '4dd369bc-aa82-4ff3-97de-514ae3000ee0',
  );
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $webhook = $resend->webhooks->rotateSigningSecret(
      '4dd369bc-aa82-4ff3-97de-514ae3000ee0'
  );
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = 're_xxxxxxxxx'

  webhook = resend.Webhooks.rotate_signing_secret(
      webhook_id='4dd369bc-aa82-4ff3-97de-514ae3000ee0',
  )
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require 'resend'

  Resend.api_key = 're_xxxxxxxxx'

  webhook = Resend::Webhooks.rotate_signing_secret(
    '4dd369bc-aa82-4ff3-97de-514ae3000ee0'
  )
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v4"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	client.Webhooks.RotateSigningSecret(
  		"4dd369bc-aa82-4ff3-97de-514ae3000ee0",
  	)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _webhook = resend
      .webhooks
      .rotate_signing_secret("4dd369bc-aa82-4ff3-97de-514ae3000ee0")
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.Resend;
  import com.resend.core.exception.ResendException;
  import com.resend.services.webhooks.model.RotateWebhookSigningSecretResponseSuccess;

  public class Main {
      public static void main(String[] args) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          RotateWebhookSigningSecretResponseSuccess webhook = resend.webhooks().rotateSigningSecret(
              "4dd369bc-aa82-4ff3-97de-514ae3000ee0"
          );
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.WebhookRotateSigningSecretAsync(
      new Guid( "4dd369bc-aa82-4ff3-97de-514ae3000ee0" )
  );
  Console.WriteLine( "Signing secret={0}", resp.Content.SigningSecret );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/webhooks/4dd369bc-aa82-4ff3-97de-514ae3000ee0/signing-secret/rotate' \
       -H 'Authorization: Bearer re_xxxxxxxxx'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend webhooks rotate-signing-secret 4dd369bc-aa82-4ff3-97de-514ae3000ee0
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "webhook",
    "id": "4dd369bc-aa82-4ff3-97de-514ae3000ee0",
    "signing_secret": "whsec_xxxxxxxxxx"
  }
  ```
</ResponseExample>
