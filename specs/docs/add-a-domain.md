> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Add and verify a domain

> Get started sending emails by adding a domain to your account.

Resend sends emails using a domain you own. Before you can send or receive emails with Resend, you must have a verified domain associated with your account.

<Info>
  If you don't own a domain, please purchase one from a domain registrar such as
  [Cloudflare](https://www.cloudflare.com/) or
  [Namecheap](https://www.namecheap.com/) before continuing.
</Info>

## Add a domain

You can add and verify a domain you own in four ways:

* in the [**Domains** Dashboard page](/docs/dashboard/domains/introduction)
* using the [Resend API](/docs/api-reference/domains/create-domain)
* with a [Resend CLI command](/docs/cli#domains)
* with the [Resend MCP server](/docs/mcp-server)

To add a new domain from the Resend Dashboard:

<Steps>
  <Step title="In your Resend Dashboard, navigate to the Domains page." />

  <Step title="Click the Add Domain button." />

  <Step title="Enter a domain including a subdomain to use for your Resend emails.">
    We strongly recommend sending emails from a subdomain (e.g., `notifications.example.com`) instead of your root domain (`example.com`) to conform to deliverability best practices.

    Choose a subdomain that reflects the purpose of your emails, such as `customers.example.com` or `updates.example.com`.

    You can have multiple subdomains associated with your root domain. But, each one must be configured and verified individually.

    If you add a domain already used by another team, the dashboard will notify you and you can [claim the domain](/docs/dashboard/domains/claim) to transfer it to your team.
  </Step>

  <Step title="Choose a region from the list provided.">
    Select a region to send your emails from. Choose one that is closest to the majority of your recipients.
  </Step>

  <Step title="(optional) Enter a custom subdomain for the Return-Path address if desired.">
    Return-Path defaults to `send.example.com`, although you can [provide a custom path](/docs/dashboard/domains/custom-return-path).
  </Step>

  <Step title="Update your DNS records with values provided by Resend.">
    View the **Records** tab for your domain to find the records to provide to your DNS host provider. Adding these records will verify that you own the domain and have the correct permissions to send and receive emails.

    Provide the DKIM and SPF configurations (`TXT` and `MX` or `CNAME` records) to your DNS provider. These records must match exactly what Resend generated. Copy and paste the records to avoid configuration errors.

    <Tip>
      Consult one of our [DNS provider guides](/docs/knowledge-base/introduction) for specific examples of updating your DNS records with your host. Also, when shown a CNAME, make sure *not* to use proxying features (e.g., Cloudflare's orange cloud) for that record, as it will prevent verification from completing.
    </Tip>
  </Step>

  <Step title="Wait for DNS verification to complete">
    When this process is completed correctly, your domain will often verify within 15 minutes of adding the DNS records. However, DNS changes can occasionally take up to 72 hours to propagate globally.

    You can use Resend's [dns.email tool](https://dns.email/) to check that your records are visible publicly. If verification has not completed after 72 hours, use the “Restart verification” button in the Resend dashboard to trigger a fresh verification check.
  </Step>

  <Step title="Add a DMARC record.">
    After your domain is verified, you can then [implement DMARC](/docs/dashboard/domains/dmarc) to build additional trust in your domain and protect against email spoofing.

    This is an email authentication protocol to verify email senders and to allow receivers to reject unauthenticated messages, and is important for email deliverability.
  </Step>

  <Step title="(optional) Update your domain's Resend configuration options.">
    After your domain is verified, you may wish to [enable open and click tracking](/docs/dashboard/domains/tracking) or [enforce Transport Layer Security (TLS)](/docs/dashboard/domains/tls).
  </Step>
</Steps>

## Learn more

<CardGroup cols={2}>
  <Card title="Manage domains" icon="tools" href="/docs/dashboard/domains/introduction">
    View, create, edit, delete, and manage your domains.
  </Card>

  <Card title="Multi-tenant domain setup" icon="people-group" href="/docs/knowledge-base/setting-up-resend-for-multi-tenants">
    Learn how to configure Resend for SaaS platforms where tenants send emails
    from their own domains.
  </Card>
</CardGroup>

## Next steps

<CardGroup cols={2}>
  <Card title="Add a DMARC record" icon="globe" href="/docs/dashboard/domains/dmarc">
    Implement DMARC to build trust in your domain and protect against email
    spoofing.
  </Card>

  <Card title="Quickstart tutorials" icon="stopwatch" href="/docs/introduction">
    Send your first transactional email with a quick tutorial for your language
    or framework.
  </Card>
</CardGroup>
