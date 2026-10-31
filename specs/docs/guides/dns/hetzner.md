> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Hetzner

> Verify your domain on Hetzner with Resend.

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

## Log in to Hetzner Console

This section covers accessing the new Hetzner Console for managing DNS records. If your domain is still using the legacy Hetzner DNS console, please skip to the [Log in to Hetzner DNS Console](#log-in-to-hetzner-dns-console) section below.

Log in to [Hetzner Console](https://console.hetzner.com/):

1. Choose your project from the `Projects` list.
2. Click on the `DNS` link from the `Networking` section of the side navigation.
3. Choose your Domain from the `DNS zones` list.

![Domain Details](https://mintcdn.com/resend/JnEHZ2RkJvy-KeG2/images/dashboard-domains-Hetzner-console-dns.png?fit=max\&auto=format\&n=JnEHZ2RkJvy-KeG2\&q=85\&s=b8f96a05c8b1115639ba85ce616716ec)

## Log in to Hetzner DNS Console

This section covers accessing the legacy Hetzner DNS Console. Hetzner recently created the new Hetzner Console for managing DNS records. If your domain is using the new Hetzner console, please go to the [Log in to Hetzner Console](#log-in-to-hetzner-console) section above then skip to the [Add MX SPF Record](#add-mx-spf-record) section.

Log in to [Hetzner DNS Console](https://dns.hetzner.com):

1. Choose your Domain from the `Your Zones` list.
2. Select the `Records` tab to get to the page to manage DNS records.

![Domain Details](https://mintcdn.com/resend/JnEHZ2RkJvy-KeG2/images/dashboard-domains-Hetzner-dns-console-domains.png?fit=max\&auto=format\&n=JnEHZ2RkJvy-KeG2\&q=85\&s=491d0aab1c3722d47159c8e42fe880ba)

## Add MX SPF Record

In the `Add Record` section on Hetzner copy and paste the values MX from Resend:

1. For the `Type` field, choose `MX`.
2. For the `Name` field, type `send` (or `send.subdomain` if you're using a subdomain).
3. For the `Priority` field, set the value to `10`.
4. For the `Value` field, add the MX SPF Record `Content` from Resend.
5. For the `TTL` field, set the value to `1800`.
6. Select `Add`.

> [!NOTE]
>
> Hetzner requires your MX record to have a trailing period when adding. Resend
> will include the trailing period when copying. Removing the period will cause
> the verification to fail.

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-spf-mx.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=bb0db2dd2809135194cfb62b695225cd)

![Domain Details](https://mintcdn.com/resend/JnEHZ2RkJvy-KeG2/images/dashboard-domains-Hetzner-console-spf-mx.png?fit=max\&auto=format\&n=JnEHZ2RkJvy-KeG2\&q=85\&s=29ce3bf6e50439348e0d3bf2f90110de)

Below is a mapping of the record fields from Resend to Hetzner Console:

| Hetzner | Resend | Example Value |
| - | - | - |
| Type | Type | `MX Record` |
| Name | Name | `send.subdomain` |
| Value | Content | `feedback-smtp.us-east-1.amazonses.com.` |
| TTL | TTL | `1800` |
| Priority | Priority | `10` |

> [!NOTE]
>
> Do not use the same priority for multiple records. If Priority `10` is already
> in use on another record, try a higher value `20` or `30`.

## Add TXT SPF Record

On the same `Add Record` section:

1. For the `Type` field, choose `TXT`.
2. For the `Name` field, type `send` (or `send.subdomain` if you're using a subdomain).
3. For the `Value` field, add the TXT SPF Record `Content` from Resend.
4. For the `TTL` field, set the value to `1800`.
5. Select `Add`.

> [!NOTE]
>
> Omit your domain from the record values in Resend when you paste. Instead of
> `send.example.com`, paste only `send` (or `send.subdomain` if you're using a
> subdomain).

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-spf-txt.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=747425d0a224baeee2846c9a707d5bbc)

![Domain Details](https://mintcdn.com/resend/JnEHZ2RkJvy-KeG2/images/dashboard-domains-Hetzner-console-spf-txt.png?fit=max\&auto=format\&n=JnEHZ2RkJvy-KeG2\&q=85\&s=9cfd4af1fd47c8bf7f0e80bd2c846497)

Below is a mapping of the record fields from Resend to Hetzner:

| Hetzner | Resend | Example Value |
| - | - | - |
| Type | Type | `TXT Record` |
| Name | Name | `send.subdomain` |
| Value | Content | `"v=spf1 include:amazonses.com ~all"` |
| TTL | TTL | `10800` |

## Add TXT DKIM Records

On the same `Add Record` section:

1. For the `Type` field, choose `TXT`.
2. For the `Name` field, type `resend._domainkey` (or `resend._domainkey.subdomain` if you're using a subdomain).
3. For the `Value` field, add the TXT DKIM Record `Content` from Resend.
4. For the `TTL` field, set the value to `1800`.
5. Select `Add`.

> [!NOTE]
>
> Omit your domain from the record values in Resend when you paste. Instead of
> `resend._domainkey.example.com`, paste only `resend._domainkey` (or
> `resend._domainkey.subdomain` if you're using a subdomain).

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-dkim.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=345d1dc6b7c138dbd92bd6928c634bd9)

![Domain Details](https://mintcdn.com/resend/JnEHZ2RkJvy-KeG2/images/dashboard-domains-Hetzner-console-dkim-txt.png?fit=max\&auto=format\&n=JnEHZ2RkJvy-KeG2\&q=85\&s=96d275fc831f3bfde0aec1c9b5325385)

Below is a mapping of the record fields from Resend to Hetzner:

| Hetzner | Resend | Example Value |
| - | - | - |
| Type | Type | `TXT Record` |
| Name | Name | `send.subdomain` |
| Value | Content | `p=example_domain_key_value` |
| TTL | TTL | `1 hour` |

## Receiving Emails

If you want to receive emails at your domain, toggle the "Receiving" switch on the domain details page.

![Enable Receiving Emails for a verified domain](https://mintcdn.com/resend/B7wTVm7aKL5pNT-6/images/inbound-domain-toggle.png?fit=max\&auto=format\&n=B7wTVm7aKL5pNT-6\&q=85\&s=46f6b4c142fb90e04b57861e338ed2d0)

![Domain Details](https://mintcdn.com/resend/JnEHZ2RkJvy-KeG2/images/dashboard-domains-Hetzner-console-inbound-mx.png?fit=max\&auto=format\&n=JnEHZ2RkJvy-KeG2\&q=85\&s=b292bfefc0c463ebe78e0f77fb283263)

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

In the `Add Record` section on Hetzner:

1. For the `Type` field, choose `MX`.
2. For the `Name` field, type `@` for the base domain or the name of the subdomain if you're using a subdomain.
3. For the `Priority` field, set the value to `10`.
4. For the `Value` field, add the Receiving MX Record `Content` from Resend.
5. For the `TTL` field, set the value to `1800`.
6. Select `Add`.

Below is a mapping of the record fields from Resend to Hetzner:

| Hetzner | Resend | Example Value |
| - | - | - |
| Type | Type | `MX Record` |
| Name | Name | `subdomain` |
| Mail server | Content | `inbound-smtp.us-east-1.amazonaws.com.` |
| TTL | TTL | `1800` |
| Priority | Priority | `10` |

After verifying your domain, create a webhook to process incoming emails. For help setting up a webhook, how to access email data and attachments, forward emails, and more, see [our guide on receiving emails with Resend](https://resend.com/docs/dashboard/receiving/introduction.md).

## Complete Verification

Now click [Verify DNS Records](https://resend.com/domains) on your Domain in Resend. It may take a few hours to complete the verification process (often much faster).

## Troubleshooting

If your domain is not successfully verified, these are some common troubleshooting methods.

> [accordion] Resend shows my domain verification failed.
>
> Review the records you added to Hetzner to rule out copy and paste errors.

> [accordion] It has been longer than 72 hours and my domain is still Pending.
>
> [Review our guide on a domain not verifying](https://resend.com/docs/knowledge-base/what-if-my-domain-is-not-verifying.md).
