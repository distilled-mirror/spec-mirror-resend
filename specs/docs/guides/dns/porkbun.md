> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Porkbun

> Verify your domain on Porkbun with Resend.

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

## Log in to Porkbun

Log in to your [Porkbun account](https://porkbun.com/account/domainsSpeedy):

1. Select the `DNS` option under your domain to manage DNS records.

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-porkbun-domains.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=44389c4ae53707e508d38a34a794cec3)

## Add MX SPF Record

In the `DNS` section on Porkbun copy and paste the values MX from Resend:

1. On the `Type` page, choose `MX`.
2. Type `send` for the `Host` of the record.
3. Copy the MX Value from Resend into the `Answer / Value` field.
4. Use the default TTL of `600`.
5. In the `Priority` field enter `10`.
6. Select `Add`.

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-spf-mx.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=bb0db2dd2809135194cfb62b695225cd)

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-porkbun-spf-mx.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=65428888fca00600f2bdf31d14db8eaf)

Below is a mapping of the record fields from Resend to Porkbun:

| Porkbun | Resend | Example Value |
| - | - | - |
| Type | Type | `MX Record` |
| Host | Name | `send` |
| Answer / Value | Content | `feedback-smtp.us-east-1.amazonses.com` |
| TTL | TTL | `600` |
| Priority | Priority | `10` |

> [!NOTE]
>
> Do not use the same priority for multiple records. If Priority `10` is already
> in use on another record, try a higher value `20` or `30`.

## Add TXT SPF Record

On the same section:

1. On the `Type` page, choose `TXT`.
2. Type `send` for the `Host` of the record.
3. Copy the TXT Value Resend into the `Answer / Value` field.
4. Use the default TTL of `600`.
5. Select `Add Record`.

> [!NOTE]
>
> Omit your domain from the record values in Resend when you paste. Instead of
> `send.example.com`, paste only `send` (or `send.subdomain` if you're using a
> subdomain).

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-spf-txt.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=747425d0a224baeee2846c9a707d5bbc)

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-porkbun-spf-txt.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=7ef4c8c51fd01d854c6404b96b2a1a27)

Below is a mapping of the record fields from Resend to Porkbun:

| Porkbun | Resend | Example Value |
| - | - | - |
| Type | Type | `TXT Record` |
| Host | Name | `send` |
| Answer / Value | Content | `"v=spf1 include:amazonses.com ~all"` |
| TTL | TTL | `600` |

## Add TXT DKIM Records

On the same `Create Record` section:

1. On the `Type` page, choose `TXT`.
2. Type `resend._domainkey` for the `Host` of the record.
3. Copy the TXT Value Resend into the `Answer / Value` field.
4. Use the default TTL of `600`.
5. Select `Add Record`.

> [!NOTE]
>
> Omit your domain from the record values in Resend when you paste. Instead of
> `resend._domainkey.example.com`, paste only `resend._domainkey` (or
> `resend._domainkey.subdomain` if you're using a subdomain).

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-dkim.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=345d1dc6b7c138dbd92bd6928c634bd9)

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-porkbun-dkim-txt.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=9f3a33882f02d34489d5adc55f28c7b8)

Below is a mapping of the record fields from Resend to Porkbun:

| Porkbun | Resend | Example Value |
| - | - | - |
| Type | Type | `TXT Record` |
| Host | Name | `send` |
| Answer / Value | Content | `p=example_domain_key_value` |
| TTL | TTL | `600` |

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

In the `DNS` section on Porkbun:

1. On the `Type` page, choose `MX`.
2. Type `inbound` (or whatever your subdomain is) for the `Host` of the record.
3. Copy the MX Value from Resend into the `Answer / Value` field.
4. Use the default TTL of `600`.
5. In the `Priority` field enter `10`.
6. Select `Add`.

Below is a mapping of the record fields from Resend to Porkbun:

| Porkbun | Resend | Example Value |
| - | - | - |
| Type | Type | `MX Record` |
| Host | Name | `inbound` |
| Answer / Value | Content | `inbound-smtp.us-east-1.amazonaws.com` |
| TTL | TTL | `600` |
| Priority | Priority | `10` |

After verifying your domain, create a webhook to process incoming emails. For help setting up a webhook, how to access email data and attachments, forward emails, and more, see [our guide on receiving emails with Resend](https://resend.com/docs/dashboard/receiving/introduction.md).

## Complete Verification

Now click [Verify DNS Records](https://resend.com/domains) on your Domain in Resend. It may take a few hours to complete the verification process (often much faster).

## Troubleshooting

If your domain is not successfully verified, these are some common troubleshooting methods.

> [accordion] Resend shows my domain verification failed.
>
> Review the records you added to Porkbun to rule out copy and paste errors.

> [accordion] It has been longer than 72 hours and my domain is still Pending.
>
> [Review our guide on a domain not verifying](https://resend.com/docs/knowledge-base/what-if-my-domain-is-not-verifying.md).
