> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Namecheap

> Verify your domain on Namecheap with Resend.

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

## Log in to Namecheap

1. Log in to your [Namecheap account](https://ap.www.namecheap.com).

2. Click `Manage` for the domain.

   <img alt="Domain Details" src="https://mintcdn.com/resend/svdlrksWLy8Dr3X-/images/dashboard-domains-namecheap-manage.png?fit=max&auto=format&n=svdlrksWLy8Dr3X-&q=85&s=cb8698fd0e0cab38eb335766a9d0b7d8" width="3404" height="1816" data-path="images/dashboard-domains-namecheap-manage.png" />

   <Info>You may need to expand a dropdown to see the `Manage` button.</Info>

3. Go to the `Advanced DNS` page for the domain you want to verify.

   <img alt="Domain Details" src="https://mintcdn.com/resend/svdlrksWLy8Dr3X-/images/dashboard-domains-namecheap-advanced-dns.png?fit=max&auto=format&n=svdlrksWLy8Dr3X-&q=85&s=b958e136050178c70eb4820e703803c6" width="3404" height="1816" data-path="images/dashboard-domains-namecheap-advanced-dns.png" />

## Add MX SPF Record

<Warning>
  If you are changing the MX configuration from `Gmail` to `Custom MX`, you need
  to [setup new MX records for
  Gmail](https://support.google.com/a/answer/174125). If you don't setup new
  records, receiving mail in your gmail inboxes will stop.
</Warning>

Under the `Mail Settings` section, click the dropdown and select `Custom MX`:

1. Type `send` for the `Host` of the record.
2. Copy the MX Value from Resend into the `Value` field.
3. Use the `Automatic` TTL.
4. Select `Save all changes`.

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-spf-mx.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=bb0db2dd2809135194cfb62b695225cd" width="3024" height="1888" data-path="images/dashboard-domains-resend-spf-mx.png" />

<br />

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-namecheap-spf-mx.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=dda5ff041cce1341e22123fd70111ef3" width="3024" height="1888" data-path="images/dashboard-domains-namecheap-spf-mx.png" />

Below is a mapping of the record fields from Resend to Namecheap:

| Namecheap | Resend   | Example Value                           |
| --------- | -------- | --------------------------------------- |
| Type      | Type     | `MX Record`                             |
| Host      | Name     | `send`                                  |
| TTL       | TTL      | `Automatic`                             |
| Value     | Content  | `feedback-smtp.us-east-1.amazonses.com` |
| -         | Priority | `10`                                    |

<Info>
  Omit your domain from the record values in Resend when you paste. Instead of
  `send.example.com`, paste only `send` (or `send.subdomain` if you're using a
  subdomain).
</Info>

<Info>
  Namecheap does not label the `priority` column. It is the empty column after
  `Value`. Do not use the same priority for multiple records. If Priority `10`
  is already in use, try a higher value `20` or `30`.
</Info>

## Add TXT SPF Record

Under the `Host Records` section, click `Add New Record`:

1. Set the `Type` to `TXT Record`.
2. Enter `send` into the `Host` field.
3. Copy the TXT Value from Resend into the `Value` field.
4. Use the `Automatic` TTL.
5. Select `Save all changes`.

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-spf-txt.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=747425d0a224baeee2846c9a707d5bbc" width="3024" height="1888" data-path="images/dashboard-domains-resend-spf-txt.png" />

<br />

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-namecheap-spf-txt.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=b742409a1de5a3291dc64e1846c2cf77" width="3024" height="1888" data-path="images/dashboard-domains-namecheap-spf-txt.png" />

Below is a mapping of the record fields from Resend to Namecheap:

| Namecheap | Resend  | Example Value                         |
| --------- | ------- | ------------------------------------- |
| Type      | Type    | `TXT Record`                          |
| Host      | Name    | `send`                                |
| TTL       | TTL     | `Automatic`                           |
| Value     | Content | `"v=spf1 include:amazonses.com ~all"` |

<Info>
  Omit your domain from the record values in Resend when you paste. Instead of
  `send.example.com`, paste only `send` (or `send.subdomain` if you're using a
  subdomain).
</Info>

## Add TXT DKIM Records

In that same `Host Records` section, click `Add New Record`.

1. Set the `Type` to `TXT Record`.
2. Enter `resend._domainkey` into the `Host` field.
3. Copy the TXT Value from Resend into the `Value` field.
4. Use the `Automatic` TTL.
5. Select `Save all changes`.

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-dkim.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=345d1dc6b7c138dbd92bd6928c634bd9" width="2992" height="1868" data-path="images/dashboard-domains-resend-dkim.png" />

<br />

<img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-namecheap-dkim-txt.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=0cd6480b613eaed711006b58c7b7a67a" width="3024" height="1888" data-path="images/dashboard-domains-namecheap-dkim-txt.png" />

Below is a mapping of the record fields from Resend to Namecheap:

| Namecheap | Resend  | Example Value                |
| --------- | ------- | ---------------------------- |
| Type      | Type    | `TXT Record`                 |
| Host      | Name    | `resend._domainkey`          |
| TTL       | TTL     | `Automatic`                  |
| Value     | Content | `p=example_domain_key_value` |

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

Under the `Mail Settings` section, click the dropdown and select `Custom MX`:

1. Type `inbound` (or whatever your subdomain is) for the `Host` of the record.
2. Copy the MX Value from Resend into the `Value` field.
3. Use the `Automatic` TTL.
4. Select `Save all changes`.

Below is a mapping of the record fields from Resend to Namecheap:

| Namecheap | Resend   | Example Value                          |
| --------- | -------- | -------------------------------------- |
| Type      | Type     | `MX Record`                            |
| Host      | Name     | `inbound`                              |
| TTL       | TTL      | `Automatic`                            |
| Value     | Content  | `inbound-smtp.us-east-1.amazonaws.com` |
| -         | Priority | `10`                                   |

After verifying your domain, create a webhook to process incoming emails. For help setting up a webhook, how to access email data and attachments, forward emails, and more, see [our guide on receiving emails with Resend](/docs/dashboard/receiving/introduction).

## Complete Verification

Now click [Verify DNS Records](https://resend.com/domains) on your Domain in Resend. It may take up to 72 hours to complete the verification process (often much faster).

## Troubleshooting

If your domain is not successfully verified, these are some common troubleshooting methods.

<AccordionGroup>
  <Accordion title="Resend shows my domain verification failed.">
    Review the records you added to Namecheap to rule out copy and paste errors.
  </Accordion>

  <Accordion title="It has been longer than 72 hours and my domain is still Pending.">
    [Review our guide on a domain not verifying](/docs/knowledge-base/what-if-my-domain-is-not-verifying).
  </Accordion>
</AccordionGroup>
