> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Open and Click Tracking

> Track open and click rates of your emails.

Open and click tracking is disabled by default for all domains. These settings apply to all emails sent from that domain.

We suggest only tracking open rates for the domain (or subdomain) used to send your [Broadcasts](/docs/dashboard/broadcasts/introduction.md) to ensure that inbox providers do not mistakenly identify your [transactional emails](/docs/dashboard/emails/introduction.md) as marketing emails.

> [!NOTE]
>
> Learn more about why it is better to [send emails from a
> subdomain](/docs/dashboard/domains/introduction.md#subdomains) than from your root
> domain.

You can enable tracking in the Resend Dashboard under the **Configuration** tab or programmatically when you create a new domain or update an existing domain.

Once verified, all tracked links in your emails will use your tracking subdomain (e.g., `links.emails.example.com`).

## Enable tracking using the Dashboard

**1. Go to the [**Domains** Dashboard page](https://resend.com/domains) and click on the domain you want to configure.**

**2. In the **Configuration** tab, click **Configure** under **Enable tracking metrics**.**

![Open and Click Tracking](https://mintcdn.com/resend/8slja5cHAobSwGo7/images/dashboard-domains-custom-tracking-domains.png?fit=max\&auto=format\&n=8slja5cHAobSwGo7\&q=85\&s=b94c649f1c22c899c144cd73ab5a8e73)

**3. Provide a name for your tracking subdomain, enable open and/or click tracking, and click **+Add domain**.**

![Verify Custom Tracking Subdomain](https://mintcdn.com/resend/aVe4W1upaT_ALaEY/images/dashboard-custom-tracking-domain-verify.png?fit=max\&auto=format\&n=aVe4W1upaT_ALaEY\&q=85\&s=aac30239e34f1fbf89bb9e41ba5540e8)

**4. Add the CNAME record to your DNS settings (e.g. Cloudflare, GoDaddy, etc.) to verify your tracking subdomain.**

![Add Custom Tracking Subdomain](https://mintcdn.com/resend/aVe4W1upaT_ALaEY/images/dashboard-domains-custom-tracking-domains-add.png?fit=max\&auto=format\&n=aVe4W1upaT_ALaEY\&q=85\&s=118b4d5f8269265c5eed074a52a2c9e5)

> [!NOTE]
>
> If we detect CAA records on your domain, we will show an additional CAA record
> that needs to be created. This ensures that we can issue a TLS certificate for
> your tracking subdomain.

**5. Click **I've added the records** to verify the domain.**

Once verified, all tracked links in your emails will use your custom tracking subdomain.

## Enable tracking via the API

**1. Provide the tracking subdomain**

When [adding a new domain](/docs/add-a-domain.md) to Resend, add tracking by passing the `tracking_subdomain` field along with `click_tracking` and/or `open_tracking`.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.domains.create({
  name: 'example.com',
  openTracking: true,
  clickTracking: true,
  trackingSubdomain: 'links',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->domains->create([
  'name' => 'example.com',
  'open_tracking' => true,
  'click_tracking' => true,
  'tracking_subdomain' => 'links',
]);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Domains.CreateParams = {
  "name": "example.com",
  "open_tracking": True,
  "click_tracking": True,
  "tracking_subdomain": "links",
}

resend.Domains.create(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

params = {
  name: "example.com",
  open_tracking: true,
  click_tracking: true,
  tracking_subdomain: "links",
}
Resend::Domains.create(params)
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
  client := resend.NewClient("re_xxxxxxxxx")

  params := &resend.CreateDomainRequest{
    Name:              "example.com",
    OpenTracking:      resend.Bool(true),
    ClickTracking:     resend.Bool(true),
    TrackingSubdomain: "links",
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
    .create(
      CreateDomainOptions::new("example.com")
        .with_open_tracking(true)
        .with_click_tracking(true)
        .with_tracking_subdomain("links"),
    )
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.*;
import com.resend.services.domains.model.CreateDomainOptions;

Resend resend = new Resend("re_xxxxxxxxx");

CreateDomainOptions params = CreateDomainOptions.builder()
        .name("example.com")
        .openTracking(true)
        .clickTracking(true)
        .trackingSubdomain("links")
        .build();

resend.domains().create(params);
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

var resp = await resend.DomainAddAsync( new DomainAddData()
{
    DomainName = "example.com",
    OpenTracking = true,
    ClickTracking = true,
    TrackingSubdomain = "links",
} );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/domains' \
    -H 'Authorization: Bearer re_xxxxxxxxx' \
    -H 'Content-Type: application/json' \
    -d $'{
  "name": "example.com",
  "open_tracking": true,
  "click_tracking": true,
  "tracking_subdomain": "links"
}'
```

If you already have a verified domain, call the `update` endpoint to add a tracking subdomain and enable tracking.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.domains.update({
  id: 'd91cd9bd-1176-453e-8fc1-35364d380206',
  openTracking: true,
  clickTracking: true,
  trackingSubdomain: 'links',
});
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->domains->update(
  'd91cd9bd-1176-453e-8fc1-35364d380206',
  [
    'open_tracking' => true,
    'click_tracking' => true,
    'tracking_subdomain' => 'links',
  ]
);
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

params: resend.Domains.UpdateParams = {
  "id": "d91cd9bd-1176-453e-8fc1-35364d380206",
  "open_tracking": True,
  "click_tracking": True,
  "tracking_subdomain": "links",
}

resend.Domains.update(params)
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Domains.update({
  id: "d91cd9bd-1176-453e-8fc1-35364d380206",
  open_tracking: true,
  click_tracking: true,
  tracking_subdomain: "links",
})
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
  client := resend.NewClient("re_xxxxxxxxx")

  params := &resend.UpdateDomainRequest{
    OpenTracking:      true,
    ClickTracking:     true,
    TrackingSubdomain: "links",
  }

  client.Domains.Update("d91cd9bd-1176-453e-8fc1-35364d380206", params)
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{types::DomainChanges, Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  let changes = DomainChanges::new()
    .with_open_tracking(true)
    .with_click_tracking(true)
    .with_tracking_subdomain("links");

  let _domain = resend
    .domains
    .update("d91cd9bd-1176-453e-8fc1-35364d380206", changes)
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.*;
import com.resend.services.domains.model.UpdateDomainOptions;

Resend resend = new Resend("re_xxxxxxxxx");

UpdateDomainOptions params = UpdateDomainOptions.builder()
        .id("d91cd9bd-1176-453e-8fc1-35364d380206")
        .openTracking(true)
        .clickTracking(true)
        .trackingSubdomain("links")
        .build();

resend.domains().update(params);
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

await resend.DomainUpdateAsync(
    new Guid( "d91cd9bd-1176-453e-8fc1-35364d380206" ),
    new DomainUpdateData()
    {
        TrackOpen = true,
        TrackClicks = true,
        TrackingSubdomain = "links",
    }
);
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X PATCH 'https://api.resend.com/domains/d91cd9bd-1176-453e-8fc1-35364d380206' \
    -H 'Authorization: Bearer re_xxxxxxxxx' \
    -H 'Content-Type: application/json' \
    -d $'{
  "open_tracking": true,
  "click_tracking": true,
  "tracking_subdomain": "links"
}'
```

**2. Add the CNAME record to your DNS settings (e.g. Cloudflare, GoDaddy, etc.) to verify your tracking subdomain.**

![Add Custom Tracking Subdomain](https://mintcdn.com/resend/aVe4W1upaT_ALaEY/images/dashboard-domains-custom-tracking-domains-add.png?fit=max\&auto=format\&n=aVe4W1upaT_ALaEY\&q=85\&s=118b4d5f8269265c5eed074a52a2c9e5)

> [!NOTE]
>
> If we detect CAA records on your domain, we will show an additional CAA record
> that needs to be created. This ensures that we can issue a TLS certificate for
> your tracking subdomain.

Whether creating or updating a domain, the API will return the required DNS records that need to be added to your domain provider's DNS settings. Note the `Tracking` record.

```json {15-22} API Response Example theme={"theme":{"light":"github-light","dark":"vesper"}}
{
  "id": "4dd369bc-aa82-4ff3-97de-514ae3000ee0",
  "name": "example.com",
  "created_at": "2026-03-28 17:12:02.059593+00",
  "status": "not_started",
  "open_tracking": true,
  "click_tracking": true,
  "tracking_subdomain": "links",
  "capabilities": {
    "sending": "enabled",
    "receiving": "disabled"
  },
  "records": [
    // ... other records ...
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

> [!NOTE]
>
> If we detect CAA records on your domain, we will show an additional CAA record
> that needs to be created. This ensures that we can issue a TLS certificate for
> your tracking subdomain.

**3. Verify the domain**

Once you've added the required DNS record(s), call the `verify` endpoint to verify the domain.

```ts Node.js theme={"theme":{"light":"github-light","dark":"vesper"}}
import { Resend } from 'resend';

const resend = new Resend('re_xxxxxxxxx');

const { data, error } = await resend.domains.verify(
  'd91cd9bd-1176-453e-8fc1-35364d380206',
);
```

```php PHP theme={"theme":{"light":"github-light","dark":"vesper"}}
$resend = Resend::client('re_xxxxxxxxx');

$resend->domains->verify('d91cd9bd-1176-453e-8fc1-35364d380206');
```

```python Python theme={"theme":{"light":"github-light","dark":"vesper"}}
import resend

resend.api_key = "re_xxxxxxxxx"

resend.Domains.verify(domain_id="d91cd9bd-1176-453e-8fc1-35364d380206")
```

```ruby Ruby theme={"theme":{"light":"github-light","dark":"vesper"}}
require "resend"

Resend.api_key = "re_xxxxxxxxx"

Resend::Domains.verify("d91cd9bd-1176-453e-8fc1-35364d380206")
```

```go Go theme={"theme":{"light":"github-light","dark":"vesper"}}
package main

import "github.com/resend/resend-go/v4"

func main() {
  client := resend.NewClient("re_xxxxxxxxx")

  client.Domains.Verify("d91cd9bd-1176-453e-8fc1-35364d380206")
}
```

```rust Rust theme={"theme":{"light":"github-light","dark":"vesper"}}
use resend_rs::{Resend, Result};

#[tokio::main]
async fn main() -> Result<()> {
  let resend = Resend::new("re_xxxxxxxxx");

  resend
    .domains
    .verify("d91cd9bd-1176-453e-8fc1-35364d380206")
    .await?;

  Ok(())
}
```

```java Java theme={"theme":{"light":"github-light","dark":"vesper"}}
import com.resend.*;
import com.resend.services.domains.model.VerifyDomainResponse;

Resend resend = new Resend("re_xxxxxxxxx");

VerifyDomainResponse verified = resend.domains().verify("d91cd9bd-1176-453e-8fc1-35364d380206");
```

```csharp .NET theme={"theme":{"light":"github-light","dark":"vesper"}}
using Resend;

IResend resend = ResendClient.Create( "re_xxxxxxxxx" );

await resend.DomainVerifyAsync( new Guid( "d91cd9bd-1176-453e-8fc1-35364d380206" ) );
```

```bash cURL theme={"theme":{"light":"github-light","dark":"vesper"}}
curl -X POST 'https://api.resend.com/domains/d91cd9bd-1176-453e-8fc1-35364d380206/verify' \
    -H 'Authorization: Bearer re_xxxxxxxxx' \
    -H 'Content-Type: application/json'
```

> [!NOTE]
>
> Tracking is active only when both of these conditions are met:
>
> <ol>
>   <li>
>     The `open_tracking` or `click_tracking` setting is enabled for the domain.
>   </li>
>
>   <li>
>     A tracking subdomain is configured (e.g., `links.example.com`) and
>     successfully verified.
>   </li>
> </ol>

All tracked links in your emails will use your tracking subdomain.

View the [API reference](/docs/api-reference/domains/create-domain.md) for more details.

## How Open Tracking Works

A 1x1 pixel transparent GIF image is inserted in each email and includes a unique reference to this image file. When
the image is downloaded, Resend can tell exactly which message was opened and by whom.

## How Click Tracking Works

To track clicks, Resend modifies each link in the body of the HTML email to point to your tracking subdomain.

When recipients clicks a link, the request is redirected to your tracking subdomain, their click event is recorded, and they are redirected to the original URL.

## Why open rates are not accurate

Open tracking is generally not accurate because each inbox handles incoming email differently.

**Clipped messages in Gmail** happen when you send a message over 102KB. A message over this size won’t be counted as an open unless the recipient views the entire message. Resend’s Deliverability Insights on the email will note if a message exceeds this threshold.

**Some inboxes do not download images by default** or block/cache assets with a corporate firewall. This approach can prevent the open event from being tracked.

**Other inboxes open the email prior to delivering** to scan for malware or to [protect user privacy](https://www.apple.com/newsroom/2021/06/apple-advances-its-privacy-leadership-with-ios-15-ipados-15-macos-monterey-and-watchos-8/). This approach can trigger an open event without the recipient reading your email.

**Emails sent with only a plain text version** will not include open tracking at all. Since open tracking relies on a 1x1 pixel image, plain text emails cannot trigger open events. Only emails with an HTML version can be tracked for opens.

Because of this, open tracking is **not a statistically accurate way** of detecting if your users are engaging with your content.

## How open tracking impacts inbox placement

Though open tracking does not impact whether your email is delivered, it most likely will impact your inbox placement. Trackers are generally **used by marketers and even spammers**. Because of this, inbox providers will often use open tracking as a signal that your email is promotional, or even spam, and categorize accordingly.

**We recommend disabling open rates for transactional email**, to maximize inbox placement.

## Alternatives to open tracking

Instead of relying on open rates, there are a few other ways to still understand your sending.

1. **Track Clicks:** Monitoring the link clicks is an even more granular way to know how a recipient engaged with your email. By knowing if they clicked, you also know that they read parts of your email and took action.
2. **Track Outside the Inbox:** Often emails are sent as a means to an end. Maybe it's to increase page visits of an announcement or convert free users to paid. Tracking your sending by metrics outside of the inbox can be a great way to understand the true impact of your sending.

## Troubleshooting

### Multiple tracking CNAME records

When you change your tracking subdomain, you may see two CNAME records in the DNS Records table: one active and one inactive (shown dimmed). The inactive record is kept intentionally to avoid breaking links in emails that were already sent using the previous subdomain. You do not need to remove it.

### Changing the Tracking Subdomain

Because tracking subdomains are used in email links, they're handled differently than other records.

* **Not removable**: After your tracking subdomain has been created, it can only be changed, never removed. This behavior preserves any
  email links that may already be sent with the current tracking subdomain. For this reason, do **not remove old tracking DNS records**. (All previously used records remain active and are included in the response.)
* **Requires verification**: After changing the tracking subdomain, a new DNS record must be verified. Until then, the previous value is used.

### Removing a Domain with a Tracking Subdomain

If you remove a domain with a configured tracking subdomain, the Resend provisioned proxy will also be removed, breaking
any existing email links that use that subdomain.

To keep links working, set up your own proxy pointing to Resend’s tracking DNS records before removing the domain.

### Unsupported Domains

Custom tracking subdomains require us to issue a TLS certificate. Some domains under regional restrictions are not
supported by our certificate provider and cannot use custom tracking subdomains. Learn more in the [certificate provider
docs](https://knowledge.digicert.com/solution/embargoed-countries-and-regions).
