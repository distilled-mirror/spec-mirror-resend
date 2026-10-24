> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Add and verify a domain

> Get started sending emails by adding a domain to your account.

Resend sends emails using a domain you own. Before you can send or receive emails with Resend, you must have a verified domain associated with your account.

> [!NOTE]
>
> If you don't own a domain, please purchase one from a domain registrar such as
> [Cloudflare](https://www.cloudflare.com/) or
> [Namecheap](https://www.namecheap.com/) before continuing.

## Add a domain

You can add and verify a domain you own in four ways:

* in the [**Domains** Dashboard page](https://resend.com/docs/dashboard/domains/introduction.md)
* using the [Resend API](https://resend.com/docs/api-reference/domains/create-domain.md)
* with a [Resend CLI command](https://resend.com/docs/cli.md#domains)
* with the [Resend MCP server](https://resend.com/docs/mcp-server.md)

To add a new domain from the Resend Dashboard:

**1. In your Resend Dashboard, navigate to the Domains page.**

**2. Click the Add Domain button.**

**3. Enter a domain including a subdomain to use for your Resend emails.**

We strongly recommend sending emails from a subdomain (e.g., `notifications.example.com`) instead of your root domain (`example.com`) to conform to deliverability best practices.

Choose a subdomain that reflects the purpose of your emails, such as `customers.example.com` or `updates.example.com`.

You can have multiple subdomains associated with your root domain. But, each one must be configured and verified individually.

If you add a domain already used by another team, the dashboard will notify you and you can [claim the domain](https://resend.com/docs/dashboard/domains/claim.md) to transfer it to your team.

**4. Choose a region from the list provided.**

Select a region to send your emails from. Choose one that is closest to the majority of your recipients.

**5. (optional) Enter a custom subdomain for the Return-Path address if desired.**

Return-Path defaults to `send.example.com`, although you can [provide a custom path](https://resend.com/docs/dashboard/domains/custom-return-path.md).

**6. Update your DNS records with values provided by Resend.**

View the **Records** tab for your domain to find the records to provide to your DNS host provider. Adding these records will verify that you own the domain and have the correct permissions to send and receive emails.

Provide the DKIM and SPF configurations (`TXT` and `MX` or `CNAME` records) to your DNS provider. These records must match exactly what Resend generated. Copy and paste the records to avoid configuration errors.

> [!TIP]
>
> Consult one of our [DNS provider guides](https://resend.com/docs/knowledge-base/introduction.md) for specific examples of updating your DNS records with your host. Also, when shown a CNAME, make sure *not* to use proxying features (e.g., Cloudflare's orange cloud) for that record, as it will prevent verification from completing.

**7. Wait for DNS verification to complete**

When this process is completed correctly, your domain will often verify within 15 minutes of adding the DNS records. However, DNS changes can occasionally take up to 72 hours to propagate globally.

You can use Resend's [dns.email tool](https://dns.email/) to check that your records are visible publicly. If verification has not completed after 72 hours, use the “Restart verification” button in the Resend dashboard to trigger a fresh verification check.

**8. Add a DMARC record.**

After your domain is verified, you can then [implement DMARC](https://resend.com/docs/dashboard/domains/dmarc.md) to build additional trust in your domain and protect against email spoofing.

This is an email authentication protocol to verify email senders and to allow receivers to reject unauthenticated messages, and is important for email deliverability.

**9. (optional) Update your domain's Resend configuration options.**

After your domain is verified, you may wish to [enable open and click tracking](https://resend.com/docs/dashboard/domains/tracking.md) or [enforce Transport Layer Security (TLS)](https://resend.com/docs/dashboard/domains/tls.md).

## Learn more

> **[Manage domains](https://resend.com/docs/dashboard/domains/introduction.md)**
>
> View, create, edit, delete, and manage your domains.

> **[Multi-tenant domain setup](https://resend.com/docs/knowledge-base/setting-up-resend-for-multi-tenants.md)**
>
> Learn how to configure Resend for SaaS platforms where tenants send emails
> from their own domains.

## Next steps

> **[Add a DMARC record](https://resend.com/docs/dashboard/domains/dmarc.md)**
>
> Implement DMARC to build trust in your domain and protect against email
> spoofing.

> **[Quickstart tutorials](https://resend.com/docs/introduction.md)**
>
> Send your first transactional email with a quick tutorial for your language
> or framework.
