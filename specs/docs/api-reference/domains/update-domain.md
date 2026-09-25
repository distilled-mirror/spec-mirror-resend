> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Domain

> Update an existing domain.

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

## Path Parameters

<ResendParamField path="domain_id" type="string" required>
  The Domain ID.
</ResendParamField>

## Body Parameters

<ResendParamField body="click_tracking" type="boolean">
  Track clicks within the body of each HTML email.

  <Info>
    This setting is only applied if a `tracking_subdomain` is configured and verified.
  </Info>
</ResendParamField>

<ResendParamField body="open_tracking" type="boolean">
  Track the open rate of each email.

  <Info>
    This setting is only applied if a `tracking_subdomain` is configured and verified.
  </Info>
</ResendParamField>

<ResendParamField body="tracking_subdomain" type="string">
  Configure a custom subdomain for click and open tracking. For example, setting
  `"links"` on domain `example.com` will produce a CNAME record for
  `links.example.com`. Avoid setting values that have a negative connotation (e.g. `tracking`).

  This value can only be changed after it has been specified, never removed. This is to preserve any email links that
  may already be sent with the current tracking subdomain.

  After changing the tracking subdomain, a new DNS record must be verified, until then, the previous value is used.
  Do not remove old tracking DNS records, all previously used records remain active and are included in the response.

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
  Update the domain capabilities for sending and receiving emails. You can specify one or both fields. Omitted fields will keep their current value. At least one capability must remain enabled.

  <Expandable title="properties">
    <ParamField body="sending" type="string">
      Enable or disable sending emails from this domain. Possible values: `'enabled' | 'disabled'`
    </ParamField>

    <ParamField body="receiving" type="string">
      Enable or disable receiving emails to this domain. Possible values: `'enabled' | 'disabled'`
    </ParamField>
  </Expandable>
</ParamField>

<RequestExample>
  ```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
  import { Resend } from 'resend';

  const resend = new Resend('re_xxxxxxxxx');

  const { data, error } = await resend.domains.update({
    id: 'b8617ad3-b712-41d9-81a0-f7c3d879314e',
    openTracking: false,
    clickTracking: true,
    trackingSubdomain: 'links',
    tls: 'enforced',
  });
  ```

  ```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
  $resend = Resend::client('re_xxxxxxxxx');

  $resend->domains->update(
    'b8617ad3-b712-41d9-81a0-f7c3d879314e',
    [
      'open_tracking' => false,
      'click_tracking' => true,
      'tracking_subdomain' => 'links',
      'tls' => 'enforced',
    ]
  );
  ```

  ```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
  import resend

  resend.api_key = "re_xxxxxxxxx"

  params: resend.Domains.UpdateParams = {
    "id": "b8617ad3-b712-41d9-81a0-f7c3d879314e",
    "open_tracking": False,
    "click_tracking": True,
    "tracking_subdomain": "links",
    "tls": "enforced",
  }

  resend.Domains.update(params)
  ```

  ```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
  require "resend"

  Resend.api_key = "re_xxxxxxxxx"

  Resend::Domains.update({
    id: "b8617ad3-b712-41d9-81a0-f7c3d879314e",
    open_tracking: false,
    click_tracking: true,
    tracking_subdomain: "links",
    tls: "enforced",
  })
  ```

  ```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
  package main

  import "github.com/resend/resend-go/v4"

  func main() {
  	client := resend.NewClient("re_xxxxxxxxx")

  	updateDomainParams := &resend.UpdateDomainRequest{
  		OpenTracking:      false,
  		ClickTracking:     true,
  		TrackingSubdomain: "links",
  		Tls:               resend.Enforced,
  	}

  	client.Domains.Update("b8617ad3-b712-41d9-81a0-f7c3d879314e", updateDomainParams)
  }
  ```

  ```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
  use resend_rs::{types::{DomainChanges, Tls}, Resend, Result};

  #[tokio::main]
  async fn main() -> Result<()> {
    let resend = Resend::new("re_xxxxxxxxx");

    let changes = DomainChanges::new()
      .with_open_tracking(false)
      .with_click_tracking(true)
      .with_tracking_subdomain("links")
      .with_tls(Tls::Enforced);

    let _domain = resend
      .domains
      .update("b8617ad3-b712-41d9-81a0-f7c3d879314e", changes)
      .await?;

    Ok(())
  }
  ```

  ```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
  import com.resend.Resend;
  import com.resend.services.domains.model.Tls;
  import com.resend.services.domains.model.UpdateDomainOptions;

  Resend resend = new Resend("re_xxxxxxxxx");

  UpdateDomainOptions params = UpdateDomainOptions.builder()
                  .id("b8617ad3-b712-41d9-81a0-f7c3d879314e")
                  .openTracking(false)
                  .clickTracking(true)
                  .trackingSubdomain("links")
                  .tls(Tls.ENFORCED)
                  .build();

  resend.domains().update(params);
  ```

  ```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
  using Resend;

  IResend resend = ResendClient.Create( "re_xxxxxxxxx" ); // Or from DI

  await resend.DomainUpdateAsync(
      new Guid( "b8617ad3-b712-41d9-81a0-f7c3d879314e" ),
      new DomainUpdateData()
      {
          TrackOpen = false,
          TrackClicks = true,
          TrackingSubdomain = "links",
          TlsMode = TlsMode.Enforced,
      }
  );
  ```

  ```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
  curl -X PATCH 'https://api.resend.com/domains/b8617ad3-b712-41d9-81a0-f7c3d879314e' \
       -H 'Authorization: Bearer re_xxxxxxxxx' \
       -H 'Content-Type: application/json' \
       -d $'{
    "open_tracking": false,
    "click_tracking": true,
    "tracking_subdomain": "links",
    "tls": "enforced"
  }'
  ```

  ```bash CLI theme={"theme":{"light":"github-light","dark":"vesper"}}
  resend domains update b8617ad3-b712-41d9-81a0-f7c3d879314e \
    --no-open-tracking \
    --click-tracking \
    --tracking-subdomain links \
    --tls enforced
  ```
</RequestExample>

<ResponseExample>
  ```json Response theme={"theme":{"light":"github-light","dark":"vesper"}}
  {
    "object": "domain",
    "id": "b8617ad3-b712-41d9-81a0-f7c3d879314e"
  }
  ```
</ResponseExample>
