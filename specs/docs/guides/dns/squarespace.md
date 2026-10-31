> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Squarespace

> Verify your domain on Squarespace with Resend.

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

## Log in to Squarespace

Log in to your [Squarespace domains page](https://account.squarespace.com/domains) and click on your domain.

![Domain Details](https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/squarespace-domains-main.png?fit=max\&auto=format\&n=OWNnQaVDyqcGyhhN\&q=85\&s=8362f1932f033cb983149883a9a459b6)

## Add MX SPF Record

Scroll down to the **Custom records** section and select `Add record` on Squarespace.

1. Type `send` for the `Host` of the record.
2. Set the `Type` to `MX`.
3. Set the `Priority` to `10`.
4. Use the Default 4 hours for `TTL`.
5. Copy the MX Value from Resend into the `Mail Server` field
6. Select `Save`.

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-spf-mx.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=bb0db2dd2809135194cfb62b695225cd)

![Domain Details](https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/squarespace-spf-mx.png?fit=max\&auto=format\&n=OWNnQaVDyqcGyhhN\&q=85\&s=1222dfd2f85a612e61a52f15c2ac9818)

Below is a mapping of the record fields from Resend to Squarespace:

| Squarespace | Resend | Example Value |
| - | - | - |
| Type | Type | `MX` |
| Host | Name | `send` |
| TTL | TTL | `4 hrs` (default) |
| Mail Server | Content | `feedback-smtp.us-east-1.amazonses.com` |
| Priority | Priority | `10` |

> [!NOTE]
>
> Omit your domain from the record values in Resend when you paste. Instead of
> `send.example.com`, paste only `send` (or `send.subdomain` if you're using a
> subdomain).

> [!NOTE]
>
> Do not use the same priority for multiple records. If Priority `10` is already
> in use, try a higher value `20` or `30`.

## Add TXT SPF Record

In the same **Custom records** section, select `Add Record` on Squarespace.

1. Type `send` for the `Host` of the record.
2. Set the `Type` to `TXT`.
3. Use the Default 4 hours for `TTL`.
4. Copy the TXT Value from Resend into the `Text` field
5. Select `Save`.

Add the **TXT Record** from your domain in Resend to Squarespace and click "Save".

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-spf-txt.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=747425d0a224baeee2846c9a707d5bbc)

![Domain Details](https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/squarespace-spf-txt.png?fit=max\&auto=format\&n=OWNnQaVDyqcGyhhN\&q=85\&s=13d1b0604c22b16161d1b99e9bc2f8d8)

Below is a mapping of the record fields from Resend to Squarespace:

| Squarespace | Resend | Example Value |
| - | - | - |
| Type | Type | `TXT` |
| Host | Name | `send` |
| TTL | TTL | `4 hrs` (default) |
| Text | Content | `"v=spf1 include:amazonses.com ~all"` |

> [!NOTE]
>
> Omit your domain from the record values in Resend when you paste. Instead of
> `send.example.com`, paste only `send` (or `send.subdomain` if you're using a
> subdomain).

## Add TXT DKIM Records

In the same **Custom records** section, select `Add Record` on Squarespace.

1. Type `resend._domainkey` for the `Host` of the record.
2. Set the `Type` to `TXT`.
3. Use the Default 4 hours for `TTL`.
4. Copy the TXT Value from Resend into the `Text` field
5. Select `Save`.

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-dkim.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=345d1dc6b7c138dbd92bd6928c634bd9)

![Domain Details](https://mintcdn.com/resend/OWNnQaVDyqcGyhhN/images/squarespace-dkim-txt.png?fit=max\&auto=format\&n=OWNnQaVDyqcGyhhN\&q=85\&s=119a6ade9688e65297e2dbff30e8256d)

Below is a mapping of the record fields from Resend to Squarespace:

| Squarespace | Resend | Example Value |
| - | - | - |
| Type | Type | `TXT` |
| Host | Name | `resend._domainkey` |
| TTL | TTL | `4 hrs` (default) |
| Text | Content | `p=example_domain_key_value` |

> [!NOTE]
>
> Omit your domain from the record values in Resend when you paste. Instead of
> `resend._domainkey.example.com`, paste only `resend._domainkey` (or
> `resend._domainkey.subdomain` if you're using a subdomain).

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

Scroll down to the **Custom records** section and select `Add record` on Squarespace:

1. Type `inbound` (or whatever your subdomain is) for the `Host` of the record.
2. Set the `Type` to `MX`.
3. Set the `Priority` to `10`.
4. Use the Default 4 hours for `TTL`.
5. Copy the MX Value from Resend into the `Mail Server` field.
6. Select `Save`.

Below is a mapping of the record fields from Resend to Squarespace:

| Squarespace | Resend | Example Value |
| - | - | - |
| Type | Type | `MX` |
| Host | Name | `inbound` |
| TTL | TTL | `4 hrs` (default) |
| Mail Server | Content | `inbound-smtp.us-east-1.amazonaws.com` |
| Priority | Priority | `10` |

After verifying your domain, create a webhook to process incoming emails. For help setting up a webhook, how to access email data and attachments, forward emails, and more, see [our guide on receiving emails with Resend](https://resend.com/docs/dashboard/receiving/introduction.md).

## Complete Verification

Now click [Verify DNS Records](https://resend.com/domains) on your Domain in Resend. It may take up to 72 hours to complete the verification process (often much faster).

## Troubleshooting

If your domain is not successfully verified, these are some common troubleshooting methods.

> [accordion] Resend shows my domain verification failed.
>
> Review the records you added to Squarespace to rule out copy and paste errors.

> [accordion] It has been longer than 72 hours and my domain is still Pending.
>
> [Review our guide on a domain not verifying](https://resend.com/docs/knowledge-base/what-if-my-domain-is-not-verifying.md).
