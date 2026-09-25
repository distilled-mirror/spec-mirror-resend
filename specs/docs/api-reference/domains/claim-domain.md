> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Claim Domain

> Claim a domain that is already verified by another team.

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
  Use this endpoint when [creating a
  domain](/docs/api-reference/domains/create-domain) fails because the domain is
  already verified by another team. Resend creates a placeholder domain on your
  team and returns a `domain_claim` with a TXT record to add to your DNS. Learn
  more in [Claiming a domain](/docs/dashboard/domains/claim).
</Note>

## Body Parameters

<ParamField body="name" type="string" required>
  The name of the domain you want to claim.
</ParamField>

<ParamField body="region" type="string" default="us-east-1">
  The region where emails will be sent from. Possible values: `'us-east-1' |
      'eu-west-1' | 'sa-east-1' | 'ap-northeast-1'`
</ParamField>

<ResendParamField body="custom_return_path" type="string" default="send">
  Choose a subdomain for the Return-Path address. Defaults to `send` (i.e.,
  `send.yourdomain.tld`). Avoid setting values that could undermine credibility
  (e.g. `testing`), as they may be exposed to recipients.
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

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.domains.claims.create({
    name: 'example.com',
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->domains->claims->create([
    'name' => 'example.com'
  ]);
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  params: resend.Domains.Claims.CreateParams = {
    "name": "example.com",
  }

  resend.Domains.Claims.create(params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  params = {
    name: "example.com",
  }
  claim = Resend::Domains::Claims.create(params)
  puts claim
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v4"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	params := &resend.CreateDomainClaimRequest{
  		Name: "example.com",
  	}

  	client.DomainClaims.Create(params)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{Resend, Result, types::CreateDomainClaimOptions};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let domain_claim = CreateDomainClaimOptions::new("example.com");
    let _data = resend.domains.claim(domain_claim).await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.Resend;
  import com.resend.core.exception.ResendException;
  import com.resend.services.domains.model.ClaimDomainOptions;
  import com.resend.services.domains.model.DomainClaimResponseSuccess;

  public class Main {
      public static void main(String[] args) throws ResendException {
          Resend resend = new Resend("re_xxxxxxxxx");

          ClaimDomainOptions params = ClaimDomainOptions
                  .builder()
                  .name("example.com").build();

          DomainClaimResponseSuccess claim = resend.domains().claims().create(params);
      }
  }
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/domains/claim' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "name": "example.com"
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend domains claim create --name example.com
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "domain_claim",
    "id": "dacf4072-4119-4d88-932f-6c6126d3a9d1",
    "name": "example.com",
    "status": "pending",
    "domain_id": "d91cd9bd-1176-453e-8fc1-35364d380206",
    "region": "us-east-1",
    "record": {
      "type": "TXT",
      "name": "example.com",
      "value": "resend-domain-verification=3f8a1c2d4e5b6a7f8091a2b3c4d5e6f7",
      "ttl": "Auto"
    },
    "blocked_reason": null,
    "failure_reason": null,
    "created_at": "2026-06-16 17:12:02.059593+00",
    "expires_at": "2026-06-23 17:12:02.059593+00"
  }
  ```
</ResponseExample>
