> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Verified Domains

> An introduction to verified domains in Resend.

## Verified domains

Resend sends emails using a domain you own (i.e., not a shared or public domain). You must [add and verify at least one domain](/docs/add-a-domain.md) to send emails with Resend. You can optionally [configure your domain to receive emails](/docs/dashboard/receiving/custom-domains.md).

## Domain features

When you add a domain, you can choose to:

* Add a [subdomain](#subdomains) instead of your root domain to communicate the kind of emails you send and receive, and for proper reputation segmentation.
* Enable [open and click tracking](/docs/dashboard/domains/tracking.md) for your emails.
* Configure [Enforced Transport Layer Security (TLS)](/docs/dashboard/domains/tls.md) to ensure that you only send encrypted emails.
* Set a custom subdomain for the [Return-Path address](/docs/dashboard/domains/custom-return-path.md).
* Choose which [geographical region](/docs/dashboard/domains/regions.md) to send emails from to reach your recipients sooner.

After your domain is verified, you can:

* Send and receive emails [using any email address at your domain](/docs/knowledge-base/how-do-I-create-an-email-address-or-sender-in-resend.md#sender-email-addresses-in-resend) without any extra configuration.
* Implement [DMARC](/docs/dashboard/domains/dmarc.md) and [BIMI](/docs/dashboard/domains/bimi.md) to build trust and improve inbox placement.

## Subdomains

We recommend sending your emails from one or more subdomains (e.g., `updates.example.com`) instead of your root domain to isolate your sending reputation and to clearly communicate your intent to your recipients.

You can [add and verify](/docs/add-a-domain.md) multiple subdomains of the same domain (e.g. `newsletter.example.com` and `account.example.com`) for different sending purposes.

For example, you can configure your newsletter for open and click tracking while keeping tracking disabled for your important transactional emails such as password resets.

Learn more about [the benefits of sending emails from a subdomain](/docs/knowledge-base/is-it-better-to-send-emails-from-a-subdomain-or-the-root-domain.md).

## Domain management

You can view and manage your domains from the [Domains Dashboard page](https://resend.com/domains). The Dashboard allows all members of your team to create, verify, retrieve, update, and delete your domains.

You can also manage your sending and receiving domains using the [API](/docs/api-reference/domains/create-domain.md), the [CLI](/docs/cli.md#domains), or the [MCP server](/docs/mcp-server.md).

Learn more about [managing your domains](/docs/dashboard/domains/manage-domains.md).

## Related Guides

See how to use Resend's verified domain features.

> **[Manage domains](/docs/dashboard/domains/manage-domains.md)**

> **[Implement DMARC](/docs/dashboard/domains/dmarc.md)**

> **[Enable Tracking](/docs/dashboard/domains/tracking.md)**

> **[Enforced TLS](/docs/dashboard/domains/tls.md)**

> **[Custom return path](/docs/dashboard/domains/custom-return-path.md)**

> **[Choose region](/docs/dashboard/domains/regions.md)**

> **[Claim a domain](/docs/dashboard/domains/claim.md)**

> **[DNS provider guides](/docs/knowledge-base/introduction.md#dns-guides)**
