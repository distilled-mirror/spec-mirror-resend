> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# DreamHost

> Verify your domain on DreamHost with Resend.

## Add Domain to Resend

First, log in to your [Resend Account](https://resend.com/login) and [add a domain](https://resend.com/domains).

![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-add-domain.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=418dd93c2f2ead0b0d83d1b7c2fb0970)

> [!TIP]
>
> It is [best practice to use a
> subdomain](https://resend.com/docs/knowledge-base/is-it-better-to-send-emails-from-a-subdomain-or-the-root-domain.md)
> (updates.example.com) instead of the root domain (example.com). Using a
> subdomain allows for proper reputation segmentation based on topics or purpose
> (e.g. marketing) and is especially important if receiving emails with Resend.

## Log in to DreamHost

1. Log in to your [DreamHost panel](https://panel.dreamhost.com).

2. Go to **Websites > Manage Websites**.

3. Select **Manage** on the domain you want to verify.

   ![DreamHost DNS TXT Record](https://mintcdn.com/resend/7M2Hdgv3dPiLlTrA/images/dashboard-domains-dreamhost-website.png?fit=max\&auto=format\&n=7M2Hdgv3dPiLlTrA\&q=85\&s=006357ac32d5cd380fdb83b995149e09)

## Add TXT SPF Record

1. Navigate to the **DNS** tab.
2. Enter `send` as Host.
3. Enter `v=spf1 include:amazonses.com ~all` as TXT Value.
4. Click **Add Record**.

Below is a mapping of the record fields from Resend to DreamHost:

| DreamHost | Resend | Example Value |
| - | - | - |
| Type | Type | `TXT Record` |
| Host | Name | `send` |
| TXT Value | Content | `v=spf1 include:amazonses.com ~all` |

![DreamHost DNS Dashboard](https://mintcdn.com/resend/7M2Hdgv3dPiLlTrA/images/dashboard-domains-dreamhost-spf.png?fit=max\&auto=format\&n=7M2Hdgv3dPiLlTrA\&q=85\&s=8c285c277231e0f0abbe68b8cdf67e66)

## Add TXT DKIM Records

1. In the same window, add another TXT record.

2. Add `resend._domainkey` as Host.

3. Copy the value from your domain configuration page in Resend and paste it into DreamHost.

   ![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-dkim.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=345d1dc6b7c138dbd92bd6928c634bd9)

4. Click **Add Record**.

   ![DreamHost DNS Dashboard](https://mintcdn.com/resend/7M2Hdgv3dPiLlTrA/images/dashboard-domains-dreamhost-dkim.png?fit=max\&auto=format\&n=7M2Hdgv3dPiLlTrA\&q=85\&s=90f2e23d3b70ff95c418e178489df7bb)

   Below is a mapping of the record fields from Resend to DreamHost:

| DreamHost | Resend | Example Value |
| - | - | - |
| Type | Type | `TXT Record` |
| Host | Name | `resend._domainkey` |
| TXT Value | Content | `p=example_domain_key_value` |

## Add MX SPF Record

1. Create a subdomain with the custom path name. Return to **Manage Websites** page. Click **Add Website**.

   ![DreamHost Website](https://mintcdn.com/resend/7M2Hdgv3dPiLlTrA/images/dashboard-domains-dreamhost-subdomain.png?fit=max\&auto=format\&n=7M2Hdgv3dPiLlTrA\&q=85\&s=7964ed472542c62a5aae1459e4a19bdb)
2. Click **Manage** on the subdomain.
3. **Add Record** > Select **MX** > **Manage Customer MX**.
4. Copy and paste the MX value replacing the default record.

   ![Domain Details](https://mintcdn.com/resend/JHWt09hsc7E33HK2/images/dashboard-domains-resend-spf-mx.png?fit=max\&auto=format\&n=JHWt09hsc7E33HK2\&q=85\&s=bb0db2dd2809135194cfb62b695225cd)

![DreamHost Website](https://mintcdn.com/resend/7M2Hdgv3dPiLlTrA/images/dashboard-domains-dreamhost-custom-mx.png?fit=max\&auto=format\&n=7M2Hdgv3dPiLlTrA\&q=85\&s=0f0aae42669dd7024fef53137458f5f4)

Below is a mapping of the record fields from Resend to DreamHost:

| DreamHost | Resend | Example Value |
| - | - | - |
| Type | Type | `MX Record` |
| Host | Name | `send` |
| Points to | Content | `feedback-smtp.us-east-1.amazonses.com` |
| Priority | Priority | `10` |

> [!NOTE]
>
> MX record will differ depending on your selected sending region.

> [!NOTE]
>
> Do not use the same priority for multiple MX records. If Priority `10` is
> already in use, try a higher value such as `20` or `30`.

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

Add an MX record for receiving:

1. Click the **Add Record** button.
2. Hover over the **MX Record** section and click **ADD**.
3. Enter `inbound` (or your receiving subdomain) in the **Host** field.
4. Copy the MX Value from Resend into the **Points to** field.
5. Enter `10` for **Priority**.
6. Click **Add Record** to save.

Below is a mapping of the record fields from Resend to DreamHost:

| DreamHost | Resend | Example Value |
| - | - | - |
| Type | Type | `MX Record` |
| Host | Name | `inbound` |
| Points to | Content | `inbound-smtp.us-east-1.amazonaws.com` |
| Priority | Priority | `10` |

After verifying your domain, create a webhook to process incoming emails. For help setting up a webhook, how to access email data and attachments, forward emails, and more, see [our guide on receiving emails with Resend](https://resend.com/docs/dashboard/receiving/introduction.md).

## Complete Verification

Now click [Verify DNS Records](https://resend.com/domains) on your Domain in Resend. It may take up to 72 hours to complete the verification process (often much faster). DNS updates at DreamHost can take several hours to propagate.

## Troubleshooting

If your domain is not successfully verified, these are some common troubleshooting methods.

> **Resend shows my domain verification failed.**
>
> Review the records you added to DreamHost to rule out copy and paste errors.
> Ensure the **Host** field uses only the subdomain (e.g., `send` or
> `resend._domainkey`) and that you did not include the full domain name.

> **It has been longer than 72 hours and my domain is still Pending.**
>
> [Review our guide on a domain not verifying](https://resend.com/docs/knowledge-base/what-if-my-domain-is-not-verifying.md).
