> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Verified Domains

> An introduction to verified domains in Resend.

## Verified domains

Resend sends emails using a domain you own (i.e., not a shared or public domain). You must [add and verify at least one domain](/docs/add-a-domain) to send emails with Resend. You can optionally [configure your domain to receive emails](/docs/dashboard/receiving/custom-domains).

## Domain features

When you add a domain, you can choose to:

* Add a [subdomain](#subdomains) instead of your root domain to communicate the kind of emails you send and receive, and for proper reputation segmentation.
* Enable [open and click tracking](/docs/dashboard/domains/tracking) for your emails.
* Configure [Enforced Transport Layer Security (TLS)](/docs/dashboard/domains/tls) to ensure that you only send encrypted emails.
* Set a custom subdomain for the [Return-Path address](/docs/dashboard/domains/custom-return-path).
* Choose which [geographical region](/docs/dashboard/domains/regions) to send emails from to reach your recipients sooner.

After your domain is verified, you can:

* Send and receive emails [using any email address at your domain](/docs/knowledge-base/how-do-I-create-an-email-address-or-sender-in-resend#sender-email-addresses-in-resend) without any extra configuration.
* Implement [DMARC](/docs/dashboard/domains/dmarc) and [BIMI](/docs/dashboard/domains/bimi) to build trust and improve inbox placement.

## Subdomains

We recommend sending your emails from one or more subdomains (e.g., `updates.example.com`) instead of your root domain to isolate your sending reputation and to clearly communicate your intent to your recipients.

You can [add and verify](/docs/add-a-domain) multiple subdomains of the same domain (e.g. `newsletter.example.com` and `account.example.com`) for different sending purposes.

For example, you can configure your newsletter for open and click tracking while keeping tracking disabled for your important transactional emails such as password resets.

Learn more about [the benefits of sending emails from a subdomain](/docs/knowledge-base/is-it-better-to-send-emails-from-a-subdomain-or-the-root-domain).

## Domain management

You can view and manage your domains from the [Domains Dashboard page](https://resend.com/domains). The Dashboard allows all members of your team to create, verify, retrieve, update, and delete your domains.

You can also manage your sending and receiving domains using the [API](/docs/api-reference/domains/create-domain), the [CLI](/docs/cli#domains), or the [MCP server](/docs/mcp-server).

Learn more about [managing your domains](/docs/dashboard/domains/manage-domains).

## Related Guides

See how to use Resend's verified domain features.

<CardGroup cols={2}>
  <Card title="Manage domains" icon="gear" href="/docs/dashboard/domains/manage-domains" />

  <Card title="Implement DMARC" icon="key" href="/docs/dashboard/domains/dmarc" />

  <Card title="Enable Tracking" icon="chart-line-up-down" href="/docs/dashboard/domains/tracking" />

  <Card title="Enforced TLS" icon="binary-lock" href="/docs/dashboard/domains/tls" />

  <Card title="Custom return path" icon="code-simple" href="/docs/dashboard/domains/custom-return-path" />

  <Card title="Choose region" icon="globe" href="/docs/dashboard/domains/regions" />

  <Card title="Claim a domain" icon="bell-concierge" href="/docs/dashboard/domains/claim" />

  <Card title="DNS provider guides" icon="book-atlas" href="/docs/knowledge-base/cloudflare" />
</CardGroup>
