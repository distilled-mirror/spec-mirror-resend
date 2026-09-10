> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# How to handle a leaked API key

> Learn what to do when a Resend API key is exposed or used without authorization.

An API key is the only credential needed to send through your account. Anyone holding a leaked key can send from any domain you've verified, spend your monthly quota, and damage the sending reputation you've built.

This guide covers how keys typically leak, what to do, how to review what was sent, and how to limit the damage next time.

## Identify how the key leaked

Replacing a key without closing the leak means the new key is exposed the same way. Common leak sources include:

* A key committed to a Git repository. Search the history rather than only the working tree, because a key stays in history after it's removed from the files.
* A public or forked repository, a Gist, or a continuous integration log that prints environment variables.
* A key bundled into client-side or mobile code, where anyone can read it out of the browser or the app package.
* A key pasted into a screenshot, a chat message, an issue tracker, or a third-party tool.
* A publicly reachable `.env` file or a framework left in debug mode on a production host.

## Delete the key first

Deleting a key revokes it right away. There's no separate revoke step, and no further requests can authenticate with it once it's gone.

1. Open the [**API keys** Dashboard page](https://resend.com/api-keys).
2. Find the key you believe was exposed, using the **last used** indicator to narrow it down.
3. Click the **More options** button, then **Remove API key**.
4. Create a replacement key and deploy it to your services.

<Warning>
  Treat the old key as compromised. You can't view an API key after it's
  created, so a replacement is always a new key rather than a reissue of the old
  one.
</Warning>

If your services are still running on the exposed key, follow the [key rotation steps](/docs/knowledge-base/how-to-handle-api-keys#key-rotation) so you don't experience downtime while you swap it out.

## Review what was sent

Two Dashboard pages hold the record of what happened:

* The [**Logs**](https://resend.com/logs) page lists every API request made against your account. Filter by API key and by date range to isolate the window.
* The [**Emails**](https://resend.com/emails) page lists the messages themselves, so you can see recipients, subjects, and delivery outcomes.

Resend keeps 30 days of activity.

## What Resend logs and what it doesn't

Each log entry records the endpoint, the HTTP method, the response status, and the timestamp. It also holds the User-Agent and the full request and response bodies.

Resend doesn't retain the following, so it isn't available during an investigation:

* Source IP addresses for API or SMTP connections
* Autonomous System Number (ASN), internet service provider, or geographic data
* `HELO` or `EHLO` hostnames
* Transport Layer Security (TLS) connection metadata

There's no separate internal store beyond what the Logs page shows. What you can export is the complete record.

## Recover your sending reputation

Deleting the key stops the unauthorized sending. Inbox providers weigh recent activity most heavily.

Watch your [**Metrics**](https://resend.com/metrics) page over the following weeks. All accounts must stay under a **4%** bounce rate and a **0.08%** spam rate. A rate above either threshold may result in a temporary pause in sending.

Recipients who marked the unauthorized messages as spam are added to your suppression list. That's expected behavior, and it protects you from sending to them again.

## Reduce the damage next time

You can't prevent every leak, but you can limit what one costs you.

* **Give each service its own key.** Per-key logs then show you which integration was abused, and you can delete one key without disrupting the rest.
* **Prefer "Sending access" over "Full access."** Most applications only need to send, and a "Sending access" key can't read your contacts even if it leaks.
* **Delete keys you aren't using.** Resend flags keys unused for 30 or more days in the Dashboard.

For the full set of practices, see [API key security](/docs/knowledge-base/how-to-handle-api-keys).

## Get more help

If you've worked through the steps above and still have questions, contact [Resend support](https://resend.com/help) with:

1. The ID of the affected API key.
2. The window when the unauthorized activity took place.
3. What you've already done to contain it.
