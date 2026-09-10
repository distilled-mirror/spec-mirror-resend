> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# How to avoid Yahoo's spam folder

> Learn how to improve inbox placement in Yahoo Mail.

<Note>
  This guide is adapted from Yahoo's [Sender Requirements &
  Recommendations](https://senders.yahooinc.com/best-practices/) and [Sender Hub
  FAQs](https://senders.yahooinc.com/faqs/). Many of these recommendations also
  apply to other providers, so be sure to read [How do I avoid Gmail's spam
  folder?](/docs/knowledge-base/how-do-i-avoid-gmails-spam-folder), [How do I avoid
  Outlook's spam folder?](/docs/knowledge-base/how-do-i-avoid-outlooks-spam-folder),
  and [How do I avoid iCloud's spam
  folder?](/docs/knowledge-base/how-do-i-avoid-icloud-spam-folder).
</Note>

Yahoo began enforcing its sender requirements in February 2024, with one-click unsubscribe enforcement following in June 2024. These rules apply to every consumer email brand and domain that Yahoo hosts, which includes AOL and thousands of other hosted domains. Yahoo Japan is a separate entity and isn't covered by these requirements.

Yahoo splits its rules into requirements for **all senders** and additional requirements for **bulk senders**. Yahoo deliberately doesn't publish a volume threshold for what counts as bulk: a bulk sender is "an email sender sending a significant volume of mail," evaluated at the authenticated domain or `From:` header domain level. Mail that spoofs your domain counts toward the volume Yahoo reviews, which is a strong reason to move to a DMARC enforcement policy.

## Authenticate Your Email

Authentication is the foundation of every other requirement on this page. Yahoo requires all senders to authenticate with SPF or DKIM at a minimum, and bulk senders to implement both alongside a valid DMARC policy.

| Authentication                    | Requires Setup | Yahoo's Requirement                                                             |
| --------------------------------- | -------------- | ------------------------------------------------------------------------------- |
| **SPF**                           | No             | Required for all senders (with DKIM, or on its own)                             |
| **DKIM**                          | No             | Required for all senders (with SPF, or on its own). Minimum 1024-bit key length |
| [DMARC](/docs/dashboard/domains/dmarc) | Yes            | Required for bulk senders. At least `p=none`, and DMARC must pass               |

A few Yahoo-specific details worth knowing:

* **Alignment matters.** The domain in your `From:` header must align with either the SPF domain or the DKIM domain. Relaxed alignment is acceptable.
* **1024-bit DKIM is enough.** Yahoo requires a key length of 1024 bits or greater and recommends 2048-bit. Resend signs with 1024-bit keys, which satisfies the requirement. See [Do you need 2048-bit DKIM?](/docs/knowledge-base/do-i-need-2048-dkim) for the reasoning.
* **Add a `rua` tag.** Yahoo strongly recommends including a working `rua` tag in your DMARC record so you can monitor authentication results while you roll out.
* **Yahoo supports BIMI.** Once you're at DMARC enforcement, publishing a [BIMI](/docs/dashboard/domains/bimi) record lets Yahoo Mail display your brand logo next to your messages. It's optional, but it reinforces recognition in the inbox.

When you verify your domain with Resend, **SPF** and **DKIM** are configured and validated for you automatically, so your email meets Yahoo's baseline authentication requirements out of the box.

**Action Items**

1. Verify your domain with Resend to set up SPF and DKIM automatically
2. [Set up DMARC](/docs/dashboard/domains/dmarc) for your domain with at least `p=none` and a `rua` tag

## Keep Your Spam Rate Below 0.3%

Yahoo publishes an explicit threshold: **keep your spam complaint rate below 0.3%**. This applies to all senders, not just bulk senders.

Yahoo calculates the rate against mail **delivered to the inbox**, not against total mail sent. That matters when you calculate the rate yourself: if a portion of your mail is already being filtered to spam, your internally-calculated rate will look lower than the number Yahoo is enforcing against.

There is also no fixed measurement window. Yahoo's systems continuously evaluate mail and may defer messages from domains with a high complaint rate at any point.

**Action Items**

1. Track your complaint rate against inbox-delivered mail, not total sends
2. Treat 0.3% as a ceiling to stay well below, not a target to approach

## Enroll in the Complaint Feedback Loop

Yahoo's Complaint Feedback Loop (CFL) is the only way to see complaint data for your domain. When a Yahoo user clicks "report spam," Yahoo sends a report in [ARF (Abuse Reporting Format)](https://datatracker.ietf.org/doc/html/rfc5965) to the address you enroll, so you can suppress that recipient.

The CFL is **domain-based and depends on DKIM**. Yahoo enrolls the domain in the `d=` tag of your DKIM signature, so your mail must be DKIM-signed to participate. Yahoo no longer offers IP or CIDR-based feedback loop reporting.

To enroll, create a Sender Hub profile, add and verify your domain, then enroll it under **Manage Services → Complaint Feedback Loop**. The reporting address can be any address you control and doesn't need to match your sending domain. Enrollment covers AOL and every other domain Yahoo hosts.

You can recognize a Yahoo CFL report by these headers:

| Header              | Value                           |
| ------------------- | ------------------------------- |
| `From:`             | `Yahoo! Mail AntiSpam Feedback` |
| SMTP `MAIL FROM`    | `feedback@arf.mail.yahoo.com`   |
| DKIM signing domain | `arf.mail.yahoo.com`            |

**Action Items**

1. [Enroll your sending domain in the CFL](https://senders.yahooinc.com/complaint-feedback-loop/)
2. Use [webhooks](/docs/webhooks/introduction) to act on `email.complained` events in your own system
3. Let [Suppressions](/docs/dashboard/emails/email-suppressions) automatically skip bounced and complained addresses

## Support One-Click Unsubscribe

Bulk senders must implement a functioning `List-Unsubscribe` header. Yahoo highly recommends the POST method defined in [RFC 8058](https://datatracker.ietf.org/doc/html/rfc8058), though the `mailto:` method is acceptable.

Three specifics from Yahoo:

* **A body link alone isn't sufficient.** You need the header. Also keep a clearly visible unsubscribe link in the body, which may point to a preference page.
* **Honor requests within 2 days.** Yahoo offers no grace period. An unsubscribe that isn't processed within 2 days doesn't meet the requirement.
* **Transactional mail is exempt.** One-click unsubscribe is only required for promotional and marketing messages, not for order confirmations, password resets, and similar. Yahoo won't decide which of your mail needs it, so rely on local regulations and your own judgment. If a non-promotional stream is generating high complaints, adding unsubscribe anyway is usually the safer choice.

Set up correctly, Yahoo may show a blue **Unsubscribe** button next to your `From:` address, though this also depends on Yahoo seeing sufficient reputation and engagement for your sending address. Test it in Yahoo webmail at [mail.yahoo.com](https://mail.yahoo.com/).

**Action Items**

1. Add [Unsubscribe Headers](/docs/dashboard/emails/add-unsubscribe-to-transactional-emails) to enable one-click unsubscribe
2. Keep a visible unsubscribe link in the body of bulk emails
3. Process unsubscribe requests within 2 days

## Send Only to Recipients Who Opted In

Yahoo asks senders to verify they are only mailing users who specifically requested it, and to use confirmed opt-in to get there. Purchased lists and pre-checked opt-in boxes on your website are called out by name as practices to avoid.

Yahoo also asks you to **honor the frequency of the list's intent**: don't start sending daily email to people who subscribed to a weekly or monthly list.

**Prevent sending to recipients who**:

* Didn't explicitly opt in to your emails
* Show no signs of engagement with your emails
* Requested to be unsubscribed
* Marked your emails as spam (complained)
* Never received your email (bounced)

**Action Items**

1. Use double opt-in to confirm new subscribers
2. Set expectations at signup about what you'll send and how often
3. Never resume sending to addresses on your suppression list

## Keep Your List Clean

Sending to people who don't read your email, or who report it as spam, damages both your delivery metrics and your reputation. Yahoo asks senders to monitor hard bounces, soft bounces, and inactive recipients, and to remove invalid recipients promptly.

Yahoo also suggests periodically sending a reconfirmation email to inactive subscribers rather than continuing to mail them indefinitely.

**Action Items**

1. Regularly prune inactive subscribers from your list, following [audience hygiene](/docs/knowledge-base/audience-hygiene) best practices
2. Send a reconfirmation campaign to inactive subscribers instead of quietly continuing to mail them
3. Remove addresses that generate bounces immediately

## Get Your DNS and RFC Compliance Right

Yahoo requires **valid forward and reverse DNS records for your sending IPs** from all senders, along with compliance with [RFC 5321](https://datatracker.ietf.org/doc/html/rfc5321) and [RFC 5322](https://datatracker.ietf.org/doc/html/rfc5322). Reverse DNS must be valid, meaningful, and non-generic. It also needs to reflect your domain name rather than looking like a dynamically-assigned IP.

When you send with Resend, forward and reverse DNS for the sending IPs is managed for you on both shared and dedicated pools.

One Yahoo-specific gotcha does fall on you. Yahoo validates the domain to the right of the `@` in `MAIL FROM` and the `From:` header using a **Start of Authority (SOA) query**. If you send from a subdomain, an A or MX record isn't enough. An SOA record must resolve for that subdomain too, or Yahoo returns an unresolvable-domain error as either a 451 timeout or a 554 permanent failure.

RFC compliance failures Yahoo calls out include duplicate headers, incorrectly formatted headers, and incorrect MIME types. Yahoo also rejects mail for policy reasons like a null MX record ([RFC 7505](https://datatracker.ietf.org/doc/html/rfc7505)), oversized headers, a `Date` outside the accepted range, and addresses containing exotic characters.

**Action Items**

1. Confirm an SOA record resolves for any [subdomain you send from](/docs/knowledge-base/is-it-better-to-send-emails-from-a-subdomain-or-the-root-domain)
2. Keep messages RFC 5321 and RFC 5322 compliant
3. Keep attachments under Yahoo's approximate 25 MB limit

## Control Your Sending Rate

Sudden volume spikes are one of the fastest ways to get flagged. Yahoo warns that if you normally send at a certain rate and then spike, you can be treated as a compromised sender and filtered to spam. Plan campaigns and spread them over a period of time.

At the connection level, Yahoo accepts a limited number of messages per SMTP connection. Once that limit is reached, the server terminates the connection without returning an error, and you can reconnect immediately. Yahoo permits concurrent connections but doesn't publish a number. Heavy use may cause Yahoo to de-prioritize connections from your servers.

**Action Items**

1. Follow a [warm-up plan](/docs/knowledge-base/warming-up) when ramping volume on a new domain
2. Spread large campaigns over time rather than sending in a single burst

## Make Content People Want to Read

Yahoo notes that poor reputation alone rarely sends mail to the spam folder. What usually does it is poor reputation combined with other negative signals, such as:

* Obfuscated URLs in the message body
* Sending IPs without a fully qualified domain name in reverse DNS
* Messages that aren't RFC compliant

Generic or unhelpful subject lines also invite complaints, which feed straight back into the 0.3% threshold. Content blocks (`PH*` errors) apply to viruses, phishing, ransomware, other malicious software, and links pointing to any of the above.

**Action Items**

1. Use visible links that match your sending domain instead of obfuscated redirects
2. Write specific subject lines that reflect the actual content of the email

## Understand Yahoo's Error Codes

Yahoo tells you a lot through SMTP responses. Treating them differently based on type is expected.

| Error        | Type      | What It Means                                                      |
| ------------ | --------- | ------------------------------------------------------------------ |
| `421`, `451` | Temporary | Unusual traffic, spam characteristics, complaints, or busy servers |
| `TS*`        | Temporary | Deferral from complaints, poor IP reputation, or unusual traffic   |
| `PH*`        | Permanent | Content block for malicious content or links                       |
| `553`, `554` | Permanent | Invalid recipient, failed DMARC or DKIM, or policy violation       |

Temporary errors can be retried later. **Never retry a permanent error.** Yahoo expects list managers to have a policy for removing addresses that generate 5xx bounces. A `554` citing Spamhaus means your IP is listed, so check with [Spamhaus](https://www.spamhaus.org/) directly.

Yahoo uses 48 hours as the point at which a recurring error stops being noise: if you've received the same excessive-complaints or excessive-volume error for more than 48 hours, review your outgoing messages for objectionable content or practices.

**Action Items**

1. Review your Resend Dashboard and mail logs for Yahoo SMTP errors
2. Stop retrying any address that returns a 5xx error
3. Escalate errors that persist beyond 48 hours

## If You're Still Having Issues

**Yahoo doesn't have a whitelisting program.** Yahoo is explicit that the term implies guaranteed inbox delivery, which they won't offer.

What they do offer is a [Sender Support Request](https://senders.yahooinc.com/contact/#sender-support-request). Submit one if you're consistently seeing the same error over an extended period, if you're a new sender or on new IPs that can't deliver, or if you anticipate difficulty ahead of a large launch or a legal notification. Include the specific error and diagnostic codes from your logs. Yahoo will review and modify your reputation if warranted, though this still doesn't guarantee inbox placement.

For general questions, Yahoo's postmaster team can be reached at **[mail-questions@yahooinc.com](mailto:mail-questions@yahooinc.com)**.

## Summary

Email deliverability is overwhelming. One way to simplify it is to think: **what would a phisher do?**

**Then do the opposite!**

Yahoo's goal is to only show emails that their users want to see. Reverse engineer phishing sending habits and consider how you can prove to Yahoo at each step that you clearly have no malicious intent.

<Info>Anything we missed? [Let us know](https://resend.com/help).</Info>
