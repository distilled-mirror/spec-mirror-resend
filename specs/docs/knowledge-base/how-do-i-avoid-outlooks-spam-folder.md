> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# How to avoid Outlook's spam folder

> Learn how to improve inbox placement in Outlook.

<Note>
  This guide is adapted from Microsoft's article to [Improve your spam
  reputation](https://support.microsoft.com/en-us/office/sender-support-in-outlook-com-05875e8d-1950-4d89-a5c3-adc355d0d652).
  For high-volume senders (5,000+ messages per day), see [Microsoft's bulk
  sending requirements for
  2025](https://resend.com/blog/microsoft-bulk-sending-requirements-2025).
</Note>

## Authenticate Your Email

Outlook uses email authentication to confirm that you are who you say you are. Microsoft requires bulk senders (5,000+ messages per day) to authenticate with SPF, DKIM, and DMARC, and it's recommended for every sender.

| Authentication                    | Requires Setup | Purpose                                                      |
| --------------------------------- | -------------- | ------------------------------------------------------------ |
| **SPF**                           | No             | Proves you are allowed to send from this domain              |
| **DKIM**                          | No             | Proves your email originated from you                        |
| [DMARC](/docs/dashboard/domains/dmarc) | Yes            | Proves you own the domain and instructs how to handle spoofs |

When you verify your domain with Resend, **SPF** and **DKIM** are configured and validated for you automatically. [DMARC](/docs/dashboard/domains/dmarc) is an additional authentication method that can build trust and further improve inbox placement.

**Action Items**

1. Verify your domain with Resend to set up SPF and DKIM automatically
2. [Set up DMARC](/docs/dashboard/domains/dmarc) for your domain

## Read What Microsoft Told You

When Outlook or Hotmail filters a message, it records why in the headers. Ask the recipient to [view the message headers](https://support.microsoft.com/en-us/office/view-internet-message-headers-in-outlook-cd039382-dc6e-4264-ac74-c048563d212c) and look for the fields below. Microsoft documents these in [Anti-spam message headers](https://learn.microsoft.com/en-us/defender-office-365/message-headers-eop-mdo). You can paste the headers into Microsoft's [Message Header Analyzer](https://mha.azurewebsites.net/) to parse the fields.

**Spam Confidence Level (SCL)** appears as `SCL:` in `X-Forefront-Antispam-Report`. It also often appears in `X-MS-Exchange-Organization-SCL`. Microsoft stamps a value of `-1`, or `0` through `9`. An SCL of 5 or higher generally indicates the message is considered bad. See [Spam confidence level](https://learn.microsoft.com/en-us/defender-office-365/anti-spam-spam-confidence-level-scl-about).

| SCL    | Meaning                                                            | Typical outcome    |
| ------ | ------------------------------------------------------------------ | ------------------ |
| -1     | Filtering was bypassed (safe sender, allowlist, or mail flow rule) | Inbox              |
| 0 to 1 | Not classified as spam                                             | Inbox              |
| 5 to 6 | Classified as spam                                                 | Junk               |
| 9      | Classified as high confidence spam                                 | Junk or quarantine |

In Microsoft 365 cloud organizations, SCL no longer determines the Spam vs High confidence spam verdict or the action taken. Microsoft says to read the category (CAT) field in `X-Forefront-Antispam-Report` instead.

| CAT    | Meaning              |
| ------ | -------------------- |
| `SPM`  | Spam                 |
| `BULK` | Bulk                 |
| `HSPM` | High confidence spam |

**Bulk Complaint Level (BCL)** appears in `X-Microsoft-Antispam` and scores how bulk-like the message is. See [Bulk complaint level](https://learn.microsoft.com/en-us/defender-office-365/anti-spam-bulk-complaint-level-bcl-about).

| BCL    | Meaning                                                 |
| ------ | ------------------------------------------------------- |
| 0      | The message isn't from a bulk sender                    |
| 1 to 3 | Bulk sender that generates few complaints               |
| 4 to 7 | Bulk sender that generates a mixed number of complaints |
| 8 to 9 | Bulk sender that generates a high number of complaints  |

Microsoft's default anti-spam policy treats BCL 7 or higher as bulk mail and delivers it to Junk.

SCL 5 and SCL 6 are the same band: Microsoft classified the message as spam. What you do next depends on BCL and CAT, not on which of those two numbers you see.

Read the two scores together. `SCL 5` or `SCL 6` with `BCL 0` means the message was classified as spam but *not* because it looked like bulk mail, which points at content and domain reputation rather than list quality. A high BCL points the other way, at how the list was built and how recipients are responding. `CAT:SPM` pairs with the first reading. `CAT:BULK` pairs with the second.

**Action Items**

1. Ask a recipient to send you the full message source
2. Note the SCL, BCL, and CAT values before changing anything
3. Use the combination to decide whether to work on content and reputation or on list quality

## Reputation Is Built on Your Domain

When a message is filtered, the sending IP in the headers is rarely the useful signal. When you send with Resend, forward and reverse DNS for the sending IPs is managed for you on both shared and dedicated pools. What Microsoft weighs, and what you control, is the sending domain and the history attached to it.

If your messages are being filtered, work on the domain. Checking the shared sending IP against a blocklist is usually a dead end.

Keep one domain or subdomain per sending type so reputation stays separable. See [Is it better to send emails from a subdomain or the root domain?](/docs/knowledge-base/is-it-better-to-send-emails-from-a-subdomain-or-the-root-domain).

**Action Items**

1. Treat the sending domain, not the sending IP, as the thing to improve
2. Keep one domain or subdomain per sending type so reputation stays separable

## Send to Engaged Recipients

Outlook monitors whether recipients want your mail. Engagement (opens, replies, and moving a message to the Inbox) builds reputation. Complaints, ignored unsubscribes, and bouncing addresses damage it.

Keep spam complaint rates under 0.3%. Don't keep sending if there is no engagement from your recipients, especially if a recipient has requested to unsubscribe or an address is bouncing.

**Prevent sending to recipients who**:

* Didn't ask to be sent to (opt-in)
* Show no signs of engagement with your emails
* Requested to be unsubscribed
* Marked your emails as spam (complained)
* Never received your email (bounced)

Ask recipients to add you to their contacts and Safe Senders list. This can be done in [Outlook](https://support.microsoft.com/en-us/office/add-recipients-of-my-email-messages-to-the-safe-senders-list-be1baea0-beab-4a30-b968-9004332336ce) or [Outlook.com](https://support.microsoft.com/en-us/office/safe-senders-in-outlook-com-470d4ee6-e3b6-402b-8cd9-a6f00eda7339). See how to add contacts in [Outlook.com](https://support.microsoft.com/en-us/office/create-view-and-edit-contacts-and-contact-lists-in-outlook-com-5b909158-036e-4820-92f7-2a27f57b9f01).

Don't blast to a BCC list. Send separate emails if you are sending to a large number of recipients. Avoid sending too many emails at once. Limits are impacted by historical engagement and sending volume, so reduce the frequency or volume if you start seeing filtering.

For bulk emails, include a clearly visible unsubscribe link and [Unsubscribe Headers](/docs/dashboard/emails/add-unsubscribe-to-transactional-emails).

Sending repeatedly to a mailbox you own gives Outlook little to learn from. Real recipients opening, replying, and moving messages out of Junk are the signals that move reputation.

**Action Items**

1. Ask recipients to move the message to the Inbox and add you to their contacts or Safe Senders list
2. Provide a clear way to opt out of bulk emails, including [Unsubscribe Headers](/docs/dashboard/emails/add-unsubscribe-to-transactional-emails)
3. Use [Webhooks](/docs/webhooks/introduction) to remove bounced or complained recipients from your list
4. Don't send to a BCC list, and don't burst a large volume at once

## When Your Sending Volume Is Low

Microsoft's filtering leans on history, and a low-volume domain accumulates that history slowly. If you send a few dozen messages a day and that is your steady state rather than a starting point, the [warm-up schedules](/docs/knowledge-base/warming-up) don't apply in the usual way. Those tables start at 150 messages a day and climb. The goal shifts from increasing volume to getting the most signal out of each message.

* **Each message carries more weight.** At a few dozen messages a day, a single spam complaint is a far larger share of your reputation than it would be at scale. Accuracy of the recipient list matters more than reach.
* **A test inbox is a thin signal.** Sending repeatedly to one mailbox you own gives Microsoft very little to learn from. Reputation moves on real recipients opening, replying, and moving messages out of Junk.
* **Ask early recipients to act.** Moving a message from Junk to Inbox and adding the sender to their contacts are the two strongest corrective signals a recipient can give.
* **Keep sending steady.** Long gaps followed by bursts read as a change in pattern. Small and regular builds reputation more reliably than irregular.
* **Expect it to take longer.** Low volume means a smaller sample, so both damage and recovery take more calendar time.

**Action Items**

1. Send to real recipients rather than a single test mailbox
2. Ask your first recipients to move the message to Inbox and add you to their contacts
3. Keep a steady daily cadence rather than batching
4. Give it weeks rather than days before judging a change

## Keep Your Content Simple

Outlook filters on content as well as reputation. Keep emails as close to plain text as possible, and add a sender name. Set your `from` like this: `"Name <name@example.com>"`.

Visible links that match the sending domain help. Open or click tracking on sensitive emails (password resets, magic links) often hurts Outlook placement.

Check [Deliverability Insights](/docs/dashboard/emails/deliverability-insights) on the email in your Dashboard. Insights flags link/domain mismatch and tracking on sensitive emails, both of which are common Outlook placement causes.

**Action Items**

1. Reduce and simplify your email content
2. Set a display name on your `from` address
3. Review [Deliverability Insights](/docs/dashboard/emails/deliverability-insights) for link mismatch and tracking warnings

## Summary

Email deliverability is overwhelming. One way to simplify it is to think: **what would a phisher do?**

**Then do the opposite!**

Outlook's goal is to only show emails that their users want to see, and malicious emails are at the bottom of the list. Reverse engineer phishing sending habits and consider how you can prove to Outlook at each step that you clearly have no malicious intent.

<Info>Anything we missed? [Let us know](https://resend.com/help).</Info>
