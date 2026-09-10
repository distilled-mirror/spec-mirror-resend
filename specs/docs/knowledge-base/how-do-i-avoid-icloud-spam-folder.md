> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# How to avoid iCloud's spam folder

> Learn how to improve inbox placement in iCloud Mail.

<Note>
  This guide is adapted from Apple's article on [bulk email sending best
  practices for iCloud Mail](https://support.apple.com/en-us/HT204137). Many of
  these recommendations also apply to Gmail and Outlook, so be sure to read [How
  do I avoid Gmail's spam
  folder?](/docs/knowledge-base/how-do-i-avoid-gmails-spam-folder) and [How do I
  avoid Outlook's spam
  folder?](/docs/knowledge-base/how-do-i-avoid-outlooks-spam-folder).
</Note>

Apple does not offer allowlists or feedback loops for iCloud Mail. Your reputation as a sender is determined automatically based on how you send and how recipients engage with your email. The best way to land in the inbox is to follow the requirements below consistently.

## Authenticate Your Email

Like every major mailbox provider, iCloud uses email authentication to confirm that you are who you say you are. Apple requires that bulk senders authenticate with SPF, DKIM, and DMARC.

| Authentication                    | Requires Setup | Purpose                                                      |
| --------------------------------- | -------------- | ------------------------------------------------------------ |
| **SPF**                           | No             | Proves you are allowed to send from this domain              |
| **DKIM**                          | No             | Proves your email originated from you                        |
| [DMARC](/docs/dashboard/domains/dmarc) | Yes            | Proves you own the domain and instructs how to handle spoofs |

When you verify your domain with Resend, **SPF** and **DKIM** are configured and validated for you automatically, so your email meets Apple's authentication requirements out of the box. Resend also signs every message with DKIM and handles SPF alignment on your behalf, so you don't have to manage these records yourself. Apple additionally requires that your sending domain publish a [DMARC](/docs/dashboard/domains/dmarc) policy.

**Action Items**

1. Verify your domain with Resend to set up SPF and DKIM automatically
2. [Setup DMARC](/docs/dashboard/domains/dmarc) for your domain

## Use Consistent, Reputable Infrastructure

iCloud builds trust over time based on the domains you send from. Keeping your sending consistent helps Apple recognize you as a legitimate sender.

* **Separate your marketing and transactional streams** so each can build its own reputation.
* Maintain a **consistent `From:` name and address** so recipients (and Apple) recognize your brand.
* Make sure your email is **RFC 5321 and RFC 5322 compliant**.

**Action Items**

1. Use dedicated sending addresses for marketing vs. transactional email

## Send Only to Recipients Who Opted In

Apple requires that you send only to recipients who explicitly subscribed to your emails. Purchased lists, rented lists, and email appends are not permitted and will damage your reputation.

**Prevent sending to recipients who**:

* Didn't explicitly opt in to your emails
* Show no signs of engagement with your emails
* Requested to be unsubscribed
* Marked your emails as spam (complained)
* Never received your email (bounced)

**Action Items**

1. Only send to recipients who explicitly subscribed
2. Use [Webhooks](/docs/webhooks/introduction) to remove bounced or complained recipients from your list
3. Never resume sending to addresses on your suppression list

## Simplify the Unsubscribe Process

Apple requires bulk senders to offer an unsubscribe link so recipients can opt out immediately. You can [implement one-click unsubscribe](/docs/dashboard/emails/add-unsubscribe-to-transactional-emails) for the best user experience.

**Action Items**

1. Include a clearly visible unsubscribe link in bulk emails
2. Add [Unsubscribe Headers](/docs/dashboard/emails/add-unsubscribe-to-transactional-emails) to enable one-click unsubscribe

## Keep Your List Clean

iCloud monitors recipient engagement closely. Continuing to send to inactive or invalid addresses lowers your reputation.

* Periodically remove inactive subscribers.
* Handle bounces with a standard suppression policy.
* Keep your spam complaint rate low.

**Action Items**

1. Regularly prune inactive subscribers from your list
2. Suppress bounced and complained addresses automatically

## Monitor SMTP Errors

When iCloud rejects or defers a message, it returns an SMTP error explaining why. Apple expects senders to track both temporary and permanent errors and respond appropriately, rather than retrying blindly.

**Action Items**

1. Review your mail logs and Resend dashboard for SMTP errors
2. Adjust your sending based on temporary (defer) vs. permanent (reject) errors

## If You're Still Having Issues

Apple does not provide allowlists or feedback loops, but for unresolved delivery problems you can contact Apple at **[icloudadmin@apple.com](mailto:icloudadmin@apple.com)**. Include your company name, domain, the SMTP errors you're seeing, and a detailed description of the issue.

## Summary

Email deliverability is overwhelming. One way to simplify it is to think: **what would a phisher do?**

**Then do the opposite!**

iCloud's goal is to only show emails that their users want to see. Reverse engineer phishing sending habits and consider how you can prove to Apple at each step that you clearly have no malicious intent.

<Info>Anything we missed? [Let us know](https://resend.com/help).</Info>
