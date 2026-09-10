> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Verify Domain Claim

> Trigger DNS verification for a domain claim.

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
  Calling this endpoint starts an **asynchronous verification process**. Resend
  checks the claim's TXT record and runs ownership-safety checks before
  transferring the domain to your team. Add the TXT record returned by [Claim
  Domain](/docs/api-reference/domains/claim-domain) before calling this, then poll
  [Retrieve Domain Claim](/docs/api-reference/domains/get-domain-claim) to follow the
  `status`.
</Note>

<Note>
  **After the claim completes:** the domain is transferred to your account as a
  brand-new domain with its own DKIM keys, so the previous account's DNS records
  can't be reused. Fetch it with [Retrieve
  Domain](/docs/api-reference/domains/get-domain), update your DNS with the new DKIM
  record(s), then run [Verify Domain](/docs/api-reference/domains/verify-domain) to
  finish setup before sending or receiving email. See [DKIM
  records](/docs/dashboard/domains/manage-domains#what-are-dkim-records) for details.
</Note>

## Path Parameters

<ResendParamField path="domain_id" type="string" required>
  The placeholder Domain ID returned when the claim was created.
</ResendParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.domains.claims.verify(
    'd91cd9bd-1176-453e-8fc1-35364d380206',
  );
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->domains->claims->verify(
    'd91cd9bd-1176-453e-8fc1-35364d380206'
  );
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  resend.Domains.Claims.verify(domain_id="d91cd9bd-1176-453e-8fc1-35364d380206")
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  Resend.api_key = ENV["RESEND_API_KEY"]

  claim = Resend::Domains::Claims.verify("d91cd9bd-1176-453e-8fc1-35364d380206")
  puts claim
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v3"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	client.DomainClaims.Verify("d91cd9bd-1176-453e-8fc1-35364d380206")
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let _data = resend
      .domains
      .verify_claim("d91cd9bd-1176-453e-8fc1-35364d380206")
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.*;

  public class Main {
      public static void main(String[] args) {
          Resend resend = new Resend("re_xxxxxxxxx");

          DomainClaimResponseSuccess claim = resend.domains().claims()
                  .verify("d91cd9bd-1176-453e-8fc1-35364d380206");
      }
  }
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X POST 'https://api.resend.com/domains/d91cd9bd-1176-453e-8fc1-35364d380206/claim/verify' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend domains claim verify d91cd9bd-1176-453e-8fc1-35364d380206
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
