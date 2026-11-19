> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Claiming a domain

> Claim a domain that is already verified by another team.

A domain can only be active on one Resend team at a time. When you try to add a domain that has already been verified by another team, Resend will alert you that the domain is already in use with a 403 error `The example.com domain has been registered already`.

* **If you own the team where the domain is registered**, delete the domain so you can add it in your desired team.

* **If you do not have access to the team where the domain is registered**, you can prove ownership and [claim the domain](#claim-a-domain-in-the-resend-dashboard) by adding a TXT record to your DNS and then verifying the claim, or do it in one click via DomainConnect for supported registrars.

## Why This Happens

Common reasons a domain you own may already be registered:

* A team member or contractor added it to a separate Resend team.
* You are logged into a different Resend team than the one where the domain was originally added.

Before claiming a domain, check with your team members or in your other teams to see if you can locate the verified domain and [transfer it between teams](https://resend.com/docs/dashboard/domains/manage-domains.md#transfer-a-domain-between-teams) instead.

## Claim a domain in the Resend dashboard

**1. Add your domain in the **Domains** Dashboard page.**

Go to the [**Domains** dashboard page](https://resend.com/domains) and click
**Add Domain**. Enter the domain name and submit the form. A prompt will
appear explaining that the domain is in use by another Resend team.

**2. Click **Start the claim**.**

This will begin the process of claiming ownership of the domain for your team. Resend will provide a DNS TXT record to add to your domain's DNS settings.

![Domain claim](https://mintcdn.com/resend/zovbQ7LtiJotsf8X/images/claim-domain-1.png?fit=max\&auto=format\&n=zovbQ7LtiJotsf8X\&q=85\&s=e585d0a2eb204c15fa59b3998b6bd581)

The claim expires in 7 days. If you started a claim previously, you can pick up where you left off within 7 days by submitting the same domain name again and clicking **Continue claim**. After 7 days, you will be prompted to start your claim over again.

**3. Log in to your DNS host provider and update your DNS records.**

Add the TXT record provided by Resend to the domain you are claiming. If you used the one-click DomainConnect option, this step is done automatically for you.

**4. Return to the Resend Dashboard and click **I've added the records**.**

Resend will verify the domain ownership, release the domain from the previous team, and let you continue the normal process to [add a domain](https://resend.com/docs/add-a-domain.md).

If you cannot add DNS records or need further assistance, contact [Resend support](https://resend.com/help).

## Claim a domain using the Domains API

**1. Start a claim**

Call [Claim Domain](https://resend.com/docs/api-reference/domains/claim-domain.md) with the domain
name. Resend creates a placeholder domain on your team and returns a
`domain_claim` containing a TXT `record` to add to your DNS.

**2. Add the TXT record**

Add the returned TXT record at your DNS provider. It proves you control the
domain.

**3. Verify the claim**

Call [Verify Domain Claim](https://resend.com/docs/api-reference/domains/verify-domain-claim.md).
Resend checks the TXT record and runs ownership-safety checks before
transferring the domain.

**4. Track the status**

Poll [Retrieve Domain Claim](https://resend.com/docs/api-reference/domains/get-domain-claim.md) until
the claim reaches `completed`.

## Claim status

| Status | Meaning |
| - | - |
| `pending` | Waiting for DNS verification. |
| `verified` | DNS proof accepted; the transfer is in progress. |
| `completed` | The domain now belongs to your team. |
| `blocked` | A safety check blocked the claim — see `blocked_reason`. |
| `expired` | The claim window passed before it completed. |
| `superseded` | A newer claim replaced this one. |
| `canceled` | The claim was canceled. |
| `failed` | The claim could not be completed. |

When a claim is `blocked`, `blocked_reason` explains why: `grace_period`,
`recent_owner_activity`, or `pending_scheduled_emails`.

## Canceling a claim

Cancel a pending claim initiated with the API by deleting its placeholder domain with
[Delete Domain](https://resend.com/docs/api-reference/domains/delete-domain.md), using the `domain_id`
from the `domain_claim` object.

## Support

If you can't locate your domain in another team, and you are unable to successfully claim the domain, contact [Resend support](https://resend.com/help) and share the domain name so the team can help you recover access.
