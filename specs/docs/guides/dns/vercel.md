> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Vercel

> Verify your domain on Vercel with Resend.

> [!NOTE]
>
> This guide helps you verify your domain on Vercel with Resend. We also have
> [an official integration for
> Vercel](https://resend.com/blog/vercel-integration) that helps you set up your
> API keys on Vercel projects so you can start sending emails with Resend. [View
> the integration here](https://vercel.com/resend/~/integrations/resend).

## Vercel Marketplace integration

If you installed Resend through the [Vercel Marketplace](https://vercel.com/marketplace/resend), Vercel manages the lifecycle of your Resend team, API keys, and domains. These resources cannot be deleted from the Resend dashboard, as they must uninstalled from Vercel to remove them.

## Add Domain to Resend

First, log in to your [Resend Account](https://resend.com/login) and [add a domain](https://resend.com/domains).

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-add-domain.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=418dd93c2f2ead0b0d83d1b7c2fb0970)

> [!TIP]
>
> It is [best practice to use a
> subdomain](https://resend.com/docs/dashboard/domains/introduction.md#subdomains) (updates.example.com)
> instead of the root domain (example.com). Using a subdomain allows for proper
> reputation segmentation based on topics or purpose (e.g. marketing) and is
> especially important if receiving emails with Resend.

## Automatic Setup (Recommended)

The fastest way to verify your domain on Vercel is using the **Auto Configure** button on Resend. This uses Domain Connect to automatically configure your DNS records.

1. Go to your [Domains page](https://resend.com/domains) in Resend.
2. (Optional) If you want to receive emails, select `Manual setup` and toggle the "Receiving" switch on the domain details page. ([Learn more below](#receiving-emails))
3. Click **Auto Configure**.
4. Authorize Resend to access your Vercel DNS settings.
5. The DNS records will be added automatically.

<video autoPlay loop src="https://mintcdn.com/resend/jXEQ5zNvzPmslxXc/images/vercel-domain-connect.mp4?fit=max&auto=format&n=jXEQ5zNvzPmslxXc&q=85&s=60b091caaaf0aa56f322e3a7bd5b03c1" aria-label="Vercel Domain Connect Setup" />

That's it. Your domain will be verified within a few minutes.

## Manual Setup

If you prefer to add DNS records manually, follow these steps.

### Log in to Vercel

Log in to your [Vercel account](https://vercel.com/login) and select the `Domains` tab.

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-vercel-domains.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=4b4ab73110a36775175b39587eea68f0)

## Add MX SPF Record

Copy and paste the values in Resend to Vercel.

1. Type `send` for the `Name` of the record in Vercel.
2. Expand the `Type` dropdown and select `MX`.
3. Copy the record value from Resend into the `Value` field in Vercel.
4. Add `10` for the `Priority`.
5. Select `Add`.

> [!NOTE]
>
> Omit your domain from the record values in Resend when you paste. Instead of
> `send.example.com`, paste only `send` (or `send.subdomain` if you're using a
> subdomain).

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-spf-mx.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=bb0db2dd2809135194cfb62b695225cd)

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-vercel-spf-mx.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=9d91de47106d0bd4005bac0cfe68779e)

Below is a mapping of the record fields from Resend to Vercel:

| Vercel | Resend | Example Value |
| - | - | - |
| Type | Type | `MX Record` |
| Name | Name | `send` |
| Value | Content | `feedback-smtp.us-east-1.amazonses.com` |
| TTL | TTL | `Use Vercel default (60)` |
| Priority | Priority | `10` |

> [!NOTE]
>
> Do not use the same priority for multiple records. If Priority `10` is already
> in use on another record, try a higher value `20` or `30`.

## Add TXT SPF Record

In the same section, add another record in Vercel.

1. Type `send` for the `Name` of the record.
2. Expand the `Type` dropdown and select `TXT`.
3. Copy the `TXT` record value from Resend into the `Value` field in Vercel.
4. Use the default TTL of `60`.
5. Select `Add`.

> [!NOTE]
>
> Omit your domain from the record values in Resend when you paste. Instead of
> `send.example.com`, paste only `send` (or `send.subdomain` if you're using a
> subdomain).

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-spf-txt.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=747425d0a224baeee2846c9a707d5bbc)

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-vercel-spf-txt.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=27b350fc1a7745dd47c623fdaf9a2df4)

Below is a mapping of the record fields from Resend to Vercel:

| Vercel | Resend | Example Value |
| - | - | - |
| Type | Type | `TXT Record` |
| Name | Name | `send` |
| Value | Content | `"v=spf1 include:amazonses.com ~all"` |
| TTL | TTL | `Use Vercel default (60)` |

## Add TXT DKIM Records

In the same section, add another record in Vercel.

1. Type `resend._domainkey` for the `Name` of the record.
2. Expand the `Type` dropdown and select `TXT`.
3. Copy the record value from Resend into the `Value` field in Vercel.

> [!NOTE]
>
> Omit your domain from the record values in Resend when you paste. Instead of
> `resend._domainkey.example.com`, paste only `resend._domainkey` (or
> `resend._domainkey.subdomain` if you're using a subdomain).

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-dkim.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=345d1dc6b7c138dbd92bd6928c634bd9)

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-vercel-dkim-txt.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=8553d093e572970b0335c1fe9b83e003)

Below is a mapping of the record fields from Resend to Vercel:

| Vercel | Resend | Example Value |
| - | - | - |
| Type | Type | `TXT Record` |
| Name | Name | `resend._domainkey` |
| Value | Content | `p=example_domain_key_value` |
| TTL | TTL | `Use Vercel default (60)` |

## Receiving Emails

If you want to receive emails at your domain, toggle the "Receiving" switch on the domain details page.

![Enable Receiving Emails for a verified domain](https://mintcdn.com/resend/B7wTVm7aKL5pNT-6/images/inbound-domain-toggle.png?fit=max\&auto=format\&n=B7wTVm7aKL5pNT-6\&q=85\&s=46f6b4c142fb90e04b57861e338ed2d0)

> [!WARNING]
>
> When you enable Inbound on a domain, Resend receives *all emails* sent to that
> specific domain depending on the priority of the MX record. For this reason,
> we strongly recommend verifying a subdomain (`subdomain.example.com`) instead
> of the root domain (`example.com`). Learn more about [avoiding conflicts with
> your existing MX
> records](https://resend.com/docs/knowledge-base/how-do-i-avoid-conflicting-with-my-mx-records.md).

> [!NOTE]
>
> Always copy the MX record value shown on your domain's page in Resend. The
> values in this guide are examples. Depending on your domain you will see
> `receive.forge.rmta.net`, a regional variant such as
> `receive-euw1.forge.rmta.net`, or `inbound-smtp.<region>.amazonaws.com`.

Copy and paste the values in Resend to Vercel:

1. Type `inbound` (or whatever your subdomain is) for the `Name` of the record in Vercel.
2. Expand the `Type` dropdown and select `MX`.
3. Copy the MX Value from Resend into the `Value` field in Vercel.
4. Add `10` for the `Priority`.
5. Select `Add`.

Below is a mapping of the record fields from Resend to Vercel:

| Vercel | Resend | Example Value |
| - | - | - |
| Type | Type | `MX Record` |
| Name | Name | `inbound` |
| Value | Content | `inbound-smtp.us-east-1.amazonaws.com` |
| TTL | TTL | `Use Vercel default (60)` |
| Priority | Priority | `10` |

After verifying your domain, create a webhook to process incoming emails. For help setting up a webhook, how to access email data and attachments, forward emails, and more, see [our guide on receiving emails with Resend](https://resend.com/docs/dashboard/receiving/introduction.md).

## Complete Verification

Now click [Verify DNS Records](https://resend.com/domains) on your Domain in Resend. It may take a few hours to complete the verification process (often much faster).

## Troubleshooting

If your domain is not successfully verified, these are some common troubleshooting methods.

> **Resend shows my domain verification failed.**
>
> Review the records you added to Vercel to rule out copy and paste errors.

> **It has been longer than 72 hours and my domain is still Pending.**
>
> [Review our guide on a domain not verifying](https://resend.com/docs/knowledge-base/what-if-my-domain-is-not-verifying.md).
