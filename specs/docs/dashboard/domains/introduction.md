> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Verified Domains

> An introduction to verified domains in Resend.

## Verified domains

Resend sends emails using a domain you own (i.e., not a shared or public domain). You must [add and verify at least one domain](https://resend.com/docs/add-a-domain.md) to send emails with Resend. You can optionally [configure your domain to receive emails](https://resend.com/docs/dashboard/receiving/custom-domains.md).

You can add and verify multiple [subdomains](#subdomains) from the same root domain (e.g., `newsletter.example.com` and `account.example.com`) to identify different sending purposes and still assure recipients and inbox providers that the emails come from you. This can protect the sending reputation of your transactional emails from any negative recipient response to your marketing emails, and allows you to configure different domain settings such as open and click tracking for each subdomain.

## Domain features

When you add a domain, you can choose to:

* Enable [open and click tracking](https://resend.com/docs/dashboard/domains/tracking.md) for your emails.
* Configure [Enforced Transport Layer Security (TLS)](https://resend.com/docs/dashboard/domains/tls.md) to ensure that you only send encrypted emails.
* Set a custom subdomain for the [Return-Path address](https://resend.com/docs/dashboard/domains/custom-return-path.md).
* Choose which [geographical region](https://resend.com/docs/dashboard/domains/regions.md) to send emails from to reach your recipients sooner.

After your domain is verified, you can:

* Send and receive emails [using any email address at your domain](https://resend.com/docs/knowledge-base/how-do-I-create-an-email-address-or-sender-in-resend.md#sender-email-addresses-in-resend) without any extra configuration.
* Implement [DMARC](https://resend.com/docs/dashboard/domains/dmarc.md) and [BIMI](https://resend.com/docs/dashboard/domains/bimi.md) to build trust and improve inbox placement.

## Subdomains

We recommend sending your emails from one or more subdomains (e.g., `updates.example.com`) instead of your root domain to isolate your sending reputation and to clearly communicate your intent to your recipients.

You must [add each subdomain](https://resend.com/docs/add-a-domain.md) individually, and they will be displayed in the [**Domains** Dashboard page](https://resend.com/domains) as separate entries where you can manage and configure them independently.

There are several benefits to sending from a subdomain:

* **Sender intent:** clearly communicate your intent to your recipients, increasing trust through transparency.
* **Reputation control:** Using separate subdomains can help segment sending reputation.
* **Configuration settings**: [Enabling open and click tracking](https://resend.com/docs/dashboard/domains/tracking.md) for your marketing emails, while keeping it disabled for your important transactional emails such as password resets.

Subdomains of your main domain also help reinforce your brand identity and build trust with inbox providers.

Domains that look like your main brand but aren’t actually your main brand (e.g., `example-alerts.com` instead of `alerts.example.com`) can appear suspicious to spam filters and confusing to your recipients. Inbox providers may flag them as phishing or spoofing attempts, and your users are more likely to ignore, delete, or even report the emails as spam.

## Domain management

You can view and manage your domains from the [Domains Dashboard page](https://resend.com/domains). The Dashboard allows all members of your team to create, verify, retrieve, update, and delete your domains.

You can also manage your sending and receiving domains using the [API](https://resend.com/docs/api-reference/domains/create-domain.md), the [CLI](https://resend.com/docs/cli.md#domains), or the [MCP server](https://resend.com/docs/mcp-server.md).

Learn more about [managing your domains](https://resend.com/docs/dashboard/domains/manage-domains.md).

## Related Guides

See how to use Resend's verified domain features.

> **[Manage domains](https://resend.com/docs/dashboard/domains/manage-domains.md)**

> **[Implement DMARC](https://resend.com/docs/dashboard/domains/dmarc.md)**

> **[Enable Tracking](https://resend.com/docs/dashboard/domains/tracking.md)**

> **[Enforced TLS](https://resend.com/docs/dashboard/domains/tls.md)**

> **[Custom return path](https://resend.com/docs/dashboard/domains/custom-return-path.md)**

> **[Choose region](https://resend.com/docs/dashboard/domains/regions.md)**

> **[Claim a domain](https://resend.com/docs/dashboard/domains/claim.md)**

> **[DNS provider guides](https://resend.com/docs/knowledge-base/introduction.md#dns-guides)**
