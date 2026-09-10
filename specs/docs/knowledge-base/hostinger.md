> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Hostinger

> Verify your domain on Hostinger with Resend.

## Add Domain to Resend

First, log in to your [Resend Account](https://resend.com/login) and [add a domain](https://resend.com/domains).

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-add-domain.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=418dd93c2f2ead0b0d83d1b7c2fb0970" width="3360" height="2100" data-path="images/dashboard-domains-resend-add-domain.png" />

<Tip>
  It is [best practice to use a
  subdomain](/docs/knowledge-base/is-it-better-to-send-emails-from-a-subdomain-or-the-root-domain)
  (updates.example.com) instead of the root domain (example.com). Using a
  subdomain allows for proper reputation segmentation based on topics or purpose
  (e.g. marketing) and is especially important if receiving emails with Resend.
</Tip>

## Log in to Hostinger

Log in to your [Hostinger account](https://auth.hostinger.com/login):

1. Select the `Domains` tab
2. Choose your Domain from the `Domain portfolio` list.
3. Select the `DNS / Nameservers` to get to the page to manage DNS records.

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-hostinger-domains.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=d7fcfa6f62bc4c8eb8c7eccbc12068c3" width="2983" height="1848" data-path="images/dashboard-domains-hostinger-domains.png" />

## Add MX SPF Record

Copy and paste the values MX in Resend to Hostinger.

1. Set the Type to `MX`.
2. Type `send` for the `Name` of the record.
3. Copy the MX Value from Resend into the `Mail Server` field.
4. Add `10` for the `Priority`.
5. Set the TTL to `3600`.
6. Select `Add Record`.

<Info>
  Omit your domain from the record values in Resend when you paste. Instead of
  `send.example.com`, paste only `send` (or `send.subdomain` if you're using a
  subdomain).
</Info>

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-spf-mx.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=bb0db2dd2809135194cfb62b695225cd" width="3024" height="1888" data-path="images/dashboard-domains-resend-spf-mx.png" />

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-hostinger-spf-mx.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=d9600d2ba927c8ee8a3222139280d396" width="2984" height="1849" data-path="images/dashboard-domains-hostinger-spf-mx.png" />

Below is a mapping of the record fields from Resend to Hostinger:

| Hostinger   | Resend   | Example Value                           |
| ----------- | -------- | --------------------------------------- |
| Type        | Type     | `MX Record`                             |
| Name        | Name     | `send`                                  |
| Mail Server | Content  | `feedback-smtp.us-east-1.amazonses.com` |
| TTL         | -        | `Set to 3660`                           |
| Priority    | Priority | `10`                                    |

<Info>
  Do not use the same priority for multiple records. If Priority `10` is already
  in use on another record, try a higher value `20` or `30`.
</Info>

## Add TXT SPF Record

In the same section, add another record in Hostinger.

1. Set the Type to `TXT`.
2. Type `send` for the `Name` of the record.
3. Copy the TXT Value Resend into the `TXT value` field.
4. Set the TTL to `3600`.
5. Select `Add Record`.

<Info>
  Omit your domain from the record values in Resend when you paste. Instead of
  `send.example.com`, paste only `send` (or `send.subdomain` if you're using a
  subdomain).
</Info>

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-spf-txt.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=747425d0a224baeee2846c9a707d5bbc" width="3024" height="1888" data-path="images/dashboard-domains-resend-spf-txt.png" />

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-hostinger-spf-txt.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=8854129a0f11574f79016d5ad56a0ed2" width="2985" height="1848" data-path="images/dashboard-domains-hostinger-spf-txt.png" />

Below is a mapping of the record fields from Resend to Hostinger:

| Hostinger | Resend  | Example Value                         |
| --------- | ------- | ------------------------------------- |
| Type      | Type    | `TXT Record`                          |
| Name      | Name    | `send`                                |
| TXT value | Content | `"v=spf1 include:amazonses.com ~all"` |
| TTL       | -       | `Set to 3600`                         |

## Add TXT DKIM Records

In the same section, add another record in Hostinger.

1. Set the Type to `TXT`.
2. Type `resend._domainkey` for the `Name` of the record.
3. Copy the record value from Resend into the `TXT value` field.
4. Set the TTL to `3600`.
5. Select `Add Record`.

<Info>
  Omit your domain from the record values in Resend when you paste. Instead of
  `resend._domainkey.example.com`, paste only `resend._domainkey` (or
  `resend._domainkey.subdomain` if you're using a subdomain).
</Info>

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-dkim.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=345d1dc6b7c138dbd92bd6928c634bd9" width="2992" height="1868" data-path="images/dashboard-domains-resend-dkim.png" />

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-hostinger-dkim-txt.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=31350bb523d1959c348a0fde5f8d5734" width="2984" height="1848" data-path="images/dashboard-domains-hostinger-dkim-txt.png" />

Below is a mapping of the record fields from Resend to Hostinger:

| Hostinger | Resend  | Example Value                |
| --------- | ------- | ---------------------------- |
| Type      | Type    | `TXT Record`                 |
| Name      | Name    | `send`                       |
| TXT value | Content | `p=example_domain_key_value` |
| TTL       | -       | `Set to 3600`                |

## Receiving Emails

If you want to receive emails at your domain, toggle the "Receiving" switch on the domain details page.

<img alt="Enable Receiving Emails for a verified domain" src="https://mintcdn.com/resend/B7wTVm7aKL5pNT-6/images/inbound-domain-toggle.png?fit=max&auto=format&n=B7wTVm7aKL5pNT-6&q=85&s=46f6b4c142fb90e04b57861e338ed2d0" width="1980" height="1244" data-path="images/inbound-domain-toggle.png" />

<Warning>
  When you enable Inbound on a domain, Resend receives *all emails* sent to that
  specific domain depending on the priority of the MX record. For this reason,
  we strongly recommend verifying a subdomain (`subdomain.example.com`) instead
  of the root domain (`example.com`). Learn more about [avoiding conflicts with
  your existing MX
  records](/docs/knowledge-base/how-do-i-avoid-conflicting-with-my-mx-records).
</Warning>

Copy and paste the values MX in Resend to Hostinger:

1. Set the Type to `MX`.
2. Type `inbound` (or whatever your subdomain is) for the `Name` of the record.
3. Copy the MX Value from Resend into the `Mail Server` field.
4. Add `10` for the `Priority`.
5. Set the TTL to `3600`.
6. Select `Add Record`.

Below is a mapping of the record fields from Resend to Hostinger:

| Hostinger   | Resend   | Example Value                          |
| ----------- | -------- | -------------------------------------- |
| Type        | Type     | `MX Record`                            |
| Name        | Name     | `inbound`                              |
| Mail Server | Content  | `inbound-smtp.us-east-1.amazonaws.com` |
| TTL         | -        | `Set to 3660`                          |
| Priority    | Priority | `10`                                   |

After verifying your domain, create a webhook to process incoming emails. For help setting up a webhook, how to access email data and attachments, forward emails, and more, see [our guide on receiving emails with Resend](/docs/dashboard/receiving/introduction).

## Complete Verification

Now click [Verify DNS Records](https://resend.com/domains) on your Domain in Resend. It may take a few hours to complete the verification process (often much faster).

## Troubleshooting

If your domain is not successfully verified, these are some common troubleshooting methods.

<AccordionGroup>
  <Accordion title="Resend shows my domain verification failed.">
    Review the records you added to Hostinger to rule out copy and paste errors.
  </Accordion>

  <Accordion title="It has been longer than 72 hours and my domain is still Pending.">
    [Review our guide on a domain not verifying](/docs/knowledge-base/what-if-my-domain-is-not-verifying).
  </Accordion>
</AccordionGroup>
