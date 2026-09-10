> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Domain

> Create a domain through the Resend Email API.

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

## Body Parameters

<ParamField body="name" type="string" required>
  The name of the domain you want to create.
</ParamField>

<ParamField body="region" type="string" default="us-east-1">
  The region where emails will be sent from. Possible values: `'us-east-1' |
      'eu-west-1' | 'sa-east-1' | 'ap-northeast-1'`
</ParamField>

<ResendParamField body="custom_return_path" type="string" default="send">
  For advanced use cases, choose a subdomain for the Return-Path address. The
  custom return path is used for SPF authentication, DMARC alignment, and
  handling bounced emails. Defaults to `send` (i.e., `send.yourdomain.tld`). Avoid
  setting values that could undermine credibility (e.g. `testing`), as they may
  be exposed to recipients.

  Learn more about [custom return paths](/docs/dashboard/domains/custom-return-path).
</ResendParamField>

<ResendParamField body="open_tracking" type="boolean">
  Track the open rate of each email.

  <Info>
    This setting is only applied if a `tracking_subdomain` is configured and verified.
  </Info>
</ResendParamField>

<ResendParamField body="click_tracking" type="boolean">
  Track clicks within the body of each HTML email.

  <Info>
    This setting is only applied if a `tracking_subdomain` is configured and verified.
  </Info>
</ResendParamField>

<ResendParamField body="tracking_subdomain" type="string">
  Configure a custom subdomain for click and open tracking. For example, setting
  `"links"` on domain `example.com` will produce a CNAME record for
  `links.example.com`. Avoid setting values that have a negative connotation (e.g. `tracking`).

  Learn more about [custom tracking subdomains](/docs/dashboard/domains/tracking).
</ResendParamField>

<ParamField body="tls" type="string" default="opportunistic">
  <ul>
    <li>
      `opportunistic`: Opportunistic TLS means that it always attempts to make a
      secure connection to the receiving mail server. If it can't establish a
      secure connection, it sends the message unencrypted.
    </li>

    <li>
      `enforced`: Enforced TLS on the other hand, requires that the email
      communication must use TLS no matter what. If the receiving server does
      not support TLS, the email will not be sent.
    </li>
  </ul>
</ParamField>

<ParamField body="capabilities" type="object">
  Configure the domain capabilities for sending and receiving emails. At least one capability must be enabled.

  <Expandable title="properties">
    <ParamField body="sending" type="string" default="enabled">
      Enable or disable sending emails from this domain. Possible values: `'enabled' | 'disabled'`
    </ParamField>

    <ParamField body="receiving" type="string" default="disabled">
      Enable or disable receiving emails to this domain. Possible values: `'enabled' | 'disabled'`
    </ParamField>
  </Expandable>
</ParamField>

<Info>
  See all available [domain `status`
  types](/docs/dashboard/domains/manage-domains#understand-a-domain-status).
</Info>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.domains.create({ name: 'example.com' });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->domains->create([
    'name' => 'example.com'
  ]);
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  params: resend.Domains.CreateParams = {
    "name": "example.com",
  }

  resend.Domains.create(params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  Resend.api_key = ENV["RESEND_API_KEY"]

  params = {
    name: "example.com",
  }
  domain = Resend::Domains.create(params)
  puts domain
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v3"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	params := &resend.CreateDomainRequest{
  		Name: "example.com",
  	}

  	client.Domains.Create(params)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{types::CreateDomainOptions, Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _domain = resend
      .domains
      .create(CreateDomainOptions::new("example.com"))
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;

  public class Main {
      public static void main(String[] args) {
          Resend resend = new Resend("re_xxxxxxxxx");

          CreateDomainOptions params = CreateDomainOptions
                  .builder()
                  .name("example.com").build();

          CreateDomainResponse domain = resend.domains().create(params);
      }
  }
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  var resp = await resend.DomainAddAsync( "example.com" );
  Console.WriteLine( "Domain Id={0}", resp.Content.Id );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/domains' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "name": "example.com"
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend domains create --name example.com --region us-east-1
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "id": "4dd369bc-aa82-4ff3-97de-514ae3000ee0",
    "name": "example.com",
    "created_at": "2026-03-28 17:12:02.059593+00",
    "status": "not_started",
    "open_tracking": true,
    "click_tracking": false,
    "tracking_subdomain": "links",
    "capabilities": {
      "sending": "enabled",
      "receiving": "disabled"
    },
    "records": [
      {
        "record": "SPF",
        "name": "send",
        "type": "MX",
        "ttl": "Auto",
        "status": "not_started",
        "value": "feedback-smtp.us-east-1.amazonses.com",
        "priority": 10
      },
      {
        "record": "SPF",
        "name": "send",
        "value": "\"v=spf1 include:amazonses.com ~all\"",
        "type": "TXT",
        "ttl": "Auto",
        "status": "not_started"
      },
      {
        "record": "DKIM",
        "name": "nhapbbryle57yxg3fbjytyodgbt2kyyg._domainkey",
        "value": "nhapbbryle57yxg3fbjytyodgbt2kyyg.dkim.amazonses.com.",
        "type": "CNAME",
        "status": "not_started",
        "ttl": "Auto"
      },
      {
        "record": "DKIM",
        "name": "xbakwbe5fcscrhzshpap6kbxesf6pfgn._domainkey",
        "value": "xbakwbe5fcscrhzshpap6kbxesf6pfgn.dkim.amazonses.com.",
        "type": "CNAME",
        "status": "not_started",
        "ttl": "Auto"
      },
      {
        "record": "DKIM",
        "name": "txrcreso3dqbvcve45tqyosxwaegvhgn._domainkey",
        "value": "txrcreso3dqbvcve45tqyosxwaegvhgn.dkim.amazonses.com.",
        "type": "CNAME",
        "status": "not_started",
        "ttl": "Auto"
      },
      {
        "record": "Tracking",
        "name": "links.example.com",
        "type": "CNAME",
        "value": "links1.resend-dns.com",
        "ttl": "Auto",
        "status": "not_started"
      }
    ],
    "region": "us-east-1"
  }
  ```
</ResponseExample>
