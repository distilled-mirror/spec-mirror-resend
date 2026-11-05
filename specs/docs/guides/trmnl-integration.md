> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Show Resend metrics on TRMNL

> Add the Resend plugin to your TRMNL e-ink display to see email volume and deliverability at a glance.

[TRMNL](https://trmnl.com) is an e-ink display that rotates through screens from plugins. The official [Resend plugin](https://trmnl.com/recipes/resend-521360) shows how many emails your team sent and how many the recipient's mail server accepted, with the same numbers as your [Metrics](https://resend.com/metrics) page.

![Resend plugin on a TRMNL display](https://mintcdn.com/resend/H-2crYdwSrv8afiu/images/trmnl-full.png?fit=max\&auto=format\&n=H-2crYdwSrv8afiu\&q=85\&s=a6408695fab57dddb12f85d77771a195)

## What the plugin shows

The plugin covers the last 15 days, including today. That's the same default range as the Metrics page.

* **Emails:** The number of emails sent.
* **Deliverability:** The share of sent emails that the recipient's mail server accepted.
* **Bounces:** The share of sent emails that bounced.
* **Complaints:** The share of delivered emails that recipients marked as spam.
* **Chart:** Emails sent per day, bucketed by the time zone set in your TRMNL account.

If your team sent no emails in the range, the three rates show a dash instead of `0%`. Every account must stay under a [4% bounce rate](https://resend.com/docs/knowledge-base/account-quotas-and-limits.md#bounce-rate) and a [0.08% spam rate](https://resend.com/docs/knowledge-base/account-quotas-and-limits.md#spam-rate).

## Connect Resend

**1. Add the plugin**

Open the [Resend plugin](https://trmnl.com/recipes/resend-521360) in TRMNL and add it.

**2. Sign in to Resend**

1. Click **Connect**.
2. Sign in to Resend.
3. Approve access for your team.

The plugin uses OAuth, so you don't need to create or paste an API key. It requests `full_access` because the Metrics API requires it; this scope permits access to every API route, including write operations, though the plugin only reads metrics.

**3. Add it to a playlist**

Add the plugin to a TRMNL playlist. The display picks it up on its next refresh.

## Layouts

The plugin supports every TRMNL layout (full, half horizontal, half vertical, and quadrant). Use it on its own or in a mashup with other plugins.

The full layout shows all four numbers and a chart with axes.

![Resend plugin in the full layout](https://mintcdn.com/resend/H-2crYdwSrv8afiu/images/trmnl-full.png?fit=max\&auto=format\&n=H-2crYdwSrv8afiu\&q=85\&s=a6408695fab57dddb12f85d77771a195)

## How often it refreshes

TRMNL fetches new metrics from Resend every 15 minutes. The [Metrics API](https://resend.com/docs/api-reference/emails/get-metrics.md) also caches responses for up to 15 minutes, so the display can trail the Metrics page by up to about half an hour. When the display shows the new data depends on your device's own refresh rate.

## Troubleshooting

### The screen says "Couldn't load metrics"

The plugin couldn't read metrics from Resend, and the screen shows the error Resend returned. This usually means the connection's access was revoked or expired.

Open the plugin in TRMNL and click **Connect** again to sign in to Resend.

### The numbers don't match the Metrics page

Check these in order:

1. **Team:** The plugin shows the team you approved access for when you connected. Make sure you're viewing that team's Metrics page.
2. **Date range:** The plugin always shows the last 15 days. Set the Metrics page to the same range to compare.
3. **Time zone:** The chart groups days by the time zone in your TRMNL account settings. If that differs from the time zone you view the Metrics page in, the daily bars can shift by a day.
4. **Delay:** The display can trail the Metrics page by up to about 30 minutes. See [How often it refreshes](#how-often-it-refreshes).

## Contribute

The plugin is open source. To report a bug or change a layout, open an issue or pull request in the [resend-trmnl-plugin](https://github.com/resend/resend-trmnl-plugin) repository. The README covers how to preview changes locally with the TRMNL preview server.
