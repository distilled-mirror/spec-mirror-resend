> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# DreamHost

> Verify your domain on DreamHost with Resend.

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

## Log in to DreamHost

1. Log in to your [DreamHost panel](https://panel.dreamhost.com).

2. Go to **Websites > Manage Websites**.

3. Select **Manage** on the domain you want to verify.
   <img alt="DreamHost DNS TXT Record" src="https://mintcdn.com/resend/7M2Hdgv3dPiLlTrA/images/dashboard-domains-dreamhost-website.png?fit=max&auto=format&n=7M2Hdgv3dPiLlTrA&q=85&s=006357ac32d5cd380fdb83b995149e09" width="2564" height="1502" data-path="images/dashboard-domains-dreamhost-website.png" />

## Add TXT SPF Record

1. Navigate to the **DNS** tab.
2. Enter `send` as Host.
3. Enter `v=spf1 include:amazonses.com ~all` as TXT Value.
4. Click **Add Record**.

Below is a mapping of the record fields from Resend to DreamHost:

| DreamHost | Resend  | Example Value                       |
| --------- | ------- | ----------------------------------- |
| Type      | Type    | `TXT Record`                        |
| Host      | Name    | `send`                              |
| TXT Value | Content | `v=spf1 include:amazonses.com ~all` |

<img alt="DreamHost DNS Dashboard" src="https://mintcdn.com/resend/7M2Hdgv3dPiLlTrA/images/dashboard-domains-dreamhost-spf.png?fit=max&auto=format&n=7M2Hdgv3dPiLlTrA&q=85&s=8c285c277231e0f0abbe68b8cdf67e66" width="2536" height="1456" data-path="images/dashboard-domains-dreamhost-spf.png" />

## Add TXT DKIM Records

1. In the same window, add another TXT record.

2. Add `resend._domainkey` as Host.

3. Copy the value from your domain configuration page in Resend and paste it into DreamHost.

   <img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-dkim.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=345d1dc6b7c138dbd92bd6928c634bd9" width="2992" height="1868" data-path="images/dashboard-domains-resend-dkim.png" />

4. Click **Add Record**.
   <img alt="DreamHost DNS Dashboard" src="https://mintcdn.com/resend/7M2Hdgv3dPiLlTrA/images/dashboard-domains-dreamhost-dkim.png?fit=max&auto=format&n=7M2Hdgv3dPiLlTrA&q=85&s=90f2e23d3b70ff95c418e178489df7bb" width="2530" height="1448" data-path="images/dashboard-domains-dreamhost-dkim.png" />
   Below is a mapping of the record fields from Resend to DreamHost:

| DreamHost | Resend  | Example Value                |
| --------- | ------- | ---------------------------- |
| Type      | Type    | `TXT Record`                 |
| Host      | Name    | `resend._domainkey`          |
| TXT Value | Content | `p=example_domain_key_value` |

## Add MX SPF Record

1. Create a subdomain with the custom path name. Return to **Manage Websites** page. Click **Add Website**.
   <img alt="DreamHost Website" src="https://mintcdn.com/resend/7M2Hdgv3dPiLlTrA/images/dashboard-domains-dreamhost-subdomain.png?fit=max&auto=format&n=7M2Hdgv3dPiLlTrA&q=85&s=7964ed472542c62a5aae1459e4a19bdb" width="2526" height="1348" data-path="images/dashboard-domains-dreamhost-subdomain.png" />
2. Click **Manage** on the subdomain.
3. **Add Record** > Select **MX** > **Manage Customer MX**.
4. Copy and paste the MX value replacing the default record.
   <img alt="Domain Details" src="https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-spf-mx.png?fit=max&auto=format&n=JHWt09hsc7E33HK2&q=85&s=bb0db2dd2809135194cfb62b695225cd" width="3024" height="1888" data-path="images/dashboard-domains-resend-spf-mx.png" />

<img alt="DreamHost Website" src="https://mintcdn.com/resend/7M2Hdgv3dPiLlTrA/images/dashboard-domains-dreamhost-custom-mx.png?fit=max&auto=format&n=7M2Hdgv3dPiLlTrA&q=85&s=0f0aae42669dd7024fef53137458f5f4" width="2526" height="1480" data-path="images/dashboard-domains-dreamhost-custom-mx.png" />

Below is a mapping of the record fields from Resend to DreamHost:

| DreamHost | Resend   | Example Value                           |
| --------- | -------- | --------------------------------------- |
| Type      | Type     | `MX Record`                             |
| Host      | Name     | `send`                                  |
| Points to | Content  | `feedback-smtp.us-east-1.amazonses.com` |
| Priority  | Priority | `10`                                    |

<Info>MX record will differ depending on your selected sending region.</Info>

<Info>
  Do not use the same priority for multiple MX records. If Priority `10` is
  already in use, try a higher value such as `20` or `30`.
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

Add an MX record for receiving:

1. Click the **Add Record** button.
2. Hover over the **MX Record** section and click **ADD**.
3. Enter `inbound` (or your receiving subdomain) in the **Host** field.
4. Copy the MX Value from Resend into the **Points to** field.
5. Enter `10` for **Priority**.
6. Click **Add Record** to save.

Below is a mapping of the record fields from Resend to DreamHost:

| DreamHost | Resend   | Example Value                          |
| --------- | -------- | -------------------------------------- |
| Type      | Type     | `MX Record`                            |
| Host      | Name     | `inbound`                              |
| Points to | Content  | `inbound-smtp.us-east-1.amazonaws.com` |
| Priority  | Priority | `10`                                   |

After verifying your domain, create a webhook to process incoming emails. For help setting up a webhook, how to access email data and attachments, forward emails, and more, see [our guide on receiving emails with Resend](/docs/dashboard/receiving/introduction).

## Complete Verification

Now click [Verify DNS Records](https://resend.com/domains) on your Domain in Resend. It may take up to 72 hours to complete the verification process (often much faster). DNS updates at DreamHost can take several hours to propagate.

## Troubleshooting

If your domain is not successfully verified, these are some common troubleshooting methods.

<AccordionGroup>
  <Accordion title="Resend shows my domain verification failed.">
    Review the records you added to DreamHost to rule out copy and paste errors.
    Ensure the **Host** field uses only the subdomain (e.g., `send` or
    `resend._domainkey`) and that you did not include the full domain name.
  </Accordion>

  <Accordion title="It has been longer than 72 hours and my domain is still Pending.">
    [Review our guide on a domain not verifying](/docs/knowledge-base/what-if-my-domain-is-not-verifying).
  </Accordion>
</AccordionGroup>
