> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# What are Resend account quotas and limits?

> Learn what quotas and limits apply to accounts.

Resend regulates email volume in three ways:

1. email volume (quota) - for [Transactional Email](/docs/knowledge-base/what-sending-feature-to-use#transactional-emails)
2. number of contacts - for [Marketing Email](/docs/knowledge-base/what-sending-feature-to-use#marketing-emails)
3. sending rate

These limits help improve your deliverability and likelihood of reaching your recipient's inbox.

<Info>
  Both **sent emails** and **received emails** (inbound) count towards your
  account's email quota. Each received email counts as 1 email against your
  daily and monthly limits, just like sent emails.
</Info>

## Free Account Quotas and Limits

Free accounts have the following:

* Transactional emails: daily email quota of 100 emails/day and 3,000 emails/month. This quota includes both sent and received emails. Multiple `To`, `CC`, or `BCC` recipients in sent emails count as separate emails towards this quota. The daily quota is a UTC calendar day (00:00–24:00 UTC) and resets at midnight UTC. It is not a rolling 24-hour window from your first send or from when you hit the limit.

* Marketing emails: unlimited emails to up to 1,000 contacts per month.

* Domains: up to 3 verified domains.

## Paid Plan Quota

* Transactional Pro, Scale and Enterprise plans have no daily quota limits, though the plan tier will dictate the monthly email quota. Both sent and received emails count towards this monthly quota. To see your current month usage, view the [**Usage page**](https://resend.com/settings/usage). Multiple `To`, `CC`, or `BCC` recipients in sent emails count as separate emails towards the monthly quota.
* Marketing Pro, Enterprise plans have unlimited emails, though the plan tier will dictate the monthly contacts.
* Pro plans include 10 domains and Scale plans include 1,000 domains. Enterprise domain limits are set by contract. Pro and Scale plans can add 100 more domains with a [\$20/month add-on](/docs/knowledge-base/what-is-resend-pricing#add-ons).

## Overage Limits

Paid plans include pay-as-you-go overages, which allow you to continue sending emails after you've reached your monthly quota. To prevent extreme overages and unexpected costs, a hard limit of 5x your monthly quota applies.

<Note>
  By default, overage usage is capped at **5x your plan's monthly quota**. Once you reach this limit, sending will be paused until the next billing cycle.

  If you need to adjust this limit, please [contact support](https://resend.com/help).
</Note>

<Tip>
  While overages provide flexibility for occasional spikes in email volume, they
  can be more expensive per email than upgrading your plan. If you consistently
  exceed your quota, consider [upgrading to a higher
  tier](https://resend.com/settings/billing) for better value and more
  predictable costs.
</Tip>

## Domain Limits

Every plan includes a set number of verified custom domains, listed on the [pricing page](https://resend.com/pricing). You can see how many domains your team is using on the [**Usage page**](https://resend.com/settings/usage).

If you need more, paid transactional plans can enable the domains add-on, which adds 100 domains on top of the number included in your plan for \$20 per month. See [How to add more domains](/docs/knowledge-base/how-to-add-more-domains).

## Rate Limits

All accounts start with a rate limit of 10 requests per second. The [rate limits](/docs/api-reference/rate-limit) follow the [IETF standard](https://datatracker.ietf.org/doc/html/draft-ietf-httpapi-ratelimit-headers) for stating the rate limit in the response header. If you have specific requirements, [contact support](https://resend.com/help) to request a rate increase.

The rate limit is enforced as a per-second window. There is no separate burst allowance above the stated limit. If your limit is 10 requests per second, an eleventh request in the same second window will receive a `429` response.

### Rate limit scope

The rate limit is **per team**, not per API key or per domain. All API keys associated with your team share the same rate limit pool. If you have multiple services or applications sending through the same Resend team, their requests count together toward the 10 req/sec limit.

For example, if Service A sends 6 requests and Service B sends 4 requests in the same second, you have hit your 10 req/sec limit for that window. Any additional requests from either service will receive a `429` response.

### High-volume workloads

If you have potential sending spikes or sustained high-volume workloads, consider these approaches:

* **Batch sending**: Use the [Batch Email API](/docs/api-reference/emails/send-batch-emails) to send up to 100 emails in a single API call. Each batch request counts as one request against your rate limit.
* **Client-side throttling**: Use the [rate Limit headers](/docs/api-reference/rate-limit) to configure client-side throttling.
* **Traffic spikes**: If you anticipate sustained traffic above your current limit, [contact support](https://resend.com/help) in advance to request a rate increase.

## Bounce Rate

All accounts must maintain a bounce rate of under **4%**. The [**Metrics page**](https://resend.com/metrics) within an account and/or [webhooks](https://resend.com/docs/webhooks/event-types#email-bounced) allow you to monitor your account bounce rates.

Maintaining a bounce rate above 4% may result in a temporary pause in sending until the bounce rate is reduced.

Tips to keep a bounce rate low:

* Remove inactive user email addresses from email lists.
* Only send to recipients who have given consent to receive email.
* When testing, avoid sending to fake email addresses. Use Resend's [test email addresses](/docs/dashboard/emails/send-test-emails) instead.
* If you are using open/click tracking, periodically remove recipients who are not engaging with your emails from your email lists.

## Spam Rate

All accounts must have a spam rate of under **0.08%**. The [**Metrics page**](https://resend.com/metrics) within an account and/or [webhooks](https://resend.com/docs/webhooks/event-types#email-complained) allow you to monitor your account spam rates.

Maintaining a spam rate over 0.08% may result in a temporary pause in sending until the spam rate is reduced.

Tips to keep a spam rate low:

* Give recipients a clear way to opt out of emails.
* Send relevant and timely emails.
* Only send to recipients who have given consent to receive email.

## Data Retention

Resend retains email data for **30 days** across all plans (Free, Pro, and Scale). This includes:

* Email content and metadata
* Delivery status and events
* Logs and metrics

Enterprise plans have access to **flexible data retention** options. [Contact support](https://resend.com/help) to discuss custom retention requirements.

<Tip>
  If you need access to historical email data beyond the 30-day retention
  window, consider storing [webhook
  events](/docs/dashboard/webhooks/how-to-store-webhooks-data) in your own database.
  This gives you full control over retention periods and ensures you never lose
  important information.
</Tip>
