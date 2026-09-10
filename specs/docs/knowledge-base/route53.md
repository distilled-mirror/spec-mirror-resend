> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# AWS Route 53

> Verify your domain on Route 53 with Resend.

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

## Log in to Route 53

Then, log in to your [AWS Management Console, and open Route 53 console](https://console.aws.amazon.com/route53/), then click on your domain name. From there, click on `Create Record`.

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-route53-createrecord.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=93d90903872f328b3f593e933d29f4fe" width="1510" height="908" data-path="images/dashboard-domains-route53-createrecord.png" />

## Add MX SPF Record

1. Type in `send` for the `Record name`.
2. Select the `Record type` dropdown, and choose `MX`.
3. Copy the MX Value from your domain in Resend into the `Value` field.
4. Be sure to include the `10` in the `Value` field, as seen in the screenshot.

<Info>
  Omit your domain from the record values in Resend when you paste. Instead of
  `send.example.com`, paste only `send` (or `send.subdomain` if you're using a
  subdomain).
</Info>

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-spf-mx.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=bb0db2dd2809135194cfb62b695225cd" width="3024" height="1888" data-path="images/dashboard-domains-resend-spf-mx.png" />

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-route53-spf-mx.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=8b798e983ecec8edb48c777143edfce5" width="1512" height="909" data-path="images/dashboard-domains-route53-spf-mx.png" />

Below is a mapping of the record fields from Resend to Route 53:

| Route 53       | Resend             | Example Value                              |
| -------------- | ------------------ | ------------------------------------------ |
| Record Type    | Type               | `MX Record`                                |
| Record name    | Name               | `send`                                     |
| Value          | Content & Priority | `10 feedback-smtp.us-east-1.amazonses.com` |
| TTL            | TTL                | `Use Route 53 Default (300)`               |
| Routing policy | -                  | `Simple routing`                           |

<Info>
  Route 53 does not label the `priority` column, and you will need to add this
  in to the `Value` section, as shown in the screenshot. Do not use the same
  priority for multiple records. If Priority `10` is already in use, try a
  number slightly higher like `11` or `12`.
</Info>

## Add TXT SPF Record

In the same section, choose `Add another record`:

1. Type in `send` for the `Record name`.
2. Click the `Record type` dropdown.
3. Select the `Record type` dropdown, and choose `TXT`.
4. Copy TXT Value from your domain in Resend into the `Value` field.

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-spf-txt.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=747425d0a224baeee2846c9a707d5bbc" width="3024" height="1888" data-path="images/dashboard-domains-resend-spf-txt.png" />

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-route53-spf-txt.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=79d4f534f637964bc06005f34cafe92b" width="1509" height="908" data-path="images/dashboard-domains-route53-spf-txt.png" />

Below is a mapping of the record fields from Resend to Route 53:

| Route 53       | Resend  | Example Value                         |
| -------------- | ------- | ------------------------------------- |
| Record type    | Type    | `TXT Record`                          |
| Record name    | Name    | `send`                                |
| Value          | Content | `"v=spf1 include:amazonses.com ~all"` |
| TTL            | TTL     | `Use Route 53 Default (300)`          |
| Routing policy | -       | `Simple routing`                      |

<Info>
  Omit your domain from the record values in Resend when you paste. Instead of
  `send.example.com`, paste only `send` (or `send.subdomain` if you're using a
  subdomain).
</Info>

## Add TXT DKIM Records

In the same section, choose `Add another record`:

1. Type in `resend._domainkey` for the `Record name`.
2. Change the `Record Type` to `TXT`.
3. Copy the TXT Value value from your domain in Resend to the `Value` text box.
4. Click on `Create Records`.

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-dkim.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=345d1dc6b7c138dbd92bd6928c634bd9" width="2992" height="1868" data-path="images/dashboard-domains-resend-dkim.png" />

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-route53-dkim-txt.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=00e9fa493cb8a6541fa0d16323b1a7af" width="1513" height="912" data-path="images/dashboard-domains-route53-dkim-txt.png" />

Below is a mapping of the record fields from Resend to Route 53:

| Route 53       | Resend  | Example Value                |
| -------------- | ------- | ---------------------------- |
| Record type    | Type    | `TXT Record`                 |
| Record name    | Name    | `resend._domainkey`          |
| Value          | Content | `p=example_domain_key_value` |
| TTL            | TTL     | `Use Route 53 Default (300)` |
| Routing policy | -       | `Simple routing`             |

<Info>
  Omit your domain from the record values in Resend when you paste. Instead of
  `resend._domainkey.example.com`, paste only `resend._domainkey` (or
  `resend._domainkey.subdomain` if you're using a subdomain).
</Info>

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

In the Route 53 console, click `Create Record`:

1. Type in `inbound` (or whatever your subdomain is) for the `Record name`.
2. Select the `Record type` dropdown, and choose `MX`.
3. Copy the MX Value from your domain in Resend into the `Value` field.
4. Be sure to include the `10` in the `Value` field (e.g., `10 inbound-smtp.us-east-1.amazonaws.com`).

Below is a mapping of the record fields from Resend to Route 53:

| Route 53       | Resend             | Example Value                             |
| -------------- | ------------------ | ----------------------------------------- |
| Record Type    | Type               | `MX Record`                               |
| Record name    | Name               | `inbound`                                 |
| Value          | Content & Priority | `10 inbound-smtp.us-east-1.amazonaws.com` |
| TTL            | TTL                | `Use Route 53 Default (300)`              |
| Routing policy | -                  | `Simple routing`                          |

After verifying your domain, create a webhook to process incoming emails. For help setting up a webhook, how to access email data and attachments, forward emails, and more, see [our guide on receiving emails with Resend](/docs/dashboard/receiving/introduction).

## Complete Verification

Now click [Verify DNS Records](https://resend.com/domains) on your Domain in Resend. It may take up to 5 hours to complete the verification process (often much faster).

## Troubleshooting

If your domain is not successfully verified, these are some common troubleshooting methods.

<AccordionGroup>
  <Accordion title="Resend shows my domain verification failed.">
    Review the records you added to Route 53 to rule out copy and paste errors.
  </Accordion>

  <Accordion title="It has been longer than 72 hours and my domain is still Pending.">
    [Review our guide on a domain not verifying](/docs/knowledge-base/what-if-my-domain-is-not-verifying).
  </Accordion>
</AccordionGroup>
