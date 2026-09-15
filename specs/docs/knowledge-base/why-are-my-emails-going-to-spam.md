> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Why Are My Emails Going to Spam?

> Troubleshoot and resolve emails landing in spam or being quarantined.

If your emails are landing in spam or being quarantined, work through this checklist to identify and fix the issue.

## Check your authentication records

Make sure your domain has all three authentication records properly configured:

* **SPF**: Automatically set up when you verify your domain with Resend. Verify it is still present with [dns.email](https://dns.email).
* **DKIM**: Also set up during domain verification. Confirm with [dns.email](https://dns.email).
* **DMARC**: Not automatically set up, but strongly recommended. See [DMARC](/docs/dashboard/domains/dmarc) for setup instructions.

<Warning>
  If any of these records are missing or misconfigured, fix them first.
  Authentication issues are the most common cause of spam placement.
</Warning>

## Use Deliverability Insights

If you sent the email through Resend, open the email in your dashboard and review
[Deliverability Insights](/docs/dashboard/emails/deliverability-insights).

Deliverability Insights runs a set of best-practice checks against your email and
flags issues that may affect inbox placement. Pay close attention to warnings
about:

* Links that do not match your sending domain
* Missing or invalid DMARC
* Missing plain text versions
* Using `no-reply` sender addresses
* Large email body size
* Open or click tracking for sensitive emails

## Check the spam banner

When an email lands in spam, providers like Gmail display a banner explaining why. Here are common messages and what they mean:

| Banner message                                                       | What it means                             | Fix                                                                                     |
| -------------------------------------------------------------------- | ----------------------------------------- | --------------------------------------------------------------------------------------- |
| "It's similar to messages that were identified as spam in the past." | Content is triggering spam filters        | Simplify your email content and remove excessive links, images, or marketing language   |
| "This message seems dangerous"                                       | A URL or content was flagged as malicious | Review the links and content in your email for anything that might be flagged as unsafe |

## Check your domain reputation

* Use [Google Postmaster Tools](https://postmaster.google.com) to see your domain and IP reputation with Gmail.
* If your domain is new, you may need to warm it up by starting with low volume and increasing over time. See our [Domain and/or IP Warm-up Guide](/docs/knowledge-base/warming-up).

## Corporate email filters

Some recipients use enterprise email security services like Mimecast, Proofpoint, or Barracuda. These services apply their own filtering on top of standard spam checks.

If your emails are being blocked by a specific corporate recipient:

* Ask the recipient to check their quarantine or junk folder and allowlist your sending domain.
* These filters often block based on domain age, content patterns, or URL reputation. The fixes in the steps above still apply.

## Review your sending practices

* Send from a dedicated address per email type, such as `notifications@` for transactional emails and `updates@` for marketing emails. For more guidance on domain setup, review [Is it better to send emails from a subdomain or the root domain?](/docs/knowledge-base/is-it-better-to-send-emails-from-a-subdomain-or-the-root-domain).
* Do not send to purchased lists or addresses that have not opted in. If you are unsure what qualifies as permission, review [What counts as email consent?](/docs/knowledge-base/what-counts-as-email-consent).
* Include a visible unsubscribe link in marketing emails.
* Keep HTML simple. Heavy formatting and image-only emails are more likely to trigger filters.

<Tip>
  For provider-specific guidance, see [How do I avoid Gmail's spam
  folder?](/docs/knowledge-base/how-do-i-avoid-gmails-spam-folder). For Outlook,
  message headers include Spam Confidence Level (SCL) and Bulk Complaint Level
  (BCL) scores. See [How do I avoid Outlook's spam
  folder?](/docs/knowledge-base/how-do-i-avoid-outlooks-spam-folder#read-what-microsoft-told-you)
  to read them.
</Tip>

## Get more help

If you have worked through the steps above and still need help, our support team
is happy to take a closer look. Contact us through our
[support form](https://resend.com/help) and share any relevant details about the
issue, such as the recipient provider, sending domain, and what you have already
tried.
